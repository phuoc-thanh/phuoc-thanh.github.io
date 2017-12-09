---
layout: post
title: "Quỳ Hoa Bửu Điển"
comments: true
description: ""
keywords: ""
---

## Chương I: Dẫn Đao Tự Cung

Cầm trên tay cuốn bí cấp võ lâm này, đại hiệp đã bước chân vào ma đạo.

Khi đã dùng bí cấp đánh cược ăn xu, bất kể là tự tay hay nhờ vả, dù một lần hay n lần, đại hiệp đã dính chàm.
Nhân vật ảo của đại hiệp sẽ bị lưu giữ thông tin.

Chương 1 của Quỳ Hoa Bửu Điển sẽ hướng dẫn đại hiệp cách đánh cược thu về ngân lượng của hảo hữu khác.

### 1. Thêm nhân vật phụ và nhân vật chính

Lưu ý, nhân vật được thêm vào bí kíp sẽ vào máy chủ mặc định dựa vào lần cuối bước chân vào giang hồ.

**Lệnh thêm nhân vật phụ (CrossWar.hs)**

> adb "username" "password"

**Lệnh thêm nhân vật chính (CrossWar.hs)**

> adp "username" "password"


### 2. Chỉnh số xu cược (Players.json và Buffs.json)

Chỉnh số xu cược của từng nhân vật bằng cách mở file Players.json (nv chính) hoặc Buffs.json (nv phụ).

Số xu nằm ở dòng "amount".

0 : đặt toàn bộ xu.

1 : đặt 1000 xu.

2 : đặt 2000 xu.

3 : đặt 3000 xu.

... (theo cấp số nhân x1000)

Ví dụ, nhân vật sau sẽ cược 50k xu:

    {
        "amount": 50,
        "displayNovice": 1,
        "chNumber": "118000019",
        "uid": "1254848116",
        "key": "4b91b2cf558602fc21f9d379ff982a86",
        "defaultsid": "118",
        "opname": "10",
        "create_time": 1503040225,
        "acc": "reply1989"
    }

### 3. Lựa chọn kèo (Match.json)

Chỉnh kèo thắng/thua bằng cách thay thế mã số đấu thủ trong dòng "win" và dòng "lose".

Toàn bộ nhân vật chính trong Players.json sẽ đặt vào đấu thủ trong dòng win. Toàn bộ nhân vật phụ trong Buffs.json sẽ đặt vào đấu thủ trong dòng lose.
 
    {
	    "mid": "1",
	    "win": "736",
	    "lose": "73000185"
    }

### 4. Cược xu (CrossWar.hs)

- Mở file CrossWar.hs bằng WinGHCi hoặc double click

- Canh giờ chính xác.

- Bấm nút Play màu đỏ của WinGHCi hoặc gõ lệnh

> main



### 5. Phụ lục

Mã số nhân vật liên chiến Kim Dung Truyện

>https://thanhdo89se.github.io/KimDungTruyen.json


Mã số nhân vật liên chiến Ta Là Vua
>https://thanhdo89se.github.io/TaLaVua.json

Chỉ đặt kèo thắng:
>winBet

Chỉ đặt kèo thua:
>loseBet

### 6. Tiện ích khác

1. Lệnh `info`

Dùng để kiểm tra số xu và hoa, lệnh `info` dùng với các nhân vật trong buffs.json

2. Lệnh `reward`

Dùng để nhận thưởng các kèo cược liên chiến, lệnh `reward` nhận nhân vật trong buffs.json

3. Lệnh `flower "code"`

Dùng để buff bông cho 1 đấu thủ, code là mã số đấu thủ.