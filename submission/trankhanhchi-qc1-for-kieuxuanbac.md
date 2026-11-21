# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): KieuXuanBac        Người kiểm (học viên): trankhanhchi  
Ngày: 2026-11-21                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `KieuXuanBac-front.zip` (sha256 `4e833b2b…2f088`), `KieuXuanBac-fisheye.zip` (sha256 `8f061c25…7fca0`); không nhận được manifest nên không có `revision`  
Số ảnh kiểm: 6 (A03, A08, A09, A10, B03, B08) (+ 0 ảnh thêm; A13–A16 và B09–B12 chưa gán, ảnh thêm nên không tính lỗi)   Số nhãn đã kiểm (shape + tag): 141 (117 shape + 24 tag)

Cách kiểm: mở `annotations.xml`, vẽ đè từng shape lên ảnh gốc và đối chiếu từng nhãn với guideline Road v1.0; chạy thêm `road_check lint` trên cả hai file. Tên nhãn ghi theo dạng của `lint`: `label#thứ tự@(x,y của điểm đầu)`.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 10 | 2 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 16 | 1 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 16 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 16 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 16 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 25 | 2 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 30 | 3 | nặng / chính (cả 3 là chính) |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 76 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 46 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 24 | 1 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Ghi chú số mục kiểm: QC1-02 tính 2 vạch (L1, R1) × 5 ảnh. B08 là camera hai bên nên không áp dụng. QC1-03 đến QC1-06 tính trên 16 polyline `lane`. QC1-07 tính 25 shape (drivable + crosswalk + road_curb). QC1-09 tính 30 đèn + 46 biển. QC1-11 tính mọi shape của B03 và B08.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-02 | A09 | lane R1 (không có) | nặng | Bỏ sót: thiếu R1. Vạch trắng đứt bên phải xe thấy được, khoảng từ (805,640) tới (712,470) |
| 2 | QC1-02 | A10 | lane R1 (không có) | nặng | Bỏ sót: thiếu R1. Vạch trắng liền bên phải làn xe (cạnh làn "ONLY") thấy rõ, khoảng từ (1168,650) tới (892,472) |
| 3 | QC1-03 | B08 | lane#0@(216,620) | nặng | Sai thuộc tính: B08 là `fisheye_right` nên lane phải có `position = other`, đang ghi `L1` |
| 4 | QC1-04 | B03 | lane#11@(676,285) R1 | chính | Sai phạm vi: polyline vẽ từ xa về gần. Điểm đầu nằm ở chỗ vạch xa nhất, điểm cuối (786,361) mới là chỗ gần xe |
| 5 | QC1-07 | A10 | drivable#18@(450,605) direct | chính | Sai phạm vi: polygon khoét quanh đuôi xe phía trước. Guideline ghi "đi được nếu đường trống, không khoét lỗ quanh xe khác" |
| 6 | QC1-07 | A10 | drivable#19@(1197,665) alternative | chính | Sai phạm vi: polygon cũng khoét quanh xe đỗ/xe chạy bên phải |
| 7 | QC1-08 | A08 | traffic_light#4@(294,138) | chính | Sai thuộc tính: ghi `red / front`, nhưng đèn này nhìn ngang (thấy hông vỏ vàng, không thấy bóng sáng). Nên là `facing = side`, `color = unknown` |
| 8 | QC1-08 | A08 | traffic_light#5@(204,104) | chính | Sai thuộc tính: như lỗi 7, ghi `red / front`, đúng ra là `side / unknown` |
| 9 | QC1-08 | A08 | traffic_light#31@(872,144) | chính | Sai thuộc tính: ghi `green / front`, nhưng đèn lớn bên phải nhìn ngang, không thấy bóng xanh. Nên là `side / unknown` |
| 10 | QC1-11 | B03 | traffic_sign#19@(458,243) | chính | Sai thuộc tính: `edge_zone = true`, nhưng tâm box (465,249) cách tâm ảnh khoảng 292 px, nằm trong 80 % bán kính (512 px). Phải là `false` |

Ảnh kiểm mà không thấy lỗi: **A03**. Ảnh có 4 lane đúng position (L1 vàng, R1, R2, other bên kia dải phân cách), đúng chiều; 7 đèn và 7 biển có thuộc tính hợp lý.

Gợi ý của `lint` ở ảnh ngoài mẫu (không tính vào tỉ lệ, chỉ để bạn tự kiểm):
- B02 `road_curb#13` chỉ có 3 điểm.
- `edge_zone` nên xem lại ở B02 `traffic_light#5` và B05 `traffic_sign#2`.
- A05 không có L1/R1; ảnh này thật sự không có vạch sơn, nên xin coach miễn.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A08 | R1 `lane#24` bắt đầu ở (769,453), ngay mép trên vạch ngựa vạn, trong khi vạch đứt còn kéo xuống tới khoảng y≈530. Có tính là dừng sớm ở đầu gần xe (QC1-04) không? | Chưa có. Chưa tính lỗi |
| B03 | `traffic_sign#10` có tâm (1142,380), cách tâm ảnh khoảng 512 px, đúng bằng ngưỡng 80 %. `edge_zone = false` có chấp nhận được không? | Chưa có. Chưa tính lỗi |

## Quyết định
Lỗi nặng: 3   Lỗi chính: 7 / 141 nhãn = 4,96 %   Lỗi nhẹ: 0   Ca chờ lead: 2  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): Còn 3 lỗi nặng (thiếu R1 ở A09 và A10; sai `position` ở B08, camera hai bên). Theo luật, chỉ cần một lỗi nặng là đủ để Rework. Tỉ lệ lỗi chính 4,96 % chưa vượt 5 %, nhưng không làm đổi kết luận. Hai ca mơ hồ cũng không đổi kết luận, nên không chọn Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
