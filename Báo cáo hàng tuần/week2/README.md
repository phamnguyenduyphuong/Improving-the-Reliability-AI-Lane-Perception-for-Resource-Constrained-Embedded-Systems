# WEEK 2 – Related work

## 1. Mục tiêu tuần

Hướng nghiên cứu được lựa chọn:

**Cải thiện độ tin cậy của nhận thức làn đường dựa trên AI cho các hệ
thống nhúng hạn chế tài nguyên – Ứng dụng cho robot giao hàng tự hành.**

Các mục tiêu chính trong tuần:

- Khảo sát các bài báo nền tảng về Lane Detection và Autonomous Driving Perception.
- Tìm hiểu các kiến trúc Multi-Task Perception.
- Khảo sát các phương pháp Lane Detection hướng đến tốc độ và chi phí tính toán thấp.
- Khảo sát các phương pháp xử lý lane bị che khuất, mờ hoặc thiếu lane feature.
- Tìm các mô hình phù hợp với Resource-Constrained Embedded Systems.
- Xác định mô hình baseline và hướng triển khai thực nghiệm cho các tuần tiếp theo.

---

## 2. Vấn đề nghiên cứu

Nhận thức làn đường trong môi trường thực tế không chỉ đơn giản là phát hiện
vạch kẻ rõ ràng.

Hệ thống cần xem xét các trường hợp:

- Vạch làn rõ.
- Vạch làn mờ.
- Vạch làn bị che khuất bởi phương tiện.
- Vạch làn bị đứt đoạn.
- Ánh sáng yếu, bóng đổ hoặc ánh sáng chói.
- Giao lộ hoặc cấu trúc lane phức tạp.
- Đường có rất ít hoặc gần như không còn lane feature.
- Phương tiện hoặc vật cản xuất hiện trong vùng di chuyển.

Ngoài độ chính xác, khi triển khai trên các thiết bị nhúng hạn chế tài nguyên
như Raspberry Pi, hệ thống còn cần cân bằng giữa:

- Accuracy
- Reliability
- Latency
- FPS
- CPU usage
- Memory usage
- Power consumption
- Model complexity

Do đó, bài toán của đề tài không chỉ là:

> **Phát hiện lane chính xác**

mà còn là:

> **Duy trì khả năng nhận thức làn đường với chi phí tính toán phù hợp trên
> các hệ thống nhúng hạn chế tài nguyên.**

---

## 3. Các hướng nghiên cứu đã khảo sát

### 3.1. SCNN – Spatial CNN

SCNN tập trung cải thiện khả năng phát hiện các cấu trúc lane dài và liên tục.

Thay vì chỉ sử dụng convolution truyền thống, SCNN truyền thông tin dọc theo
các hàng và cột của feature map.

Điều này giúp mô hình khai thác quan hệ không gian giữa các phần của lane,
đặc biệt trong các trường hợp:

- lane bị che khuất;
- lane bị đứt đoạn;
- điều kiện ánh sáng phức tạp.

SCNN cho thấy việc khai thác **spatial context** có thể cải thiện độ tin cậy
của Lane Detection.

Tuy nhiên, mô hình chủ yếu tập trung vào Lane Detection và chưa giải quyết
đồng thời Drivable Area, Vehicle Detection hoặc Ego-Lane.

---

### 3.2. DeepDriving

DeepDriving khảo sát hướng chuyển thông tin thị giác thành các
**driving affordances** phục vụ controller.

Thay vì chỉ phát hiện từng đối tượng riêng biệt, hệ thống có thể ước lượng:

- góc của xe so với hướng đường;
- khoảng cách tới lane markings;
- khoảng cách tới xe phía trước;
- thông tin về lane hiện tại và lane bên cạnh.

Nghiên cứu này cho thấy perception cần tạo ra thông tin có ý nghĩa trực tiếp
đối với quá trình điều khiển xe.

Tuy nhiên, các hệ thống perception đầy đủ có thể trở nên phức tạp khi phải
kết hợp nhiều nguồn dữ liệu và nhiều mô hình riêng biệt.

---

### 3.3. YOLOP – Multi-Task Driving Perception

YOLOP là một hướng quan trọng vì thực hiện đồng thời ba nhiệm vụ:

1. Traffic Object Detection
2. Drivable Area Segmentation
3. Lane Line Segmentation

Kiến trúc sử dụng một encoder chung để trích xuất feature, sau đó chia thành
các nhánh xử lý cho từng nhiệm vụ.

Ý tưởng quan trọng thu được:

> **Các nhiệm vụ perception có thể chia sẻ feature thay vì sử dụng nhiều
> mô hình độc lập.**

Điều này giúp giảm tính toán lặp lại và tạo ra perception tổng hợp cho hệ thống
tự hành.

---

### 3.4. A-YOLOM

A-YOLOM tiếp tục hướng Multi-Task Perception với ba yêu cầu:

- High Precision
- Lightweight
- Real-Time

Các output chính:

- Object Detection
- Drivable Area Segmentation
- Lane Line Segmentation

Mô hình sử dụng backbone chung và các nhánh detection / segmentation.

Một điểm đáng chú ý là **Adaptive Concatenate**, được sử dụng để lựa chọn
và kết hợp feature phù hợp cho từng nhiệm vụ segmentation.

Qua A-YOLOM, nhóm nhận thấy việc tối ưu cách sử dụng và kết hợp feature
có vai trò quan trọng trong việc cân bằng giữa:

- độ chính xác;
- tốc độ;
- chi phí tính toán.

---

### 3.5. HybridNets

HybridNets cũng giải quyết đồng thời:

- Traffic Object Detection
- Drivable Area Segmentation
- Lane Line Segmentation

Kiến trúc sử dụng:

- EfficientNet-B3 làm backbone;
- BiFPN để kết hợp feature đa tỉ lệ;
- Detection Head;
- Segmentation Head.

BiFPN cho phép kết hợp feature theo cả hai hướng:

- Top-down
- Bottom-up

nhằm khai thác đồng thời:

- thông tin ngữ nghĩa từ feature sâu;
- thông tin chi tiết từ các feature có độ phân giải cao hơn.

HybridNets cho thấy lợi ích của **multi-scale feature fusion** đối với các
đối tượng có kích thước khác nhau.

Tuy nhiên, một số hạn chế vẫn tồn tại:

- lane line có thể bị gián đoạn tại giao lộ;
- drivable area có thể bị dự đoán sang phần đường khác;
- chưa xác định trực tiếp Ego-Lane.

---

### 3.6. Row-Based Lane Detection

Một hướng khác nhằm giảm chi phí của dense segmentation là
**Row-Based Selection**.

Thay vì phân loại gần như toàn bộ pixel của ảnh, phương pháp:

1. Chọn trước một số Row Anchors.
2. Chia mỗi hàng thành các grid cell.
3. Với mỗi lane, chỉ dự đoán vị trí grid cell chứa lane.

Cách biểu diễn này giảm đáng kể số lượng phép phân loại so với
pixel-wise segmentation.

Ngoài ra, các phương pháp theo hướng này còn sử dụng:

- Global Features;
- Structural Loss;
- Auxiliary Segmentation trong quá trình training.

Ưu điểm:

- tốc độ cao;
- giảm chi phí tính toán;
- phù hợp với Lane Detection.

Hạn chế:

- hiệu quả giảm khi lane gần như không còn tồn tại;
- gặp khó khăn tại giao lộ hoặc điều kiện ánh sáng phức tạp;
- chỉ tập trung vào Lane Detection;
- chưa có Drivable Area, Vehicle Detection hoặc Ego-Lane.

---

### 3.7. LaneATT

LaneATT sử dụng **anchor-based lane representation** kết hợp attention.

Các bước chính:

1. Backbone tạo feature map.
2. Anchor-based feature pooling lấy feature dọc theo hình dạng lane giả định.
3. Attention cho phép các anchor trao đổi thông tin với nhau.
4. Mỗi anchor dự đoán xác suất lane và hình dạng lane.
5. NMS loại bỏ các proposal trùng nhau.

Điểm quan trọng:

> **Thông tin từ các lane khác có thể hỗ trợ suy luận lane bị che hoặc thiếu.**

LaneATT-ResNet18 là cấu hình đáng chú ý cho nghiên cứu hệ thống hạn chế
tài nguyên do sử dụng backbone nhẹ hơn các phiên bản lớn.

Tuy nhiên:

- tốc độ được báo cáo trên GPU;
- chưa có benchmark trực tiếp trên Raspberry Pi;
- chưa báo cáo RAM, power hoặc INT8;
- NMS vẫn là một thành phần hậu xử lý có chi phí.

---

### 3.8. CondLaneNet

CondLaneNet tập trung xử lý các trường hợp:

- nhiều lane nằm gần nhau;
- lane phân nhánh;
- topology phức tạp.

Phương pháp sử dụng cách tiếp cận:

> **Phát hiện lane instance trước → sinh kernel riêng → dự đoán hình dạng lane.**

Các thành phần chính gồm:

- Backbone + Transformer;
- Proposal Head;
- Dynamic Kernel;
- Row-Wise Lane Formulation;
- Offset Refinement;
- Recurrent Instance Module.

CondLaneNet-Small sử dụng ResNet-18 và là cấu hình đáng khảo sát hơn đối
với môi trường hạn chế tài nguyên.

Tuy nhiên:

- benchmark tốc độ được thực hiện trên GPU;
- chưa đánh giá trực tiếp trên embedded hardware;
- chưa có thông tin đầy đủ về RAM, power hoặc quantization;
- Dynamic Kernel và Transformer có thể ảnh hưởng tới khả năng triển khai.

---

### 3.9. Map-Enhanced Ego-Lane Detection

Một vấn đề quan trọng được phát hiện trong quá trình khảo sát là:

> **Các phương pháp dựa hoàn toàn vào camera có thể thất bại khi lane feature
> gần như biến mất.**

Map-Enhanced Ego-Lane Detection giải quyết vấn đề này bằng cách kết hợp:

- Camera;
- LiDAR;
- OpenStreetMap;
- Search-Based Optimization.

Khi lane feature bị thiếu, hình dạng đường từ bản đồ được sử dụng làm thông
tin tham chiếu để hỗ trợ ước lượng:

- biên trái Ego-Lane;
- biên phải Ego-Lane;
- vùng Ego-Lane của xe.

Kết quả cho thấy hướng này có khả năng duy trì Ego-Lane trong các trường hợp:

- lane bị mòn;
- lane bị che;
- tunnel;
- vùng quá tối hoặc quá sáng;
- lane feature gần như biến mất.

Tuy nhiên, hệ thống có các hạn chế:

- phụ thuộc vào map;
- phụ thuộc vào độ chính xác vị trí xe;
- sử dụng nhiều nguồn cảm biến;
- hệ thống phức tạp hơn;
- chưa được kiểm chứng đầy đủ trên nhiều loại đường phức tạp.

Điều này cho thấy khả năng cải thiện reliability thường đi kèm với
**tăng độ phức tạp hệ thống**.

---

### 3.10. TriLiteNet

TriLiteNet được khảo sát như một mô hình gần với mục tiêu triển khai của đề tài.

Mô hình thực hiện đồng thời:

- Vehicle Detection
- Drivable Area Segmentation
- Lane Line Segmentation

