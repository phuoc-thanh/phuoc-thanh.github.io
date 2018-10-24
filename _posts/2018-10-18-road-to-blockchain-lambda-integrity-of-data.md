---
layout: post
title: "Lambda Chain: Integrity of Data"
comments: true
description: "Road to Blockchain: Integrity of Data"
keywords: "blockchain, proofofstake, proofofwork, bitcoin, haskell, lambada"
---

Như có nhắc đến ở bài "lý thuyết" trước, tính toàn vẹn của dữ liệu được đảm bảo nhờ kỹ thuật mã hoá hiện đại.

Mỗi dữ liệu mới được ghi vào một block và những block này được mã hoá băm - a.k.a hash chặt chẽ với nhau thành một chuỗi, mà mọi người hay gọi là blockchain.

Vậy để đảm bảo toàn vẹn cho dữ liệu, thì trước tiên là phải định nghĩa dữ liệu, sau đó mới đến mã hoá dữ liệu. 2 modules được thêm vào project là Crypto.hs và Block.hs.

## Define a block

Về cơ bản, một block bao gồm 2 phần:

1. Block Data, lưu các dữ liệu đi kèm block, đó có thể là giao dịch, thư từ, phiếu bầu, chứng nhận, vé số, hồ sơ... bất kì loại dữ liệu nào mà bạn nghĩ nó phù hợp để thành lập blockchain.
2. Block Metadata, hay còn gọi là header. Header lưu mã hash của block trước nó, ngày giờ tạo ra block, độ khó của block, và số nonce.

Ở lambda-chain, tôi giả sử dữ liệu mình cần lưu là giao dịch, thì một block có cấu trúc như sau:

```haskell
-- A block consists of four parts:
-- - block header,
-- - base transaction body,
-- - the number of transactions,
-- - list of transaction identifiers.
data Block = Block {
    blockHeader :: BlockHeader,  -- Metadata
    -- baseTx      :: Transaction,  -- Coin base Transaction, or Miner Transaction
    origin      :: ByteString,   -- to be replaced with the baseTx as above
    txNum       :: Int,          -- Number of Transactions
    txHashes    :: [ByteString]  -- List of Transaction Identifiers
} deriving (Show, Eq, Read)

data BlockHeader = BlockHeader {
    prevId      :: ByteString, -- Identifier of the previous block
    timestamp   :: Int,        -- The creation time of block
    merkleRoot  :: ByteString,
    bits        :: Int,        -- Difficulty of block
    nonce       :: Int         -- Nonce number
} deriving (Show, Eq, Read)
```

lambda-chain thay vì lưu toàn bộ dữ liệu transaction thì chỉ lưu id của transaction và thêm merkle root của list transaction để xác định mối liên kết. Transaction data sẽ được lưu riêng, đó là cách làm của Monero, dựa trên [Cryptonote's Standards](https://cryptonote.org/standards/)

Và để xác định một block có hợp lệ hay ko, ta có validate function:

Tính lại hash của block xem có đúng ko?

Kiểm tra thông tin hash của block trước có đúng ko?

Note: this will be changed

```haskell
-- Is a block valid?
is_valid_block :: ByteString -> Block -> Block -> Bool
is_valid_block block_id block prev
    | block_id /= Block.hash_id (blockHeader block) (txHashes block) = False
    | prev_id  /= Block.hash_id (blockHeader prev)  (txHashes prev)  = False
    -- | -- validate transactions here
    | otherwise = True
    where prev_id = prevId $ blockHeader block
```

Tôi định nghĩa lại blockchain type:

```haskell
-- Chain of Blocks / List of Block_Hash
type Blockchain = [ByteString]
```
Và validate nguyên cả chain thì sao? cứ đệ quy thoi ahehe.

## Hashing data

Và hash là cái gì, sử dụng như thế nào?

Đoạn này ko phải xây dựng từ đầu, vì SHA256 là một thuật toán hash nổi tiếng và ngôn ngữ nào cũng có. Với haskell, hãy cài Cryptonite bằng cabal, và import vào Crypto.hs:

```haskell
import Crypto.Hash
```

Re-write lại hash function để khỏi phải khai báo SHA256 mỗi lần sử dụng:

```haskell
-- | Hash raw data with SHA256 hash function
hash :: ByteString -> Digest SHA256
hash m = hashWith SHA256 m
```

Và phần Crypto này chưa xong đâu nhé, về sau lambda-chain implement thêm phần Digital Signature nữa.

Rồi ta có thể tính toán block_hash kiểu như:

```haskell
block_hash :: Block -> Digest SHA256
block_hash block = hash . pack . show
```
Vì block là một data structure nên phải show dạng string, sau đó pack lại thành bytestring rồi mới tính hash :)

## Validate and Calculate Hash Id

Vì tôi muốn lưu id của block vào db ở dạng hash, theo cryptonote, thì nó được tính như sau:

```haskell
-- | The identifier of a block

-- Is the result of hashing the following data with SHA256 hash function:
-- - size of [block_header, Merkle root hash, and the number of transactions] in bytes,
-- - block_header,
-- - Merkle root hash,
-- - number of transactions.
hash_id :: BlockHeader -> [ByteString] -> ByteString
hash_id header txs = showBS . hash $ append (showBS $ length blob) blob
    where blob = append (showBS header) $ append (merkle_root txs) (showBS $ size txs)
```
Tuy nhiên tôi đang phân vân là có nên dùng luôn block hash để làm id hay ko?