<p align="center">
   <a href="https://www.uit.edu.vn/">
      <img src="https://i.imgur.com/WmMnSRt.png" border="none">
   </a>
</p>
<h1 align="center">
    CS114.N11.KHCL - Máy Học
    **Nhận diện và phân loại rác thải sinh hoạt - Trash Classification**
</h1>
# Danh sách thành viên
| STT | Họ và tên | MSSV | Email |
|:-----:|:-------:|:------:|:-------:|
| 1 | [Phạm Thiện Bảo](https://github.com/beetibao) | 20521107 | 20521107@gm.uit.edu.vn |
| 2 | [Lê Văn Khoa](https://github.com/Levankhoa150102) | 20521467 | 20521467@gm.uit.edu.vn |
| 3 | [Lê Nguyễn Tiến Đạt](https://github.com/lenguyentiendat) | 20521167 | 20521167@gm.uit.edu.vn |

# Tổng hợp
* Source code: [code](https://github.com/beetibao/CS114/blob/main/CS114_Trash_Classification.ipynb)
* File báo cáo: [TrashClassification_Report.pdf](https://github.com/beetibao/CS114/blob/main/CS114_TrashClassification.pdf)
* Dataset: [Dataset](https://drive.google.com/drive/folders/1Q8_Lf4WAmG5liwTWXvCyb0F4seT4MOHF?usp=sharing)
* Hình kết quả trên tập test: [Kết quả tập test](https://drive.google.com/drive/folders/10r2PK0sCLg5Yc848NnAPypgc3bllLl-0?usp=sharing)
# Giới thiệu đề tài
- Cuộc sống đang ngày càng phát triển hiện đại, đời sống vật chất và tinh thần của người dân được cải thiện rõ rệt. Tuy nhiên, đối lập với nó, tình trạng ô nhiễm môi trường lại có những diễn biến phức tạp và là một vấn đề cấp bách cần phải giải quyết kịp thời. Trong năm 2021, thế giới thải ra 353 triệu tấn rác thải nhựa nhưng lượng rác được tái chế chỉ đạt 9%. Việt Nam nằm trong số 20 quốc gia có lượng rác thải lớn nhất và cao hơn mức trung bình của thế giới. Riêng tại Việt Nam, trung bình mỗi năm lượng rác thải nhựa khoảng 1,8 triệu tấn. Trên thế giới, chỉ có khoảng 19% số rác được tiêu hủy và chỉ gần 50% được chôn lấp tại các hố rác đủ tiêu chuẩn. 
- Từ việc nhận thức sai lầm rằng rác thải sẽ do bên đơn vị thu gom rác xử lý và không có nghĩa vụ phải phân loại chúng dẫn đến việc lượng rác thải gây hại cho môi trường ngày càng tăng, ảnh hưởng vô cùng lớn đến sức khoẻ của con người.
- _**"Nhận diện và phân loại rác thải sinh hoạt"**_ là bài toán áp dụng mô hình Object Detection, nhằm giúp nhận biết tên loại rác thải sinh hoạt từ đó hỗ trợ trong việc phân loại chúng vào nhóm rác tái chế và không tái chế được. Con người cần phải có một công cụ thông minh hỗ trợ phân loại rác để giảm bớt chi phí cho các nhà máy tái chế, giúp thu gom và phân loại rác từ lúc chúng vừa mới được vứt bỏ. Áp dụng máy học thông qua sử dụng thuật toán Yolov5, nhóm chúng em muốn tạo ra một thiết bị hỗ trợ nhận diện và phân loại rác thải sinh hoạt hằng ngày. Tuy nhiên, nhằm giới hạn phạm vi bài toán, nhóm chúng em chỉ tiếp cận và giải quyết bài toán phân loại 28 loại rác quen thuộc như lon, chai nhựa, hộp xốp, bao nylon, khẩu trang,…
- Ngữ cảnh ứng dụng: Tích hợp hệ thống nhận diện vào con robot để đi gom kết hợp phân loại rác ở các nơi công cộng như công viên, trường học, khu dân cư hay cống rãnh, ven biển và cả dưới đại dương.
# Thách thức của bài toán
Phân loại quy mô lớn: Số lượng rác là vô cùng lớn có thể lên đến hàng chục nghìn loại dẫn đến vượt xa khả năng thông thường của máy dò đối tượng. Số lượng lớn cũng ảnh hưởng đến việc thu gom và tích trữ rác phân loại được.
Sự phức tạp của các loại rác thải: Có nhiều loại rác thải khác nhau với các đặc điểm vật lý, hình dạng và màu sắc khác nhau. Rác để lâu qua thời sẽ sẽ có những biến đổi, nó không còn hình dạng, kích thước hoặc màu sắc như ban đầu. Điều này có thể gây khó khăn cho mô hình phân loại rác bằng Machine Learning.
Nhiều loại rác bị biến dạng thì mô hình khó có để đưa ra dự đoán chính xác cho đối tượng đó. Một số trường hợp các loại rác chất chồng lên nhau làm nhiễu khả năng dự đoán của mô hình. 

# Mô tả bài toán
+ Input: Là một bức ảnh chụp từ trên chiếu xuống, cách mặt đất 1-2m với ánh sáng rõ ràng; trong đó bao gồm không hay nhiều đối tượng như lon, chai nhựa, hộp nhựa, túi rác,…
+ Output: Là bức ảnh từ input nhưng có không hoặc nhiều bounding box trong bức ảnh thể hiện nhãn và vị trí của đối tượng trong bức ảnh mà mô hình dự đoán được. 

# Đánh giá
Để đánh giá model Object detection người ta sử dụng IoU, AP, mAP,….
- Intersection over Union (IoU) là một số liệu đánh giá được sử dụng để đo độ chính xác trong bài toán phát hiện đối tượng trên một tập dữ liệu cụ thể. Nó sử dụng trong việc đánh giá xem bounding box dự đoán đối tượng khớp với ground truth thật của đối tượng hay không. Chỉ số IoU trong khoảng [0,1] và nếu IoU càng gần 1 thì bounding box dự đoán càng gần ground truth.
- AP: là chỉ số có quan hệ mật thiết với chỉ số Precision (phần trăm bounding box được dự đoán đúng) và Recall (tỉ lệ phần trăm các bounding box được đoán đều chính xác). 
  + AP50: là độ chính xác với IoU = 0.5 
  + AP75: là độ chính xác với IoU = 0.75
Khi quá trình training kết thúc, ta sẽ có được các kết prediction của mỗi vật thể trong hình. Thông qua quá trình tính toán IoU để đo độ chính xác dự đoán, ta tính được giá trị TP, FP, FN. Từ đó dễ dàng tính được thông số của Precision và Recall. Hai giá trị này nhằm để vẽ được biểu đồ Precision – Recall Curve, áp dụng công thức tính để tìm được AP cho từng class.
- mAP: Bài toán có một hoặc nhiều class, mỗi class ta sẽ tiến hành đo AP, sau đó lấy trung bình tất cả các giá trị AP của các class thì ta tìm được chỉ số mAP của mô hình. Do đó, mAP được hiểu là giá trị trung bình của các tất cả các class.
  + **mAP@.5**: có nghĩa là mAP trung bình khi chọn IoU = 0.5
Ví dụ: mAP@0.5 = 0.7  Tại IoU = 0.5, AP của mô hình là 70%.
  + **mAP@[.5:.95]** có nghĩa là mAP trung bình trên các ngưỡng IoU khác nhau, từ 0,5 đến 0,95 ,bước nhảy 0,05.
Người ta thường chọn khoảng IoU từ **[.5:.95]** bởi vì rất khó để predicted bounding box trùng khớp với ground truth thực sự của vật thể, dẫn tới việc kết quả luôn sai mặc dù mô hình đã dự đoán gần như chính xác vật thể.

# Dataset
## Cách xây dựng
Để thực hiện đề tài, chúng em đã tự xây dựng bộ dataset riêng và có những ràng buộc, thông tin cụ thể là:
- Số lượng ảnh: 1500 tấm ảnh màu. 
- Kích thước: 918 x 1224 → 4000 x 3000
- Vật thể trong bức hình: gồm 28 loại rác khác nhau, quy định sử dụng tên tiếng Anh của rác.
- Độ sáng: Trời sáng, ánh sáng đủ để nhìn thấy rõ vật thể; không bị chói, bị nhòe.
- Background: Nền gạch đường, bãi lá khô, nền cỏ, ven mép đường, dưới gốc cây, quanh bãi rác…
- Góc chụp: hướng nhìn từ trên xuống, cách vật thể khoảng 1m, không quá 2m.
Dataset sẽ được chia thành 3 tập train, valid, test với tỉ lệ 70:15:15, tương ứng với 1200:150:150 ảnh, các ảnh được chia đảm bảo ở mỗi tập đều có đầy đủ các class.
Link dataset: [Trash_Dataset](https://drive.google.com/drive/folders/1Q8_Lf4WAmG5liwTWXvCyb0F4seT4MOHF?usp=sharing)

# Mô tả về thuật toán máy học
- Vài năm trở lại đây, object detection là một trong những đề tài quan trọng bởi khả năng ứng dụng cao, dữ liệu dễ chuẩn bị và kết quả ứng dụng rất nhiều. Các thuật toán mới của object detection có thể thực hiện được các tác vụ dường như là real time, thậm chí là nhanh hơn so với con người mà độ chính xác không giảm. Trong đó, YOLO - You Only Look Once có thể không phải là thuật toán tốt nhất nhưng nó là thuật toán nhanh nhất trong các lớp mô hình object detection. Các phiên bản của mô hình này đều có những cải tiến rất đáng kể sau mỗi phiên bản. Chính vì vậy, nhóm thử nghiệm chọn Yolov5 để thực hiện đồ án.
- Yolov5 là sản phẩm của tác giả Glenn Jocher - nhà nghiên cứu, giám đốc điều hành của Ultralystic. Đây là tổ chức hướng tới việc giúp cho người học AI nói chung và những người đam mê công nghệ nói riêng có thể tiếp cận với các mô hình máy học một cách đơn giản, hiệu quả và trực quan hơn.

Ta sử dụng train model theo hướng dẫn của nhà phát hành Yolov5: [Hướng dẫn sử dụng của Yolov5](https://github.com/ultralytics/yolov5)

# Kết quả
| **Độ đo**                |  **Kết quả**    | 
| :----------------------: |:--------------: | 
|  **mAP (IoU[0.5])**      |  0.83           |  
|  **mAP (IoU[0.5:0.95]**  |  0.56           |  

# Nhận xét
Với bộ dataset chuẩn bị và việc áp dụng mô hình Yolov5, chúng em nhận thấy kết quả đánh giá mAP (IoU[0.5:0.95]) là 0.56, thấp hơn với các kết quả của các nghiên cứu khác.
Lý do:
+ Thứ nhất, Yolov5 có khả năng phát hiện chính xác các vật thể nhỏ, quan tâm nhiều đến các tiểu tiết trong bức hình để trích xuất đặc trưng tốt hơn. Chính vì thế, trong bộ dataset của chúng em có xuất hiện nhiều loại rác thải bị biến dạng, xếp chồng lên nhau khiến Yolov5 khó khăn hơn trong việc detect. Trong khi đó, các vật thể rác trong bộ dataset mà các tác giả trước nghiên cứu hầu như không bị biến dạng và được đặt ở background không có nhiều vật thể nhiễu như sỏi đá, lá cây… Do đó, kết quả trả về của chúng em sẽ có phần thấp hơn.
+ Thứ hai, theo như lời tác giả khuyến khích khi xây dựng dataset để sử dụng mô hình Yolov5 thì cần phải thêm một số hình ảnh không được có vật thể nhãn (background) để tăng độ chính xác, chiếm khoảng 5-10% trong bộ dataset. Trong bộ dataset của chúng em, tất cả các hình đều có một hoặc nhiều object khác nhau và không có tấm nào là background. Chính vì vậy có thể đã làm ảnh hưởng một phần đến kết quả.
+ Thứ ba, khi muốn đánh giá để có kết quả tốt nhất, người ta thường sử dụng mô hình pretrained có kích thước lớn như Yolov5l,  Yolov5n – phù hợp training trên các thiết bị đám mây. Tuy nhiên, khi sử dụng Yolov5l chúng em xuất hiện hiện tượng tràn bộ nhớ nên không thể tiếp tục đánh giá trên mô hình này. 

# Hướng phát triển
+ Về data:
-	Xây dựng dataset có thêm nhiều loại rác khác 
-	Tìm hiểu và nghiên cứu thêm về các quy tắc xây dựng dataset để nâng cao chất lượng bộ dữ liệu, gom các loại rác liên quan vào cùng 1 nhóm nhằm giảm thiểu số lớp để học, thuận tiện cho việc xử lý.
+ Về model:
-	Tiến hành cài đặt và thử nghiệm trên các đời Yolo mới hơn như v7,v8 
-	Sử dụng pretrained model phức tạp hơn để train.
