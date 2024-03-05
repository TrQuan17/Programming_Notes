# **NodeJS**

## 🔷Lý thuyết cơ sở

### NodeJS
- **NodeJS** là một nền tảng (Platform) phát triển độc lập được xây dựng ở trên JS Runtime của Chrome mà chúng ta có thể xây dựng được các ứng dụng mạng một cách nhanh chóng và dễ dàng mở rộng.
- Ứng dụng NodeJS chạy trong một quy trình duy nhất mà không tạo chuỗi mới cho mọi yêu cầu, nó cung cấp một tập hợp các nguyên hàm I/O bất đồng bộ trong thư viện tiêu chuẩn của nó để ngăn mã JavaScript chặn và nói chung, các thư viện trong Node.js được viết bằng cách sử dụng mô hình không chặn, khiến hành vi chặn trở thành ngoại lệ thay vì chuẩn mực.
- Phần Core bên dưới của NodeJS được viết hầu hết bằng C++ nên cho tốc độ xử lý và hiệu năng khá cao.
- NodeJS áp dụng cho các sản phẩm có lượng truy cập lớn, cần mở rộng nhanh, cần đổi mới công nghệ, có thể tạo ra được các ứng dụng có tốc độ xử lý nhanh, realtime thời gian thực..

### REPL (Real - Eval - Print - Loop)
- **REPL** là một đặc tính của NodeJS cho phép lập trình viên viết code  và chạy trực tiếp trên màn hình shell/console/terminal để debug, kiểm tra code mà không cần tạo ra bất cứ file hay folder nào.

- Khi gõ code JS lên màn hình shell, NodeJS sẽ thực hiện việc đọc thông tin (Read) và tự động lưu trữ trong bộ nhớ; tự động đánh giá cấu trúc dữ liệu và sự hợp lệ của các dòng lệnh (Eval); xử lý thực thi code sau đó in ra kết quả nếu có (Print) và hỗ trợ lặp lại các dòng lệnh trên để thực thi chương trình (Loop).

## 🔷CORS (Cross-Origin Resource Sharing)
- **CORS** là một cơ chế cho phép chia sẻ tài nguyên có nhiều nguồn gốc khác nhau. Định nghĩa của tương đồng là protocol, domain và port của liên kết truy cập là giống nhau

- Tiêu chuẩn CORS xác định cách trình duyệt và server giao tiếp khi truy cập tài nguyên miền chéo. Ý tưởng cơ bản là sử dụng tiêu đề HTTP để cho phép trình duyệt giao tiếp với server để xác định xem yêu cầu có thể thành công hay không

- Một số các cài đặt CORS sử dụng NodeJS
    + Set vào response header
        ```JS
        const app = express()

        app.use((req, res, next) => {
            res.header('Access-Control-Allow-Origin', '*')
            res.header('Access-Control-Allow-Methods', 'GET, POST, PUT, PATCH, DELETE')
            res.header('Access-Control-Allow-Headers', 'Origin, X-Requested-With, Content-Type, Accept, Authorization')

            next()
        })
        ```

    + Sử dụng thư viện cors của npm
        ```JS
        const cors = require('cors')
        const app = express()

        app.use(cors({
            origin: '*',
            methods: 'GET,HEAD,PUT,PATCH,POST,DELETE',
            preflightContinue: false,
            optionsSuccessStatus: 204,
            allowedHeaders: ['Content-Type', 'Authorization']
        }))
        ```

## 🔷REST API (REpresentational State Transfer)

### HATEOAS (Hypermedia As The Engine Of Application State)
- **HATEOAS** là một trong những chuẩn được khuyến nghị cho RESTful API. Thuật ngữ 'Hypermedia' có nghĩa là bất kỳ nội dung nào có chứa các liên kết (link) đến các media khác như image, movie và text.

- Kiểu kiến trúc này cho phép bạn sử dụng các liên kết hypermedia trong nội dung response để client có thể tự động điều hướng đến tài nguyên phù hợp bằng cách duyệt qua các liên kết hypermedia. Nó tương tự như một người dùng web điều hướng qua các trang web bằng cách nhấp vào các link thích hợp để chuyển đến nội dung mong muốn.

- HATEOAS mong muốn phía client không cần biết chút nào về cấu trúc phía server, client chỉ cần request đến một URL duy nhất, rồi từ đó mọi đường đi nước bước tiếp theo sẽ do chỉ dẫn của phía server trả về.

    ```JS
    HTTP/1.1 200 OK
    {
        "account": {
            "account_number": 12345,
            "balance": {
                "currency": "usd",
                "value": 100.00
            },
            "links": {
                "deposits": "/accounts/12345/deposits",
                "withdrawals": "/accounts/12345/withdrawals",
                "transfers": "/accounts/12345/transfers",
                "close-requests": "/accounts/12345/close-requests"
            }
        }
    }
    ```
## 🔷Authentication và Json Web Token (JWT)

- Một JWT gồm 3 phần cơ bản:
    + **Header**: chứa kiểu dữ liệu , và thuật toán sử dụng để mã hóa ra chuỗi JWT
    + **Payload**: chứa các thông tin mình muốn đặt trong chuỗi token như username, userId, …
    + **Verify signature**: được tạo ra bằng cách mã hóa phần header, payload kèm theo một chuỗi secret (khóa bí mật)

## 🔷Tip

### Một số thư viện cần thiết khi tạo dự án (dành cho dev)
- **dotenv**: cài đặt file môi trường (file .env)
    ```
    npm i dotenv
    ```     
    ```JS
    require('dotenv').config()
    const PORT = process.env.PORT
    ```
- **Nodemon**: tự động reload lại project khi code có sự thay đổi
    ```
    npm i nodemon
    ```
    ```JSONC
    // config package.json
    "scripts": {
        "start": "nodemon app.js"
    }
    ```

- **Helmet**: giúp bảo mật các ứng dụng Express bằng cách đặt tiêu đề phản hồi HTTP
    ```
    npm i helmet
    ```
    ```JS
    const helmet = require('helmet')
    app.use(helmet())
    ```

- **morgan**: HTTP request logger middleware dành cho NodeJS
    ```
    npm i morgan
    ```
    ```JS
    const morgan = require('morgan')
    app.use(morgan('common')) // tiny, dev, ...
    ```

### Config router tránh bị nhập sai đường dẫn
- `/ab?cd`: router có thể có chứa b hoặc không (router `/acd` và `/abcd` là giống nhau)
- `/ab+cd`: router có thể chứa nhiều chữ b (router `/abbbbcd` và `/abcd` là giống nhau)
- `/ab\*cd`: `/ab` + anything + `cd` (router `/abtrquancd` và `/abcd` là giống nhau)
- `/a/`: router sử dụng regex (router `/abc`, `/bca`, `trquan` là giống nhau)
