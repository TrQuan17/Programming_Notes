# **NodeJS**

## Khái niệm
* NodeJS là một nền tảng (Platform) phát triển độc lập được xây dựng ở trên JS Runtime của Chrome mà chúng ta có thể xây dựng được các ứng dụng mạng một cách nhanh chóng và dễ dàng mở rộng.

* Phần Core bên dưới của NodeJS được viết hầu hết bằng C++ nên cho tốc độ xử lý và hiệu năng khá cao.
NodeJS tạo ra được các ứng dụng có tốc độ xử lý nhanh, realtime thời gian thực.

* NodeJS áp dụng cho các sản phẩm có lượng truy cập lớn, cần mở rộng nhanh, cần đổi mới công nghệ, hoặc tạo ra các dự án Startup nhanh nhất có thể.

## REPL (Real - Eval - Print - Loop)
* Là một đặc tính của NodeJS cho phép lập trình viên viết code và chạy trực tiếp trên màn hình shell/console/terminal để debug, kiểm tra code mà không cần tạo ra bất cứ file hay folder nào.

* Khi gõ code JS lên màn hình shell, NodeJS sẽ thực hiện việc đọc thông tin (Read) và tự động lưu trữ trong bộ nhớ; tự động đánh giá cấu trúc dữ liệu và sự hợp lệ của các dòng lệnh (Eval); xử lý thực thi code sau đó in ra kết quả nếu có (Print) và hỗ trợ lặp lại các dòng lệnh trên để thực thi chương trình (Loop).

## Module
### Exports và export
* Module.exports (CommonJS Modules):
    ``` JS
    module.exports = { function, class }
    ...
    const fileImport = require('fileModuleExports.js')
    const function = fileImport.function()
    const class = fileImport.class
    ```
* Import / export (ES6 - ECMAScript 6 Module):
    ``` JS
    export const func = () => {
        ...
    }

    export default funcDefault = () => {
        ...
    }

    import funcDefault from 'fileModuleExports.js'
    import { func } from 'fileModuleExports.js'
    ```