# **MongoDB**

## 🔷 Mục lục
- **[Tổng quan MongoDB](#-tổng-quan-mongodb)**
- **[Tip](#tip)**

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

### BSON trong MongoDB

- Với việc sử dụng JSON để biểu diễn các cấu trúc dữ liệu trong Document Data Model của MongoDB, việc xây dựng các ứng dụng bằng công nghệ ngăn xếp (stacks) như MEAN (được xây dựng dựa trên **M**ongoDB, **E**xpress, **A**ngular và **N**odeJS) và MERN (được xây dựng dựa trên **M**ongoDB, **E**xpress, **R**eactJS và **N**odeJS) sẽ dễ dàng hơn vì các nhà phát triển có thể sử dụng một ngôn ngữ lập trình duy nhất (**JavaScripts**) từ đầu đến cuối. Tuy nhiên, có một số vấn đề khiến JSON không lý tưởng để sử dụng bên trong cơ sở dữ liệu:
    + JSON chỉ hỗ trợ một số lượng hạn chế các kiểu dữ liệu cơ bản. Đặc biệt là JSON không hỗ trợ dữ liệu datetime và binary
    + Các đối tượng và thuộc tính JSON không có độ dài cố định khiến việc duyệt chậm hơn
    + JSON không cung cấp Metadata và Type information, khiến việc truy xuất dữ liệu mất nhiều thời gian hơn

> Một biểu diễn nhị phân để lưu trữ dữ liệu dưới dạng tài liệu JSON, được tối ưu hoá về tốc độ, bộ nhớ và hiệu quả. Về mặt phương pháp, nó không khác gì các định dạng trao đổi nhị phân khác như Protocol Buffers hoặc Thrift. Đó chính là **BJSON (Binary JSON)**

- **BJSON** hỗ trợ nhiều kiểu dữ liệu hơn như ngày, giờ và dữ liệu nhị phân. Với khả năng cung cấp siêu dữ liệu bổ sung như thông tin về length, type, ... và cấu trúc nhị phân, **BJSON** cho phép duyệt và truy xuất dữ liệu nhanh hơn

- Ví dụ về BJSON: 
    ```json
        {"hello": "world"} 
    ```
    ```js
        \x16\x00\x00\x00           // total document size
        \x02                       // 0x02 = type String
        hello\x00                  // field name
        \x06\x00\x00\x00world\x00  // field value
        \x00                       // 0x00 = type EOO ('end of object')
    ```

## 🔷 Tương tác với cơ sở dư liệu

### Truy vấn dữ liệu

- **db.collection.find(query, projection, options)** Trả về con trỏ đến các document khớp với tiêu chí query. Mặc dù khi sử dụng find sẽ trả về document hoặc mảng các document nhưng thực tế thì phương thức này đang trả về con trỏ đến các document. Mặc định của MongoDB, **find()** không cung cấp tất cả các document, nó chỉ cung cấp 20 document đầu tiên. Tuy nhiên, có thể sử dụng phương thức **ToArray()** hoặc **forEach()** để có thể truy cập tất cả document
    ```js
    db.products.find({price: { $gte: 100000 }}) // return document[] with price >= 100000
    ```
    
    Với phương thức **forEach()** cho phép lại lại con trỏ và truy cập document
    ```js
    db.products.find().forEach(element => {
        printjson(element.name) // show value of name key in document[]
    })
    ```
    Với phương thức **forEach()**, nó thực sự sẽ chỉ tìm và nạp các document tiếp theo cho mỗi chu kì vòng lặp, do đó tất nhiên không sư dụng quá nhiều băng thông và không tải quá nhiều vào bộ nhớ

    Một số phương thức cho phép sửa đổi hành vi của con trỏ như **sort()**, **limit()**, **skip()**, ...
    ```js
    db.products.find().sort({ name: 1}) // return document[] sorted in ASC order by name key

    db.products.find().limt(5) // return document[] with max length = 5

    db.products.find().skip() // return document[] skip the first 5 documents
    ```

- **db.collection.find(query, projection, options)** Trả về một document duy nhất khớp với tiêu chí query được chỉ định trên collection hoặc view. Nếu có nhiều document thoả mãn điều kiện, phương thức này chỉ trả về document đầu tiên theo thứ tự tự nhiên của các document lưu trữ trong bộ nhớ.
    ```js
    db.products.findOne({ name: 'Keyboard' })   // return document first in memory with name: Keyboard
    ```

### Thêm mới dữ liệu

- **db.collection.insertOne()** Chèn một document duy nhất vào collection.
    ```js
    db.products.insertOne({
        name: 'Keyboard',
        price: 500000
    })
    ```
    ```json
    {
        "_id": {
            "$oid": "66b2feb5f5e99a509c228fb6"
        },
        "name": "Keyboard",
        "price": 500000,
    }
    ```

    Với **insertOne()** khi truyền một mảng document, mongoDB sẽ thêm mới một document với data là mảng các document truyền vào
    ```js
        db.products.insertOne([
            {
                name: 'Keyboard',
                price: 500000
            },
            {
                name: 'HDMI Cabel',
                price: 125000
            }
        ])
    ```
    ```json
    {
        "0": {
            "name": "Keyboard",
            "price": 500000
        },
        "1": {
            "name": "HDMI Cabel",
            "price": 125000
        },
        "_id": {
            "$oid": "66b3260978839d9bce228fb9"
        }
    }

    ```

- **db.collection.insertMany()** Chèn một hoặc nhiều document vào collection. Theo mặc định, document được chèn theo thứ tự được cung cấp. Tuy nhiên, document có thể được **mongod** sắp xếp lại để tăng hiệu suất. Chính vì vậy, các ứng dụng không nên phụ thuộc vào thứ tự chèn nếu sử dụng **insertMany()**. Khi thực hiện **insertMany()** với option là **ordered: true**, nếu việc chèn không thành công, server sẽ không tiếp tục chèn bản ghi, ngược lại, với **ordered: false**, nếu việc chèn không thành công, server vẫn sẽ tiếp tục chèn bản ghi tiếp theo
    ```js
        db.products.insertMany([
            {
                name: 'Keyboard',
                price: 500000
            },
            {
                name: 'HDMI Cabel',
                price: 125000
            }
        ])
    ```

    Với **insertMany()**, số lượng thao tác trong mỗi nhóm không được vượt quá giá trị **maxWriteBatchSize**(mặc định là 100,000). Giới hạn này ngăn ngừa các vấn đề với thông báo lỗi quá khổ. Nếu một nhóm vượt quá giới hạn này, trình điều khiển máy khách sẽ chia thành các nhóm nhỏ hoạc bằng giá trị giới hạn. Ví dụ với maxWriteBatchSize là 100,000, nếu queue bao gồm 200,000 operations, trình điều khiển sẽ tạo ra 2 nhóm với mỗi nhóm bao gồm 100,000 operations

### Cập nhật dữ liệu

- **db.collection.updateOne(filter, update, options)** Cập nhật một document duy nhất trong collection. Nếu nhiều document trong DB thoả mãn điều kiện filter thì mongoDB chỉ cập nhật cho document thoả mãn điêu kiện đầu tiên
    ```js
    db.products.updateOne({
        price: {$gte: 5000}
    }, {
        $set: { discout: true }
    })
    ```

- **db.collection.updateMany(filter, update, options)** Cập nhật tất cả document phù hợp với filter được chỉ định cho một collection
    ```js
    db.products.updateMany({
        price: {$gte: 5000}
    }, {
        $set: { discout: true }
    })
    ```

- Sự khác nhau giữa **replaceOne()** và **updateOne()**: **db.collection.replaceOne(filter, update, options)** được sử dụng để thay thế một document duy nhất trong collection thoả mãn filter. Điều này có nghĩa là document hiện tại sẽ bị xoá và được thay thế bằng một document mới. Tuy nhiên, với **updateOne()**, document sẽ không được thay thế hoàn toàn mà thay vào đó, chỉ các trường được chỉ định sẽ được cập nhật
