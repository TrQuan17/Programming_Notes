# **Genexus**

## 🔹 Transactions
### Rule triggering Event
- AfterLevel
	```
	on AfterLevel level <tên level>
	```

	+ Sau quá trình thêm dữ liệu vào thì mới thực hiện
	+ Dữ liệu được lưu nhưng chưa được xác thực

- BeforeInsert: Thực hiện trước khi dữ liệu được chèn từng dòng vào DB

- AfterInsert: Thực hiện sau khi dữ liệu được chèn từng dòng vào DB

- AfterComplete: Thực hiện sau cả AfterLevel, khi dữ liệu đã được xác thực và thêm vào thành công

=> Tất cả các rule với sự kiện kích hoạt với tiền tố on ở cuối câu lệnh sẽ được thực thi tương ứng với sự kiện đó, những sự kiện này chỉ diễn ra trên máy chủ và ghi lại khoảnh khắc trước hoặc sau cột mốc thường liên quan đến cơ sở dữ liệu

### Event
- Start: xác định một hành động sẽ được thực hiện 	khi chúng ta mở và bắt đầu làm việc với Transactions

	=> Thường được dùng để gán giá trị cho các biến

- Track Context: cho phép lên lịch hành động cần thực hiện khi có thay đổi được thực hiện trong bối cảnh

- OnMessage: sự kiện này liên quan đến thông báo trên web cho phép thực hiện các hành động trong thời gian thực

- Insert, Update và Delete: được liên kết với khái niệm cập nhật các Dynamic Transactions, áp dụng cho các giao dịch đặc biệt

- Exit: chỉ ra những hành động cần thực hiện khi quá trình thực hiện Transactions hoàn tất tức là đã được đóng lại

- After Trn: chỉ ra hành động cần thực hiện sau mỗi chu kỳ thực hiện Transactions, đó là ngay sau khi Commit được thực hiện.
	+ Tương tự như AfterComplete
	+ Kết thúc khối lệnh sẽ có lệnh Return để quay + lại màn hình chính

### Index trong database
- Đánh dấu dữ liệu giúp truy vấn dữ liệu nhanh hơn
- Tạo mối quan hệ 1 - 1 hoặc cấu hình Attribute với 1 giá trị là duy nhất (không lặp lại)

### Cơ sở dữ liệu chuẩn hoá (Normalization DB)
- Không có dữ liệu trùng lặp, không có dữ liệu dư thừa
- Các thuộc tính phụ hiện diện trong một bảng duy nhất
- Các thuộc tính được suy ra không được lưu trữ (Genexus nhận giá trị của chúng từ các khoá ngoại tương ứng)
- Các thuộc tính duy nhất có thể bao gồm trong nhiều bảng là khoá chính vì chúng là khoá ngoại trong các bảng khác

### Mối quan hệ giữa các chủ thể trong hiện thực
- Một thực thể chỉ có ý nghĩa nếu nó được thể hiện trong mối quan hệ với một thực thể khác được gọi là thực thể yếu
- Mối quan hệ yếu 1 - N thường được thể hiện bằng một giao dịch hai cấp duy nhất, với thực thể yếu là cấp độ thứ 2
- Thể hiện mối quan hệ N - N: trong bảng 1 có thể nhập tất cả giá trị của bảng 2 (bảng 2 là thực thể yếu của bảng 1) và ngược lại

## 🔹 Danh sách và truy cập dữ liệu theo code
### Formulas
- Global Formulas 
	+ Được xác định ở cấp thuộc tính trong cấu trúc Transaction. Nó được chỉ ra rằng một thuộc tính nhất định luôn được tính toán một cách nhất định
	+ Khi cần truy xuất giá trị thuộc tính trong bất kì đối tượng nào, công thức này sẽ được đánh giá để có kết quả
	+ Không thể sử dụng với biến, chỉ có thể sử dụng với attribute
	=> Lý do thuộc tính công thức là thuộc tính ảo không được lưu trữ trong bảng

- Local Formulas (Inline Formulas)
	+ Có thể được thiết lập để chỉ được đánh giá trong mã đối tượng nơi chúng được đặt 
	+ Là công thức được nên dưới dạng hướng dẫn cụ thể trong một mã nhất định
	+ Có thể sử dụng cả biến và attribute

### Truy vấn dữ liệu với ForEach
- Dữ liệu được hiểu thị độc lập với nhau 
	```
	for each Category
		...
	endfor

	for each Attraction
		...
	endfor
	```
- Dữ liệu có mối quan hệ và hiểu thị liên quan với nhau
	```
	for each Category
		for each Attraction
			...
		endfor
	endfor
	```
- Để sắp xếp các dữ liệu được in ra, sử dụng order
	```
	for each Attraction order AttractionName ...   // sắp xếp AttractionName theo ASC
	for each Attraction order (AttractionName) ... // sắp xếp AttractionName theo DESC
	```


## 🔹 Giao tiếp giữa các đối tượng
- Biến có thể được sử dụng tự do trong lập trình như nó có thể được sử dụng làm điều kiện lọc cho các bộ lọc như đẳng thức lớn hơn, lớn hơn hoặc bằng, ... Ngoài ra còn có thể được sử dụng cho phép toán số học hoặc bất cứ điều gì cần thiết

- Quy tắc Pam: tham số có thể được sử dụng để nhận một giá trị, để trả về một giá trị hay cả hai
	+ Được thực hiện bằng các toán tử in, out, inout:
		- IN: chỉ ra rằng tham số này là tham số đầu vào, tham số đi kèm với một giá trị và giá trị đó không thể thay đổi
		- OUT: chỉ các tham số đầu ra, chúng không mang lại bất cứ giá trị nào và sau khi đối tượng được gọi được thực thi, nó sẽ chứa giá trị kết quả sẽ được trả về đối tượng gọi
		- INOUT: thực hiện việc nhập xuất tham số cùng một lúc. Tham số đi kèm với một giá trị và có thể được thay đổi trong quá trình thực thi đối tượng. Khi hoàn tất, tham số sẽ chứa giá trị được trả về cho đối tượng đã gọi nó
	+ Mặc định: Genexus sẽ gán toán tử INOUT cho tất cả các tham số, ngay cả khi điều này không được hiển thị

## 🔹 Structured Data Type
### Kiểu dữ liệu có cấu trúc
- Phương thức của collection:
	+ &collections = New(): khởi tạo collection mới
	+ &collections.Add(): thêm phần tử mới
	+ &collections.Remove(index): xoá phần tử tại index trong collection, index bắt đầu từ 1
	+ &collections.Clear(): xoá toàn bộ collection 
	+ &collections.Sort(key): sắp xếp collection theo key
- Truy vấn dữ liệu:
	```
	for &collectionItem in &collections
		...
	endfor
	```
