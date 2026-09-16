# Báo cáo Ngày 4 - Keypoint & Pose

Họ tên: Nguyễn Đôn Quốc Tuấn   Nhóm: L2-3   Ngày: 16/09/2026

## 1. Nhãn của tôi

<!-- Lấy số từ reports/visibility_report.md hoặc outputs/visibility_report.json sau Chặng 4.
Số ảnh phải là 20; số skeleton là tổng số người trong 20 ảnh. Thời gian trung bình = tổng
thời gian gán / 20. -->

| Chỉ số | Giá trị |
| --- | ---: |
| Số ảnh đã gán | 20 |
| Số skeleton | 29 |
| v=2 / v=1 / v=0 | 339 / 123 / 31 |
| Thời gian trung bình mỗi ảnh | ~2.5 phút |

Ba khớp có `%v=1` cao nhất (chép từ `reports/visibility_report.md`):

1. `left_ear` (59%)
2. `right_ear` (41%)
3. `left_eye` / `right_eye` (34%)

Chúng có đúng là những khớp bạn thấy khó gán nhất không? Nếu không, giải thích.

Không hoàn toàn. Mặc dù tai và mắt có tỷ lệ `%v=1` cao nhất vì vùng đầu người thường bị xoay nghiêng hoặc bị tóc/mũ che khuất, vị trí giải phẫu của chúng vẫn tương đối dễ định vị dựa trên đối xứng khuôn mặt. Ngược lại, các khớp như cổ tay (`wrist`) và hông (`hip`) (đạt 28% `v=1`) mới là những vị trí khó gán nhất trên thực tế do quần áo rộng che mất mốc xương và các cử động tay phức tạp.

## 2. Chấm với gold

<!-- Lấy hai cột từ outputs/eval_vs_gold.json: một lần ngay khi protected release mở và một
lần sau rework. Đếm số phần tử trong từng danh sách lỗi, không tự làm tròn. -->

| Chỉ số | Trước rework | Sau rework |
| --- | ---: | ---: |
| OKS trung bình | *(Chờ protected release)* | *(Chờ protected release)* |
| OKS@0.50 | | |
| OKS@0.75 | | |
| Lỗi `dao_trai_phai` | | |
| Lỗi `nham_nguoi` | | |
| Lỗi `xoa_khop_bi_che` | | |

**Tôi đã sửa gì giữa hai lần chạy** (ghi cụ thể: ảnh nào, người thứ mấy, khớp nào):

<!-- Mỗi dòng phải có: tên ảnh + người thứ mấy + keypoint + thao tác sửa. Không viết “đã sửa
lại một số lỗi”. -->

- *(Điền sau khi đối chiếu kết quả bài chấm)*
-
-

**Lỗi đảo trái/phải của tôi xảy ra ở ảnh nào?** Ảnh đó dễ hay khó? Nếu là ảnh dễ,
bạn nghĩ vì sao mình vẫn sai?

<!-- Nếu không có lỗi, ghi rõ “Không có lỗi đảo trái/phải trong toàn bộ 20 ảnh.” -->
*(Điền sau khi đối chiếu kết quả bài chấm)*

## 3. Kiểm chéo

Bạn cùng nhóm: Đối chiếu bài nhóm L2-3

Khớp lệch `%v=1` nhiều nhất giữa hai bảng đếm:

| Khớp | Bạn | Họ | Lệch | Nguyên nhân (guideline hay gán sai?) |
| --- | ---: | ---: | ---: | --- |
| right_knee | 21% | 0% | 21% | Guideline chưa nói rõ trường hợp quần ống thụng che đầu gối |
| left_wrist | 28% | 0% | 28% | Một bên đánh v=0 khi bị che, một bên ước lượng v=1 |

Luật mới đã bổ sung vào `GUIDELINE_MINI.md` sau khi thống nhất:

<!-- Viết một rule kiểm chứng được: điều kiện nhìn thấy/căn cứ vị trí → chọn v=1 hoặc v=0.
Không chỉ ghi “cẩn thận hơn khi gán”. -->

- Với quần dài ống rộng che lấp đầu gối: ước lượng vị trí đầu gối tại trung điểm giữa hông và mắt cá chân, đánh dấu `v=1` (không đánh `v=0` vì khớp vẫn nằm trong khung hình).

## 4. Model

<!-- Chép số từ outputs/eval_model.json sau Chặng 6. “Chênh” = sau fine-tune trừ baseline;
đây là quan sát trên tập test, không phải chất lượng sản phẩm. -->

| Chỉ số | yolo26n-pose gốc | Sau fine-tune | Chênh |
| --- | ---: | ---: | ---: |
| pose_mAP50 | *(Chờ chạy eval_model)* | | |
| pose_mAP50-95 | | | |
| pose_precision | | | |
| pose_recall | | | |
| box_mAP50-95 | | | |

### Trả lời năm câu hỏi ở cuối notebook

> Mỗi câu cần trỏ tới ảnh/chỉ số cụ thể. Một con số thấp không tự chứng minh nhãn sai;
> kiểm lại bằng bằng chứng thị giác và kết quả gold.

1. `pose_mAP50-95` thay đổi bao nhiêu? Nếu nó giảm, 20 ảnh của bạn dạy được model
   điều gì mà COCO chưa dạy, và nó làm hỏng điều gì?

2. `box_mAP` và `pose_mAP` chênh nhau bao nhiêu? Model tìm *người* dễ hơn hay tìm
   *khớp* dễ hơn? Vì sao?

3. Một ảnh test model đoán sai - gọi tên lỗi theo bốn loại của slide 43
   (lệch nhẹ / đảo trái/phải / nhầm người / trượt hẳn):

4. Ảnh nào có OKS thấp nhất giữa nhãn của bạn và model? Ai đúng, và bạn dựa vào đâu?

5. Ảnh bạn gán tệ nhất có *cũng* là ảnh model đoán tệ nhất không? Nếu có, điều đó
   nói gì về bức ảnh đó?

## 5. Một rule evidence bạn đã dùng

Chọn một keypoint trong ảnh core mà bạn phải quyết định giữa `v=1` và `v=0`. Nêu ảnh, người,
khớp, bằng chứng nhìn thấy và lý do chọn trạng thái đó trong 3-5 câu.

<!-- Cấu trúc gợi ý: (1) train_XX + người thứ mấy + keypoint; (2) căn cứ thị giác như phần cơ
thể liền kề, trang phục hoặc vật che; (3) vì sao khớp còn trong khung (v=1) hay đã ra khỏi
khung (v=0). -->

Tại ảnh `000000000139.jpg`, người thứ 1, khớp `left_ankle`: Bàn chân của đối tượng vẫn nhìn thấy rõ trên sàn nhưng phần cổ chân bị che khuất bởi vật cản phía trước. Dựa vào vị trí cẳng chân bên trên và bàn chân bên dưới, ta có căn cứ thị giác khẳng định khớp cổ chân vẫn nằm trọn trong khung hình. Do đó, tôi chọn trạng thái `v=1` và chấm ước lượng vị trí giải phẫu thay vì chọn `v=0` (vì `v=0` chỉ dành cho khớp nằm ngoài mép ảnh).
