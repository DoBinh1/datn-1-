# Chẩn đoán hư hỏng hỗn hợp hệ Rotor – Bearing

## 1. Bài toán (Problem Statement)
Trong thực tế công nghiệp, các hư hỏng cơ khí thường xuất hiện đồng thời (lỗi hỗn hợp) và bị che lấp bởi nhiễu môi trường hoặc thay đổi theo tốc độ vận hành. Đồ án tập trung giải quyết việc phân loại chính xác các cụm lỗi: **Lỗi cơ khí (Mechanical Faults)** và **Hư hỏng ổ lăn (Bearing Faults)** xảy ra đồng thời trên cùng một hệ thống.

## 2. Giải pháp kỹ thuật (Methodology)
Đồ án đề xuất quy trình kết hợp giữa kiến thức vật lý (Xử lý tín hiệu) và khả năng tự học đặc trưng (Deep Learning):

### A. Xử lý tín hiệu (Domain Expertise)
Thay vì sử dụng tín hiệu thô, hệ thống thực hiện trích xuất đặc trưng đa miền:
* **Fast Fourier Transform (FFT):** Chuyển sang miền tần số để xác định các thành phần dao động đặc trưng của Rotor.
* **Hilbert Transform (Envelope Analysis):** Giải điều chế tín hiệu để tách biệt các xung va đập cơ khí định kỳ của ổ lăn khỏi các thành phần tần số thấp.

### B. Kiến trúc Mạng Deep Learning
Xây dựng mô hình dựa trên mạng CNN 1D và được lấy cảm hứng từ nghiên cứu *"Multi-head de-noising autoencoder-based multi-task model for fault diagnosis of rolling element bearings under various speed conditions"* :
* **Multi-branch Input:** Tiếp nhận đồng thời hai nhánh dữ liệu (FFT và Envelope) để mô hình có cái nhìn toàn diện về lỗi.
* **CBAM Attention Mechanism:** Cơ chế chú ý giúp mạng tự động tập trung vào các dải tần số nhạy với mỗi loại hư hỏng.
* **Cơ chế chú ý hợp nhất đặc trưng:** Thay vì cộng hoặc nối (concatenate) dữ liệu một cách thụ động, mô hình sử dụng **Cơ chế chú ý (Attention Mechanism)** để tự động đánh giá tầm quan trọng của từng miền đặc trưng. Giúp mô hình tập trung vào nhánh chứa thông tin lỗi rõ ràng nhất tại từng thời điểm, tăng cường khả năng kháng nhiễu và độ chính xác khi các lỗi chồng lấn lên nhau.
* **Bộ phân loại đa nhãn (Multi-label Classifier):** Cho phép mô hình dự đoán độc lập sự tồn tại của từng loại lỗi.



## 3. Kết quả đạt được (Key Results)
* **Độ chính xác:** Đạt hiệu suất vượt trội trong việc tách biệt các lỗi hỗn hợp phức tạp.
* **Độ tin cậy:** Hoạt động ổn định trên tập dữ liệu thực nghiệm với nhiều cấp độ nhiễu (SNR) và dải tốc độ thay đổi từ 600 - 1600 RPM.
