---
layout: post
title: "Tịch Tà Kiếm Phổ"
comments: true
description: ""
keywords: ""
---

## Config.json

Config.json là trang hướng dẫn cho cuốn bí kíp:

    {
        "apiHost": "",
        "payHost": "",
        "loginPath": "",
        "armyGroup": 20,
        "cloneCamp": "2",
        "cloneKeyword": "tichta",
        "cloneServer": "77",
        "defaultPass": "zzz",
        "huntTarget": "ZM49,ZM51",
        "huntDelay": 7000000
    }

3 dòng đầu chư vị đại hiệp ko cần quan tâm


`armyGroup`: Số lượng nhân vật phụ đồng loạt vào bang làm nhiệm vụ, tùy vị trí còn trống trong bang mà chỉnh

`cloneCamp`: 1 hoặc 2, chỉ phe cho nhân vật phụ vào: Tụ Hiền (1) hoặc Ma Giáo (2)

`cloneKeyword`: Tên dùng chung cho nhân vật phụ

`closeServer`: Máy chủ tạo nhân vật phụ

`defaultPass` : Mật khẩu mặc định

`huntTarget` : Mã số "Ma" cần trảm

-- Hoàng Dung ZM40, Vô Nhai Tử ZM43, Vương Tuyết Mai ZM44, Hoàng Thường ZM45, Vô Kỵ ZM48, Kiều Phong ZM49, Tiêu Diêu Lão Tổ ZM51..


----------


## dailyMis (Play.hs)

lệnh `dailyMis` dành cho chư vị bằng hữu gia nhập bang và nhận lương bang mỗi ngày (sau đó lập tức rời bang).

`dailyMis` áp dụng trên những nhân vật trong file Buffs.json (có thể thêm acc bằng lệnh `adb`)


## main (Play.hs)

lệnh `main` dành cho quần hùng gia nhập bang, cống hiến để thăng cấp bang hội. Mỗi 45 giây sẽ có 1 đợt quần hùng xin vào bang, làm nhiệm vụ, cầu khấn, xong xuôi sẽ rời bang.

`main` áp dụng trên những nhân vật trong file Clone.json (có thể thêm acc bằng lệnh `add n` hoặc `adc`)


## add n (Play.hs)

lệnh `add` dùng để chiêu mộ thêm vô danh tiểu tốt, rèn luyện tới cấp độ 23 để trở thành quần hùng cống hiến bang. Nhân vật mới được chiêu mộ dựa theo file Config.json và nhân vật cuối cùng trong file Clone.json.

ví dụ với file Config như trên, và nhân vật cuối cùng trong Clone.json là "tichta1001", khi gõ

`add 20`

Bí cấp sẽ chiêu mộ thêm 20 nhân vật "tichta1002", "tichta1003"... đến "tichta1022" và tự thêm vào Clone.json

Chư vị đại hiệp, hãy chiêu mộ từ tốn, khoảng 20-40 tiểu tốt mỗi lần, tránh tình trạng chen lấn đua xe dẫn đến tẩu hỏa nhập ma cho những kẻ vô danh.

## main (Hunt.hs)

lệnh `main` trong Hunt.hs dùng để trảm ma, sau khi gõ lệnh, quần hùng và vô danh tiểu tốt trong Clone.json sẽ đồng loạt xả ngân lượng để truy tìm tung tích ma đầu cần trảm (như ma Kiều Phong chẳng hạn).

Một khi tìm được ma đầu, tên tiểu tốt sẽ tạo phòng trảm và chờ một vị đại hiệp vào phòng trảm, sau đó 7 giây, cả 2 sẽ cùng trảm ma thu thập hồn phách.

## Một số lưu ý.

Các lệnh `adp` (dành cho Players.json), `adb` (dành cho Buffs.json) và `adc` (dành cho Clone.json) có thể chạy ở bất cứ file nào: CrossWar.hs, Hunt.hs, Play.hs