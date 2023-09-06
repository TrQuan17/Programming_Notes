# **Javascript**

## 🔹 Lý thuyết
### Kiểu dữ liệu và khai báo biến
- **const**: không thể thay đổi giá trị nguyên thuỷ, tuy nhiên có thể thay đổi thuộc tính của đối tượng const cũng như các thao tác như thêm, xoá, thay đổi phần tử với mảng const
    ``` JS
    const num = 12
    num = 16 // TypeError: Assignment to constant variable

    const info = {
        language: 'Javascript',
        plaform: 'NodeJS'
    }
    info.language = 'Python'

    info = {} // TypeError: Assignment to constant variable

    const arr = [1, 2, 3, 4]
    arr.push(5)
    arr.pop()

    arr = [7, 8, 9] // TypeError: Assignment to constant variable
    ```
### Hoisting
- Được hiểu là khai báo biến và hàm được xử lý trước khi được thực thi 
    ``` JS
    console.log(hello) // undefined
    var hello = 'hello'

    helloFunc() // hello
    function helloFunc() {
        console.log('hello')
    }
    ```
- Khai báo hàm được đưa lên trên để thực thi tuy nhiên biển thức hàm thì không
    ``` JS
    helloFunc() // TypeError: helloFunc is not a function
    var helloFunc = () => {
        console.log('hello')
    }

    ```
## 🔹 Bất đồng bộ
### Callback
- Là hàm được sử dụng như một tham số của hàm khác
- Được sử dụng như gọi API, kết nối cơ sở dữ liệu, xử lý file, xử lý sự kiện, ...

### Callback hell
###
## 🔹 Tip
- Chuyển đổi nhanh giữa string sang number và ngược 
lại: 
    ``` JS
    const str = '12'
    console.log(typeof +str) // number

    const num = 12 + ''
    console.log(typeof num) // string
    ```