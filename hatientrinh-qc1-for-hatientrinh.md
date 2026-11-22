# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Hà Tiến Trịnh (tự kiểm lô của mình)        Người kiểm (học viên): Hà Tiến Trịnh (2A202603154)  
Ngày: 21/11/2026                          Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): hatientrinh-front.zip, hatientrinh-fisheye.zip, revision 1  
Số ảnh kiểm: 6 (+ 0 ảnh thêm, ghi riêng)   Số nhãn đã kiểm (shape + tag): 90 (66 shape + 24 tag)  

## Ảnh đã kiểm
| Ảnh | Camera | Số shape | Số tag | Kết quả |
| --- | --- | ---: | ---: | --- |
| A01 | front | 11 | 4 | không lỗi |
| A04 | front | 14 | 4 | không lỗi |
| A07 | front | 12 | 4 | có lỗi (vùng lái khoét quanh xe phía trước) |
| A09 | front | 10 | 4 | có lỗi (R1 quá ngắn) |
| B03 | fisheye_rear | 14 | 4 | không lỗi |
| B06 | fisheye_left | 5 | 4 | không lỗi |
| **Tổng** |  | 66 | 24 | 90 nhãn |

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 6 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 10 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 20 | 0 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 20 | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 6 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 20 | 0 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 19 | 1 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 24 | 0 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 16 | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 19 | 0 | chính |
| QC1-12 file | lỗi file | 2 | 0 | nhẹ / nặng |

Cách đếm số mục kiểm:
- QC1-01: 1 tag camera mỗi ảnh.
- QC1-02: L1 + R1 trên 4 ảnh front và B03 (fisheye_rear). Không tính B06 vì camera hai bên không dùng L1/R1.
- QC1-03, QC1-04, QC1-06: số polyline `lane`.
- QC1-05: số vạch đứt.
- QC1-07: `drivable` + `crosswalk` trên cả 6 ảnh, cộng `road_curb` trên ảnh front.
- QC1-08: số box đèn. QC1-09: đèn + biển. QC1-10: số biển.
- QC1-11: mọi shape trên B03 và B06.
- QC1-12: 2 file zip.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A09 | lane #4, R1, điểm đầu (1111,597) | chính | Chỉ 2 điểm, đoạn quá ngắn: điểm đầu chưa sát xe (vạch còn thấy tới mép phải ảnh, khoảng y ≈ 655) và dừng sớm ở (975,530) trong khi vạch còn thấy tới khoảng (790,440). |
| 2 | QC1-07 | A07 | drivable #11, direct, điểm đầu (1,583) | chính | Polygon khoét vùng quanh xe phía trước: dừng ở đuôi xe (y ≈ 405, x 437–720), bỏ phần làn phía sau xe. Guideline yêu cầu gán vùng lái như khi đường trống, không khoét quanh xe khác. |

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A09 | Vạch R1 sát lề phải trông hơi ngả vàng. Nên ghi `color = yellow` hay `white`? (đang ghi white) |  |
| B03 | Ở `fisheye_rear`, L1/R1 tính theo hướng xe (vạch bên phải ảnh là bên trái xe, nên là L1) hay theo hướng ảnh? Hiện đang theo hướng xe. | Đã có câu trả lời trong guideline mục 3: "position tính theo làn đang đi: L1 và R1 là hai vạch sát xe", tức là tính theo hướng xe. Cách gán hiện tại đúng, không có lỗi. |

Ghi chú: vạch đôi ở A04 (vàng đôi) và A09 (trắng đôi) được vẽ thành hai polyline, mỗi polyline trên một nửa vạch, `kind = double`. Coach hướng dẫn như vậy, nên không tính là lỗi QC1-03 hay QC1-04. Cách đặt `position` nhất quán: nửa gần xe lấy vị trí kế tiếp, nửa ngoài lấy vị trí sau đó, hoặc `other` khi hết vị trí.

## Quyết định
Lỗi nặng: 0   Lỗi chính: 2 / 90 nhãn = 2,2 %   Lỗi nhẹ: 0   Ca chờ lead: 1 (A09, không ảnh hưởng kết luận)  
Quyết định (Release / Hold / Rework): **Release**  
Lý do (theo luật của phiếu): Không có lỗi nặng. Tỉ lệ lỗi chính là 2,2 %, không vượt 5 %. Ca B03 đã có câu trả lời trong guideline. Ca A09 (màu R1) chưa có lời đáp, nhưng không đổi kết luận: nếu tính thêm một lỗi chính thì tỉ lệ là 3/90 = 3,3 %, vẫn ≤ 5 %. Vì vậy không cần Hold, quyết định là Release.
Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](docs/qc_severity_road_v1.0.md).
