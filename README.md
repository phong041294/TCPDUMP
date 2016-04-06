#Tổng quan về tcpdump

##1.TCPDUMP là gì?
* Là phần mềm bắt gói tin trong mạng làm việc trên hầu hết các phiên bản hệ điều hành unix/linux. Tcpdump cho phép bắt và lưu lại những gói tin bắt được, từ đó chúng ta có thể sử dụng để phân tích.
* Tcpdump xuất ra màn hình nội dung các gói tin (chạy trên card mạng mà máy chủ đang lắng nghe) phù hợp với biểu thức logic chọn lọc mà khách hàng nhập vào.
* Sau khi kết thúc việc bắt các gói tin, tcpdump sẽ báo cáo các cột sau:
+Packet capture: số lượng gói tin bắt được và xử lý.
+Packet received by filter: số lượng gói tin được nhận bởi bộ lọc.
+Packet dropped by kernel: số lượng packet đã bị dropped bởi cơ chế bắt gói tin của hệ điều hành.

##2.Ví dụ thực tiễn về tcpdump

**1.Bắt gói tin từ một giao tiếp mạng (cổng mạng) ethernet cụ thể trên máy tính/máy chủ với tham số tcpdump -i**

    tcpdump -i eth0

Sau lệnh này,chương trình sẽ bắt gói tin liên tục cho tới khi bạn ngắt tiến trình chạy của chương trình bằng phím tắt Ctrl+C

<img src="http://i.imgur.com/cd0yQFp.png">

**2.Bắt một số hữu hạn gói tin bằng lệnh có tham số tcpdump -c**

    tcpdump -c 2 -i eth0

Bằng cách sử dụng tham số -c đi kèm lệnh, bạn sẽ ấn định trước bao nhiêu gói tin chương trình sẽ thực hiện bắt trước khi dừng tiến trình “lắng nghe” dữ liệu.Ở đây ta ấn định chỉ bắt 2 gói tin.

<img src="http://i.imgur.com/CSqKPzN.png">

**3.Hiện các gói tin dưới dạng mã ASCII với tham số tcpdump -A**

    tcpdump -A -i eth0

Đây là 1 ví dụ khi sử dụng tham số -A

<img src="http://i.imgur.com/sTzepEe.png">

**4.Hiện các gói tin dưới dạng mã ASCII & Hex (mã thập lục phân) với tham số tcpdump -XX**

    tcpdump -XX -i eth0

Vì một lý do nào đó,người dùng có thể muốn đánh giá gói tin hoặc đọc nội dung gói tin dưới dạng mã thập lục phân (hex), tcpdump hỗ trợ sẵn một cách thức hiển thị cùng một lúc nội dung gói tin dưới dạng mã ASCII và mã hex.

<img src="http://i.imgur.com/szvNz9x.png">

**5.Bắt các gói tin và ghi kết quả vào file bằng tham số -w**

    tcpdump -w phong.pcap -i eth0

Với tham số -w,tcpdump sẽ ghi lại toàn bộ gói tin vào file cho mục đích phân tích sau này,ở đây ta sẽ ghi vào file phong.pcap(Phần mở rộng của file nên đặt là .pcap, cho phép các chương trình phân tích nhật ký (log) mạng khác dễ dàng đọc được nội dung và xử lý)

<img src="http://i.imgur.com/qtZwp69.png">

Và đây là file phong.pcap

<img src="http://i.imgur.com/HfAbqba.png">

**6.Bắt các gói tin với địa chỉ IP thông qua tcpdump -n**

Ví dụ dưới đây bắt các gói tin và hiển thị địa chỉ IP của thiết bị liên quan.

     tcpdump -n -i eth0
     
<img src="http://i.imgur.com/R0XXlbr.png">

**7.Đọc các gói tin lớn hơn hoặc nhỏ hơn N byte**

Ở đây là những gói lớn hơn 1024 byte

    tcpdump -w phong.pcap greater 1024

Nếu cần nhỏ hơn 1024 ta thay "greater" bằng "less"

    tcpdump -w phong.pcap less 1024

**8.Chỉ nhận những gói tin trong với một kiểu giao thức cụ thể.**

Bạn có thể lọc gói tin dựa vào giao thức.Ví dụ dưới đây chỉ bắt các gói tin arp thông qua giao diện eth0.

    tcpdump -i eth0 arp

<img src="http://i.imgur.com/3t3ociO.png">
