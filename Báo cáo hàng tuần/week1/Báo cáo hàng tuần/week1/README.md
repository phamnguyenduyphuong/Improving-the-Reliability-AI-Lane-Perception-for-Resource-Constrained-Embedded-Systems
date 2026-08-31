# WEEK 1 – Khảo sát và đề xuất hướng đồ án

## 1. Mục tiêu tuần

Mục tiêu của tuần đầu tiên là khảo sát các hướng đề tài phù hợp với ngành
Điện tử – Viễn thông, tập trung vào sự kết hợp giữa:

- Trí tuệ nhân tạo (AI)
- Hệ thống nhúng
- Thị giác máy tính
- Điều khiển
- Robot/xe giao hàng tự hành

Từ quá trình khảo sát, nhóm bước đầu đề xuất mô hình:

**Mô phỏng xe giao hàng tự hành tích hợp AI trên mô hình xe RC tỷ lệ 1/10.**

---

## 2. Công việc đã thực hiện

- Tìm kiếm và đọc các tài liệu, bài báo liên quan đến:
  - xe tự hành;
  - robot giao hàng;
  - nhận diện làn đường;
  - xử lý ảnh trên hệ thống nhúng;
  - điều khiển xe RC.

- Phân tích tính khả thi của đề tài ở quy mô đồ án tốt nghiệp.

- Xây dựng sơ đồ khối ban đầu của hệ thống.

- Xác định sơ bộ các thành phần:
  - Raspberry Pi;
  - camera;
  - ESP32/vi điều khiển;
  - servo lái;
  - ESC và động cơ;
  - cảm biến khoảng cách;
  - giao diện web.

- Xây dựng slide và tài liệu tóm tắt để trình bày ý tưởng ban đầu.

---

## 3. Kiến thức thu được

Nhóm nhận thấy một hệ thống robot giao hàng tự hành không chỉ gồm một
mô hình AI mà bao gồm nhiều khối:

Camera / Sensors
        ↓
Perception
        ↓
Path / Navigation
        ↓
Controller
        ↓
MCU
        ↓
Servo + ESC
        ↓
Vehicle

Trong đó Raspberry Pi phù hợp với xử lý ảnh và AI, trong khi ESP32 hoặc
vi điều khiển phù hợp hơn với các tác vụ điều khiển thời gian thực như
PWM cho servo và ESC.

---

## 4. Kết quả đạt được

Kết quả chính của Week 1 là hình thành được kiến trúc tổng thể ban đầu
và xác định tính khả thi của mô hình xe.

Đề tài được định hướng ở mức proof-of-concept, tập trung vào việc chứng
minh các khối chức năng thay vì xây dựng một xe tự hành thương mại hoàn chỉnh.

Các chức năng được xem xét gồm:

- nhận thức môi trường bằng camera;
- nhận diện làn/vùng đường;
- điều khiển hướng xe;
- tránh vật cản;
- giao tiếp giữa Raspberry Pi và vi điều khiển;
- quản lý quá trình giao/nhận hàng.

---

## 5. Vấn đề và hạn chế nhận thấy

Phạm vi ban đầu của đề tài còn tương đối rộng, bao gồm nhiều khối như:

- AI;
- định vị;
- điều hướng;
- điều khiển;
- IoT;
- cảm biến;
- web;
- cơ cấu giao hàng.

Do đó cần tiếp tục khảo sát tài liệu để xác định phần nghiên cứu chính
có giá trị học thuật rõ ràng và phù hợp với nguồn lực của nhóm.

---

## 6. Hướng thực hiện tiếp theo

Trong Week 2, nhóm tập trung vào:

1. Khảo sát các bài báo nền tảng về lane perception.
2. Tìm hiểu các mô hình AI thực hiện:
   - Lane Detection;
   - Drivable Area Segmentation;
   - Vehicle/Object Detection.
3. Khảo sát các mô hình lightweight dành cho embedded systems.
4. Xác định vấn đề nghiên cứu và hướng cải thiện cụ thể của đề tài.

---

## 7. Tài liệu trong thư mục

- `demo.pptx`  
  Slide trình bày sơ đồ và ý tưởng hệ thống ban đầu.

- `Tóm tắt đề tài.pdf`  
  Tài liệu mô tả mục tiêu, phạm vi, kiến trúc và đánh giá tính khả thi
  của mô hình xe giao hàng tự hành RC 1/10.
