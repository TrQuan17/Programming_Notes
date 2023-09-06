# **HTML & CSS**
## 🔹 Lý thuyết
### HTML DOM
- DOM là tên gọi viết tắt của (Document Object      Model – tạm dịch Mô hình Các Đối tượng Tài liệu). Là một chuẩn được định nghĩa bởi W3C (Tổ Chức Web Toàn Cầu – World Wide Web Consortium). DOM được dùng để truy xuất và thao tác trên các tài liệu có cấu trúc dạng HTML hay XML bằng các ngôn ngữ lập trình thông dụng như Javascript, PHP…

- **HTML DOM** là một tiêu chuẩn cho phép bạn thực hiện những công việc thao tác với bất kì một trang web: get, change, add, or delete các thành phần của HTML.

* HTML DOM là một chuẩn mô hình object và programming interface cho HTML. Nó định nghĩa:
    - HTML elements như là objects
    - properties của tất cả HTML elements
    - methods để truy cập đến tất cả HTML elements
    - events cho tất cả HTML elements

- Có 3 thành phần cơ bản bao gồm Element, Atrribute, Text

## 🔹 Image 
### Fallback image
``` HTML
<img onerror='path image or function'>
```

``` CSS
div {
    background: url('path'), url('path image replace');
}
```
### Tối ưu performance image với srcset

* Theo kích thức image
``` HTML
<img
    srcset="
        elva-fairy-480w.jpg 480w,
        elva-fairy-800w.jpg 800w
        "
    sizes="
        (max-width: 600px) 480px,
        800px"
    src="elva-fairy-800w.jpg"
    alt="Elva dressed as a fairy" 
/>
```

* Theo DPR
``` HTML
<img
    srcset="
        elva-fairy-480w.jpg 1x,
        elva-fairy-800w.jpg 2x
        "
    src="elva-fairy-800w.jpg"
    alt="Elva dressed as a fairy" 
/>
```

* Theo bối cảnh nội dung image
``` HTML
<picture>
    <source media='(max-width: 575px)' srcset="small.jpg" type="image/svg+xml">
    <img src="large.jpg" class="img-fluid img-thumbnail" alt="...">
</picture>
```