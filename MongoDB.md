# **MongoDB**

## 🔷 Mục lục
- **[Tổng quan MongoDB](#-tổng-quan-mongodb)**
- **[Tương tác với cơ sở dữ liệu](#-tương-tác-với-cơ-sở-dữ-liệu)**
- **[Lược đồ (Schemas)](#-lược-đồ-schemas)**
- **[Quan hệ (Relations)](#-quan-hệ-relations)**
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

## 🔷 Tương tác với cơ sở dữ liệu

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

- **Projection** Trong quá trình truy vấn dữ liệu với phương thức **find()**, mặc định sẽ truy vấn tất cả các field trong document. Để giới hạn số lượng các field mà MongoDB gửi tới ứng dụng truy vấn, có thể chỉ rõ những field cần thiết để cho phép trả về. Quá trình này gọi là **Projection**
    ```js
    db.products.find({}, {name: 1})     // return document with field name and _id
    db.products.find({}, {name: 0})     // return document without field name and _id
    ```
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
        // both products are under the Hoco brand and contain information from this brand.
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
            name: 'Bi'
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

    + Hoạt động của `$lookup` tương tự với câu lệnh SQL như sau
        ```SQL
        SELECT *, (
            SELECT ARRAY(*)
            FROM Collection_to_join
            WHERE ForeignField = Collection_input.localField
        ) AS Output_array_field
        FROM Collection_input;
        ```
        
## 🔷 Tip