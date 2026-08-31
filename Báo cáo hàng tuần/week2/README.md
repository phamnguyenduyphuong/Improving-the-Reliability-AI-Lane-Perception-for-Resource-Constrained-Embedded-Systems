# WEEK 2 – Khảo sát nghiên cứu và xác định hướng AI-Based Lane Perception

## 1. Mục tiêu tuần

Từ ý tưởng hệ thống tổng thể của Week 1, Week 2 tập trung thu hẹp bài toán
nghiên cứu và xác định hướng có giá trị học thuật rõ ràng hơn.

Hướng được lựa chọn:

**Cải thiện độ tin cậy của nhận thức làn đường dựa trên AI cho các hệ
thống nhúng hạn chế tài nguyên – Ứng dụng cho robot giao hàng tự hành.**

---

## 2. Vấn đề nghiên cứu

Một hệ thống nhận thức cho robot giao hàng cần xử lý các tình huống:

- vạch làn rõ;
- vạch làn mờ;
- vạch bị che khuất;
- vạch đứt đoạn;
- đường không có vạch rõ ràng;
- phương tiện/vật cản xuất hiện phía trước.

Đồng thời, khi triển khai trên Raspberry Pi hoặc các embedded board có
tài nguyên hạn chế, mô hình phải cân bằng giữa:

- Accuracy
- Reliability
- Latency
- FPS
- CPU usage
- Memory usage
- Power consumption

---

## 3. Các hướng nghiên cứu đã khảo sát

### SCNN – Spatial CNN

Nghiên cứu cách truyền thông tin không gian dọc theo feature map để cải
thiện khả năng nhận diện các cấu trúc lane dài, liên tục hoặc bị gián đoạn.

### DeepDriving

Khảo sát hướng chuyển thông tin thị giác thành các driving affordances
phục vụ điều khiển, thay vì chỉ phát hiện từng đối tượng độc lập.

### YOLOP

Khảo sát kiến trúc multi-task sử dụng một encoder chung và ba nhánh:

1. Traffic Object Detection
2. Drivable Area Segmentation
3. Lane Line Segmentation

Điều này cho thấy khả năng chia sẻ feature giữa nhiều nhiệm vụ perception
thay vì sử dụng ba model hoàn toàn độc lập.

### Các lightweight multi-task models

Tiếp tục khảo sát các kiến trúc gần với mục tiêu đề tài, bao gồm các mô
hình hướng đến sự cân bằng giữa:

- độ chính xác;
- độ nhẹ;
- khả năng xử lý gần thời gian thực.

---

## 4. Kiến thức thu được

Nhóm xác định rằng việc chỉ phát hiện Lane Line chưa đủ cho các đường
thực tế không có vạch rõ ràng.

Do đó hướng perception của đề tài được mở rộng thành:

Camera
   ↓
AI-Based Perception
   ├── Lane Line
   ├── Drivable Area
   └── Vehicle / Obstacle
           ↓
Ego-Lane / Virtual Ego-Lane
           ↓
Center Path
           ↓
Vehicle Controller

Đối với thiết bị nhúng hạn chế tài nguyên, multi-task learning là hướng
phù hợp vì các nhiệm vụ có thể chia sẻ backbone/feature thay vì chạy
nhiều mô hình độc lập.

---

## 5. Kết quả đạt được

Week 2 đã:

- thu hẹp phạm vi nghiên cứu;
- xác định các output perception cần thiết;
- xác định nhóm chỉ số benchmark;
- khảo sát các mô hình nền tảng;
- khảo sát các mô hình multi-task gần với bài toán;
- định hình hướng lightweight perception cho Raspberry Pi;
- xác định TriLiteNet là một baseline phù hợp để bắt đầu triển khai thử nghiệm.

---

## 6. Vấn đề còn mở

Các vấn đề cần thực nghiệm để trả lời:

1. TriLiteNet có đủ nhanh trên Raspberry Pi hay không?
2. Hiệu năng giảm bao nhiêu so với các embedded GPU mạnh hơn?
3. FPS và latency thực tế trên ảnh/video là bao nhiêu?
4. CPU/RAM/power có phù hợp cho chạy lâu dài hay không?
5. Lane + Drivable Area có đủ để xây dựng Ego-Lane hay không?
6. Camera góc rộng ảnh hưởng thế nào đến perception?

---

## 7. Hướng Week 3

Week 3 chuyển từ literature review sang implementation:

- triển khai TriLiteNet;
- chạy ảnh tĩnh;
- chạy video quay sẵn;
- đo latency và FPS;
- theo dõi tài nguyên Raspberry Pi;
- chuẩn bị Camera Module 3 Wide;
- bắt đầu nghiên cứu BEV/Ego-Lane từ output perception.

---

## 8. Tài liệu trong thư mục

- `Advanced_Topics.pptx`
  - Định nghĩa bài toán nghiên cứu.
  - Tổng hợp các bài báo nền tảng.
  - Phân tích các mô hình multi-task.
  - Xác định tiêu chí đánh giá và hướng nghiên cứu.
