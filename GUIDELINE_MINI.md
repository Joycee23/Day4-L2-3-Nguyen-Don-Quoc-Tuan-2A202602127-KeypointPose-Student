# Mini guideline - nhóm: L2-3  |  người gán: Nguyen Don Quoc Tuan  |  ngày: 2026-09-16

> Điền file này **trong lúc** gán nhãn, không phải sau khi xong. Mỗi lần bạn dừng lại
> hơn 10 giây để phân vân, đó là một dòng phải ghi vào đây.

## 1. Luật bắt buộc (đã thống nhất cả lớp - không sửa)

- Bộ 17 điểm COCO, đúng tên, đúng thứ tự. Lấy từ file `.SVG` chung.
- Mọi người trong ảnh đều có **đủ 17 điểm**. Điểm không dùng được thì gắn cờ, không xoá.
- Trái/phải tính theo **cơ thể người**, không theo bức ảnh.
- Bị che, còn trong khung -> `v = 1`, **vẫn đặt chấm** ở vị trí ước lượng.
- Ra ngoài mép ảnh -> `v = 0`, **không** đặt chấm.
- Không dùng `Hidden` (`h`) - nó không được lưu vào file.

## 2. Luật của nhóm bạn (phải điền)

| Tình huống | Luật nhóm bạn chọn | Vì sao |
| --- | --- | --- |
| Hông của người mặc quần áo dài | Đoán vị trí hông dựa trên tỷ lệ cơ thể và đùi, đánh dấu v=1. | Để đảm bảo cấu trúc xương không bị gãy đoạn lớn. |
| Tai bị tóc hoặc mũ bảo hiểm che một phần | Đánh dấu tại vị trí ước tính tai v=1. | Tai vẫn nằm trong khung hình, model cần học vị trí tương đối. |
| Người bị cắt ở mép ảnh (chỉ thấy từ hông trở lên) | Các điểm ngoài ảnh (chân) đánh v=0. | Tuân thủ luật chung ra ngoài mép ảnh thì v=0. |
| Cổ tay nằm sau tay lái / sau thân mình | Ước lượng vị trí cổ tay dựa trên cẳng tay, đánh v=1. | Cổ tay vẫn nằm trong khung, giữ cấu trúc cánh tay. |
| Hai người chồng lên nhau | Nếu thấy rõ hoặc đoán được vị trí khớp người bị che, đánh v=1. | Tránh nối nhầm sang người khác, model cần phân biệt độ sâu. |
| Người nhỏ đến mức nào thì không gán nữa | Dưới 30x30 pixels. | Model sẽ khó học và dễ bị nhiễu do điểm quá sát nhau. |

Với mỗi luật, chèn **một ảnh mẫu** (screenshot từ CVAT) thay vì chỉ viết một câu.
Slide 12 nói rõ: khớp không có bề mặt nhìn thấy được thì phải có ảnh mẫu, không phải
một câu văn chung chung.

## 3. Ba ca mơ hồ đã gặp (bắt buộc, ghi ít nhất 3)

### Ca 1 - ảnh `000000000139.jpg`, người thứ `1`, khớp `left_ankle`

- Mơ hồ ở chỗ nào: Cổ chân bị che bởi vật cản, nhưng bàn chân lại lộ ra.
- Bạn quyết thế nào: Ước lượng vị trí cổ chân, đánh v=1.
- Vì sao: Do bàn chân lộ ra, cổ chân vẫn có thể xác định được vị trí tương đối.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Nếu đánh v=0, model sẽ không có dữ liệu để học cách suy diễn vị trí cổ chân khi bị che khuất một phần.

### Ca 2 - ảnh `000000000285.jpg`, người thứ `2`, khớp `right_eye`

- Mơ hồ ở chỗ nào: Người quay mặt đi, chỉ nhìn thấy góc nghiêng, không rõ vị trí mắt phải.
- Bạn quyết thế nào: Ước lượng dựa trên mắt trái và tai phải, đánh v=1.
- Vì sao: Mắt phải vẫn nằm trong khung hình (trên đầu người), chỉ bị che.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model có thể dự đoán sai góc xoay của đầu.

### Ca 3 - ảnh `000000000632.jpg`, người thứ `1`, khớp `left_shoulder`

- Mơ hồ ở chỗ nào: Hai người đứng sát nhau, khó phân biệt vai của ai.
- Bạn quyết thế nào: Phân tích dựa trên đường áo và tư thế, đánh dấu cẩn thận vai của người 1 (v=2 nếu thấy rõ).
- Vì sao: Để tránh tình trạng xương kéo dài sang người khác.
- Nếu người khác quyết ngược lại thì model học sai cái gì: Model sẽ học sai cấu trúc, gắn nhầm các phần cơ thể giữa các người khác nhau.

## 4. Sau khi so visibility report với bạn cùng nhóm

- Khớp lệch `%v=1` nhiều nhất: `right_knee` (bạn `12%` / họ `18%`)
- Nguyên nhân là **guideline chưa rõ** hay **một trong hai bên gán sai**: Guideline chưa quy định rõ về trường hợp đầu gối bị quần rộng che lấp hoàn toàn.
- Luật mới bổ sung vào mục 2 sau khi thống nhất: Với quần ống rộng, ước lượng đầu gối ở điểm giữa của hông và mắt cá chân (v=1).
