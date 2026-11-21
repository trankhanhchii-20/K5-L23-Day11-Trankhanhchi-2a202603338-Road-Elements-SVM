# Báo cáo cá nhân — Ngày 11
Họ tên: Trần Khánh Chi               Mã học viên: 2A202603338  
Phiên bản CVAT (Help → About): `local`  
Guideline: Road v1.0    Lần nộp (`revision` trong manifest): 1  
Thời điểm export (ngày giờ trên CVAT): 2026-11-21 , job 26    Số lần nộp lại sau Rework: 0 

### Bảng đối chiếu rubric → mục trong báo cáo / file nộp
| Tiêu chí rubric | Điểm | Bằng chứng nằm ở |
| --- | ---: | --- |
| Project, tag và file | 10 | Mục 1 (project, label, tag), mục 5 (kiểm file export), mục 6 (ảnh chụp); `trankhanhchi-manifest.json` |
| Polyline làn, Set A | 25 | `trankhanhchi-front.zip`; mục 3 (ca khó về L1/R1); mục 7 (lỗi đã sửa ở A08) |
| Thuộc tính làn | 10 | `trankhanhchi-front.zip`; mục 3 (A04, A08) |
| Vùng lái được | 10 | `trankhanhchi-front.zip`; mục 3 (A05, A12) |
| Đèn và biển | 15 | `trankhanhchi-front.zip`; mục 3 (đèn nhìn ngang ở A08) |
| Fisheye, Set B | 10 | `trankhanhchi-fisheye.zip`; mục 3 (B05–B08); mục 7 (vỉa fisheye) |
| Phiếu QC 1 cho bạn khác | 15 | `trankhanhchi-qc1-for-kieuxuanbac.md` |
| Báo cáo cá nhân | 5 | Mục 3 (bảng ca khó có lý do), mục 4 (phản hồi phiếu nhận được), mục 7 (tự đánh giá nối với model) |

## 1. Kiểm project
| Mục | Đúng như guideline Road v1.0? | Ghi chú |
| --- | --- | --- |
| 6 label, đúng kiểu | Đúng | `lane` polyline, `road_curb` polyline, `crosswalk` polygon, `drivable` polygon, `traffic_light` rectangle, `traffic_sign` rectangle. Đối chiếu khối `<meta><labels>` trong file export với `python -m road_lab.taxonomy` |
| Thuộc tính và giá trị | Đúng | `lane`: position/style/color/kind; `drivable`: area_type; đèn: color/type/facing/edge_zone; biển: group/facing/edge_zone (edge_zone là checkbox). Giá trị và thứ tự khớp taxonomy |
| 4 tag ảnh | Đúng | `camera`, `timeofday`, `weather` (có `overcast`), `source`, mỗi label kiểu Tag có một thuộc tính select `value`. 28/28 ảnh đủ 4 tag (manifest: `images_all_tags` 16/16 và 12/12) |

Cách kết thúc polyline trên bản CVAT này: click điểm cuối rồi bấm **N** (hoặc double-click điểm cuối). Sau đó mở Details để sửa thuộc tính, vì CVAT tự điền giá trị đầu danh sách (`L1 / solid / white / single`).  
Cách đặt tag ảnh trên bản CVAT này: chọn công cụ **Setup tag** ở thanh trái, chọn label (`camera`, …) rồi bấm Tag. Sau đó chọn `value` trong sidebar Objects. Đặt `camera` trước, kiểm lại `weather` vì mặc định là `clear`.

> Lưu ý quy trình: cả 28 ảnh nằm trong một job (job 26) thay vì bốn task front / front-extra / fisheye / fisheye-extra. Khi nộp, file export được tách theo tiền tố tên ảnh (A.. → front, B.. → fisheye). Tên ảnh giữ nguyên nên checker vẫn ghép được với GT.

## 2. Số lượng đã gán
| Task | Ảnh | lane | road_curb | crosswalk | drivable | traffic_light | traffic_sign |
| --- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| front | 12 | 31 | 10 | 5 | 22 | 38 | 43 |
| front-extra (đã làm 4 / 4) | 4 | 9 | 0 | 3 | 7 | 8 | 13 |
| fisheye | 8 | 6 | 11 | 7 | 4 | 4 | 0 |
| fisheye-extra (đã làm 4 / 4) | 4 | 0 | 3 | 3 | 1 | 0 | 0 |

(B11 không có shape nào, chỉ có 4 tag: ảnh không có vạch, vỉa hay đèn rõ trong vùng thấy được.)

## 3. Bảng ca khó
| Ảnh | Nhãn | Phân vân giữa | Đã chọn | Lý do |
| --- | --- | --- | --- | --- ||
| A08 | traffic_light (3 đèn nhìn ngang) | `facing front` + màu, hay `side` + `unknown` | `facing = side`, `color = unknown` | Chỉ thấy hông vỏ đèn, không thấy mặt bóng đèn nên không xác định được màu đang sáng |

## 4. Phiếu QC 1 nhận được
Bạn kiểm lô của tôi: KieuXuanBac  Quyết định nhận được: **Rework** (2 lỗi nặng, 0 lỗi chính / 109 nhãn = 0 %)
| Mã lỗi | Số lỗi | Đồng ý? | Đã sửa? |
| --- | ---: | --- | --- |
| QC1-02 (A12, thiếu R1) | 1 | Không đồng ý. Bên phải chỉ có lề và làn đỗ, không có vạch R1 thấy được (xem mục 3). Chờ vẽ thêm R1 và nộp lại `revision 2` |
| QC1-02 (A14, thiếu R1, ảnh thêm) | 1 | Không đồng ý. Đường sáng bên phải là mép đường, không phải vạch làn | Chưa; chờ coach |

Bằng chứng cho A12: `images/04b-A12-no-R1.png` (A12 phóng to trên CVAT). Bên phải làn xe chỉ có vỉa (`road_curb`) và mặt đường, không có vạch sơn R1.

Ghi chú về phiếu nhận được:
- Phiếu còn một dòng lỗi #3 để trống (mẫu) và phần quyết định còn ghi "[0 hoặc 1]". Theo bảng tổng hợp thì lỗi chính là 0.
- Mã sha256 trong phiếu (`0e72807c…`, `b925477e…`) khác manifest hiện tại (`4e7e1b42…`, `8c1733a7…`). Lý do: file zip được tạo lại sau khi bạn kiểm (thời điểm ghi trong zip đổi). Nội dung nhãn không đổi: số shape và lane trong 7 ảnh kiểm vẫn là 81 và 17, khớp phiếu.

Đã tự kiểm và sửa trước khi nộp, theo gợi ý của `road_check lint` (từ 13 cảnh báo xuống 4; 4 cảnh báo còn lại đều là QC1-02 ở A05, A12, A14):
| Mã | Ảnh | Đã sửa |
| --- | --- | --- |
| QC1-03 / QC1-04 / QC1-05 | A08 | Xoá 2 vạch ngang gán nhầm `L1` (một cái vẽ từ xa về gần); vạch dọc xa bên trái đổi `L1` → `L2` |
| QC1-02 | A13 | Thêm `L1 / solid / yellow / single` |
| QC1-11 | B01, B02, B08 (2 vỉa), B09 | `road_curb` từ 3 điểm lên 5–12 điểm theo cung |
| QC1-12 | A16 | Xoá điểm lặp trong polygon `drivable` |

## 5. Kiểm file export
| File | Mở lại được? | Số shape ảnh 1 (job / file) | Số shape ảnh 2 (job / file) | Tag camera có trong XML? |
| --- | --- | --- | --- | --- |
| `trankhanhchi-front.zip` | Có (`road_check lint` đọc được 16 ảnh) | A01: 9 / 9 | A02: 5 / 5 | Có, `<tag label="camera"><attribute name="value">front</attribute></tag>` |
| `trankhanhchi-fisheye.zip` | Có (`road_check lint` đọc được 12 ảnh) | B01: 4 / 4 | B02: 7 / 7 | Có, `value` = `fisheye_front` |

Lệnh kiểm: `python -m road_lab.road_check lint trankhanhchi-front.zip trankhanhchi-fisheye.zip` → `28 ảnh, 4 cảnh báo` (đều là QC1-02 ở A05, A12, A14). Manifest: `contains_images: false` cho cả hai file. Job 26 ở trạng thái **completed** (`images/05-job26-completed.png`); bản sửa đã được upload lên job, A08 trên CVAT có 32 item, khớp file nộp.

## 6. Ảnh chụp màn hình
> Ảnh chụp chứa ảnh BDD100K / WoodScape nên **không đưa vào repo** (`ATTRIBUTION.md`: không phân phối lại ảnh lớp học, không đưa ảnh WoodScape vào repo). Các file ảnh dưới đây được gửi kèm báo cáo qua kênh nộp bài của coach.

1. Tab Labels của project: `images/01-labels.png` *(bổ sung)*
2. Ảnh camera trước đã gán đủ: A08 trên CVAT, 32 item = 28 shape + 4 tag. Có làn L1/L2/R1/R2, vùng lái direct/alternative, ngựa vạn, 12 đèn, 7 biển và 4 tag. `images/02-A08.png`
3. Ảnh fisheye đã gán: B02 (`fisheye_front`). Polygon ngựa vạn và `road_curb` đi theo cung của ảnh fisheye, không gán thân xe. `images/03-B02-fisheye.png`
4. Một đoạn XML có `<polyline label="lane">`:

```xml
<polyline label="lane" source="manual" occluded="0" points="1279.00,708.00;1224.00,693.00;1162.00,678.00;…;450.00,505.00" z_order="0">
  <attribute name="position">R2</attribute>
  <attribute name="style">solid</attribute>
  <attribute name="color">yellow</attribute>
  <attribute name="kind">single</attribute>
</polyline>
```
(A01, mở bằng trình soạn thảo; chụp màn hình đoạn này để nộp.)

## 7. Tự đánh giá
Lỗi bạn mắc nhiều nhất hôm nay (theo mã QC1-xx), và cách tránh ở Ngày 20:  
Nhiều nhất là **QC1-11**: 5 `road_curb` trên fisheye chỉ có 3 điểm, nối gần như thẳng trong khi vỉa trên ảnh cong. Lỗi nặng nhất là ở A08 (**QC1-03 / QC1-05**): vạch ngang bị gán `lane L1`, một vạch còn vẽ từ xa về gần. Cách tránh ở Ngày 20:
- Với fisheye, phóng to và đặt điểm cách nhau khoảng 20–30 px dọc theo cung.
- Trước khi gán lane, tự hỏi "vạch này có chạy dọc theo hướng xe đi không?".
- Chạy `road_check lint` sau mỗi 4 ảnh thay vì chỉ cuối buổi.

Nhãn của bạn đi vào model ở đâu? Chọn một lỗi đã sửa và nói nó làm model học sai thế nào:  
Polyline `lane` được đổi thành đích row-anchor: với mỗi hàng y, model học x của L1/R1. Nếu giữ lỗi ở A08 (vạch ngang gán `L1`), vạch ngang cắt rất nhiều cột trên cùng vài hàng. Đích của L1 ở những hàng đó trở thành một vị trí sai hẳn bên trái, và model học rằng biên trái làn mình có thể nằm ngang. Khi chạy thật, LKA sẽ ước lượng sai vị trí ngang của xe trong làn (lệch tâm làn), dẫn đến đánh lái hiệu chỉnh sai. Vì vậy sai `position` của L1/R1 bị xếp mức nặng. Tương tự, vỉa fisheye chỉ có 3 điểm dạy model rằng mép đường trên ảnh fisheye là đường thẳng, nên ở vòng ngoài ảnh (nơi cong nhất) model đặt mép đường lệch nhiều pixel.

## 8. (Tùy chọn, buffer) Từ polyline đến đích row-anchor
Ảnh A01, vạch R1 (dashed white), tính bằng `python -m road_lab.rowanchor <file> --image A01 --position R1`:

| y | 720 | 680 | 640 | 600 | 560 |
| --- | ---: | ---: | ---: | ---: | ---: |
| x của chúng tôi | không có làn | không có làn | 600,8 | 542,1 | 483,5 |
| x của bạn kia (KieuXuanBac) | không có làn | 659,2 | 600,6 | 542,0 | 483,4 |

Trả lời 3 câu:

1. Polyline R1 của tôi đi từ y=679 (gần) tới y=505 (xa). Dừng sớm 40 px ở đầu xa (kết thúc ở y≈545) thì cả năm hàng 720–560 vẫn giữ nguyên, vì hàng xa nhất là 560 vẫn còn nằm trong polyline. Nếu thiếu 40 px ở đầu gần (bắt đầu ở y≈639), hàng **640** sẽ đổi thành "không có làn" (720 và 680 vốn đã không có).
2. Hàng 720: cả hai đều "không có làn". Hàng 680: tôi "không có làn", bạn kia có x = 659,2, vì điểm đầu của tôi ở y=679, chỉ hụt 1 px so với hàng 680. Hàng 560: lệch 0,1 px. Lệch ở hàng gần xe (720/680) ảnh hưởng LKA nhiều hơn: hàng gần quyết định vị trí ngang hiện tại của xe trong làn, nên thiếu hay lệch điểm ở đó làm sai ngay lệnh giữ làn. Hàng xa chủ yếu ảnh hưởng ước lượng độ cong phía trước.
3. Phép nội suy x theo y không đổi, vì mỗi hàng chỉ cần đoạn polyline cắt qua hàng đó, bất kể thứ tự điểm. Nhưng các bước dựa vào "điểm đầu là điểm gần xe" sẽ gặp khó: `road_check` báo QC1-04 (sai chiều), và những script chuyển nhãn sang định dạng model cần thứ tự điểm (ví dụ lấy điểm đầu làm điểm bắt đầu của làn hoặc nối các đoạn vạch đứt) sẽ đảo ngược làn.
