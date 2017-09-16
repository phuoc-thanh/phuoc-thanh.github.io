---
layout: post
title: "Tịch Tà Kiếm Phổ"
comments: true
description: ""
keywords: ""
---

## Config.json

Đây là file cấu hình cho toàn bộ tool, config.json có các thông tin sau:

    {
        "apiHost": "",
        "payHost": "",
        "loginPath": "",
        "armyId": "",
        "armyLead": {},
        "armyGroup": 20,
        "cloneCamp": "2",
        "cloneKeyword": "tichta",
        "cloneServer": "77",
        "defaultPass": "zzz",
        "huntTarget": "ZM49,ZM51",
        "huntDelay": 7000000
    }

3 dòng đầu các đại hiệp ko cần quan tâm

`armyId` : Mã số bang, phải do chính tay tại hạ lấy

`armyLead`: Copy thông tin bang phó bỏ vào đây

`armyGroup`: Số lượng clone đồng loạt vào bang làm nhiệm vụ, tùy slot còn trống trong bang mà chỉnh

`cloneCamp`: 1 hoặc 2, chỉ đường cho Clone vào Tụ Hiền (1) hay Ma Giáo (2)

`cloneKeyword`: tên dùng chung cho Clone

`closeServer`: server tạo clone và up bang

`defaultPass` : mật khẩu mặt định

`huntTarget` : Mã số tướng cần trảm ma

-- Hoàng Dung ZM40, Vô Nhai Tử ZM43, Vương Tuyết Mai ZM44, Hoàng Thường ZM45, Vô Kỵ ZM48, Kiều Phong ZM49, Tiêu Diêu Lão Tổ ZM51..


----------


## dailyMis (Play.hs)

lệnh `dailyMis` dành cho vip3 (hoặc vip3 tương lai) vào bang nhận xu mỗi ngày và thoát.

`dailyMis` áp dụng trên những account trong file Buffs.json (có thể thêm acc bằng lệnh `adb`)


## main (Play.hs)

lệnh `main` dùng để up bang. Mỗi 2 phút sẽ có 1 đợt clone xin vào bang, làm nhiệm vụ, cầu khấn, xong xuôi sẽ out.

`main` áp dụng trên những account trong file Clone.json (có thể thêm acc bằng lệnh `add n` hoặc `adc`)


## add n (Play.hs)

lệnh `add` dùng để tạo thêm clone. Clone sẽ tạo dựa theo file Config.json và acc cuối cùng trong file Clone.json.

ví dụ với file Config như trên, và acc cuối cùng trong Clone.json là "tichta1001", khi gõ

`add 20`

chương trình sẽ tạo thêm 20 acc "tichta1002", "tichta1003"... đến "tichta1022". Clone sẽ tự động cày lên lvl 23 và tự update vào Clone.json

Các vị đại hiệp, để an toàn, hãy chạy 20-40 acc 1 lần, ko nên tạo quá đà, sẽ sớm bị tẩu hỏa nhập ma.

## main (Hunt.hs)

lệnh `main` trong Hunt.hs dùng để trảm ma, chương trình sẽ tự động log toàn bộ acc trong Clone.json vào sver và  quay xu tìm cho ra mục tiêu trảm (như Kiều Phong chẳng hạn).

Nếu tìm thấy mục tiêu, sẽ tạo phòng và chờ. Khi có người vào phòng trảm, tool sẽ chạy sau 7 giây.

## Một số lưu ý.

Các lệnh `adp` (dành cho Players.json), `adb` (dành cho Buffs.json) và `adc` (dành cho Clone.json) có thể chạy ở bất cứ file nào: CrossWar.hs, Hunt.hs, Play.hs

Acc cuối cùng trong Clone.json luôn phải có 4 chữ số sau cùng, và phải lớn hơn 999. Ví dụ như 1000, 1001, 1234...

Chư vị đại hiệp có thể dùng lệnh : `adc "username" "password"` để thêm acc vào Clone.json