# CSC4005 – Lab 1 Report Template

## 1. Mục tiêu

### 1.1 Mục tiêu bài thực hành
Mục tiêu chính của bài lab này là xây dựng một pipeline huấn luyện hoàn chỉnh cho bài toán phân loại hình ảnh bằng mạng nơ-ron truyền thẳng (MLP). Thay vì tập trung tối ưu hóa điểm số, bài thực hành chú trọng vào việc giúp sinh viên nắm vững quy trình bài bản trong học sâu, bao gồm:

- Xử lý dữ liệu: Chuẩn bị và chuẩn hóa dữ liệu hình ảnh đúng cách.

- Huấn luyện & Đánh giá: Hiểu rõ vai trò của các tập dữ liệu Train, Validation, Test và lựa chọn hàm mất mát (Loss function) phù hợp.

- Kiểm soát mô hình: Theo dõi và xử lý hiện tượng Overfitting và Underfitting thông qua các kỹ thuật Regularization.

- Tối ưu hóa: So sánh hiệu quả của các bộ tối ưu (Optimizer) khác nhau.

- Quản lý thí nghiệm: Sử dụng công cụ Weights & Biases (W&B) để ghi lại toàn bộ quá trình thực nghiệm, từ biểu đồ học tập (Learning curves) đến bảng so sánh cấu hình.

### 1.2 Bộ dữ liệu sử dụng

Bài thực hành sử dụng bộ dữ liệu NEU Surface Defect Database. Đây là bộ dữ liệu thực tế dùng để nhận diện các lỗi trên bề mặt thép, bao gồm 1.800 ảnh được chia thành 06 lớp đối tượng:

- Crazing (Vết nứt bề mặt)

- Inclusion (Tạp chất)

- Patches (Mảng bám)

- Pitted Surface (Bề mặt rỗ)

- Rolled-in Scale (Vảy cán thép)

- Scratches (Vết trầy xước)

## 2. Cấu hình thí nghiệm

Phần này trình bày các thiết lập thông số cho 3 kịch bản huấn luyện khác nhau nhằm so sánh hiệu năng giữa các bộ tối ưu (Optimizer) và mức độ tác động của các kỹ thuật điều chuẩn (Regularization).

### 2.1 Các tham số chung
Tất cả các thí nghiệm đều sử dụng chung các cấu hình nền tảng sau để đảm bảo tính khách quan khi so sánh:
- Dữ liệu: NEU-CLS dataset.
- Kích thước ảnh: 64 x 64 pixels.
- Batch size: 32.
- Số Epoch tối đa: 20.
- Early Stopping: Dừng sớm nếu không cải thiện sau 5 epoch (patience=5).
- Augmentation: Có sử dụng tăng cường dữ liệu.
- Công cụ theo dõi: Weights & Biases (wandb).
### 2.2 Chi tiết các cấu hình chạy (Runs)
Dưới đây là bảng tổng hợp thông số chi tiết cho 3 lần chạy:

Tham số |	Run 1: Baseline (AdamW) |	Run 2: SGD |	Run 3: Strong Reg
---------  | --------- | --------- | ---------
Run Name |	baseline_adamw |	run_b_sgd |	run_c_strong_reg
Optimizer |	AdamW |	SGD |	AdamW
Learning Rate |	0.001 |	0.01 |	0.0005
Weight Decay |	0.0001 |	0.0 |	0.001
Dropout |	0.3 |	0.3 |	0.5

### 2.3 Mô tả mục tiêu từng cấu hình
#### Cấu hình Baseline (baseline_adamw):

- Sử dụng bộ tối ưu AdamW với các tham số tiêu chuẩn.

- Mục tiêu: Thiết lập một mốc hiệu năng cơ bản để so sánh với các thay đổi sau này.

#### Cấu hình So sánh Optimizer (run_b_sgd):

- Thay đổi sang bộ tối ưu SGD với Learning Rate lớn hơn (0.01) và tắt Weight Decay.

- Mục tiêu: Đánh giá tốc độ hội tụ và độ ổn định của SGD so với AdamW trên bài toán phân loại ảnh lỗi thép.

#### Cấu hình Điều chuẩn mạnh (run_c_strong_reg):

- Giảm Learning Rate, tăng Weight Decay lên gấp 10 lần và tăng Dropout lên 0.5.

- Mục tiêu: Quan sát khả năng kiểm soát hiện tượng Overfitting, giúp mô hình tổng quát hóa tốt hơn trên tập Validation và Test.
## 3. Kết quả
Đưa bảng configs → metrics, learning curves và nhận xét.

## 4. Phân tích
- Cấu hình nào tốt nhất?
- Dấu hiệu overfitting / underfitting là gì?
- AdamW và SGD khác nhau ra sao trong thí nghiệm của bạn?

## 5. Kết luận
Chọn best config và nêu lý do.
