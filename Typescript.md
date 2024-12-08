# **Typescript**

## 🔷 MỤC LỤC

- **[Tổng quan Typescript](#-tổng-quan-typescript)**

## 🔷 Tổng quan Typescript

### Typescript

- **Typescript** là một ngôn ngữ lập trình kiểu tĩnh, là siêu tập hợp cú pháp nghiêm ngặt của **Javascript**. Ngôn ngữ này được phát triển và duy trì bởi Microsoft. **Typescript** được tạo ra để giải quyết những thách thức trong việc xây dựng các ứng dụng Javascript quy mô lớn và thêm các **class**, **interface** và các tính năng khác vào ngôn ngữ

- Một số ưu điểm nổi bật của **Typescript**
    + **Error Detection** Typescript xác định lỗi tại thời điểm biên dịch. Trong khi đó. Javascript phát hiện lỗi tại thời điểm chạy
    + **Kiểu dữ liệu tĩnh** Cung cấp các lợi ích của các tuỳ chọn kiểu dữ liệu tĩnh, cho phép thêm kiểu vào biến, hàm, thuộc tính, ...
    + **Cấu trúc code** Tổ chức và cấu trúc code một cách hiệu quả
    + **Hỗ trợ Namespace** Giới thiệu về các khái niệm Namespace bằng các xác định các Module

- Bên cạnh đó, **Typescript** vẫn còn tồn tại một số nhược điểm như sau
    + **Thời gian biên dịch** Việc biên dịch Typescript mất nhiều thời gian hơn so với việc biên dịch Javascript bởi vì cần có thêm bước biên dịch để chuyển đổi Typescript sang Javascript để trình duyệt thực thi
    + **Tích hợp và cấu hình bổ sung** Để sử dụng Typescript cần phải cấu hình trình biên dịch và có thể tích hợp các công cụ đóng gói và xây dựng khác như Webpack, Rollup, hoăc Parcel. Điều này có thể tăng thêm độ phức tạp cho quá trình thiết lập dự án
    + **Một số lỗi ngầm khi biên dịch qua Javascript** Việc biên dịch từ Typescript sang Javascript đôi khi có thể che giấu các lỗi hoặc hành vi không mong muốn, đặc biệt là nếu tính nghiêm ngặt của kiểm tra kiểu dữ liệu không được cấu hình đúng cách

- Cấu hình **Typescript**
    + Cài đặt  **Typescript**
    
        ```sh
        npm install -g typescript
        ```
    
    + Biên dịch file **Typescript**

        ```sh
        tsc index.ts
        ```

## 🔷 Các kiểu dữ liệu cơ bản trong Typescript

### Static Types (kiểu dữ liệu tĩnh)

- **Static Types** là kiểu dữ liệu của biến được biết tại thời điểm biên dịch thay vì tại thời điểm chạy. Một khi biến được khai báo là có kiểu nhất định, nó không được gán lại thành một kiểu khác sau đó. Điều này có thể ngăn ngừa nhiều lỗi phổ biến có thể xảy ra trong ngôn ngữ với Dynamic Types (kiểu dữ liệu động) đó là kiểu của một biến có thể thay đổi trong quá trình thực thi chương trình

- Có 3 kiểu **dữ liệu nguyên thuỷ** trong TS đó là:
    + **number** Bao gồm tất cả các số, không có sự phân biệt giữa số nguyên và số thực
    
    + **string** Bao gồm tất cả các giá trị văn bản

    + **boolean** Chỉ có duy nhất 2 giá trị `true` và `false`, không có giá trị `truthy` hoặc `falsy`

- Khai báo kiểu dữ liệu

    ```ts
        // Init [age] with data type [number]
        const age: number = 21
    ```

- Ngoài ra, trong JS, cách cơ bản để nhóm và truyền dữ liệu là thông qua các đối tượng. Trong TS, chúng ta biểu diễn chúng thông qua **Object Types**

    ```ts
        // Init [persion] with key [name] and [age]
        const persion: {
            name: string,
            age: number
        } = {
            name: 'QuanTT',
            age: 18
        }

        // Init [persion] with key [name] and [age = 20]
        const persion: {
            name: string,
            age: 20
        } = {
            name: 'QuanTT',
            age: 18 // Type '18' is not assignable to type '20'.ts(2322)
        }
    ```

- Một số lợi ích của việc sử dụng **Static Types** như sau
    + **Phát hiện lỗi** Một trong những lợi ích chính của **Static Types** là phát hiện lỗi sớm. Trình biên dịch Typescript kiểm tra các kiểu và cung cấp phản hồi ngay lập tức về các kiểu không khớp hoặc các lỗi liên quan đến kiểu khác

    + **Khả năng đọc code** Bằng các khai báo rõ ràng các kiểu dữ liệu, code trở nên dễ đọc hơn. Điều này giúp những người bảo trì code trong tương lai có thể nhanh chống hiểu được các cấu trúc dữ liệu và kiểu dữ liệu dự kiến sử dụng

    + **Chú thích** Thay vì dựa vào các chú thích để truyền đạt kiểu dữ liệu mong đợi của một biến hoặc kiểu dữ trả về của một hàm, các chú thích kiểu dữ liệu trong code đã cung cấp thông tin này

## 🔷 Generic type

## 🔷 Interface, Class
