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

### Cơ chế Event-Loop
- Câu lệnh **Asynchronous** được đưa vào **call stack**
- **Call stack** nhận diện đưa qua **Web APIs**
- **Call stack** tiếp tục được nhận những câu lệnh khác
- **Asynchronous** xử lý xong đưa vào **callback queue**
- **Call stack** xử lý xong các câu lệnh **synchronized,** đưa hàm **callback** từ **callback queue** thực hiện

### Callback
- Là hàm được sử dụng như một tham số của hàm khác
- Được sử dụng như gọi API, kết nối cơ sở dữ liệu, xử lý file, xử lý sự kiện, ...

### Callback hell

## 🔹 Module

### Module Inport và Export
- Module.exports (CommonJS Modules)
    ``` JS
    // fileModuleExports.js
    module.exports = { function, class }
    
    // app.js
    const fileImport = require('fileModuleExports.js')
    const function = fileImport.function()
    const class = fileImport.class
    ```
    
- Import / export (ES6 - ECMAScript 6 Module)
    ``` JS
    // fileModuleExports.js
    export const func = ( /* variable */ ) => { /* code */ }

    // fileModuleExports.js
    export default funcDefault = ( /* variable */ ) => { /* code */ }

    // app.js
    import funcDefault from 'fileModuleExports.js'
    import { func } from 'fileModuleExports.js'
    ```

## 🔹 Tip
- Chuyển đổi nhanh giữa string sang number và ngược 
lại: 
    ``` JS
    const str = '12'
    console.log(typeof +str) // number

    const num = 12 + ''
    console.log(typeof num) // string
    ```