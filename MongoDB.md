# **MongoDB**

## 🔷 Mục lục
- [Tổng quan MongoDB**](#-tổng-quan-mongodb)
- [Tip](#tip)

## 🔷 Tổng quan MongoDB

### MongoDB

- **MongoDB** là một hệ quản trị cơ sở dữ liệu NoSQL mã nguồn mở đa nền tảng viết bằng C++. Bản ghi trong MongoDB được lưu trữ dạng một dữ liệu văn bản (document), là một cấu trúc dữ liệu bao gồm các cặp giá trị và trường tương tự như các đối tượng JSON.

- Một số ưu điểm nổi bật của MongoDB:
    + **Không yêu cầu lược đồ (Schema)** MongoDB không yêu cầu lược đồ được xác định trước, nhưng việc chuyển đổi lược đồ có thể cần thiết để phát triển cấu trúc dữ liệu. Tuy nhiên, MongoDB linh hoạt hơn so với cơ sở dữ liệu qua hệ truyền thống yêu câu lược đồ nghiêm ngặt

    + **Truy vấn tài liệu (Document Queries)** Phương pháp tiếp cận hướng tài liệu của MongoDB phù hợp với các truy vấn động. Nó cho phép các hoạt động truy vấn truy vấn linh hoạt và đa dạng dựa trên bản chất của tài liệu, không giống các truy vấn dựa trên bảng tĩnh của RDBMS

    + **Tối ưu hoá hiệu suất đơn giản** So với cơ sở dữ liệu quan hệ, tối ưu hoá hiệu suất của MongoDB tương đối đơn giản hơn do kiến trúc và cách quản lý dữ liệu nội bộ của MongoDB

    + **Sử dụng bộ nhớ hiệu quả** MongoDB sử dụng bộ nhớ trong để lưu trữ dữ liệu. Do đó, MongoDB truy cập dữ liệu rất nhanh và nâng cao hiệu suất tổng thể

    + **Mở rộng theo chiều ngang với Sharding (Horizontal Scaling)** Với MongoDB, chúng ta có thể mở rộng cơ sở dữ liệu theo chiều ngang bằng cách phân phối dữ liệu trên nhiều máy chủ, phương pháp này được gọi Sharding. Sharding đảm bảo phân tách dữ liệu và phân phối đều trên các Shard, rất hiệu quả cho việc truy xuất dữ liệu

    + **Dễ bảo trì** MongoDB thường được xem là dễ bảo trì hơn so với cơ sở dữ liệu truyền thống do có lượt đồ linh hoạt và quy trình tối ưu hoá đơn giản hơn

    + **Nhân rộng và phân phối khối lượng công việc** Bằng cách tạo bản sao dữ liệu và phân bổ công việc trên các phần khác nhau, MongoDB đảm bảo thông tin luôn khả dụng và hệ thống hoạt động thực sự nhanh. Điều này xảy ra vì các tác vụ được chia sẻ giữa nhiều nơi thay vì chỉ một nơi, giúp mọi thứ nhanh hơn và đáng tin cậy hơn

- Tuy nhiên, MongoDB còn có một số nhược điểm đáng cân nhắc:
    + **Phạm vi Transactions hạn chế** Trong MongoDB, các Transaction hoạt động với từng phần dữ liệu (được gọi là tài liệu), nhưng chúng không bao phủ đầy đủ các tình huống mà bạn cần thực hiện nhiều việc cùng lúc trên nhiều dữ liệu. Điều này có thể gây khó khăn cho các ứng dụng thực sự cần mọi thứ diễn ra hoàn hảo cùng nhau

    + **Thiếu sự tuân thủ ACID đầy đủ** Mặc dù MongoDB cung cấp tính nguyên tử (**A**tomicity), tính nhất quán (**C**onsistency), tính cô lập (**I**solation) và tính bền vững (**D**urability) ở cấp độ tài liệu, nhưng nó không cung cấp sự tuân thử **ACID** đầy đủ trên nhiều tài liệu hoặc collection. Hạn chế này có thể gây khó khăn cho các ứng dụng yêu cầu đảm bảo Transaction nghiêm ngặt và phức tạp

    + **Khả năng liên kết hạn chế** Không giống như cơ sở dữ liệu truyền thống, MongoDB không hỗ trợ liên kết theo cách tương tự. Mạc dù có thể thực hiện thủ công các hoạt động giống như liên kết bằng Code, nhưng nó có thể làm chậm quá trình thực thi và ảnh hưởng đến hiện suất

    + **Dư thừa dữ liệu và sử dụng bộ nhớ** MongoDB lưu trữ bao gồm cặp key-value, gây ra một số dư thừa dữ liệu do hạn chế của các liên kết trong MongoDB. Sự dư thừa này có thể dẫn đến việc sử dụng bộ nhớ tăng lên so với mức cần thiết

    + **Giới hạn kích thước tài liệu** MongoDB áp dụng giới hạn kích thước tài liệu tối đa là 16MB. Các tài liệu lớn hơn có thể cần được xử lý khác nhau hoặc chia thành các tài liệu nhỏ hơn để phù hợp với ràng buộc này

    + **Mức tài liệu lồng nhau** Trong MongoDB các tài liệu có thể lồng nhau nhưng bị giới hạn ở mức tối đa là 100. Hạn chế này có thể ảnh hưởng nhỏ hoặc lớn đến việc tổ chức cấu trúc dữ liệu của dự án 