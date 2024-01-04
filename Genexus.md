# **Genexus**
## 🔹 Quá trình Build của Genexus
 - Khi nhấn F5, thực hiện phân tích tác động cơ sở dữ liệu để kiểm tra xem có cần thay đổi cấu trúc CSDL hay không
 - Nếu CSDL cần đã điều chỉnh, một báo cáo phân tích tác động được hiển thị nêu chi tiết những thay đổi cần thực hiện và các câu lệnh SQL sẽ được thực thi nếu được tổ chức lại
 - Đến gia đoạn đặc tả, Genexus kiểm tra chính tả và cú pháp các đối tượng KB, cập nhật các module và phiên bản mẫu cũng như các tài nguyên cần thiết
 - Cuối giai đoạn Genexus tạo ra khung nhìn điều hướng danh sách rất hữu ít để kiểm tra bất kì lỗi nào trong đặc tả và cũng xem điều hướng đến các công thức và bảng, xác định các bảng cơ sở lọc thứ tự và các phần tử khác 
 - Sau quá trình kiểm tra hoàn tất, quá trình tạo ra source code bắt đầu, sau đó source code sẽ được biên dịch
 - Nếu nguyên mẫu được lưu trên Genexus Cloud sau khi biên dịch, ứng dụng sẽ được chuyển sang Cloud để được thực thi ở đó
## 🔹 Transaction
### Rule triggering Event
- **AfterLevel**
	```
	on AfterLevel level <tên level>
	```

	+ Sau quá trình thêm dữ liệu vào thì mới thực hiện
	+ Dữ liệu được lưu nhưng chưa được xác thực

- **BeforeInsert**: Thực hiện trước khi dữ liệu được chèn từng dòng vào DB

- **AfterInsert**: Thực hiện sau khi dữ liệu được chèn từng dòng vào DB

- **AfterComplete**: Thực hiện sau cả AfterLevel, khi dữ liệu đã được xác thực và thêm vào thành công

=> Tất cả các rule với sự kiện kích hoạt với tiền tố on ở cuối câu lệnh sẽ được thực thi tương ứng với sự kiện đó, những sự kiện này chỉ diễn ra trên máy chủ và ghi lại khoảnh khắc trước hoặc sau cột mốc thường liên quan đến cơ sở dữ liệu

### Event
- **Start**: 
	+ Luôn là sự kiện diễn ra đầu tiên
	+ Xác định một hành động sẽ được thực hiện khi chúng ta mở và bắt đầu làm việc với Transactions
	+ Không thể thực hiện load dữ liệu vào Grid

	=> Thường được dùng để gán giá trị cho các biến

- **Refresh**:
	+ Diễn ra sau event Start
	+ Web : Nó được thực thi cho mỗi lần GET hoặc POST.
	+ Smart Devices : Nó không được thực thi khi sự kiện máy khách kích hoạt.
	
- **Load**:
	+ Diễn ra sau event Refresh
	+ Hành vi của nó phụ thuộc vào đối tượng (Web Panel, Panel), vào việc có Grid trong Layout hay không và liệu có Base table (Grid là &Variable hay Attribute của Transaction) được liên kết hay không.
	+ Load N lần với N là số lần dữ liệu transaction (trong TH Attribute) và 1 lần (trong TH &Variable)

- **Track Context**: cho phép lên lịch hành động cần thực hiện khi có thay đổi được thực hiện trong bối cảnh

- **OnMessage**: sự kiện này liên quan đến thông báo trên web cho phép thực hiện các hành động trong thời gian thực

- **Insert, Update và Delete**: được liên kết với khái niệm cập nhật các Dynamic Transactions, áp dụng cho các giao dịch đặc biệt

- **Exit**: chỉ ra những hành động cần thực hiện khi quá trình thực hiện Transactions hoàn tất tức là đã được đóng lại

- **After Trn**: chỉ ra hành động cần thực hiện sau mỗi chu kỳ thực hiện Transactions, đó là ngay sau khi Commit được thực hiện.
	+ Tương tự như AfterComplete
	+ Kết thúc khối lệnh sẽ có lệnh Return để quay + lại màn hình chính

### Index trong database
- Có 3 loại Index:
	+ **Primary index**: xác định khóa chính và nó được sử dụng để kiểm soát tính duy nhất của bản ghi. Nó cũng kiểm soát khi các bản ghi được tạo trong bảng cấp dưới, bản ghi tương ứng có tồn tại trong bảng cấp trên hay không. GeneXus tự động xác định tất cả các chỉ mục chính từ transaction id

	+ **Forgen index**: được sử dụng để thực hiện kiểm soát tính toàn vẹn giữa các bảng hiệu quả hơn. Chúng cũng được xác định tự động. Khi một bản ghi bị xóa khỏi bảng phụ, sẽ không có bản ghi tương ứng nào trong bảng phụ.

	+ **User index**: chủ yếu được xác định để truy vấn dữ liệu một cách hiệu quả.

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
- **Global Formulas**
	+ Được xác định ở cấp thuộc tính trong cấu trúc Transaction. Nó được chỉ ra rằng một thuộc tính nhất định luôn được tính toán một cách nhất định
	+ Khi cần truy xuất giá trị thuộc tính trong bất kì đối tượng nào, công thức này sẽ được đánh giá để có kết quả
	+ Không thể sử dụng với biến, chỉ có thể sử dụng với attribute
	=> Lý do thuộc tính công thức là thuộc tính ảo không được lưu trữ trong bảng

- **Local Formulas (Inline Formulas)**
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

- **Quy tắc Pam**: tham số có thể được sử dụng để nhận một giá trị, để trả về một giá trị hay cả hai
	+ Được thực hiện bằng các toán tử in, out, inout:
		- **IN**: chỉ ra rằng tham số này là tham số đầu vào, tham số đi kèm với một giá trị và giá trị đó không thể thay đổi
		- **OUT**: chỉ các tham số đầu ra, chúng không mang lại bất cứ giá trị nào và sau khi đối tượng được gọi được thực thi, nó sẽ chứa giá trị kết quả sẽ được trả về đối tượng gọi
		- **INOUT**: thực hiện việc nhập xuất tham số cùng một lúc. Tham số đi kèm với một giá trị và có thể được thay đổi trong quá trình thực thi đối tượng. Khi hoàn tất, tham số sẽ chứa giá trị được trả về cho đối tượng đã gọi nó
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

## 🔹 Cập nhật Database
### Cập nhật DB sử dụng Business Components

	```
	// Insert
	&collectionTable = new()

	&collectionTable.attribute1 = 'value1'
	&collectionTable.attribute1 = 'value1'
	...

	// Update
	&collectionTable.Load(collectionTableId)

	&collectionTable.attribute1 = 'value update'
	...

	if &collectionTable.Insert() and
	   &collectionTable.Update()  
		Commit
	endif

	// Delete
	&collectionTable.Load(collectionTableId)
	&collectionTable.Delete()

	if &collectionTable.Success()
		Commit
	endif
	```

- Khi cập nhật dữ liệu, dữ liệu vẫn phải tuân theo các Rule đã được quy định (chẳng hạn nếu trong Rule quy định Name không được để trống thì khi cập nhật dữ liệu sẽ không thể thêm được)

- Sau khi cập nhật, dữ liệu vẫn chưa thể đảm bảo chắc chắn lưu vào DB vì vậy phải sử dụng lệnh Commit để dữ liệu chắc chắn được cập nhật vào DB

- Trong trường hợp xoá dữ liệu, nếu dữ liệu đó có liên quan đến bảng khác (có quan hệ), kiểm soát tính toàn vẹn tham chiếu được thực hiện bởi Transaction và Business Components sẽ ngăn chặn và thông báo lỗi

### Cập nhật DB sử dụng các lệnh dành riêng cho Produce
- Sử dụng các lệnh như New, Delete,... để cập nhật dữ liệu, tuy nhiên cách này có nhiều hạn chế:
	+ Không thể kiểm tra tính toàn vẹn của tham chiếu
	+ Không thể kích hoạt được các Rule
- Ưu điểm là hiệu suất cao hơn, ví dụ khi sử dụng lệnh Delete với dữ liệu hàng triệu thì tốc độ xử lý nhanh hơn so với những các khác.

## 🔹 Tip
- Xóa object không dùng (transaction, attribute, variable, domain, ... ): Chọn tất cả rồi nhấn Delete để xóa những thứ không cần thiết, những object có liên quan hoặc được sử dụng sẽ không thể xóa