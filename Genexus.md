# **Genexus**

## 🔷  MỤC LỤC

- **[Tổng quan Genexus](#-tổng-quan-genexus)**
- **[Transaction](#-transaction)**
- **[Danh sách và truy cập dữ liệu theo code](#-danh-sách-và-truy-cập-dữ-liệu-theo-code)**
- **[Giao tiếp giữa các đối tượng](#-giao-tiếp-giữa-các-đối-tượng)**
- **[Structured Data Type](#-structured-data-type)**
- **[Cập nhật Database](#-cập-nhật-database)**
- **[Thiết kế và mô hình hoá màn hình](#-thiết-kế-và-mô-hình-hoá-màn-hình)**
- **[Tip](#-tip)**

## 🔷 Tổng quan Genexus

### Khái niệm

- **Genexus** là một nền tảng thông minh giúp đơn giản hoá việc phát triển phần mềm, tối đa việc tự động hoá cho quá trình phát triển, hay còn được gọi là Low Code. Thông qua các kĩ thuật trí tuệ nhân tạo, Genexus tự động tạo mã nguồn, giảm thiểu thời gian cần thiết cho việc phát triển, cải tiến và bảo trì ứng dụng

- **Genexus** cung cấp các tính năng cơ bản sau:
	+ Phát triển linh hoạt và gia tăng với việc tạo nhanh các nguyên mẫu chức năng
	+ Đa nền tảng, cho phép xây dựng nhiều loại ứng dụng khác nhau như là hệ thống Cobol, RPG, đến các ứng dụng Web hiện đại trong Angular Framework, các ứng dụng cho các thiết bị di động như đồng hồ, điện thoại thông minh, ... cũng như các ứng dụng AI, Chatbots, mô hình hoá quy trình kinh doanh, ...
	+ Tích hợp các hệ thống hiện có và cơ sở dữ liệu kế thừa
	+ Làm việc theo nhóm, triển khai phiên bản, Testing, Deployment, DevOps
	+ Liên tục thích ứng với sự thay đổi công nghệ, giúp các tổ chức đổi mới nhanh chóng và hiệu quả

### Quá trình build ứng dụng Genexus

- Khi nhấn F5, thực hiện phân tích tác động cơ sở dữ liệu để kiểm tra xem có cần thay đổi cấu trúc CSDL hay không
- Nếu CSDL cần đã điều chỉnh, một báo cáo phân tích tác động được hiển thị nêu chi tiết những thay đổi cần thực hiện và các câu lệnh SQL sẽ được thực thi nếu được tổ chức lại
- Đến gia đoạn đặc tả, Genexus kiểm tra chính tả và cú pháp các đối tượng KB, cập nhật các module và phiên bản mẫu cũng như các tài nguyên cần thiết
- Cuối giai đoạn Genexus tạo ra khung nhìn điều hướng danh sách rất hữu ít để kiểm tra bất kì lỗi nào trong đặc tả và cũng xem điều hướng đến các công thức và bảng, xác định các bảng cơ sở lọc thứ tự và các phần tử khác
- Sau quá trình kiểm tra hoàn tất, quá trình tạo ra source code bắt đầu, sau đó source code sẽ được biên dịch
- Nếu nguyên mẫu được lưu trên Genexus Cloud sau khi biên dịch, ứng dụng sẽ được chuyển sang Cloud để được thực thi ở đó

## 🔷 Transaction

### Base Table và Extended Table

- **Base Table (Bảng cơ sở)**: là bảng bất kì được định vị để chỉnh sửa trong một khoảng thời gian cụ thể
- **Extended Table (Bảng mở rộng)**: tại một thời điểm nhất định, Extended table của một Base table là tổng tất cả thuộc tính của chính Base table đó, cộng với tất cả thuộc tính của các bảng liên quan trực tiếp hoặc gián tiếp đến nó thông quan quan hệ N - 1

### Rule

- Xử lý ở phía Client (Client-Side Validation - xử lý và hiển thị tức thời khi người dùng thao tác) và được thực hiện tại Server thêm một lần nữa như thể đó là người dùng (đối với các rule check lỗi)

- **Serial**: Tự động đánh số cấp độ level 2, level 3 hoặc các level lồng nhau khác của đối tượng Transaction.

	```js
	Serial(attr1, attr2, step);
	// attr1: Attribute cần tăng tự động (Attribute của bảng level 2, level 3, ...)
	// attr2: Attribute cuối của level 1
	// step: bước tăng
	```

- **NoAccept**:
	+ Ngăn chặn nhập giá trị cho Attribute hoặc Variable từ màn hình (chuyển đổi thành Read Only) khi áp dụng điều kiện (nếu có)
	+ Nếu không thể ngăn chặn được đầu vào (ví dụ Business Component, iSeries, ...) thì giá trị input sẽ bị bỏ qua

	```js
	NoAccept(att | &var) [ IF condition ][ ON triggering event];
	// att: Attribute input
	// &var: Variable input
	// condition: điều kiện thực hiện Rule
	// triggering event: kích hoạt triggering event (BeforeInsert, AfterInsert, ...)
	```

### Rule triggering Event

- Tất cả các Rule có sự kiện kích hoạt liên quan (có tiền tố ON đi kèm) sẽ được thực thi tại thời điểm tương ứng với sự kiện đó, đây là những sự kiện chỉ diễn ra trên Server thường liên quan đến CSDL
- **On AfterLevel**

	```js
	on AfterLevel level <tên level>
	```

	+ Sau quá trình thêm dữ liệu vào thì mới thực hiện
	+ Dữ liệu được lưu nhưng chưa được xác thực

- **On BeforeInsert**: Thực hiện trước khi dữ liệu được chèn từng dòng vào DB

- **On AfterInsert**: Thực hiện sau khi dữ liệu được chèn từng dòng vào DB

- **On AfterComplete**: Thực hiện sau cả AfterLevel, khi dữ liệu đã được xác thực và thêm vào thành công (ngay sau Commit)

### Event

- Không thể cập nhật Database: Không thể gán trực tiếp giá trị cho một Attribute nhưng có thể gọi một thủ tục để thực hiện cập nhật cần thiết

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

- **Track Context**: cho phép lên lịch hành động cần thực hiện khi có thay đổi được thực hiện trong bối cảnh thực thi Transaction

	```js
	Event TrackContent(&AttractionId)
		WCDetails.Object = AttractionsDetail.Create(&AttractionId)
	EndEvent
	```

- **OnMessage**: sự kiện này liên quan đến thông báo trên web cho phép thực hiện các hành động trong thời gian thực

- **Insert, Update và Delete**: được liên kết với khái niệm cập nhật các Dynamic Transactions, áp dụng cho các giao dịch đặc biệt

- **Exit**: chỉ ra những hành động cần thực hiện khi quá trình thực hiện Transactions hoàn tất tức là đã được đóng lại

- **After Trn**: chỉ ra hành động cần thực hiện sau mỗi chu kỳ thực hiện Transactions, đó là ngay sau khi Commit được thực hiện.
	+ Tương tự như AfterComplete
	+ Kết thúc khối lệnh sẽ có lệnh Return để quay + lại màn hình chính

### Index trong Transaction

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

### Formulas

* Phân loại theo định nghĩa
	- **Global Formulas**
		+ Được xác định ở cấp thuộc tính trong cấu trúc Transaction. Nó được chỉ ra rằng một thuộc tính nhất định luôn được tính toán một cách nhất định
		+ Khi cần truy xuất giá trị thuộc tính trong bất kì đối tượng nào, công thức này sẽ được đánh giá để có kết quả
		+ Không thể sử dụng với Variable, chỉ có thể sử dụng với Attribute
		=> Lý do thuộc tính công thức là thuộc tính ảo không được lưu trữ trong DB

	- **Local Formulas (Inline Formulas)**
		+ Có thể được thiết lập để chỉ được đánh giá trong mã đối tượng nơi chúng được đặt
		+ Là công thức được nên dưới dạng hướng dẫn cụ thể trong một mã nhất định
		+ Có thể sử dụng cả Variable và Attribute
  
* Phân loại theo điều hướng
	- **Aggregate Formulas** :
		+ Cho phép xác định một số loại tính toán hoặc tìm kiếm, bao gồm nhiều bản ghi của một bảng (và được liên kết bằng Extended Table).
		+ Bao gồm: Sum, Count, Average, Max, Min, Find.

	- **Horizontal Formulas** :
		+ Cho phép xác định các biểu thức (số học hoặc bất kỳ loại nào khác).
		+ Điều xác định một công thức có tính chiều ngang là thực tế là các Attribute liên quan thuộc về một Extended Table.

	- **Compound Formulas**: là sự kết hợp sử dụng giữa Aggregate Formula và Horizontal Formula

- So sánh việc sử dụng Attribute Formula và Formula trong Rule:
	+ **Attribute Formula** (Global): khi có bất kì đối tượng nào truy vấn giá trị Attribute thì Formula được kích hoạt và cập nhật giá trị một cách nhanh chóng. Tuy nhiên nếu việc tính toán liên quan đến nhiều bản ghi và mỗi lần phải thực hiện thường xuyên thì có thể gây ảnh hưởng đến hiệu suất ứng dụng

	+ **Formular trong Rule** (Local): giá trị Attribute được gán cục bộ bởi quy tắc trong Rule, chính vì vậy nó không thể bị ép buộc kích hoạt Rule theo yêu cầu. Attribute vẫn được lưu trữ và giá trị của nó có thể chỉnh sửa thông qua biểu mẫu. Trong trường hợp Formula phức tạp thì nên sử dụng để tránh gây ảnh hưởng đến hiệu suất ứng dụng

## 🔷 Danh sách và truy cập dữ liệu theo code

### Truy vấn dữ liệu các giữa các Transaction

- Sử dụng For Each Command truy xuất dữ liệu từ cơ sở dữ liệu. Khi được sử dụng với Procedure, ngoài việc đọc dữ liệu nó còn được sử dụng để cập nhật cơ sở dữ liệu
- Để sắp xếp các dữ liệu được in ra, sử dụng order

	```js
	For Each Attraction Order AttractionName ...   // sắp xếp AttractionName theo ASC
	For Each Attraction Order (AttractionName) ... // sắp xếp AttractionName theo DESC
	```

- Inner Join (Natural Join) và Outer Join (Left Join)
	+ Inner Join (Natural Join):

		```js
		For Each Attraction, Category
			Where Attraction.CategoryId = Category.CategoryId
			Where Attraction.CountryId = Category.CountryId
			/* code */
		EndFor
		```

	+ Outer Join (Left Join):

		```js
		For Each Attraction
			For Each Category
				Where Category.CountryId = Attraction.CountryId
				/* code */
			EndFor
			/* code */
		EndFor
  		```

- Các trường hợp For Each lòng nhau (Nested For Each)
	+ **Control Break**: các Base Table của mỗi vòng For là giống nhau

	+ **Cartesian Product**: các Base Table của mỗi vòng For đều khác nhau và chúng không có mối quan hệ trực tiếp hoặc gián tiếp N - 1. Vì vậy, kết quả thu được là Tích Descartes của các bảng này: đối với mỗi bảng ghi của bảng For Each cơ sở chính, nó truy xuất tấp cả bản ghi của bảng For Each cơ sở lòng nhau

	+ **Join**: các Base Table của mỗi vòng For đều khác nhau và có mỗi quan hệ trực tiếp hoặc gián tiếp 1 - N. Vì vậy, đối với mỗi bản ghi của bảng For Each cơ sở chính, Genexus tìm thấy N bản ghi có liên quan trực tiếp hoặc gián tiếp đến nó trong bảng For Each cơ sở lòng nhau

### Subroutine

- Là các chương trình con, chúng là các code block cho phép chúng ta module hoá code và có thể sử dụng bao nhiêu lần tuỳ thích trong cùng một đối tượng
- Các đối tượng có thể sử dụng được ở Web Panels, Procedures, Transactions, ...
- Không hỗ trợ gửi tham số, các biến được sử dụng để trao đổi dữ liệu. Nếu một Attribute có một giá trị thì khi gọi Subroutine nó sẽ thay đổi. Khi Return từ Subrountine và truy vấn giá trị, nó sẽ có giá trị được gán trong đó (vì các thuộc tính là toàn cục đối với đối tượng)
- Nếu lệnh gọi được thực hiện từ bên trong lệnh For Each và Subroutine cũng có lệnh For Each thì chúng sẽ không được lồng nhau, nghĩa là sẽ không có suy luận hoặc bộ lọc nào được thực hiện

### Unique Clause

- Cho phép chỉ ra Attribute hoặc tập hợp các Attribute có giá trị không được lặp lại trong đầu ra truy vấn
	
	```js
	// Unique clause with For Each
	For Each Attraction
		Unique CategoryId
	EndFor

	// Unique clause with Data Provider
	ReservationByDay from Reservation unique ReservationDate
	{
		ReservationByDayItem
		{
			ReservationDate
			ReservationTotal
		}
	}
	```

- Các hạn chế khi sử dụng Unique Clause
	+ Không thể sử dụng biểu thức trong danh sách các Attribute được khai báo trong Unique Clause
		```js
		// Cannot use
		Unique ReservationDate.Year()
  		```

	+ Cả trong nội dung lệnh For Each và trong nhóm của Data Provider (trừ các công thức nội tuyến) chỉ có thể bao gồm các Attribute có giá trị duy nhất được khai báo trong Unique Clause và Attribute liên quan (cùng 1 record)
	+ Không thể sử dụng Unique Commnand trong Nested For Each. Cho đến nay, nó không thể sử dụng để thực hiện Control Break.

### Data Selector

- **Data Selector** cho phép lưu trữ một tập hợp các Parameters, Conditions, Orders và Defined By để người dùng có thể gọi từ các truy vấn và tính toán khác nhau đồng thời tái sử dụng cùng một cơ chế điều hướng nhiều lần
	
	```js
	// Filter using Data Selector with For Each command
	For Each Customer
		USING CustomerDataSelector(&DateFrom, &DateTo)
	EndFor

	// Query using Data Selector with For Each command
	For Each Country
		Where CountryId IN CustomerDataSelector(&DateFrom, &DateTo)
	EndFor

	// Data Selector in Formula
	For Each Invoice
		&Qty = Count(InvoiceDate, USING CustomerDataSelector(&DateFrom, &DateTo))
	EndFor
	```

- Việc xác định Data Selectors mang lại những lợi ích sau:
	+ Lưu và tái sử dụng code: chỉ cần định nghĩa Data Selector một lần, sau đó có thể tái sử dụng nhiều nơi trong KB
	+ Giảm thiểu công tác bảo trì: chỉ cần thay đổi định nghĩa Data Selector tại một nơi, và mọi thay đổi sẽ tự động được áp dụng cho mọi nơi nó được sử dụng trong KB
	+ Hỗ trợ đào tạo người dùng Genexus mới: Data Selector cung cấp tính đóng gói code và dễ dàng học, định nghĩa và sử dụng

## 🔷 Giao tiếp giữa các đối tượng

### Parm

- **Parm**: khai báo danh sách các tham số mà đối tượng Genexus nhận được từ một hoặc nhiều đối tượng khác gọi nó.
  
- **Quy tắc Pam**: tham số có thể được sử dụng để nhận một giá trị, để trả về một giá trị hay cả hai
	+ Được thực hiện bằng các toán tử in, out, inout:
		- **IN**: chỉ ra rằng tham số này là tham số đầu vào, tham số đi kèm với một giá trị và giá trị đó không thể thay đổi
		- **OUT**: chỉ các tham số đầu ra, chúng không mang lại bất cứ giá trị nào và sau khi đối tượng được gọi được thực thi, nó sẽ chứa giá trị kết quả sẽ được trả về đối tượng gọi
		- **INOUT**: thực hiện việc nhập xuất tham số cùng một lúc. Tham số đi kèm với một giá trị và có thể được thay đổi trong quá trình thực thi đối tượng. Khi hoàn tất, tham số sẽ chứa giá trị được trả về cho đối tượng đã gọi nó

	+ Mặc định: Genexus sẽ gán toán tử INOUT cho tất cả các tham số, ngay cả khi điều này không được hiển thị

### Global Events

- **Global Events**: cho phép xác định các sự kiện toàn cục cho tất cả các thành phần của ứng dụng. Một Web Page có thể được tạo thành từ một số Component, vì vậy ý tưởng của Global Events là để các Component và Web Panel có thể giao tiếp với nhau. Thông qua Global Events, tất cả các thành phần của màn hình có thể tương tác với nhau vì các sự kiện có thể định nghĩa và được gọi từ bất kì thành phần nào.
  
- **Global Events** được triển khai thông qua GlobalEvents External Object, được import tự động bởi Genexus, nó cho phép bạn tạo Global Events để đạt được sự tương tác linh hoạt hơn giữa các thành phần của Form, trong ứng dụng Web và thiết bị thông minh

	```js
	// Home Web Panel
	// Define ShowMsg in GlobalEvents with paramater &piMsg
	Event GlobalEvents.ShowMsg(&piMsg)
		&piMsgs.Add(&piMsg)
		
		for &piMsg in &piMsgs
			msg(&piMsg)
		endfor
	Endevent
	```

	```js
	// Home Component is component of Home Web Panel
	Event Start
		GlobalEvents.ShowMsg('This is Home Component')
	EndEvent
	```

	```js
	// Menu Component isn't component of Home Web Panel
	Event Start
		// Show Msg not working
		GlobalEvents.ShowMsg('This is Menu Component')
	EndEvent
	```

## 🔷 Structured Data Type

- Phương thức của collection:
	+ &collections = New(): khởi tạo collection mới
	+ &collections.Add(): thêm phần tử mới vào cưới danh sách
	+ &collections.Remove(index): xoá phần tử tại index trong collection, index bắt đầu từ 1
	+ &collections.Clear(): xoá toàn bộ collection
	+ &collections.Sort(key): sắp xếp collection theo key (Sort theo nhiều key)

- Truy vấn dữ liệu:
	
	```js
	For &collectionItem in &collections
		/* code */
	EndFor

	For &index = 1 to &collections.Count
		&collections.Item(&index) ...
	EndFor
	
	&collections.Sort('key1, key2')
	```

## 🔷 Cập nhật Database

### Business Component

- **Business Component** không chỉ đại diện cho các bảng dữ liệu, mà còn chứa đựng cả hành vi (Methods) và quy tắc (Rules) liên quan đến dữ liệu đó. Các thành phần này giúp đơn giản hóa các thao tác liên quan đến dữ liệu (CRUD), đồng thời giúp quản lý các quy tắc kinh doanh ở mức độ đối tượng, giảm thiểu sự lặp lại và tăng cường khả nặng tái sử dụng trong các ứng dụng

- Business Component thường được mô tả thông qua các thuộc tính sau:
	+ Attribute: Các trường dữ liệu mà đối tượng cần để xác định trạng thái của nó
	+ Methods: Các hành động mà đối tượng có thể thực hiện, ví dụ: Save, Delete, Load, ...
	+ Rules: Các quy tắc kinh doanh mà đối tượng cần tuân theo

### Cập nhật DB sử dụng Business Components

	```js
	// Insert
	&collectionTable = new()

	&collectionTable.attribute1 = 'value1'
	&collectionTable.attribute1 = 'value1'
	...

	// Update
	&collectionTable.Load(collectionTableId)

	&collectionTable.attribute1 = 'value update'
	...

	If &collectionTable.Insert() And &collectionTable.Update()  
		Commit
	EndIf

	// Delete
	&collectionTable.Load(collectionTableId)
	&collectionTable.Delete()

	If &collectionTable.Success()
		Commit
	EndIf
	```

- Khi cập nhật dữ liệu, dữ liệu vẫn phải tuân theo các Rule đã được quy định (chẳng hạn nếu trong Rule quy định Name không được để trống thì khi cập nhật dữ liệu sẽ không thể thêm được)

- Sau khi cập nhật, dữ liệu vẫn chưa thể đảm bảo chắc chắn lưu vào DB vì vậy phải sử dụng lệnh Commit để dữ liệu chắc chắn được cập nhật vào DB

- Trong trường hợp xoá dữ liệu, nếu dữ liệu đó có liên quan đến bảng khác (có quan hệ), kiểm soát tính toàn vẹn tham chiếu được thực hiện bởi Transaction và Business Components sẽ ngăn chặn và thông báo lỗi

### Cập nhật DB sử dụng các lệnh dành riêng cho Produce

- Sử dụng các lệnh như New, Delete,... để cập nhật dữ liệu, tuy nhiên cách này có nhiều hạn chế:
	+ Không thể kiểm tra tính toàn vẹn của tham chiếu
	+ Không thể kích hoạt được các Rule
	+ Chỉ được sử dụng ở Procedure
	
	```js
	// Create with new command
	New
		AttractionName = 'attraction'
		AttractionCountryId = find(CountryId, CountryName = 'countryName')
		AttractionCategoryId = find(CategoryId, CategoryName = 'categoryName')
	EndNew

	// Update with For Each
	For Each Attraction
		Where AttractionCountryId < 10
			AttractionCountryId = 10
	EndFor

	// Delete with delete command
	For Each Attraction
		Where AttractionCountryId < 10
			Delete
	EndFor
	```

- Tuy nhiên nó cũng có những ưu điểm như sau:
	+ Hiệu suất cao hơn, ví dụ khi sử dụng lệnh Delete với dữ liệu hàng triệu thì tốc độ xử lý nhanh hơn so với những các khác.
	+ Cú pháp ngắn gọn, dễ dàng sử dụng. Thay vì phải khai báo Business Component để cập nhật dữ liệu thì chúng ta có thể thực hiện hoàn toàn bằng các Command

- Một số lưu ý khi sử dụng Procedure Command:
	+ Với mọi Procedure Command, tất cả Attribute của bản ghi và các Attribute liên quan của Extended Table đều có thể cập nhật, ngoại trừ Primary Key
	+ Khi sử dụng New Command, nếu Primary Key của bản ghi thêm mới vào trùng với Primary Key đã tồn tại trong CSDL, thì quá trình thêm mới sẽ không được thực hiện. Vì vậy có thể sử dụng New Command như để kiểm tra dữ liệu, bản ghi thêm mới chưa có trong CSDL (chỉ kiểm tra tồn tại đối với Primary Key) thì thêm mới bản ghi, ngược lại thì cập nhật bản ghi đã có.
		
		```js
		New
			AttractionId = 1
			AttractionName = 'Eiffel Tower'

		When Duplicate
			For Each Attraction
				AttractionName = 'Eiffel Tower'
			EndFor
		EndNew
		```

	+ Khi cần cập nhật với một số lượng lớn bản ghi, việc giảm số lượng khứ hồi về hệ quản trị CSDL (Database Management System - DBMS) là một giải pháp. Việc chặn các hoạt động cập nhật dữ liệu yêu cầu phải lưu trữ chúng trong bộ nhớ và gửi chúng theo nhóm tới DBMS. Thay vì thao tác với DBMS trong mọi thao tác cập nhật CSDL, tương tác chỉ diễn ra sau mỗi N thao tác cập nhật, trong đó N là số chỉ định. Vì vậy Blocking Command là giải pháp cho vấn đề trên, nó sẽ giảm số lượng khứ hồi đến Server, một tập hợp các bản cập nhật CSDL chỉ được gửi tới DBMS sau N lần chỉ định
		
		```js
		For Each Attraction
			Blocking 100
				AttractionName = ...
		EndFor
		```

	+ Mặc dù các Procedure Command không kiểm tra tính toàn vẹn, tuy nhiên trong CSDL sẽ có. Chẳng hạn nến thêm mới một bản ghi có trường là khoá ngoại đến bảng khác và giá trị của trường đó là không tồn tại trong bảng đó, mặc dù New Command đã có gắng thực hiện thêm mới nhưng CSDL không cho phép và Server sẽ đưa ra SQLExeception. Để tắt tính năng này của CSDL, trong Data Stores SQL Server Properties, đổi Declare referential integrity property thành No (mặc định là Yes)

	+ Nếu Formula Attribute phụ thuộc vào Attribute đang được cập nhật, Genexus sẽ không tìm kiếm hoặc tính toán giá trị mới, vì vậy, quá trình này phải được thực hiện thủ công

	+ Khi sử dụng các lệnh New, Delete, ... hoặc cập nhật dữ liệu của Procedure, chỉ khi thực hiện Commit thì dữ liệu mới được cập nhật, tuy nhiên cấu hình mặc định của Genexus là tự động commit khi kết thúc Procedure. Để tắt tính năng này, trong Property của Procedure, có tuỳ chọn Commit On Exit mặc định là Yes, vì vậy nên chuyển về No để tránh việc không kiểm soát được dữ liệu commit lên CSDL

### Tính toàn vẹn trong Transaction

- **Logical Unit of Work (LUW)**:
	+ Đơn vị công việc logic là tập hợp các thao tác đối với CSDL phải được thực thi tất cả hoặc không thực hiện bất kỳ thao tác nào trong số đó
	+ Tập hợp các bản cập nhật xác định LUW đảm bảo tính toàn vẹn của CSDL ở mức logic

- **Customizing LUWs**:
	+ Nếu từ một Transaction, một Procedure được gọi để gọi một Procedure khác, tất cả đều bị vô hiệu hoá Commit ngoại trừ Commit cuối cùng hoặc tất cả Commit đều vô hiệu hoá trừ Commit của Transaction, nó sẽ Commit các bản ghi của Transaction và của tất cả Procedure
	+ Tuy nhiên nếu Transaction A gọi một Transaction B khác thì Commit của Transaction B sẽ không Commit các bản ghi do Transaction A đầu tiên xử lý vì đây là các hoạt động Commit độc lập

## 🔷 Thiết kế và mô hình hoá màn hình

### Unanimo

- **Unanimo**: là một hệ thống thiết kế (Design System) cho phép củng cố và tăng cường tính nhất quán trong việc thiết kế ứng dụng

- Có các đặc điểm chính như sau:
	+ **Đa trải nghiệm**: Web responsive, Native Mobile, Chatbots, Inbox-driven
	+ **Cross product** (có khả năng tích hợp vào các Product khác nhau): GAM, Genexusflow(Hệ thống quản lý quy trình làm việc - Workflow Management System), Chatbots và Dashboards
	+ **Standard Module**: được phát triển trong một Genexus Module và được phát hành dưới dạng là một Module
	+ **Xây dựng dựa trên công nghệ mới nhất**: DSO (Design System Object) xác định các tính năng style cho Screen controls, nhằm mục đích tăng cường sự trừu tượng trong thiết kế ứng dụng, cho phép tái sử dụng và lắp ghép dễ dàng hơn
	+ **Cá nhân hoá và mở rộng**: thiết kế riêng cho bản thân, cho giải pháp hoặc doanh nghiệp

- **Unanimo** bao gồm 4 phần chính:
	+ Design System (Tokens - Styles)
	+ Hình ảnh và các tài nguyên khác
	+ User Controls (Custom UI - Chameleon Library)
	+ Stencils

## 🔷 Tip

- **Xóa object không dùng (transaction, attribute, variable, domain, ... )**

	Chọn tất cả rồi nhấn Delete để xóa những thứ không cần thiết, những object có liên quan hoặc được sử dụng sẽ không thể xóa

- **Sử dụng Formula Attribute như một Attribute thông thường và tồn tại vật lý**

	Để sử dụng như một Formula Attribute (Virual Attribute) nhưng Attribute vẫn được lưu trong DB thì có thể sử dụng Formula trong Rule
	
	```js
	// Rule
	FlightCapacity = count(FlightSeatLocation)
	```

- **Một số lưu ý khi khởi tạo Procedure**

	Với Call Protocol property của Procedure là Command Line, thì Parm không được chứa Variable input theo dạng Collection

- **Lưu ý khi sử dụng Aggregate Formula**

	Không nên dùng Aggregate Formula trong For Each với điều kiện chứa các Attribute của Transaction truy vấn, lúc này Genexus sẽ tự động đặt các Attribute vào ngữ cảnh của For Each vì vậy Aggregate Formula chỉ được tính với 1 record
	
	```js
	// Should not be used
	For Each Trip
		Where TripId = Max(TripDate, TripDate < &Today, 0, TripId)
	EndFor

	// Should use
	&TripIdWithMaxTripDate = Max(TripDate, TripDate < &Today, 0, TripId)
	For Each Trip
		Where TripId = &TripIdWithMaxTripDate
	EndFor
	```

- **Hiển thị Blank với giá trị Empty của Data Type DateTime, Numberic, ...**

	Với mỗi atttribute hoặc biến (kiểu dữ liệu nguyên thuỷ) đều có thuộc tính Picture để mô tả hiển thị dữ liệu của attribute hoặc biến đó trên màn hình. Riêng về dữ liệu có dạng số (numeric hoặc date/datetime), với chữ số `9` biểu diễn cho hiển thị `0` khi giá trị là rỗng, với chữ cái là `Z` biểu diễn cho hiển thị `blank` khi giá trị rỗng, với dấu `#` không hiển thị số `0` ở bên trái hoặc bên phải (số `0` không có ý nghĩa - 0009.120), với dấu `?` hiển thị `blank` thay cho số `0` ở bên trái hoặc bên phải(số `0` không có ý nghĩa - 0009.120) và duy trì sự căn chỉnh của số

	```js
	// display Price with picture ZZ,ZZZ,ZZ9.99

	Price 12,124,245.32
	Price 0.00

	// display Price with picture ####9.###

	Price 21351.1
	Price 251.121
	Price 0

	// display Price with picture ????9.???
	
	Price 24590.254
	Price    12.24
	Price     0
	```

	Trong mục **Property** của attribute/biến, có thể chỉnh ở phần Picture. Ngoài ra, ta có thể set picture với control name bằng thuộc tính **Picture**
	
	```js
	price.picture = 'ZZ,ZZZ,ZZ9.99' // set picture with control name of price
	```

- **Auto refresh trang web**

	Để bật chức năng tự động Refresh Web Panel trong một khoảng thời gian có thể sử dụng thuộc tính Refresh TimeOut với Lapse là số giây trôi qua để thực hiện lần Refresh tiếp theo

- **Cách query View trong Database**

	Tạo một Transaction với các field giống với View trong Database. Trước khi thực hiện Build, mở Default (Java) Property (có thể tuỳ theo ngôn ngữ được setting lúc khởi tạo KB), trong option Reorganize server tables chọn No để tránh trường hợp tạo ra Table trong DB đè lên View. GX sẽ tự động mapping Transaction với View trong DB, lúc này có thể thực hiện query bình thường
