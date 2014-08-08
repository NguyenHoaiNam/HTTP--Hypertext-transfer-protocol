HTTP--Hypertext-transfer-protocol--
======
####Nội dung trình bày:
##### 1. Khái niệm
##### 2. Nguyên tắc hoạt động của trình duyệt web với Web-server
##### 3. Chi tiết bản tin request và respond

---

- **1. Khái niệm:**

HTTP(hypertext transfer protocol)là giao thức thuộc tầng ứng dụng tronng mô hình OSI, là trung tâm của Web. HTTP được thực hiện trong hai chương trình: một chương trình máy khách và chương trình máy chủ. Chương trình máy khách và chương trình máy chủ, thực hiện trên các hệ thống đầu cuối khác nhau, nói chuyện với nhau khác bằng cách trao đổi các thông điệp HTTP. Dùng để trao đổi ngôn ngữ văn bản,hình ảnh, đồ họa, âm thanh và được sử dụng rất phổ biến trên các máy chủ web-server.

- **2. Nguyên tắc hoạt động:**

HTTP chạy trên tầng ứng dụng trong mô hinh OSI và chạy dướt nên giao thức tcp ở tầng vận chuyển. HTTP sử cổng port 80 để giao tiếp với các client, và sử dụng bản tin respond để đáp ứng các bản tin request của client.

<img class="image__pic js-image-pic" src="http://i.imgur.com/hPdPxcR.png" alt="" id="screenshot-image">

**Các bước giao tiếp giữa web-client và web-server**

* Bước 1: Http chạy trên nền tcp nền đầu tiên web-client khởi tạo phiên kết nối tới máy chủ web bằng phương thức bắt tay 3 bước thông qua cổng port 80 của máy chủ web.
          *phương thức bắt tay 3 bước:

<img class="image__pic js-image-pic" src="http://i.imgur.com/xXfDBmn.png" alt="" id="screenshot-image">
Quá trình bắt tay 3 bước được diễn ra như sau:

---------------------------------

| *Quá trình 1: Web-client sẽ gửi một bản tin SYN đến cổng port 80 của máy chủ web để yêu cầu kết nối với các trường bản tin như seq, ack, windown size, len, stt.* |
---------------------------------

| *Quá trình 2: Khi máy chủ nhật được bản tin SYN của client sẽ gửi lại bản tin (SYN+ACK)trong đó bản tin ACK là để xác nhận đã nhận được bản tin SYN của clien và bản tin SYN của server để yêu câu khởi tạo với client với các trường bản tin tương tự như bản tin SYN của clien* |
---------------------------------

| *Quá trình 3: Cient gửi lại bản tin ACK cho máy server và xác nhận phiên kết nối đã được khởi tạo* |
---------------------------------

* Bước 2: Sau khi đã thiết lập phiên kết nối với máy chủ web-client sẽ gửi bản tin request đến server để yêu cầu lấy dữ liệu từ server

* Bước 3: Khi nhận được bản tin resquest từ client. Server gửi lại bản tin ACK cho client xác nhận đã nhận được bản tin request của client và ngay sau đó sẽ gửi cho client gói tin có chưa dữ liệu mà client yêu cầu.

-

- **3. Chi tiết từng bản tin:**

**a. Bản tin request :** là bản tin yêu cầu từ client gửi đến cho server để yêu cầu lấy thông tin nào đó.

Trong bản tin resquest của client có các kiểu bản tin như sau:

*GET:* nó là bản tin yêu cầu lấy một nguồn tài nguyên hiện có. URL chứa tất cả các thông tin cần thiết các máy chủ cần phải xác định vị trí và trả lại tài nguyên.

<img class="image__pic js-image-pic" src="http://i.imgur.com/Fgz9QEO.png" alt="" id="screenshot-image">

*POST*: tạo ra một nguồn tài nguyên mới. POST yêu cầu thường mang một tải trọng mà xác định các dữ liệu về tài nguyên mới.
<img class="image__pic js-image-pic" src="http://i.imgur.com/3X5sxhq.png" alt="" id="screenshot-image">

*PUT*: cập nhật một nguồn tài nguyên hiện có. Tải trọng có thể chứa dữ liệu cập nhật của nguồn tài liệu.

*DELETE*: xóa một nguồn tài nguyên hiện có.

 có một số kiểu bản tin được sử dụng ít hơn như:
 
*HEAD:* đây là tương tự như GET, nhưng không có nội dung thư. Nó được sử dụng để lấy các tiêu đề máy chủ cho một tài nguyên cụ thể, thường để kiểm tra xem tài nguyên đã thay đổi, qua thời gian.

*TRACE:* sử dụng để lấy các bước nhảy là một yêu cầu cần thiết để làm tròn chuyến đi từ máy chủ. Mỗi proxy trung gian hoặc gateway sẽ bơm IP hoặc tên DNS vào trường “Via”. Điều này có thể được sử dụng cho mục đích chẩn đoán.

*OPTIONS:* sử dụng để lấy các khả năng máy chủ. Về phía khách hàng, nó có thể được sử dụng để chỉnh sửa theo yêu cầu dựa trên những gì các máy chủ có thể được hỗ trợ

*b. Bản tin respond:* là bản tin đáp ứng yêu cầu từ phía client:
Bản tin respond có các mã trạng thái khi đến với client:

| Mã trạng thái | Ý nghĩa |
|---------------|---------|
|1xx | Thông tin |
|2xx | Truy vấn thành công |
|3xx | Client được chuyển hướng đến một địa chỉ khác |
|4xx | Lỗi đến từ phía người dùng |
|5xx | Lỗi trong server |

Đối với mã 2xx:
* 202 Chấp nhận: yêu cầu được chấp nhận nhưng có thể không bao gồm các nguồn tài nguyên trong các phản ứng. Điều này rất hữu ích để chế biến async ở phía máy chủ. Các máy chủ có thể chọn để gửi thông tin để theo dõi.
* 204 Không có nội dung: không có cơ quan thông báo trong các phản ứng.
* 205 Đặt lại Nội dung: chỉ ra cho khách hàng để thiết lập lại xem tài liệu của nó.
* 206 phần nội dung: chỉ ra rằng phản ứng chỉ chứa nội dung từng phần. Tiêu đề bổ sung cho phạm vi chính xác và thông tin hết nội dung.

Đối với mã 3xx:
* 301 Moved Permanently: tài nguyên hiện tại là một URL mới.
* 303 Xem khác: tài nguyên được tạm thời đặt tại một URL mới. Vị trí phản ứng tiêu đề chứa URL tạm thời.
* 304 Không thay đổi: máy chủ đã xác định rằng tài nguyên không thay đổi và khách hàng nên sử dụng bản sao lưu trữ của nó. Điều này dựa trên thực tế là khách hàng đang gửi ETag (Enttity Tag) thông tin đó là một hash của nội dung. Các máy chủ so sánh điều này với ETag tính toán riêng của mình để kiểm tra xem có sửa đổi.

Đối với mã 4xx:
* 400 Yêu cầu: yêu cầu đã bị thay đổi.
* 401 Không được quyền: yêu cầu yêu cầu xác thực. Khách hàng có thể lặp lại các yêu cầu với tiêu đề ủy quyền. Nếu khách hàng đã bao gồm tiêu đề ủy quyền, sau đó các thông tin đã sai.
* 403 Forbidden: máy chủ đã bị từ chối truy cập vào các tài nguyên.
* 405 Phương thức không được phép: động từ HTTP không hợp lệ được sử dụng trong các dòng yêu cầu, hoặc máy chủ không hỗ trợ động từ.
* 409 xung đột: máy chủ không thể hoàn thành yêu cầu do khách hàng đang cố gắng để sửa đổi một nguồn tài nguyên đó là mới hơn so với dấu thời gian của khách hàng. Xung đột phát sinh chủ yếu là cho các yêu cầu PUT trong hợp tác chỉnh sửa trên một tài nguyên.

Đối với mã 5xx: Lỗi trong server
* 501 Không thực hiện: máy chủ chưa hỗ trợ các chức năng được yêu cầu.
* 503 Dịch vụ không: điều này có thể xảy ra nếu một hệ thống nội bộ trên máy chủ đã bị lỗi hay máy chủ bị quá tải. Thông thường, các máy chủ sẽ thậm chí không đáp ứng và các yêu cầu sẽ thời gian chờ.

*VD1*: Các trường của bản tin GET:
```
GET /?p=17 HTTP/1.1\r\n
Host: 192.168.1.245\r\n
Cache-Control: max-age=0\r\n
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8\r\n
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.127 CoRom/36.0.1985.127 Safari/537.36\r\n
Referer: http://192.168.1.245/?p=17\r\n
Accept-Encoding: gzip,deflate,sdch\r\n
Accept-Language: vi-VN,vi;q=0.8,fr-FR;q=0.6,fr;q=0.4,en-US;q=0.2,en;q=0.2\r\n
```
**Trong đó**:
* Dòng 1:`GET` cho ta biết đây là bản tin `GET` và truy vấn đến `/?p=17` của server và dùng phiên bản http 1.1
* Dòng 2: `Host` cho biết địa chỉ host của server ví dụ nhưng khi truy vấn đến trang `24h.com.vn` thì host lúc này là 24h.com.vn
* Dòng 3: `Cache-Control`
* Dòng 4:`Accept` Báo cho server biết web-client có thể đọc được dữ liệu nào.
* Dòng 5: `User-Agent` Thông báo cho web-server biết web-client sử dụng những phiên bản nào để trình duyệt web điều này có tác dụng khi ta sử dụng điện thoại lên web thì server sẽ biết và gửi lại sử dụng version dành cho điện thoại
* Dòng 6: `Referer:` cho biết URL có nguồn gốc từ địa chỉ nào
* Dòng 7: `Accept-Encoding` Web-client có thể đọc được kiểu mã hóa nào.
* Dòng 8: `Accept-Language` Ngôn ngữ của web-client nếu web-server có ngôn ngữ đó sẽ trả về ngôn ngữ đó cho web-client, nếu không nó sẽ trả về ngôn ngữ mặc định của nó.

*VD2*: Các trường của bản tin Respont từ web-server
```
HTTP/1.1 200 OK\r\n
Date: Sat, 12 Jul 2014 19:23:57 GMT\r\n
Server: Apache/2.2.22 (Ubuntu)\r\n
X-Powered-By: PHP/5.3.10-1ubuntu3.12\r\n
Expires: Wed, 11 Jan 1984 05:00:00 GMT\r\n
Cache-Control: no-cache, must-revalidate, max-age=0\r\n
Pragma: no-cache\r\n
Link: <http://192.168.1.245/?p=17>; rel=shortlink\r\n
Vary: Accept-Encoding\r\n
Content-Encoding: gzip\r\n
Content-Length: 7128\r\n
Keep-Alive: timeout=5, max=100\r\n
Connection: Keep-Alive\r\n
Content-Type: text/html; charset=UTF-8\r\n
```
**Trong đó**:
* Dòng 1: `HTTP` bản tin respond với mã 200 báo cho web-client biết truy suất thành công và đã gửi dữ liệu yêu cầu.
* Dòng 2: `Date` ngày dữ liệu được lưu trên server
* Dòng 3: `Server` chỉ ra thông tin server sử dụng phiên bản của chương trình máy chủ
* Dòng 4: `X-Powered-By` 
* Dòng 5: `Expires:`
* Dòng 6: `Cache-Control` bảo cho web-client không lưu trong bộ nhớ cache
* Dòng 7: `Pragma`
* Dòng 8: `Link` đia chỉ URL trên web-client
* Dòng 9: `Vary`
* Dòng 10:`Content-Encoding` kiểu web-server mã hóa, phương pháp này giúp giảm dữ liệu trên đường truyền
* Dòng 11: `Content-Length` thông báo cho web-client dung lượng gói tin vừa gửi cho web-client
* Dòng 12:`Keep-Alive` thông báo phiên kết nối sẽ được giữ trong vòng 5s và max=100s
* Dòng 13:`Connection` thông báo web-server sẽ giữ phiên kết nối sau khi gửi xong dữ liệu web-client yêu cầu
* Dòng 14: `Content-Type` kiểu dữ liệu gửi cho web-client ở đây là dữ liệu dạng html

**Note:** Trên đây mình xin giới thiệu về giao thức http. nguyên tắc hoạt động và các trường cơ bản nhất của bản tin Request và Respond. Tìm hiểu sâu về các bản tin http và trong thực tế mô hình triển khai như thế nào, sử dụng cache-server ra sao các bạn có thể tham khao tại link sau:

[Link 1](http://dev.vast.vn/tuananh/Web/C%C4%90055#caches)--
[Link 2](http://www.expressmagazine.net/development/2160/http-giao-thuc-ma-moi-lap-trinh-vien-nen-biet)--
[Link 3](http://passionery.blogspot.com/2014/01/http-header-la-gi.html#.U-T5YaiVNN1)

Ngoài ra tìm hiểu thêm về giao thức TCP được triển khai ở tầng transport.

[Giao thức TCP](http://quantrimang.edu.vn/he-thong/he-thong-mang-lan/giao-thuc-tcp-ip-lam-viec-nhu-the-nao.htm)


