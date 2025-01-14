# **Typescript**

## 🔷 MỤC LỤC

- **[Tổng quan Typescript](#-tổng-quan-typescript)**
- **[Cấu hình Typescript](#-cấu-hình-typescript)**
- **[Kiểu dữ liệu trong Typescript](#-kiểu-dữ-liệu-trong-typescript)**
- **[Classes & Interface](#-classes--interface)**
- **[Tip](#-tip)**

## 🔷 Tổng quan Typescript

### Typescript (TS)

- **Typescript** là một ngôn ngữ lập trình kiểu tĩnh, là siêu tập hợp cú pháp nghiêm ngặt của **Javascript (JS)**. Ngôn ngữ này được phát triển và duy trì bởi Microsoft. **Typescript** được tạo ra để giải quyết những thách thức trong việc xây dựng các ứng dụng JS quy mô lớn và thêm các **class**, **interface** và các tính năng khác vào ngôn ngữ

- Một số ưu điểm nổi bật của **Typescript**

    + **Kiểu dữ liệu** TS có chú thích kiểu dữ liệu tuỳ chọn trong khi JS là kiểu dữ liệu động. Với TS, có thể chỉ định kiểu dữ liệu của biến, tham số và giá trị trả về, có thể giúp phát hiện lỗi liên quan đế kiểu dữ liệu tại thời điểm biên dịch

    + **Cú pháp** TS mở rộng cú pháp JS với các tính năng như **Interface**, **Class** và **Namespaces**. Điều này cung cấp cấu trúc mạnh mẽ và có tổ chức hơn trong các dự án quy mô lớn

    + **Công cụ** TS hỗ trợ công cụ tốt hơn, chẳng hạn như tích hợp trình soạn thảo, kiểm tra kiểu dữ liệu và tái cấu trúc mã tốt hơn

    + **Khả năng tương thích** TS có thể biên dịch thành bất kì phiên bản nào của mã JS

- Bên cạnh đó, **Typescript** vẫn còn tồn tại một số nhược điểm như sau

    + **Thời gian biên dịch** Việc biên dịch TS mất nhiều thời gian hơn so với việc biên dịch JS bởi vì cần có thêm bước biên dịch để chuyển đổi TS sang JS để trình duyệt thực thi

    + **Tích hợp và cấu hình bổ sung** Để sử dụng TS cần phải cấu hình trình biên dịch và có thể tích hợp các công cụ đóng gói và xây dựng khác như Webpack, Rollup, hoăc Parcel. Điều này có thể tăng thêm độ phức tạp cho quá trình thiết lập dự án

    + **Một số lỗi ngầm khi biên dịch qua Javascript** Việc biên dịch từ TS sang JS đôi khi có thể che giấu các lỗi hoặc hành vi không mong muốn, đặc biệt là nếu tính nghiêm ngặt của kiểm tra kiểu dữ liệu không được cấu hình đúng cách

### Cài đặt Typescript

- Cài đặt **Typescript**

    ```ts
    npm install -g typescript       // init global package

    npm install --save typescript   // init project package
    ```

## 🔷 Cấu hình Typescript

### Công cụ tsc và tệp cấu hình tsconfig.json

- **tsc** là công cụ command line cho **Typescript Compiler**. Nó biên dịch mã TS thành mã JS, làm cho nó tương thích với trình duyệt hoặc bất kỳ môi trường chạy JS nào

    ```ts
    tsc             // compile all TS file config in tsconfig.json
    tsc index.ts    // compile index.ts
    ```

- **Typescript Compiler** chấp nhận một số tuỳ chọn dòng lệnh cho phép tuỳ chình quá trình biên dịch. Các option này có thể được chuyển đến trình biên dịch bằng cách sử dụng tiền tố `--`.

- Ví dụ như **Watch option** - Thực hiện biên dịch khi file có thay đổi. Tuỳ theo việc config trong file `tsconfig.json` mà có thể thực hiện cho một hoặc nhiều file  `.ts`

    ```ts
    // Compiler app.ts
    tsc app.ts --watch
    ```

- `tsconfig.json` là một tệp cấu hình trong TS chỉ định các tuỳ chọn biên dịch để thực hiện xây dựng dự án. Nó giúp Typescript Compiler hiểu cấu trúc dự án và cách biên dịch thành JS. Một số tuỳ chọn cơ bản bao gồm

    + `target` Phiên bản Javascript cần biên dịch `es5`, `es6`, ...
    + `module` Thiết lập hệ thống module sử dụng `node16`, `esnext`, ...
    + `strict` Bật/tắt kiểm tra nghiêm ngặt
    + `outDir` Thư mục để xuất ra các tập tin JS đã biên dịch
    + `rootDir` Chỉ định thư mục gốc của project
    + `include` Mảng các file hoặc thư mục để thực hiện biên dịch
    + `exclude` Mảng các file hoác thư mục để loại trừ khỏi quá trình biên dịch

    ```ts
    // Init tsconfig.json 
    tsc --init
    ```

    ```json5
    // tsconfig.json example
    {
        "compilerOptions": {
            "target": "es6",
            "module": "commonjs",
            "strict": true,
            "outDir": "./src/js/compiler",
            "rootDir": "/src/js"
        },
        "include": ["src"],
        "exclude": ["node_mudules", ".vscode"]    
    }
    ```

### Emit Option

- `sourceMap` Cho phép tạo tệp sourceMap. Các tệp này cho phép debug và các công cụ khác hiển thị mã nguồn TS gốc cùng với các tệp JS đã được biên dịch. Các tệp sourceMap được hiển thị dưới dạng `.js.map` hoặc `.jsx.map`. Các tệp `.js` sẽ chú thích trong mã nguồn để chỉ ra vị trí của tệp `sourceMap`, chẳng hạn:

    ```js
    // File name: app.ts
    const log = (mess: string) => { console.log(mess) }

    log('Hello world!')
    ```

    ```js
    // File name: app.js
    "use strict";
    const log = (mess) => { console.log(mess); };
    log('Hello world!');
    //# sourceMappingURL=app.js.map
    ```

    ```json5
    // File name: app.js.map
    {
        "version": 3,
        "file": "app.js",
        "sourceRoot": "",
        "sources": [
            "app.ts"
        ],
        "names": [],
        "mappings": ";AAAA,MAAM,GAAG,GAAG,CAAC,IAAY,EAAE,EAAE,GAAG,OAAO,CAAC,GAAG,CAAC,IAAI,CAAC,CAAA,CAAC,CAAC,CAAA;AAEnD,GAAG,CAAC,cAAc,CAAC,CAAA"
    }
    ```

### Type Check Option

- Trong một số trường hợp biến không được khai báo, TS sẽ đặt mặc định kiểu dữ liệu cho một biến là `any` khi không thể suy ra kiểu dữ liệu của biến đó. Điều này có thể dẫn đến một số lỗi bị bỏ sót. Với **noImplicitAny option** - Cho phép báo cáo lỗi cho các biểu thức và khai báo kiểu dữ liệu có ngụ ý là `any`

    ```js
    // config tsconfig.json
    {
        "compilerOptions": {
            "noImplicitAny": true
        }
    }
    ```

    ```ts
    // Error: Parameter 's' implicitly has an 'any' type.ts(7006)
    function fn(obj) {
        return obj
    }
    ```

## 🔷 Kiểu dữ liệu trong Typescript

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

- Một số lợi ích của việc sử dụng **Static Types** như sau:

    + **Phát hiện lỗi** Một trong những lợi ích chính của **Static Types** là phát hiện lỗi sớm. Trình biên dịch TS kiểm tra các kiểu và cung cấp phản hồi ngay lập tức về các  kiểu không khớp hoặc các lỗi liên quan đến kiểu khác

    + **Khả năng đọc code** Bằng các khai báo rõ ràng các kiểu dữ liệu, code trở nên dễ đọc hơn. Điều này giúp những người bảo trì code trong tương lai có thể nhanh chống hiểu được các cấu trúc dữ liệu và kiểu dữ liệu dự kiến sử dụng

    + **Chú thích** Thay vì dựa vào các chú thích để truyền đạt kiểu dữ liệu mong đợi của một biến hoặc kiểu dữ trả về của một hàm, các chú thích kiểu dữ liệu trong code đã cung cấp thông tin này

### Tuples

- **Tuples** là một kiểu dữ liệu trong **Typescript** được sử dụng để biểu diễn một mảng trong đó kiểu của một số phần tử cố định được khai báo từ ban đầu, nhưng không phải cho tất cả các phần tử. Nó cung cấp một cách để biểu diễn tập hợp các kiểu phần tử được sắp xếp cho các phần tử được sắp xếp cho các phần tử nhất định trong một mảng TS. **Tuples** luôn có một số phần tử cố định và mỗi phần tử trong số chúng có các kiểu được liên kết với chúng

    ```ts
    let point: [number, number] = [1, 2]

    const role: [string, number] = ['admin', 0]

    // Error
    // Type '[string, number, number]' is not assignable to type '[string, number]'.
    // Source has 3 element(s) but target allows only 2
    const role: [string, number] = ['admin', 0, 4]

    // Success
    // Link refer: https://stackoverflow.com/questions/64069552/typescript-array-push-method-cant-catch-a-tuple-type-of-the-array
    role.push(4)
    ```

### Enums

- **Enums** là tập hợp các **const** được đặt tên. Sử dụng **Enums** có thể giúp ghi lại ý định dễ dàng hơn hoặc tạo một tập hợp các trường hợp riêng biệt. TS cung cấp cả enums dạng **string** và dạng **number**

- Các loại **Enums** cơ bản:

    + **Number Enums** TS xác định giá trị số của một thành phần Enums dựa trên thứ tự của thành phần đó xuất hiện trong định nghĩa Enums

        ```ts
        enum MOVE {
            Up,     // default Up = 0
            Down,   // default Down = 1
            Left,   // default Left = 2
            Right   // default Right = 4
        }

        enum MOVE {
            Up = 1, // set Up = 1
            Down,   // default set Down = 2
            Left,   // default set Left = 3
            Right   // default set Right = 4
        }
        ```

    + **String Enums** Đối với mỗi element phải được khởi tạo hằng số là một chuỗi kí tự hoặc một string enums element khác

        ```ts
        enum ROLE {
            ADMIN       = 'admin',
            READ_ONLY   = 'read only',
            WRITE_READ  = 'write read'
        }

        // Error
        enum ROLE {
            ADMIN       = 'admin',
            READ_ONLY   = 'read only',
            WRITE_READ  // Error: Enum member must have initializer
        }
        ```

### Một số kiểu dữ liệu đặc biệt

- **Any Types** Là một kiểu dữ liệu đặc biệt của TS, **Any Types** có thể sử dụng bất cứ khi nào mà không muốn một giá trị cụ thể nào đó gây ra lỗi kiểu tra kiểu dữ liệu

- Khi một giá trị có kiểu là **any**, có thể truy cập bất kì thuộc tính vào của nó, có thể gọi nó như một hàm, gán cho nó một giá trị có kiểu dữ liệu bất kì hoặc một thứ gì đó khác miễn là hợp lệ về mặt cú pháp

    ```ts
    let obj: any = { x: 0}
    
    // No error
    obj.foo()
    obj()
    obj.bar = 100
    obj = 'Hello'
    ```

- **Union Types** Cho phép chỉ định nhiều loại có thể có cho một biến hoặc tham số. **Union Types** được viết dưới dạng danh sách các loại được phân tách bằng `|`

    ```js
    // variable
    const log: number | string = 'log'

    // arrow function
    const logData = (data: number | boolean | string): number | boolean | string => data
    ```

- **Literal Types** Chỉ định chính xác giá trị của biến hoặc tham số thay vì chỉ định kiểu dữ liệu. **Literal Types** có thể được sử dụng để thực thi rằng một giá trị phải thuộc một kiểu cụ thể và một giá trị cụ thể

    ```ts
    let season: 'spring' | 'summer' | 'autumn' | 'winter'

    // Error: Type '"season"' is not assignable to type '"spring" | "summer" | "autumn" | "winter"'
    season = 'season'
    ```

- **Custom Types (Type Aliases)** Cho phép đặt bí danh cho một kiểu dữ liệu

    ```ts
    // create account type
    type Account = {
        username: string,
        password: string,
        fullname: string,
        age: number
    }

    const acc: Account = {
        username: 'TrQuan17',
        password: '12345678',
        fullname: 'Quan',
        age: 24
    }
    ```

- **Unknown Types** là một kiểu dữ liệu tương tự **Any Types**. Bất kì thứ gì cũng có thể gán cho **Unknown Types** tuy nhiên nó không thể được gán cho bất kì thứ gì ngoài chính nó và **Any Types**. Không có thao tác nào được phép trên **Unknown Types** mà không được khẳng định hoặc thu hẹp thành một kiểu dữ liệu cụ thể

    ```ts
    let obj: unknown
    let variable: any
    let age: number

    // Success
    variable = obj

    // Error: Type 'unknown' is not assignable to type 'number'.ts(2322)
    age = obj
    ```

- **Never Types** là kiểu dữ liệu mà **Typescript** để biểu diễn trạng thái không nên tồn tại. **Never Types** có thể gán cho mọi kiểu, tuy nhiên, không có kiểu dữ dữ liệu nào có thể gán cho **Never Types** (trừ chính nó)

- **Never Types** thường được sử dụng cho `Switch clause` để thực hiện kiểm tra toàn diện (khi đã loại bỏ tất cả khả năng và không còn gì nữa)

- Ngoài ra, **Never Types** là kiểu trả về cho biểu thức hàm hoặc biểu thức hàm

    ```ts
    enum SEASON {
        SPRING,
        SUMMER,
        AUTUMN,
        WINTER
    }

    const getTemperature = (season: SEASON) => {
        switch(season) {
            case SEASON.SPRING:
                return 30
            case SEASON.SUMMER:
                return 36
            case SEASON.AUTUMN:
                return 25
            case SEASON.WINTER:
                return 15
            default:
                // Success
                const _exhaustiveCheck:never = season
                return _exhaustiveCheck
        }
    }

    // Error: Type '404' is not assignable to type 'never'.ts(2322)
    const _exhaustiveCheck:never = 404
    ```

## 🔷 Classes & Interface

### Classes

- **Classes** là bản thiết kế để tạo đối tượng, cung cấp cách để cấu trúc đối tượng và đóng gói dữ liệu và hành vi. Một **class** trong TS được định nghĩa bằng từ khoá `class`, theo sau là tên của **class**. Định nghĩa một **class** có thể bao gồm các **trường (properties hoặc attributes)**, **phương thức (functions)** và một **constructor**

    ```ts
    class Account {
        /* Attributes */
        public username?: string
        public password?: string
        public firstName?: string
        lastName?: string

        /* Constructor */
        constructor(
            username?: string,
            pass?: string,
            first?: string,
            last?: string
        ) {
            this.username = username
            this.password = pass
            this.firstName = first
            this.lastName = last
        }

        /* Methods */
        public showFullName(): string {
            return `${this.firstName} ${this.lastName}`
        }
    }

    const account = new Account('TrQuan17', '12345678', 'Quan', 'Tran')

    console.log(account.showFullName())
    ```

## 🔷 Tip

- **Rest Parameters**

    + Cho phép một hàm chấp nhận không hoặc nhiều đối số của kiểu được chỉ định

    + Trong TS các **Rest Parameters** tuân theo các quy tắc sau:

        - Một hàm chỉ có một **Rest Parameters**
        - **Rest Parameters** chỉ xuất hiện ở cuối danh sách tham số
        - Loại của **Rest Parameters** là mảng

    ```ts
    // Init sum function
    const sum = (...nums: number[]) => {
        return nums.reduce((sum, current) => sum + current)
    }

    // Limit params with tuple
    const sum = (...nums: [number, number, number]) => {
        return nums.reduce((sum, current) => sum + current)
    }
    ```
