HTTP--Hypertext-transfer-protocol--
======
##Nội dung:
### 1. Khái niệm
### 2. Nguyên tắc hoạt động của trình duyệt web với Web-server

---
1. Khái niệm:

HTTP(hypertext transfer protocol)là giao thức thuộc tầng ứng dụng tronng mô hình OSI, là trung tâm của Web. HTTP được thực hiện trong hai chương trình: một chương trình máy khách và chương trình máy chủ. Chương trình máy khách và chương trình máy chủ, thực hiện trên các hệ thống đầu cuối khác nhau, nói chuyện với nhau khác bằng cách trao đổi các thông điệp HTTP. Dùng để trao đổi ngôn ngữ văn bản,hình ảnh, đồ họa, âm thanh và được sử dụng rất phổ biến trên các máy chủ web-server.

2. Nguyên tắc hoạt động:

HTTP chạy trên tầng ứng dụng trong mô hinh OSI và chạy dướt nên giao thức tcp ở tầng vận chuyển. HTTP sử cổng port 80 để giao tiếp với các client, và sử dụng bản tin respond để đáp ứng các bản tin request của client.

**Các bước giao tiếp giữa web-client và web-server**

* Bước 1: Http chạy trên nền tcp nền đầu tiên web-client khởi tạo phiên kết nối tới máy chủ web bằng phương thức bắt tay 3 bước thông qua cổng port 80 của máy chủ web.
          *phương thức bắt tay 3 bước:

<img class="image__pic js-image-pic" src="http://i.imgur.com/xXfDBmn.png" alt="" id="screenshot-image">
Quá trình bắt tay 3 bước được diễn ra như sau:

*Quá trình 1: Web-client sẽ gửi một bản tin SYN đến cổng port 80 của máy chủ web để yêu cầu kết nối với các trường bản tin như seq, ack, windown size, len, stt.*

*Quá trình 2: Khi máy chủ nhật được bản tin SYN của client sẽ gửi lại bản tin (SYN+ACK)trong đó bản tin ACK là để xác nhận đã nhận được bản tin SYN của clien và bản tin SYN của server để yêu câu khởi tạo với client với các trường bản tin tương tự như bản tin SYN của clien*

*Quá trình 3: Cient gửi lại bản tin ACK cho máy server và xác nhận phiên kết nối đã được khởi tạo*

* Bước 2: Sau khi đã thiết lập phiên kết nối với máy chủ web-client sẽ gửi bản tin request đến server để yêu cầu lấy dữ liệu từ server

* Bước 3: Khi nhận được bản tin resquest từ client. Server gửi lại bản tin ACK cho client xác nhận đã nhận được bản tin request của client và ngay sau đó sẽ gửi cho client gói tin có chưa dữ liệu mà client yêu cầu.

---

3. Chi tiết tưng bản tin:

a. Bản tin request : là bản tin yêu cầu từ client gửi đến cho server để yêu cầu lấy thông tin nào đó.

Trong bản tin resquest của client có các kiểu bản tin như sau:

*GET:* nó là bản tin yêu cầu lấy một nguồn tài nguyên hiện có. URL chứa tất cả các thông tin cần thiết các máy chủ cần phải xác định vị trí và trả lại tài nguyên.

<img class="image__pic js-image-pic" src="http://i.imgur.com/Fgz9QEO.png" alt="" id="screenshot-image">

*POST*: tạo ra một nguồn tài nguyên mới. POST yêu cầu thường mang một tải trọng mà xác định các dữ liệu về tài nguyên mới.
<img class="image__pic js-image-pic" src="http://i.imgur.com/wEKqTSI.png" alt="" id="screenshot-image">

*PUT*: cập nhật một nguồn tài nguyên hiện có. Tải trọng có thể chứa dữ liệu cập nhật của nguồn tài liệu.

*DELETE*: xóa một nguồn tài nguyên hiện có.

 có một số kiểu bản tin được sử dụng ít hơn như:
 
*HEAD:* đây là tương tự như GET, nhưng không có nội dung thư. Nó được sử dụng để lấy các tiêu đề máy chủ cho một tài nguyên cụ thể, thường để kiểm tra xem tài nguyên đã thay đổi, qua thời gian.

*TRACE:* sử dụng để lấy các bước nhảy là một yêu cầu cần thiết để làm tròn chuyến đi từ máy chủ. Mỗi proxy trung gian hoặc gateway sẽ bơm IP hoặc tên DNS vào trường “Via”. Điều này có thể được sử dụng cho mục đích chẩn đoán.

*OPTIONS:* sử dụng để lấy các khả năng máy chủ. Về phía khách hàng, nó có thể được sử dụng để chỉnh sửa theo yêu cầu dựa trên những gì các máy chủ có thể được hỗ trợ
b. Bản tin respond: là bản tin đáp ứng yêu cầu từ phía client:
Bản tin respond có các mã trạng thái khi đến với client:

| Mã trạng thái | Ý nghĩa |
|---------------|---------|
|1xx | Thông tin |
|2xx | Truy vấn thành công |
|3xx | Client được chuyển hướng đến một địa chỉ khác |
|4xx | Lỗi đến từ phía người dùng |
|5xx | Lỗi trong server |

########## Đối với mã 2xx:
########### * 202 Chấp nhận: yêu cầu được chấp nhận nhưng có thể không bao gồm các nguồn tài nguyên trong các phản ứng. Điều này rất hữu ích để chế biến async ở phía máy chủ. Các máy chủ có thể chọn để gửi thông tin để theo dõi.
########### * 204 Không có nội dung: không có cơ quan thông báo trong các phản ứng.
########### * 205 Đặt lại Nội dung: chỉ ra cho khách hàng để thiết lập lại xem tài liệu của nó.
########### * 206 phần nội dung: chỉ ra rằng phản ứng chỉ chứa nội dung từng phần. Tiêu đề bổ sung cho phạm vi chính xác và thông tin hết nội dung.

########## Đối với mã 3xx:
###########


