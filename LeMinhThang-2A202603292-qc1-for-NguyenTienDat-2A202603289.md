# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Nguyễn Tiến Đạt-2A202603289       Người kiểm (học viên):  Lê Minh Thắng - 2A202603292
Ngày:     20 tháng 11 năm 2026                     Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest):  
Số ảnh kiểm: 6 (A01–A06) (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 67 (43 shape + 24 tag)  

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 13 | 3 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 13 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 13 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 13 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 13 | 4 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 12 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 19 | 2 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 7 | 1 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính |
| QC1-12 file | lỗi file | 1 | 2 | nhẹ |

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A01 | lane #0 | nặng | `position = L1` gán cho vạch liền mép đường ngoài cùng bên trái; vạch trái của làn xe mình là vạch đứt (#1) → phải là L2 |
| 2 | QC1-03 | A01 | lane #1 | nặng | Vạch đứt ngay bên trái làn xe mình gán `L2` → phải là L1 (đổi nhầm L1/L2 với #0) |
| 3 | QC1-03 | A01 | lane #3 | nặng | Vạch mép phải ngoài cùng gán `R1`, trùng với R1 thật (#2, vạch đứt) → phải là R2 |
| 4 | QC1-06 | A01 | lane #1 | chính | `kind = double` nhưng vạch là vạch đứt đơn → `single` |
| 5 | QC1-10 | A01 | traffic_sign (thiếu) | chính | Bỏ sót biển chỉ dẫn xanh nhỏ ở xa, khoảng (440, 475), cao hơn 8 px |
| 6 | QC1-04 | A02 | lane #1 (L1) | chính | Polyline vẽ từ xa về gần (điểm đầu ở đường chân trời) và dừng sớm ở y ≈ 500, chưa kéo xuống phần gần xe |
| 7 | QC1-07 | A03 | drivable #4 (alternative) | chính | Polygon tràn sang làn đỗ xe và thân các xe đỗ bên phải (góc dưới phải tới x = 1280) |
| 8 | QC1-09 | A03 | traffic_sign #6 | chính | Biển hình thoi màu cam (công trường) gán `group = prohibitory` → `warning` |
| 9 | QC1-07 | A04 | drivable (thiếu) | chính | Bỏ sót vùng `alternative` cho làn cùng chiều bên phải R1 |
| 10 | QC1-07 | A05 | drivable #0 (direct) | chính | Polygon tràn lên thân dãy xe đỗ bên phải (x ≈ 750–910, y ≈ 270–340) |
| 11 | QC1-07 | A06 | crosswalk (thiếu) | chính | Bỏ sót hai vùng vạch ngựa vằn hai bên làn xe mình (y ≈ 410–490) |
| 12 | QC1-09 | A06 | traffic_sign #7 | chính | Biển hình thoi màu cam gán `group = prohibitory` → `warning` |
| 13 | QC1-12 | A05 | drivable #0 | nhẹ | Bật cờ `occluded` trên polygon vùng lái; cờ này chỉ dùng cho polyline lane nối qua chỗ che |
| 14 | QC1-12 | A06 | drivable #9 | nhẹ | Như #13: bật `occluded` trên polygon vùng lái |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A05 | Đường không kẻ vạch nên không có L1/R1. Lint báo QC1-02 nặng; có miễn theo ngoại lệ "không thấy vạch" không? (người kiểm chưa tính lỗi) | |
| A06 | Chỉ có L1, thiếu R1. Bên phải làn xe mình gần như không thấy vạch dọc (chỉ có vạch ngang qua đường). Có miễn QC1-02 không? (người kiểm chưa tính lỗi) | |
| A03 | Checkpoint ghi A03 có vạch bị che, nhưng không lane nào bật `occluded`; R1 (#1) chỉ bắt đầu từ y ≈ 467. R1 có cần nối xuống gần xe kèm `occluded` không? | |
| A03 | 7 đèn ở xa rất nhỏ, đều gán `green`. Người kiểm không xác nhận được màu ở độ phân giải này | |
| A04 | Tag `weather = clear` trong khi trời nhiều mây; có nên là `overcast` không? (nếu sai thì chỉ là QC1-01 nhẹ) | |
| A06 | Đèn #0 góc trên trái gán `off`, `facing = front`; nhìn giống đèn quay ngang (`side`) | |

## Quyết định
Lỗi nặng: 3   Lỗi chính: 9 / 67 nhãn = 13,4 %   Lỗi nhẹ: 2   Ca chờ lead: 6  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Có 3 lỗi nặng (QC1-03 đổi nhầm `position` ở A01), một lỗi nặng là đủ để Rework. Ngoài ra tỉ lệ lỗi chính 13,4 % vượt ngưỡng 5 %. Các ca mơ hồ không đổi được kết luận nên không chọn Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
