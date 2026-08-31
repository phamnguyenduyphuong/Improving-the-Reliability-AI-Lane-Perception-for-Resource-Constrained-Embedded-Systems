# WEEK 1 – Khảo sát và đề xuất hướng đồ án

## 1. Mục tiêu tuần

Trong tuần đầu tiên, nhóm tập trung khảo sát và lựa chọn hướng đề tài
phù hợp với chuyên ngành Điện tử – Viễn thông, có sự kết hợp giữa:

- Trí tuệ nhân tạo (AI)
- Hệ thống nhúng
- Thị giác máy tính
- Điều khiển
- Robot/xe giao hàng tự hành

Từ quá trình khảo sát, nhóm bước đầu đề xuất mô hình:

**Mô phỏng xe giao hàng tự hành tích hợp AI trên mô hình xe RC tỷ lệ 1/10.**

---

## 2. Công việc đã thực hiện

Trong Week 1, nhóm đã thực hiện:

- Tìm kiếm và đọc các tài liệu, bài báo liên quan đến:
  - xe tự hành;
  - robot giao hàng tự hành;
  - nhận diện làn đường;
  - xử lý ảnh;
  - hệ thống nhúng;
  - điều khiển xe RC.

- Khảo sát tính khả thi của việc xây dựng mô hình xe giao hàng tự hành
  ở quy mô đồ án tốt nghiệp.

- Xây dựng sơ đồ tổng quát của hệ thống.

- Xác định sơ bộ các thành phần phần cứng:
  - Raspberry Pi;
  - Camera;
  - ESP32 / vi điều khiển;
  - Servo lái;
  - ESC;
  - Động cơ;
  - Cảm biến khoảng cách.

- Xây dựng slide và tài liệu tóm tắt để trình bày ý tưởng ban đầu.

---

## 3. Kiến thức và hướng hệ thống ban đầu

Qua quá trình khảo sát, nhóm nhận thấy một hệ thống xe/robot tự hành
không chỉ sử dụng một thuật toán AI duy nhất mà gồm nhiều khối chức năng.

Kiến trúc sơ bộ:

```text
Camera / Sensors
       ↓
AI / Perception
       ↓
Lane / Drivable Area / Object
       ↓
Path / Navigation
       ↓
Controller
       ↓
Raspberry Pi
       ↓
ESP32 / MCU
       ↓
Servo + ESC
       ↓
RC Vehicle
