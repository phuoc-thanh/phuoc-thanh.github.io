---
layout: post
title: "Lambda Chain: Consensus Protocol"
comments: true
description: "Road to Blockchain: Consensus Protocol"
keywords: "blockchain, proofofstake, proofofwork, bitcoin, haskell, lambada"
---

Và cuối cùng là consensus protocol, nơi mà các node accept blockchain dựa vào độ dài của chain. Các node cũng giành quyền verify block bằng cách tính toán hash theo số nonce, gọi là quá trình mining.

Như lý thuyết said, hash của block phải tính toán bằng cách tăng số nonce lên và tính toán sao cho hash đảm bảo có x ký tự '0' ở đầu.

x bao nhiêu cho đủ?

x là độ khó của việc tính toán, x càng lớn thì càng tốn thời gian để tìm ra.

x được định nghĩa trong header của block, field tên là `bits`, header của block cũng có số nonce để khi tìm ra hash thì các node khác có thể xác minh là block hợp lệ hay ko.

```haskell
data BlockHeader = BlockHeader {
    prevId      :: ByteString, -- Identifier of the previous block
    timestamp   :: Int,        -- The creation time of block
    merkleRoot  :: ByteString,
    bits        :: Int,        -- Difficulty of block
    nonce       :: Int         -- Nonce number
} deriving (Show, Eq, Read)
```

Và độ khó này phải được tự động tăng giảm sao cho phù hợp với năng lực tính toán của toàn mạng.

```haskell
-- The mine rate of bitcoin is 10 min (600s).
-- This is just demonstration, so I set it to only 3s.
mine_rate = 3

-- Adjust the difficulty of mining process                                
adjust_diff :: IO Int                                
adjust_diff = do
    blk <- last_block
    let b = bits (blockHeader blk)
    let t = timestamp (blockHeader blk)
    n    <- now
    if t + mine_rate > n then return $ b - 1 else return $ b + 1
```

Ở đây mine_rate là 3, 3 giây chỉ để thử nghiệm, thực tế với bitcoin là 600s.
Có nghĩa là độ khó sẽ tăng lên nếu như block được tìm ra với thời gian nhỏ hơn 3 giây, và giảm đi nếu thời gian quá 3 giây. Time đều tính theo POSIX milisecond nhé.


Và Node bây giờ đã có thể Mine Block:

```haskell
mine_block :: [Transaction] -> IO Block
mine_block txs = do
    timestamp  <- now
    origin     <- getPublicAddress
    let txH    =  Transaction.hash_id <$> txs
    let m_root =  merkle_root txH
    prev_id    <- last_block_id
    bits       <- adjust_diff
    header     <- hash_calculate origin prev_id m_root bits 0
    return $ Block header origin (size txH) txH

-- | Calcualte block_hash, then return a BlockHeader (that holds nonce n timestamp)
hash_calculate origin prev_id m_root bits nonce = do
    timestamp  <- now
    let hashed = showBS . hash . append prev_id 
                               . append (showBS timestamp) 
                               . append m_root 
                               $ append origin (showBS nonce)
    if take bits hashed == replicate bits '0'
        then return $ BlockHeader prev_id timestamp m_root bits nonce
        else hash_calculate origin prev_id m_root bits (nonce + 1)
```
`hash_calculate` chính là vòng lặp để brute force block hash, cho tới khi nó tìm đúng hash có chứa 'bits' số 0 ở đầu chuỗi hash. Nếu đã tìm được thì nó sẽ trả ra một header để xây dựng lên block mới.
