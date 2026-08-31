# Cải thiện độ tin cậy của nhận thức làn đường bằng AI cho các hệ thống nhúng hạn chế tài nguyên

**Ứng dụng cho robot giao hàng tự hành**

## Giới thiệu

Đây là repository phục vụ cho đồ án tốt nghiệp của nhóm mình.

Mục tiêu chính của đề tài là nghiên cứu cách triển khai các mô hình AI nhận thức làn đường trên những thiết bị nhúng có tài nguyên hạn chế như Raspberry Pi 3B+ và Raspberry Pi 4, sau đó đánh giá khả năng chạy thực tế về tốc độ xử lí, độ ổn định, mức sử dụng tài nguyên và điện năng.

Ngoài việc nhận diện vạch làn, nhóm cũng tìm giải pháp cho các trường hợp đường thực tế không có vạch kẻ rõ ràng đặc biệt là đường ở Việt Nam. Vì vậy đề tài hướng đến việc kết hợp Drivable Area và Ego-Lane / Virtual Ego-Lane để giúp xe xác định phần đường phù hợp để di chuyển.

## Mục tiêu chính

- Triển khai mô hình AI nhẹ trên các thiết bị nhúng.
- Nhận diện:
  - làn đường;
  - vùng có thể di chuyển;
  - phương tiện phía trước.
- Giảm sự phụ thuộc hoàn toàn vào vạch kẻ đường.
- Xác định Ego-Lane hoặc vùng di chuyển phù hợp cho xe.
- Thử nghiệm trên đường có vạch và đường không có vạch.
- So sánh hiệu năng giữa các board khác nhau.
- Đánh giá:
  + FPS;
  + độ trễ;
  + CPU;
  + RAM;
  + công suất tiêu thụ;
  + độ ổn định của kết quả.
- Ứng dụng kết quả nhận thức lên mô hình xe RC 1/10 phục vụ bài toán robot giao hàng tự hành.

## Mô hình đang sử dụng

Hiện tại nhóm đang sử dụng **TriLiteNet Tiny** làm mô hình baseline.

TriLiteNet cho phép thực hiện đồng thời ba nhiệm vụ:
      -> Phát hiện phương tiện
      -> Phân vùng Drivable Area
      -> Phân vùng Lane

## Phần cứng dự kiến

- Raspberry Pi 3B+
- Raspberry Pi 4
- Camera Raspberry Pi
- ESP32 hoặc vi điều khiển tương đương
- Servo lái
- ESC + động cơ
- LiDAR hoặc cảm biến khoảng cách

## Hướng đánh giá

Nhóm không chỉ so sánh FPS, mà còn quan tâm đến sự đánh đổi giữa:

```text
Tốc độ
+
Độ ổn định
+
Độ tin cậy
+
Tài nguyên sử dụng
+
Công suất tiêu thụ
```
