# CS114 - Nhận diện rác thải sinh hoạt
## Danh sách thành viên
| STT | Họ và tên | MSSV | Email |
|-----|-------|------|-------|
| 1 | [Phạm Thiện Bảo] (https://github.com/beetibao)| 20521107 | 20521107@gm.uit.edu.vn |
| 2 | [Lê Văn Khoa] (https://github.com/Levankhoa150102) | 20521467 | 20521467@gm.uit.edu.vn |
| 3 | [Lê Nguyễn Tiến Đạt] (https://github.com/lenguyentiendat) | 20521167 | 20521167@gm.uit.edu.vn |

## Giới thiệu đề tài
- Cuộc sống đang ngày càng phát triển hiện đại, đời sống vật chất và tinh thần của người dân được cải thiện rõ rệt. Tuy nhiên, đối lập với nó, tình trạng ô nhiễm môi trường lại có những diễn biến phức tạp và là một vấn đề cấp bách cần phải giải quyết kịp thời. Trong năm 2021, thế giới thải ra 353 triệu tấn rác thải nhựa nhưng lượng rác được tái chế chỉ đạt 9%. Việt Nam nằm trong số 20 quốc gia có lượng rác thải lớn nhất và cao hơn mức trung bình của thế giới. Riêng tại Việt Nam, trung bình mỗi năm lượng rác thải nhựa khoảng 1,8 triệu tấn. Trên thế giới, chỉ có khoảng 19% số rác được tiêu hủy và chỉ gần 50% được chôn lấp tại các hố rác đủ tiêu chuẩn. 
- Từ việc nhận thức sai lầm rằng rác thải sẽ do bên đơn vị thu gom rác xử lý và không có nghĩa vụ phải phân loại chúng dẫn đến việc lượng rác thải gây hại cho môi trường ngày càng tăng, ảnh hưởng vô cùng lớn đến sức khoẻ của con người. Chính vì thế, cần phải có một công cụ hỗ trợ phân loại rác để để giảm bớt chi phí cho các nhà máy tái chế, giúp thu gom và phân loại rác từ lúc chúng vừa mới được vứt bỏ. 
- *"Nhận diện rác thải sinh hoạt"* là bài toán áp dụng mô hình Object Detection, nhằm giúp nhận biết tên loại rác thải sinh hoạt từ đó hỗ trợ trong việc phân loại chúng vào nhóm rác tái chế và không tái chế được. Ngoài ra, bài toán còn giúp thống kê các loại rác thải ra môi trường mỗi ngày ở nơi công cộng mà chưa qua xử lý ở địa phương, từ đó có biện pháp giải quyết ô nhiễm.
- Ngữ cảnh ứng dụng: Tích hợp hệ thống vào con robot đi gom rác kết hợp phân loại ở các nơi công cộng như công viên, trường học, khu dân cư hay cống rãnh, ven biển và cả dưới đại dương.

## Mô tả bài toán
- Input: Một ảnh màu được chụp bằng máy ảnh hoặc điện thoại có hướng từ trên xuống, góc chụp cách mặt đất khoảng 1m, ánh sáng đủ để nhìn rõ, bao gồm một hoặc nhiều loại rác thải không xếp chồng lên nhau.
- Output: Là bức ảnh từ input nhưng có các đường viền vuông bao quanh các rác thải nhận diện được và ô vuông đó gán nhãn tên rác thải.

## Đánh giá
Để đánh giá model Object detection người ta sử dụng các thông số như IoU, AP, mAP,….
- Intersection over Union (IoU) là một số liệu đánh giá được sử dụng để đo độ chính xác trong bài toán phát hiện đối tượng trên một tập dữ liệu cụ thể. Nó sử dụng trong việc đánh giá xem bounding box dự đoán đối tượng khớp với ground truth thật của đối tượng hay không. Chỉ số IoU trong khoảng [0,1] và nếu IoU càng gần 1 thì bounding box dự đoán càng gần ground truth.
<img src="https://929687.smushcdn.com/2633864/wp-content/uploads/2016/09/iou_equation.png?lossy=1&strip=1&webp=1">

## Dataset
### Cách xây dựng
Do các dữ liệu có sẵn trên mạng không đáp ứng được ngữ cảnh của bài toán như: background xung quanh, các rác thải không phải ở Việt Nam, rác thải chụp sát…
Việc tự thu thập dữ liệu giúp kiểm soát được các yếu tố ngoại cảnh như góc quay, ánh sáng, khung cảnh... Do vậy, chúng tôi đã đưa ra các tiêu chí để thu thập dữ liệu như sau: 
- Kích thước hình tối thiểu 918 x 1224 → 4000x3000
- Vật thể: 
 - Các rác thải sinh hoạt: lon, chai, bao nilon, ly nhựa, hộp xốp, chai thủy tinh...
 - Các rác thải trên có thể bị biến dạng, không xếp chồng lên nhau, nằm ngang hoặc đứng.
- Độ sáng: Trời sáng, ánh sáng đủ để nhìn thấy rõ vật thể, không bị chói.
- Background: Nền gạch đường, bãi lá khô, nền cỏ, ven mép đường, dưới gốc cây…
- Góc chụp: hướng nhìn từ trên xuống, cách vật thể khoảng 1m, góc camera 45 - 90 độ.
Link dataset: [Trash_Dataset](https://drive.google.com/drive/folders/1--Qa6LCG188SyTX5cwfzCBE9V1-eYBOB?usp=sharing)

## Mô tả về thuật toán máy học
- Vài năm trở lại đây, object detection là một trong những đề tài quan trọng bởi khả năng ứng dụng cao, dữ liệu dễ chuẩn bị và kết quả ứng dụng rất nhiều. Các thuật toán mới của object detection có thể thực hiện được các tác vụ dường như là real time, thậm chí là nhanh hơn so với con người mà độ chính xác không giảm. Trong đó, YOLO - You Only Look Once có thể không phải là thuật toán tốt nhất nhưng nó là thuật toán nhanh nhất trong các lớp mô hình object detection. Các phiên bản của mô hình này đều có những cải tiến rất đáng kể sau mỗi phiên bản. Chính vì vậy, nhóm thử nghiệm chọn Yolov5 để thực hiện đồ án.
- Yolov5 là sản phẩm của tác giả Glenn Jocher - nhà nghiên cứu, giám đốc điều hành của Ultralystic. Đây là tổ chức hướng tới việc giúp cho người học AI nói chung và những người đam mê công nghệ nói riêng có thể tiếp cận với các mô hình máy học một cách đơn giản, hiệu quả và trực quan hơn.
Ta sử dụng train model theo hướng dẫn của nhà phát hành Yolov5: https://github.com/ultralytics/yolov5
