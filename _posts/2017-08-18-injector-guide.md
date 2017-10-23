---
layout: post
title: "Quỳ Hoa Bửu Điển"
comments: true
description: ""
keywords: ""
---

## Chương I: Dẫn Đao Tự Cung


### 1. Add clone và Acc chính

Lưu ý, acc được add vào phần mềm sẽ vào server mặc định dựa vào lần cuối log vào game.

**Lệnh add clone buff xu (CrossWar.hs)**

> adb "username" "password"

**Lệnh add nhân vật chính cược xu (CrossWar.hs)**

> adp "username" "password"


### 2. Chỉnh số xu cược (Players.json và Buffs.json)

Chỉnh số xu cược của từng acc bằng cách mở file Players.json (acc chính) hoặc Buffs.json (acc clone).

Số xu nằm ở dòng "amount".

0 : đặt toàn bộ xu.

1 : đặt 1000 xu.

2 : đặt 2000 xu.

3 : đặt 3000 xu.

... (theo cấp số nhân x1000)

Ví dụ acc sau sẽ cược 50k xu:

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

Chỉnh kèo thắng/thua bằng cách thay thế mã số người chơi trong dòng "win" và dòng "lose".

Toàn bộ acc chính trong Players.json sẽ đặt vào nhân vật trong dòng win. Toàn bộ clone trong Buffs.json sẽ đặt vào nhân vật trong dòng lose.
 
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

----------

##