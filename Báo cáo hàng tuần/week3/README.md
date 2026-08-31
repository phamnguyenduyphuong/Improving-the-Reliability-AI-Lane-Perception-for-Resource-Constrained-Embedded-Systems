# WEEK 3 – Triển khai TriLiteNet và benchmark bước đầu trên Raspberry Pi

## 1. Mục tiêu tuần

Week 3 chuyển từ khảo sát lý thuyết sang thực nghiệm.

Các mục tiêu chính:

1. Triển khai TriLiteNet Tiny trên Raspberry Pi.
2. Kiểm tra inference trên ảnh tĩnh.
3. Kiểm tra inference trên video quay sẵn.
4. Đo latency và FPS ban đầu.
5. Quan sát khả năng triển khai trên thiết bị hạn chế tài nguyên.
6. Chuẩn bị Camera Module 3 Wide cho giai đoạn realtime.
7. Bắt đầu khảo sát phương pháp xây dựng Ego-Lane từ output perception.

---

## 2. Mô hình thử nghiệm

Baseline:

**TriLiteNet Tiny**

Các output chính:

- Vehicle Detection
- Drivable Area Segmentation
- Lane Line Segmentation

Input thử nghiệm:

**416 × 416**

Thiết bị chính:

- Raspberry Pi 4
- Raspberry Pi 3B+
- Camera Module 3 Wide – giai đoạn kiểm tra camera

---

## 3. Kết quả triển khai ban đầu

### Raspberry Pi 4

TriLiteNet Tiny đã chạy được trên Raspberry Pi 4 bằng CPU.

Kết quả inference ban đầu:

| Chỉ số | Giá trị sơ bộ |
|--------|---------------|
| Input | 416 × 416 |
| Inference latency | ~241 ms/frame |
| Inference FPS | ~4.15 FPS |
| Video pipeline | ~2.77 FPS |
| Accelerator | Không |
| Processing | CPU |

Model tạo được ba output:

- Vehicle Detection
- Drivable Area
- Lane Line

Các số liệu trên hiện được xem là **preliminary benchmark** và sẽ được
đo lại theo cùng một protocol ở các tuần tiếp theo.

---

### Raspberry Pi 3B+

TriLiteNet Tiny cũng đã chạy forward thành công trên Raspberry Pi 3B+.

Kết quả ban đầu:

- Input: 416 × 416
- Forward time: khoảng 1.223 s
- Drivable Area output: [1, 2, 416, 416]
- Lane Line output: [1, 2, 416, 416]

Kết quả cho thấy model có khả năng chạy trên board tài nguyên thấp hơn,
nhưng latency lớn hơn đáng kể so với Raspberry Pi 4.

---

## 4. Camera Module 3 Wide

Camera Module 3 Wide được lựa chọn để phục vụ giai đoạn realtime.

Trong Week 3, camera được kiểm tra riêng về:

- khả năng hoạt động với Raspberry Pi;
- độ phân giải;
- frame rate;
- góc nhìn rộng;
- khả năng sử dụng làm nguồn video cho perception.

**TriLiteNet realtime với Camera Module 3 Wide chưa được xem là kết quả
hoàn chỉnh trong tuần này.**

Mục tiêu trước tiên là xác định camera hoạt động ổn định trước khi ghép
với pipeline AI.

---

## 5. Ego-Lane / BEV

Bên cạnh inference, nhóm bắt đầu khảo sát bước hậu xử lý:

Lane / Drivable Area
        ↓
BEV / IPM
        ↓
Ego-Lane
        ↓
Center Path
        ↓
Controller

Bước thử nghiệm ban đầu đã xem xét:

- chuyển ảnh sang Bird's-Eye View;
- sử dụng thông tin lane/drivable area;
- xác định vùng di chuyển của xe;
- xây dựng ý tưởng Ego-Lane bên phải;
- chuẩn bị cho Center Path.

Phần này hiện là **work in progress**, chưa phải thuật toán điều khiển xe
hoàn chỉnh.

---

## 6. Vấn đề gặp phải

### 6.1 Hiệu năng trên CPU

TriLiteNet có thể chạy trên Raspberry Pi nhưng tốc độ thấp hơn các nền
tảng có GPU/accelerator.

Do đó cần tiếp tục đánh giá:

- inference latency;
- end-to-end latency;
- FPS;
- CPU;
- RAM;
- nhiệt độ;
- power consumption.

### 6.2 Benchmark chưa chuẩn hóa hoàn toàn

FPS inference và FPS của toàn bộ video pipeline không giống nhau.

Cần tách rõ:

Model inference time
        ≠
Total system latency

Total pipeline còn bao gồm:

- đọc frame;
- resize/pre-processing;
- inference;
- post-processing;
- visualization;
- ghi/hiển thị output.

### 6.3 Thiết lập remote Raspberry Pi

Trong quá trình thử nghiệm có vấn đề về độ ổn định khi truy cập Raspberry
Pi từ xa.

Giải pháp hiện tại tách:

- Ethernet trực tiếp Laptop ↔ Raspberry Pi cho PuTTY/VNC;
- Wi-Fi cho Internet/download.

Điều này giúp tránh nhầm lẫn giữa lỗi mạng và lỗi inference khi benchmark.

---

## 7. Đánh giá sơ bộ

Kết quả Week 3 chứng minh bước đầu rằng TriLiteNet Tiny có thể triển khai
trên Raspberry Pi mà không cần GPU rời.

Tuy nhiên, việc model "chạy được" chưa đủ để kết luận model "phù hợp".

Cần tiếp tục đánh giá đồng thời:

Accuracy / Reliability
        +
Latency / FPS
        +
CPU / RAM
        +
Power
        +
Stability

Đây sẽ là cơ sở để đánh giá tính phù hợp của lightweight AI perception
trên resource-constrained embedded systems.

---

## 8. Hướng Week 4

Các công việc tiếp theo:

1. Chuẩn hóa benchmark.
2. Đo CPU và RAM trong quá trình inference.
3. Đo nhiệt độ và kiểm tra throttling.
4. Kiểm tra video dài hơn để đánh giá độ ổn định.
5. Triển khai camera realtime.
6. So sánh Raspberry Pi 3B+ và Raspberry Pi 4.
7. Tiếp tục Ego-Lane / Virtual Ego-Lane.
8. Xây dựng Center Path.
9. Chuẩn bị giao tiếp controller → ESP32 → servo.

---

## 9. Files / Evidence

Nên bổ sung vào thư mục này:

- ảnh input;
- ảnh output TriLiteNet;
- video output;
- screenshot Terminal;
- benchmark CSV;
- cấu hình Raspberry Pi;
- Camera Module 3 Wide test;
- BEV/Ego-Lane result;
- Week3 slide.
