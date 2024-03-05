# **HTML - HyperText Markup Language**

## 🔷 Lý thuyết cơ sở

### HTML & HTML DOM

- **HTML**: là một ngôn ngữ đánh dấu được thiết kế để tạo nên các trang wev trên Word Wide Web. Được hỗ trợ bởi các công nghệ như CSS và các ngôn ngữ kịch bản như JavaScripts. HTML được sử dụng để tạo và cấu trúc các thành phần trên trang web và ứng dụng và đây không phải là ngôn ngữ lập trình

- **DOM** (Document Object Model – Mô hình Các Đối tượng Tài liệu): là một chuẩn được định nghĩa bởi W3C (Tổ Chức Web Toàn Cầu – World Wide Web Consortium). DOM được dùng để truy xuất và thao tác trên các tài liệu có cấu trúc dạng HTML hay XML bằng các ngôn ngữ lập trình thông dụng như Javascript, PHP…

- **HTML DOM**: là một tiêu chuẩn cho phép bạn thực hiện những công việc thao tác với bất kì một trang web: get, change, add, hoặc delete các thành phần của HTML.

- HTML DOM là một chuẩn mô hình object và programming interface cho HTML. Nó định nghĩa:
    - HTML elements như là objects
    - Properties của tất cả HTML elements
    - Methods để truy cập đến tất cả HTML elements
    - Events cho tất cả HTML elements

- Có 3 thành phần cơ bản bao gồm Element, Atrribute, Text

## 🔷 Truy vấn Element

- Một số hàm truy vấn cơ bản
    ``` HTML
    <div class="wrapper">
        <h1 id="title"> Title </h1>
        <a href="www.google.com"> Google </a>
        <form id="firstForm"> </form>
        <div class="content"> </div>
        <p class="content"> </p>
    </div>    
    ```

    ```JS
    document.getElementById('title') // h1#title
    document.getElementsByClassName('wrapper') // [div.wrapper]
    document.getElementsByTagName('h1') // [h1]
    document.querySelector('.wrapper #title') // h1#title
    document.querySelectorAll('.content') // [div.content, p.content]
    docment.forms['firstForm'] // [form#firstForm]
    docment.forms[0] // [form#firstForm]
    docment.forms.firstForm // [form#firstForm]
    ```   
- **innerText và textContent**
    + **innerText**: Lấy nội dung văn bản trong thẻ đó ( Những nội dung mà mình có thể nhìn thấy ), thuộc tính chỉ tồn tại trên ElementNode
    + **textContent**: Lấy tất cả TextNode trong thẻ đó ( Khoảng trắng, xuống dòng, code trong thẻ script, style cũng được xem như là một TextNode ), thuộc tính tồn tại ở cả TextNode và ElementNode

- **innerHTML và outerHTML**

    ``` HTML
    <div class='box'></div>
    ```

    ``` JS
    const boxDiv = document.querySelector('.box')
    console.log(boxDiv.innnerHTML) // ''
    console.log(boxDiv.outerHTML) // '<div class='box'></div>'

    boxDiv.innnerHTML = '<span>Hello</span>'
    // <div class='box'>
    //    <span> Hello </span>
    // </div>

    boxDiv.outerHTML = '<span>Hello</span>' // <span> Hello </span>
    ```

    + **innerHTML**: Đối với get, lấy tất cả nội dung HTML chứa bên trong tag, với set thì nó sẽ ghi đè nội dung HTML bên trong tag
    + **outerHTML**: Đối với get, Lấy tất cả nội dung HTML chứa bên trong tag và chính nó, với set thì nó sẽ ghi đè tất cả nội dung HTML bên trong cũng như chính nó

## 🔷Tip
- Attribute 'contenteditable': một số ElementNode có thể chỉnh sửa như thẻ input cũng như có thể thực hiện các thao tác định dạng chữ như Bôi đậm (Ctrl + B), In nghiệm (Ctrl + I), Gạch chân (Ctrl + U), ...