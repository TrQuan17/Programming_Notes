# **MongoDB**

## 🔷 Mục lục
- **[Tổng quan MongoDB](#-tổng-quan-mongodb)**
- **[Lược đồ (Schemas)](#-lược-đồ-schemas)**
- **[Quan hệ (Relations)](#-quan-hệ-relations)**
- **[Tương tác với cơ sở dữ liệu](#-tương-tác-với-cơ-sở-dữ-liệu)**
- **[Một số toán tử cơ bản](#-một-số-toán-tử-cơ-bản)**

- **[Tip](#-tip)**

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

> Một biểu diễn nhị phân để lưu trữ dữ liệu dưới dạng tài liệu JSON, được tối ưu hoá về tốc độ, bộ nhớ và hiệu quả. Về mặt phương pháp, nó không khác gì các định dạng trao đổi nhị phân khác như Protocol Buffers hoặc Thrift. Đó chính là **BSON (Binary JSON)**

- **BSON** hỗ trợ nhiều kiểu dữ liệu hơn như ngày, giờ và dữ liệu nhị phân. Với khả năng cung cấp siêu dữ liệu bổ sung như thông tin về length, type, ... và cấu trúc nhị phân, **BSON** cho phép duyệt và truy xuất dữ liệu nhanh hơn

- Ví dụ về BSON: 

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

## 🔷 Lược đồ (Schemas)

- **Schema** là đối tượng **JSON** xác định cấu trúc và nội dung dữ liệu cụ thể của ứng dụng, mô tả các trường mà document có, loại giá trị mà các trường đó chứa và các điều kiện phải đáp ứng để thay đổi giá trị là hợp lệ. Mặc định, MongoDB thực thi không sử dụng **Schema**, các document có thể có cấu trúc khác nhau trong cùng một collection, tuy nhiên điều đó không có nghĩa là không thể sử dụng **Schema**

- Trong MongoDB, **Schema** được định nghĩa ở cấp độ collection, nó không chỉ bao gồm lược đồ JSON tiêu chuẩn, ngoài ra còn hỗ trợ cho các loại BSON tích hợp của MongoDB, cho phép mô tả một cách đầy đủ các kiểu dữ liệu trong MongoDB

- **Schema** sẽ được thực thi khi có bất kì dữ liệu nào được ghi vào MongoDB. Điều này bao gồm thêm mới, cập nhật và xoá từ dịch vụ API, hàm (Function) hoặc đồng bộ hoá thiết bị (Device Sync)

- Cú pháp cơ bản của một Schema như sau
    ```json
    {
        "bsonType": "object",
        "title": "<type name>",
        "required": ["<required field names>"],
        "properties": {
            "<field name>": "Schema"
        }
    }
    ```
    ```json5
    {
        // basic schema for product about products
        "title": "product",
        "required": [
            "_id",
            "name",
            "price"
        ],
        "properties": {
            "_id" : { "bsonType": "objectId"},
            "name" : { "bsonType": "string"},
            "price" : { "bsonType": "number"}
        }
    }
    ```

- Để thực hiện nhúng Schema cho collection, ta sử dụng kết hợp **db.createCollection(name, options)** để tạo các collection mới với các tuỳ chọn cụ thể và toán tử **$jsonSchema** sẽ so khớp các document tương ứng **JSON Schema** đã chỉ định
    ```js
    db.createCollection('products', {
        validator: {
            $jsonSchema: {
                bsonType: 'object',
                required: ['name', 'price', 'brand'],
                properties: {
                    name: {
                        bsonType: 'string',
                        description: 'must be a string and is required!'
                    },
                    price: {
                        bsonType: 'number',
                        description: 'must be a number and is required!'
                    },
                    brand: {
                        bsonType: 'objectId',
                        description: 'must be an ObjectId and is exist in the Brand document!'
                    }
                }
            }
        }
    })
    ```

- Cập nhật Schema với **db.runCommand(command, [options])**
    ```js
    db.runCommand({ 
        collMod: 'products',
        validator: {
            $jsonSchema: {
                bsonType: 'object',
                required: ['name', 'price'],
                properties: {
                    name: {
                        bsonType: 'string',
                        description: 'must be a string and is required!'
                    },
                    price: {
                        bsonType: 'number',
                        description: 'must be a number and is required!'
                    },
                    brand: {
                        bsonType: 'objectId',
                        description: 'is exist in the Brand document!'
                    }
                }
            }
        }
    })
    ```

## 🔷 Quan hệ (Relations)

### Mô hình One - One Relationships với Embedded Document
- Trong MongoDB, mô hình **One - One** là một mô hình dữ liệu mô tả mối liên hệ giữa hai collection mà trong đó một document trong collection này được liên kết chính xác với một document trong collection khác

- Embedded Document được sử dụng tối ưu nhất để mô tả mối quan hệ **One - One** giữa dữ liệu được kết nối. Embedded Document được kết nối vào một document duy nhất có thể giảm số lượng thao tác truy vấn cần thiết để lấy dữ liệu
    ```js
    {
        username: 'QuanTT',
        setting: {
            themeColor: '#000000',
            language: 'VietNam',
            backgroundURL: 'www.background.com?image=1'
        }
    }
    ```

### Mô hình One - Many Relationships với References Document
- Trong MongoDB, mô hình **One - Many** là một mô hình dữ liệu mô tả mối liên hệ giữa hai collection mà trong đó một document trong collection này có thể liên kết với nhiều document trong collection khác

- References Document được sử dụng tối ưu nhất để mô tả mối quan hệ **One - Many** giữa dữ liệu được kết nối
    ```js
    // OS
    {
        _id: ObjectId('66cfe183ab74488678228fb6')
        name: 'Microsoft Windows',
        developed: 'Microsoft',
        packageManager: 'Windows Installer(.msi .msp)',
        platforms: 'X86-64',
        InitialRelease: '20/11/1985'
    }
    ```
    ```js
    // products
    {
        name: 'Lenovo LOQ 15IAX9 83FQ0005VN',
        detail: {
            CPU: 'Intel Core i5-12450HX',
            RAM: '2x 8GB DDR5-4800Mhz',
            Memory: '512GB SSD M.2 2242 PCIe 4.0x4 NVMe',
            Screen: '15.6inch FHD (1920x1080)'
        },
        OS: ObjectId('66cfe183ab74488678228fb6')
    }
    ```

### Mô hình Many - Many Relationships với References Document
- Trong MongoDB, mô hình **Many - Many** là một mô hình dữ liệu mô tả mối liên hệ giữa hai collection mà trong đó một document trong collection này có thể liên kết với nhiều document trong collection khác, và ngược lại

- References Document được sử dụng tối ưu nhất để mô tả mối quan hệ **Many - Many** giữa dữ liệu được kết nối
    ```js
    // courses
    [
        {
            _id: ObjectId('66cfe115ab74488678228fb5'),
            name: 'Software Engineering',
            students: [
                ObjectId('66b2feb5f5e99a509c228fb6'),
                ObjectId('66b31747f5e99a509c228fb7')
            ]
        },
        {
            _id: ObjectId('66b2fbfcf5e99a509c228fb5'),
            name: 'Artificial Intelligence'
        }   
    ]
    ```
    ```js
    // students
    [
        {
            _id: ObjectId('66b2feb5f5e99a509c228fb6'),
            name: 'Quan',
            courses: [
                ObjectId('66cfe115ab74488678228fb5'),
                ObjectId('66b2fbfcf5e99a509c228fb5')
            ]
        }, 
        {
            _id: ObjectId('66b31747f5e99a509c228fb7'),
            name: 'Bi',
            courses: [
                ObjectId('66cfe115ab74488678228fb5')
            ]
        }
    ]
    ```

### Hợp nhất các quan hệ tham chiếu (Merging Reference Relations)
- **Left Outer Join**
    + `$lookup` Thực hiện **Left Outer Join** vào một collection khác trong cùng cơ sở dữ liệu để lọc các document từ collection joined để xử lý
    
    + `$lookup` thêm một trường là mảng mới vào mỗi document đầu vào. Mảng này chứa các document khớp từ collection joined 

    + Cú pháp thực hiện
        ```js
        {
            $lookup:
            {
                from: '<collection to join>',
                localField: '<field from the input documents>',
                foreignField: '<field from the documents of the from collection>',
                as: '<output array field>'
            }
        }
        ```
        - `from`: chỉ định collection trong cùng một cơ sở dữ liệu để thực hiện liên kết

        - `localField`: chỉ định trường từ các document đầu vào. `$lookup` thực hiện so khớp `localField` với `foreignField` từ document trong from collection. Nếu document đầu vào không chứa `localField`, thì `$lookup` sẽ xem trường đó có giá trị `null` cho mục đích so khớp

        - `foreignField`: chỉ định field từ các document trong from collection. `$lookup` thực hiện so khớp `foreignField` với `localField` của document đầu vào. Nếu một document trong from collection không chứa foreignField, thì `$lookup` xem trường đó có giá trị là `null` cho mục đích so khớp

        - `as`: chỉ định tên của trường mảng mới để thêm vào document đầu vào. Trường mảng mới chứa các document khớp từ from collection. Nếu tên được chỉ định đã tồn tại trong document đầu vào, trường hiện tại sẽ bị **ghi đè**

        ```js
        db.products.aggregate({
            $lookup: {
                from: 'brands',
                localField: 'brand',
                foreignField: '_id',
                as: 'brandRefer'
            }
        })
        ```
        ```js
        // products data output
        [
            {
                _id_: ObjectId('66dc2337c6bc1310cec73bfa'),
                name: 'Type C Cable',
                brand: ObjectId('66dc1690c6bc1310cec73bf9'),        // localField
                price: 125500,
                brandRefer: [
                    {
                        // data from in brands collection
                        _id: ObjectId('66dc1690c6bc1310cec73bf9'),  // foreignField
                        name: 'Hoco Technology',
                        industry: 'Technology',
                        founded: '2024',
                        headquarters: {
                            city: 'Tokyo',
                            country: 'Japan'
                        },
                        website: 'www.hoco.com',
                        products: [
                            'Charging Cable',
                            'Wireless Charger',
                            'Headphones'
                        ]
                    }
                ]
            }
        ]
        ```

    + Hoạt động của `$lookup` tương tự với câu lệnh SQL như sau
        ```SQL
        SELECT *, (
            SELECT ARRAY(*)
            FROM Collection_to_join
            WHERE ForeignField = Collection_input.localField
        ) AS Output_array_field
        FROM Collection_input;
        ```

## 🔷 Tương tác với cơ sở dữ liệu

### Truy vấn dữ liệu

- **db.collection.find(query, projection, options)** Trả về con trỏ đến các document khớp với tiêu chí query. Mặc dù khi sử dụng find sẽ trả về document hoặc mảng các document nhưng thực tế thì phương thức này đang trả về con trỏ đến các document. Mặc định của MongoDB, **find()** không cung cấp tất cả các document, nó chỉ cung cấp 20 document đầu tiên. Tuy nhiên, có thể sử dụng phương thức **ToArray()** hoặc **forEach()** để có thể truy cập tất cả document

    ```js
    // Return product documents with price = 100000
    db.products.find({
        price: 100000 
    }) 
    ```

    + Truy cập document bằng phương thức **next()**
        - Trả về document tiếp theo trong con trỏ

            ```js
            const products = db.products.find()

            while(products.hasNext()) {
                printjson(products.next())
            }
            ```

    + Truy cập document bằng phương thức **forEach()**
        - Cho phép lại lại con trỏ và truy cập vào từng document

            ```js
            db.products.find().forEach(element => {
                printjson(element.name) // show value of name key in document[]
            })
            ```

        - Phương thức **forEach()** thực sự sẽ chỉ tìm và nạp các document tiếp theo cho mỗi chu kì vòng lặp, do đó tất nhiên không sử dụng quá nhiều băng thông và không tải quá nhiều vào bộ nhớ

    + Một số phương thức cho phép sửa đổi hành vi của con trỏ
        - **sort(sort)** Chỉ định thứ tự mà truy vấn trả về các document khớp. Tham số của method chứa cặp giá trị **field** và **value** với **value** chỉ gồm 2 giá trị **-1 (ASC)** và **1 (DESC)**

            ```js
            // Return product documents sorted in ASC order by name key
            db.products.find().sort({ name: 1})
            ```

        - **limit(number)**

            ```js
            // Return product documents with max length = 5
            db.products.find().limt(5)
            ```
        
        - **skip(number)**
        
            ```js
            // Return product documents skip the first 5 documents
            db.products.find().skip(5) 
            ```

- **db.collection.findOne(query, projection, options)** Trả về một document duy nhất khớp với tiêu chí query được chỉ định trên collection hoặc view. Nếu có nhiều document thoả mãn điều kiện, phương thức này chỉ trả về document đầu tiên theo thứ tự tự nhiên của các document lưu trữ trong bộ nhớ.

    ```js
    db.products.findOne({ name: 'Keyboard' })   // return document first in memory with name: Keyboard
    ```

- **Projection** Trong quá trình truy vấn dữ liệu với phương thức **find()** hoặc **findOne()**, mặc định sẽ truy vấn tất cả các field trong document. Để giới hạn số lượng các field mà MongoDB gửi tới ứng dụng truy vấn, có thể chỉ rõ những field cần thiết để cho phép trả về. Quá trình này gọi là **Projection**

    ```js
    // Return product documents with field _id amd name 
    db.products.find({}, {name: 1})

    // Return product documents without field name    
    db.products.find({}, {name: 0})

    // Return account documents with _id and country field of address embedded document 
    db.accounts.find({}, {
        'address.country': 1
    })
    ```

    + **Projection với mảng bẳng toán tử `$`**: Toán tử vị trí `$` giới hạn nội dung của một mảng để trả về phần tử đầu tiên khớp với điều kiện truy vấn. 
     
        ```js 
        // Return brand documents with _id and branchs[] field with branchs[0] data
        // and branchs[0].city = 'DN'
        db.brands.find({
            'branchs.city': {$in: ['DN']}
        }, {
            'branchs.$': 1
        })
        ```

        ```js
        {
            "_id": ObjectId('66dc1690c6bc1310cec73bf9'),
            branchs: [
                city: 'DN',
                detail: 'Hoa Minh'
            ]
        }
        ```
        + Tuy nhiên, khi không được truyền điều kiện truy vấn thì khi câu lệnh được thực thi, MongoDB sẽ xảy ra lỗi

        ```js
        db.brands.find({}, {
            'branchs.$': 1
        })
        ```
        ```
        MongoServerError[Location51246]: 
        Executor error during find command :: caused by :: positional operator '.$' couldn't find a matching element in the array
        ```

    + **Projection với mảng bằng toán tử `$slice`**: Chỉ định số lượng phần tử sẽ trả về của trường mảng trong kết quả truy vấn
        
        ```js
        {arrayField: {$slice: '<number>'}}        
        ```

        - `number` chỉ định số lượng phần tử trả về của trường mảng, với `number` là số dương thì trả về `number` phần tử đầu tiên, với `number` là số âm trả về `number` phần tử cuối cùng và với `number` lớn hơn phần tử của mảng thì trả về tất cả phần tử của mảng

        ```js
        {arrayField: {$slice: ['number to skip', 'number to return']}}
        ```

        - `number to skip` chỉ định số lượng phần tử bỏ qua từ đầu mảng, nếu giá trị `number to skip` lớn hơn kích thước của mảng thì truy vấn sẽ trả về một mảng rỗng. Nếu là một giá trị âm sẽ bỏ qua `number to skip` phần tử lùi lại từ cuối mảng. Nếu giá trị tuyệt đố số âm của `number to skip` lớn hơn kích thước mảng, thì vị trí bắt đầu là vị trí đầu tiên của mảng

        - `number to return` chỉ định số lượng phần tử để trả về các phần tử tiếp theo (`number to return` phải là một số lớn hơn 0)

### Thêm mới dữ liệu

- **db.collection.insertOne()** Chèn một document duy nhất vào collection. Với mỗi document được thêm mới, MongoDB sẽ tự động thêm trường **_id** với giá trị là duy nhất trong database.
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

    + Với **insertOne()** khi truyền một mảng document, mongoDB sẽ thêm mới một document với data là mảng các document truyền vào
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

- **db.collection.insertMany()** Chèn một hoặc nhiều document vào collection. Theo mặc định, document được chèn theo thứ tự được cung cấp. Tuy nhiên, document có thể được **mongod** sắp xếp lại để tăng hiệu suất. Chính vì vậy, các ứng dụng không nên phụ thuộc vào thứ tự chèn nếu sử dụng **insertMany()**
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

    + **Thêm mới có thứ tự** Khi thực hiện **insertMany()** với option là **ordered: true**, nếu việc chèn không thành công, server sẽ không tiếp tục chèn bản ghi, ngược lại, với **ordered: false**, nếu việc chèn không thành công, server vẫn sẽ tiếp tục chèn bản ghi tiếp theo

    + Với **insertMany()**, số lượng thao tác trong mỗi nhóm không được vượt quá giá trị **maxWriteBatchSize**(mặc định là 100,000). Giới hạn này ngăn ngừa các vấn đề với thông báo lỗi quá khổ. Nếu một nhóm vượt quá giới hạn này, trình điều khiển client sẽ chia thành các nhóm nhỏ hơn hoặc bằng giá trị giới hạn. Ví dụ với maxWriteBatchSize là 100,000, nếu queue bao gồm 180,000 operations, trình điều khiển sẽ tạo ra 2 nhóm bao gồm 100,000 operations và 80,000 operations

### Cập nhật dữ liệu

- **db.collection.updateOne(filter, update, options)** Cập nhật một document duy nhất trong collection. Nếu nhiều document trong DB thoả mãn điều kiện filter thì MongoDB chỉ cập nhật document đầu tiên thoả mãn điêu kiện

    ```js
    db.products.updateOne({
        price: {$gte: 5000}
    }, {
        $set: { discout: true }
    })
    ```

- **db.collection.updateMany(filter, update, options)** Cập nhật tất cả document phù hợp với filter được chỉ định

    ```js
    db.products.updateMany({
        price: {$gte: 5000}
    }, {
        $set: { discout: true }
    })
    ```

- Sự khác nhau giữa **replaceOne()** và **updateOne()**: **db.collection.replaceOne(filter, update, options)** được sử dụng để thay thế một document duy nhất trong collection thoả mãn filter. Điều này có nghĩa là document hiện tại sẽ bị xoá và được thay thế bằng một document mới. Tuy nhiên, với **updateOne()**, document sẽ không được thay thế hoàn toàn mà thay vào đó, chỉ các trường được chỉ định sẽ được cập nhật

### Xoá dữ liệu

- **db.collection.deleteOne(filter, options)** Xoá một document duy nhất trong collection. Nếu nhiều document trong DB thoả mãn điều kiện filter thì MongoDB chỉ xoá document đầu tiên thoả mãn điêu kiện 

    ```js
    // Delete product document with name is Type C Cable
    db.products.deleteOne({ name: 'Type C Cable' })
    ```

- **db.collection.deleteMany(filter, options)** Xoá tất cả document phù hợp với filter được chỉ định

    ```js
    // Delete all product documents with price >= 1,200,000
    db.products.deleteMany({price: {$gte: 1200000}})
    ```

### Toàn vẹn dữ liệu (Atomicity)
- **Tính nguyên tử (Atomicity) - tính toàn vẹn dữ liệu** trong MongoDB đảm bảo rằng các hoạt động CRUD trên document là thành công toàn bộ hoặc thất bại toàn bộ. Nghĩa là, nếu chỉ với một field của document xảy ra lỗi trong quá trình truy vấn dữ liệu thì toàn bộ field của document đó cũng sẽ rollback

- Atomicity ở cấp độ mỗi document, nghĩa là document có cấp cao nhất vì vậy nó bao gồm tất cả field trong document kể cả các Embedded Document, các mảng, ... 

- Khi một thao tác thực hiện thêm mới hoặc sửa đổi nhiều document (insertMany, updateMany) thì việc đó với mỗi document là Atomicity nhưng toàn bộ thao tác không phải Atomacity
    ```js
    db.insertMany([
        {
            // document insert success
            name: 'Xinmmeng X98 Keyboard',
            price: 1050000
        }, 
        {
            // document insert fail with price field error
            name: 'Hoco H35 Air',
            price: 'aaaaa'          
        },
        {
            // document insert success
            name: 'NB F80 Arm',
            price: 355000
        }
    ], {
        // insert without order
        ordered: false
    })
    ```

## 🔷 Một số toán tử cơ bản

### Toán tử truy vấn và tham chiếu

- **Toán tử so sánh (Comparison Operator)**

    ```js
    {field: {$operator : value}}

    // Example
    db.products.find({price: {$gte: 24000}})
    ```

    + `$eq` - `$ne` So sánh bằng và không bằng
    + `$gt` - `$gte` So sánh lớn hơn và lớn hơn bằng
    + `$lt` - `$le` So sánh nhỏ hơn và nhỏ hơn bằng

- **Toán tử Logic (Logical Operator)**

    ```js
    {$operator: [expression1, expression2, ...]}

    // Example
    // Return product documents with price <= 12000 or price >= 360000
    db.products.find({
        $or: [
            {price: {$le: 12000}},
            {price: {$gte: 360000}}
        ]
    })
    ```

    + `$and` Nối mệnh đề truy vấn bằng logic **AND**, trả về document khớp với các mệnh đề
    + `$or` Nối các mệnh đề truy vấn bằng logic **OR**, trả về document khớp ít nhất một trong các mệnh đề
    + `$nor` Nối các mẹnh đề truy vấn bằng logic **NOR**, trả về document không khớp với các mệnh đề truy vấn
    + `$not` Đảo ngược logic của biểu thức truy vấn và trả về document không khớp với biểu thức truy vấn, cú pháp thực hiện như sau

        ```js
        {field: {$not: {expression}}}

        // Example
        // Return product documents with price not >= 30000 (price < 30000)
        db.products.find({
            price: {$not: {$gte: 30000}}
        })
        ```

- **Toán tử phần tử (Element Operator)**
    + `$exists` Trả về những document chứa hoặc không chứa field được chỉ định

        ```js
        // Return product documents with brand field exist
        db.products.find({
            brand: {$exists: true}
        })
        ```

    + `$type` Trả về document nếu field có type được chỉ định

        ```js
        // Return product documents with price data type is double
        db.products.find({
            price: {$type: 'double'}
        })
        ```

- **Toán tử đánh giá (Evaluation Operator)**
    + `$regex` Trả về document có giá trị khớp với biểu thức chính quy (regex) được chỉ định

        ```js
        // Return product documents with name contain 'cable' case-insentive
        db.products.find({
            name: {$regex: /cable/i}
        })
        ```

- **Toán tử truy vấn mảng (Array Query Operator)**
    + `$size` Trả về document nếu field mảng có kích thước được chỉ định

        ```js
        // Return brand documents with branchs[] size = 3
        db.brands.find({
            branchs: {$size: 3}
        })
        ```

    + `$all` Trả về document chứa tất cả phần tử được chỉ định trong truy vấn

        ```js
        // Return brand documents with branchs[] 
        // Contain city is 'DN' and 'HN' 
        db.brands.find({
            'branchs.city': {$all: ['DN', 'HN']}
        })
        ```

    + `$elemMatch` Trả về các document có chứa trường mảng với ít nhất một phần tử khớp với tất cả các tiêu chí truy vấn đã chỉ định

        ```js
        // Return brand documents with branchs[] element 
        // Contain city is 'DN' or 'HN' and detail field exist
        db.brands.find({
            branchs: {$elemMatch: {
                city: {$in: ['DN', 'HN']},
                detail: {$exists: true}
            }}
        })
        ```

    + `$in` - `$nin` Tồn tại và không tồn tại các giá trị trong mảng chỉ định

        ```js
        {field: {$operator : [value1, value2...]}}

        // Example
        // Return brand documents with branchs[] 
        // Contain city is 'DN' or 'HN'
        db.brands.find({
            'branchs.city': {$in: ['DN', 'HN']}
        })
        ```

### Toán tử cập nhật

- **Toán tử cập nhật trường**

    + `$inc` Tăng hoặc giảm giá trị của trường theo giá trị (có thể âm hoặc dương) đã chỉ định

        ```js
        // Update X98 Keyboard product with price increased by 12,000
        db.products.updateOne({
            name: 'X98 Keyboard'
        }, {
            $inc: {price: 12000}
        })
        ```

    + `$min` - `$max` Chỉ cập nhật trường nếu giá trị nhỏ hơn / lớn hơn giá trị trường hiện tại. Giá trị cập nhật chính là giá trị toán tử chỉ định

        ```js
        // Update X98 Keyboard product with max price 1,060,000
        // If price is less than max value
        db.products.updateOne({
            name: 'X98 Keyboard'
        }, {
            $max: {price: 1060000}
        })
        ```
    + `$mul` Nhân giá trị của trường theo giá trị đã chỉ định

        ```js
        // Update X98 Keyboard product with price increased by 20%
        db.products.updateOne({
            name: 'X98 Keyboard'
        }, {
            $mul: {price: 1.2}
        })
        ```

    + `$unset` Xoá trường được chỉ định
        
        ```js
        // Update X98 Keyboard product with brand field deleted
        db.products.updateOne({
            name: 'X98 Keyboard'
        }, {
            $unset: {brand: '<anything>'}
        })
        ```

    + `$rename` Cập nhật tên trường được chỉ định

        ```js
        // Update X98 Keyboard product with reduce field rename to discount field
        db.products.updateOne({
            name: 'X98 Keyboard'
        }, {
            $rename: {reduce: 'discount'}
        })
        ```
- **Toán tử cập nhật mảng**
    + `$push` Thêm mới một phần tử vào phần tử cuối của trường mảng. 
        
        ```js
        // Update brand document with exist branchs[] element have city is HCM
        // Set the first elememt matching with founding is 2024
        db.brands.updateOne({
            'branchs.city': 'HCM'
        }, {
            $set: {'branchs.$.founding': 2024}
        })
        ```

        Ngoài ra, toán tử `$push` có hỗ trợ thêm các modifier operator để thay đổi hành vi thực hiện bao gồm
        - `$each` Thêm nhiều giá trị vào trường mảng
        - `$slice` Giới hạn số lượng phần tử mảng
        - `$sort` Sắp xếp các phần tử của mảng
        - `$position` Chỉ định vị trí trong mảng để chèn các phần tử mới

    + `$pull` Xoá khỏi mảng hiện có tất cả các trường hợp của một giá trị hoặc các giá trị khớp với điều kiện đã chỉ định

    + `$addToSet` thêm một giá trị chưa tồn tại vào trường mảng. Nếu giá trị đó đã tồn tại, toán tử này sẽ không được thực thi. Vì vậy, với các giá trị được thêm mới thông qua `$addToSet` là giá trị độc nhất trong mảng. Ngoài ra, có thể sử dụng toán tử `$each` để thêm mới nhiều phần tử vào trường mảng

## 🔷 Làm việc với Indexes

### Tổng quan về Indexes

- **Indexes** là cấu trúc dữ liệu đặc biệt lưu trữ một phần nhỏ dữ liệu của collection theo dạng dễ duyệt hơn. MongoDB Indexes sử dụng cấu trúc dữ liệu **B-Tree**

- **Indexes** lưu trữ giá trị của một trường hoặc một tập hợp các trường cụ thể, được sắp xếp theo giá trị của trường. Việc sắp xếp này hỗ trợ cho các phép so khớp bằng nhau và các hoạt động truy vấn dựa trên phạm vi

- **Indexes** hỗ trợ hiệu quả các truy vấn trong MongoDB. Nếu không có Indexes, MongoDB phải quét mọi document trong collection để trả về kết quả truy vấn. Nếu có Indexes phù hợp, MongoDB sử dụng Indexes để giới hạn số document nó phải quét. Ngoài ra, Indexes cũng đảm bảo tính nhất quán dữ liệu và tránh dữ liệu trùng lắp với `unique` option

- Indexes cũng có một số hạn chế, mặc dù nó giúp cải thiện hiệu suất truy vấn, tuy nhiên chỉ đúng với tỷ lệ `phần tử truy vấn / tập dữ liệu truy vấn` <= 20%. Ngoài ra Indexes làm giảm hiệu suất đối với các hoạt động đọc - ghi. Đối với các collection có tỷ lệ ghi - đọc cao, các Indexes gây tốn kém vì mỗi lần chèn cũng phải cập nhất bất kì Indexes nào

### Config Indexes

- **Default Indexes** Trong MongoDB, trường `_id` đã được khởi tạo Indexs sẵn. Vì vậy khi thực hiện truy vấn dữ liệu với điều kiện sử dụng là `_id` thì tốc độ truy vấn thường rất nhanh 

- Để có thể khởi tạo Indexes trên collection, sử dụng phương thức **db.collection.createIndex()**
    
    ```js
    // Create price index of product collection with ASC order 
    db.products.createIndex({ price: 1 })   // Create index name is price_1
    ```

- Để huỷ Indexes trên collection, sử dụng phương thức **db.collection.dropIndex()**

    ```js
        // Drop price index of product collection with object
        db.products.dropIndex({ price: 1 })

        // Drop price index of product collection with name
        db.products.dropIndex('price_1')
    ```

### Time-To-Live (TTL) Index

- **Time-To-Live Index** là single-field index đặc biệt mà MongoDB có thể sử dụng để tự động xoá document khỏi collection sau một khoảng thời gian nhất định hoặc tại một thời điểm cụ thể. **TTL Index** phù hợp cho một số loại thông tin như thông tin nhật kí, thông tin log, thông tin session của trang web, ...

    ```js
    // Create createtAt TTL index 
    db.sessions.createIndex({ createdAt: 1}, {
        expireAfterSeconds: 10
    })
    ```

- **Hết hạn dữ liệu** **TTL Index** sẽ hết hạn tài liệu sau khi số giây được chỉ định trôi qua kể từ giá trị trường được lập index. Ngưỡng hết hạn là giá trị trường được lập chỉ mục cộng với số giây được chỉ định

- Một số lưu ý khi sử dụng **TTL Index**:
    + Sau khi tạo chỉ mục **TTL Index** có thể có rất nhiều document đủ điều kiện để xoá cùng lúc. Khối lượng công việc này có thể gây sự cố về hiệu suất trên server
    
    + Trường chỉ định để tạo Index phải có kiểu dữ liệu là Date hoặc mảng chứa giá trị kiểu Date. Nếu trường chỉ định có kiểu dữ liệu khác với Date, thì TTL Index sẽ không hoạt động

    + Nếu giá trị `expireAfterSeconds` của collection thấp hơn giá trị `expireAfterSeconds` của TTL Index thì collection sẽ thực hiện xoá các document trước, do đó TTL không có tác dụng

### Multikey Indexes

- **Multikey Indexes (Compound Multikey Indexes)** thu thập và sắp xếp dữ liệu từ các giá trị của mảng, nó giúp cải thiện hiệu suất cho các truy vấn trên các trường mảng. MongoDB có thể tạo các index trên các mảng chứa giá trị nguyên thuỷ và embedded document

    ```js
    // brand document
    {
        _id: ObjectId('66e7aef1f80f4efb68d07e76'),
        name: 'Hoco',
        branchs: [
            {
                city: 'HN',
                detail: '16 Dong Da',
                year: 2021
            },
            {
                city: 'DN',
                detail: 'Hoa Minh',
                year: 2024
            },
            {
                city: 'HCM',
                detail: 'Quan 7',
                year: 2021
            }
        ],
        products: ['Changer', 'Cable', 'Hub']
    }
    ```

    ```js
    db.brands.createIndex({ products: 1 })        // products_1 is multikey index
    db.brands.createIndex({ 'branchs.city': 1 })  // branchs.city_1 is multikey index
    ```

    - Đối với Multikey Indexes, mỗi document chỉ được lập index có thể có nhiều nhất một trường có giá trị là một mảng

        ```js
        db.brands.createIndex({ products: 1, 'branchs.city': 1 })

        // Error
        // MongoServerError[CannotIndexParallelArrays]: 
        // Collection shop.brands :: caused by :: cannot index parallel arrays [branchs] [products]
        ```

### Text Indexes

- **Text indexes** hỗ trợ truy vấn tìm kiếm văn bản trên trên các trường chứa nội dung chuỗi. **Text Indexes** cải thiện hiệu suất khi tìm kiếm các từ hoặc cụm từ cụ thể trong nội dung chuỗi. Mỗi collection chỉ có thể có một text index, nhưng index đó có thể bao gồm nhiều trường

    ```js
    // Create text index with name and type field
    db.products.createIndex({
        name: 'text', type: 'text'
    })
    ```

- **Text indexes** hỗ trợ các hoạt động truy vấn với `$text` và **Text indexes** cũng là điều kiện tiên quyết để có thể sử dụng được `$text`

    ```js
    // Return product document with name or type contain logitech or mouse
    db.products.find({
        $text: {$search: 'logitech mouse'}
    })

    // Search with phrase logitech mouse
    db.products.find({
        $text: {$search: '"logitech mouse"'}
    })

    // Search with logitech and without mouse
    db.products.find({
        $text: {$search: '"logitech -mouse"'}
    })
    ```

## 🔷 Làm việc với một số dữ liệu đặc biệt

### Tài liệu nhúng (Embedded Document)

- **Embedded Document** là document được lồng trong một document khác và được lưu trữ như một field của document đó

    ```js
    {
        _id: ObjectId('66b31747f5e99a509c228fb7'),
        name: 'LG MP400-B',
        price: 2390000,
        technical: { 
            screen_size: 24,
            resolution: 'FHD 1080p', 
            aspect_ratio: '16:9' 
        }
    }
    ```

- Những ưu điểm khi sử dụng **Embedded Document**:
    + **Nhất quán dữ liệu** Tất cả dữ liệu liên quan đều nằm trong một document nên việc cập nhật docmument đảm bảo tính nhất quán dữ liệu
    + **Hiệu suất truy vấn** Việc truy vấn tất cả dữ liệu liên quan trong một truy vấn duy nhất nhanh hơn và hiệu quả hơn vì nó tránh được nhu cầu sử dụng nhiều truy vấn và 
    + **Vị trí lưu trữ** Việc lưu trữ các dữ liệu liên quan với nhau có thể cải thiện hiệu suất, đặc biệt là khi dữ liệu thường được truy cập cùng nhau

- Tuy nhiên, **Embedded Document** cũng tồn tại một số nhược điểm như sau:
    + **Kích thước document** MongoDB có giới hạn kích thước document là 16MB. Việc nhúng quá nhiều document có thể dẫn đến quá tải giới hạn này
    + **Sự trùng lặp** Dữ liệu Embedded document trên nhiều document có thể giống nhau dẫn đến tăng nhu cầu lưu trữ dữ liệu không cần thiết

        ```js
        // Both products are have the Hoco brand and contain information from this brand
        // => Duplicate data
        {
            _id: ObjectId('66b31747f5e99a509c228fb8'),
            name: 'HDMI Hoco Cabel',
            price: 75000,
            brand: {                                    
                name: 'Hoco Technology',
                industry: 'Technology',
                founded: '2024',
                headquarters: {
                    city: 'Tokyo',
                    country: 'Japan'
                },
                website: 'www.hoco.com',
                products: [
                    'Charging Cable',
                    'Wireless Charger',
                    'Headphones'
                ]
            }
        },
        {
            _id: ObjectId('66b31abff5e99a509c228fb9'),
            name: 'TypeC Hoco Cabel',
            price: 32000,
            brand: {
                name: 'Hoco Technology',
                industry: 'Technology',
                founded: '2024',
                headquarters: {
                    city: 'Tokyo',
                    country: 'Japan'
                },
                website: 'www.hoco.com',
                products: [
                    'Charging Cable',
                    'Wireless Charger',
                    'Headphones'
                ]
            }
        }
        ```
    
    + **Cập nhật phức tạp** Với những cấu trúc lòng nhau sâu, việc cập nhật có thể trở nên phức tạp và có thể yêu cầu thao tác rộng trên dữ liệu. Ngoài ra, nếu nhiều dữ liệu có chung thông tin tài liệu nhúng (như ví dụ ở trên) thì khi cập nhật, phải cập nhật tất cả dữ liệu có liên quan, điều này khó kiểm soát được tính thống nhất dữ liệu

- Các trường hợp có thể sử dụng **Embedded Document**:
    + Quan hệ **One - One**: Khi một document liên quan trực tiếp đến một document khác (ví dụ như hồ sơ người dùng và các thiết lập của người dùng đó với hệ thống)
    + Quan hệ **One-Many**: Trong trường hợp này **Embedded Document** cũng có thể được sử dụng nhưng với phía "Many" không quá lớn và thường xuyên được truy cập bằng document gốc

        ```js
        {
            name: 'Quan',
            address: {
                province: 'Quang Tri',
                country: 'Viet Nam'
            }
        }
        ```

### Dữ liệu không gian địa lý (Geospatial Data - Geospatial Document)

- **GeoJSON** là một định dạng dựa trên JSON được thiết kế để thể hiện các đối tượng địa lý với các thuộc tính phi không gian của chúng. Các toạ độ là một mảng trong đó phần tử đầu tiên là kinh độ và phần tử thứ hai là vĩ độ

- **GeoJSON** hỗ trợ các kiểu hình học bao gồm **Point** (địa chỉ và vị trí),  
**LineString** (đường phố, đường cao tốc và ranh giới), **Polygon** (quốc gia, vùng đất) và collection nhiều phần của các kiểu đó.

    ```js
    // Point GeoJSON
    {
        type: 'Feature',
        properties: {},
        geometry: {
            coordinates: [
                108.22690714836239,
                16.061204191628278
            ],
            type: 'Point'
        }
    }

    // LineString GeoJSON
    {
        type: 'Feature',
        properties: {},
        geometry: {
            coordinates: [
                [
                    108.22506156144277,
                    16.061162214166274
                ],
                [
                    108.22637203736156,
                    16.061193697264017
                ]
            ],
            type: 'LineString'
        }
    }

    // Polygon GeoJSON
    {
        type: 'Feature',
        properties: {},
        geometry: {
            coordinates: [
                [
                    [
                        // Start point
                        108.22508340270889,
                        16.06218016512605
                    ],
                    [
                        108.22512708523942,
                        16.061372101388613
                    ],
                    [
                        108.22654676748556,
                        16.06181286383412
                    ],
                    [
                        108.22594613268814,
                        16.06276784578317
                    ],
                    [
                        // End point = start point
                        108.22508340270889,
                        16.06218016512605
                    ]
                ]
            ],
            type: 'Polygon'
        }
    }
    ```

* **Geo Queries**

    - Thêm mới địa điểm vào trong DB

        ```js
        db.travels.insertOne({
            name: 'Dragon Bridge',
            location: {
                // Required ------------------- //
                coordinates: [
                    108.22690714836239,
                    16.061204191628278
                ],
                type: 'LineString'
                // ---------------------------- //
            }
        })
        ```

    - Khởi tạo **Geospatial Indexes**

        ```js
        // Create Geospatial Indexes with location field
        db.travels.createIndex({location: '2dsphere'})
        ```

    - Theo dõi khoảng cách giữa các địa điểm thông qua toán tử `$near`. Toán tử `$near` chỉ định một điểm mà truy vấn không gian địa lý trả về các document từ gần nhất đến xa nhất với điểm chỉ định đó. Để có thể sử dụng toán tử `$near` cần phải tạo Geospatial Indexes 

        ```js
        // Return travel documents with location close to the specified point
        // And max distance is 100m and min distance is 10m
        db.travels.find({
            location: { $near: {
                $geometry: {
                    coordinates: [
                        108.2231048261848,
                        16.06015109621802
                    ],
                    type: 'Point'
                },
                $maxDistance: 450,
                $minDistance: 10
            }}
        })
        ```

    - Tìm kiếm địa điểm bên trong khu vục nhất định thông qua toán tử `$geoWithin`. Toán tử `$geoWithin` chọn các document có dữ liệu không gian địa lý tồn tại hoàn toàn trong một hình dạng được chỉ định

        ```js
        // Return travel documents with location in specified area
        db.travels.find({
            location: { $geoWithin: {
                $geometry: {
                    coordinates: [[
                        [
                            108.22515312551542,
                            16.061925392767847
                        ],
                        [
                            108.22471114746241,
                            16.059082991445223
                        ],
                        [
                            108.22940287555207,
                            16.05958939251417
                        ],
                        [
                            108.22862094345913,
                            16.062872850511795
                        ],
                        [
                            108.22515312551542,
                            16.061925392767847
                        ]
                    ]],
                    type: 'Polygon'
                }
            }}
        })
        ```

    - Tìm kiếm khu vực cụ thể mà vị trí chỉ định nằm bên trong thông qua toán tử `$geoIntersects`. Toán tử `$geoIntersects` chọn các document có dữ liệu không gian địa lý giao nhau với một đối tượng GeoJSON được chỉ định, có thể hiểu là nơi giao nhau của dữ liệu và đối tượng được chỉ định không trống

        ```js
        // Return travel documemts with location contain specified point
        db.travels.find({
            location: { $geoIntersects: {
                    $geometry: {
                        coordinates: [
                            108.2231048261848,
                            16.06015109621802
                        ],
                        type: 'Point'
                    }
                }
            }
        })
        ```

## 🔷 Aggregation Framework

### Tổng quan Aggregation Framework

- **Aggregation Framework** là truy vấn nâng cao của MongoDB, cho phép thực hiện tính toán, xử lý và kết hợp từ nhiều document để truy vấn thông tin cần thiết

- **Aggregation Pipeline** bao gồm một hoặc nhiều giải đoạn xử lý dữ liệu:
    + Mỗi giai đoạn thực hiện một thao tác trên các document đầu vào
    + Các document được xuất ra từ một giai đoạn sẽ được chuyển đến giai đoạn tiếp theo
    + Một đường **Aggregation Pipeline** có thể trả về kết quả cho các nhóm document. Chẳng hạn như trả về giá trị tổng, trung bình, tối đa hoặc tối thiểu



## 🔷 Tip

- **Thêm mới hoặc cập nhật chỉ với một lệnh duy nhất**
    
    Trong một số quy trình nhất định, việc thực hiện cập nhật hoặc thêm mới tuỳ thuộc vào dữ liệu có tồn tài trong DB hay không. Trong những trường hợp, để hợp lý hoá logic trên có một tuỳ chọn **upsert**. Tuỳ chọn này có sẵn trong các phương pháp **updateOne**, **updateMany**, **replaceOne**

    ```js
    // Update Sonic G941 Headphones product if DB exist
    // Else insert Sonic G941 Headphones product
    // With name Sonic G941 Headphones, type Over-ear, price 675,000
    db.products.updateOne({
        name: 'Sonic G941 Headphones'
    }, {
        $set: {type: 'Over-ear'},
        $max: {price: 675000}
    }, {
        upsert: true    // default upsert: false
    })
    ```  
