# **Angular**

## 🔹 Tổng quan Angular

### Angular

- **Angular**: là một platform và là một framework để xây dựng các ứng dụng single-page client sử dụng HTML và Typescript. Angular được viết bằng Typescript, nó được triển khai các chức năng cốt lỗi và tùy chọn dưới dạng một tập hợp các thư viện Typescript được import vào ứng dụng

- Kiến trúc của ứng dụng Angular dựa trên các khái niệm cơ bản nhất định. Các khối xây dựng cơ bản của Angular framework là Angular Components

- **Angular CLI**: là một công cụ command line để khởi tạo, phát triển và duy trì các ứng dụng Angular trực tiếp từ shell lệnh

### Một số câu lệnh cài đặt môi trường cơ bản
- Cài đặt công cụ Angular CLI
    ```
    npm install -g @angular/cli
    ```

- Khởi tạo và build Angular project
    ```
    ng new angular-project
    ng serve --port 4000
    ```

## 🔹 Component

### Khái niệm
- **Component** là các khổi xây dựng chính cho ứng dụng Angular. Mỗi component bao gồm:
    + HTML Template kiểm soát những gì được hiển thị vào DOM
    + TypeScript class để xác định hành vi như xử lý dữ liệu đầu vào của client và lấy dữ liệu từ server
    + CSS Selector xác định cách component được sử dụng trong HTML
    + Ngoài ra, còn có CSS Styles áp dụng cho template

- Khởi tạo một component:
    ```
    // full command
    ng generate component <component_name>
    ng generate component <folder/component_name>

    // short command
    ng g c <component_name>
    ```

- Trong file component.ts, component sẽ được khai báo như sau
    ```TS
    @Component({
        selector: 'app-component-name',                 // CSS Selector
        templateUrl: './component-name.component.html', // HTML Template
        styleUrls : ['./component-name.component.scss'] // CSS Styles []
    })

    // TypeScripts class
    export class ComponentNameComponent {
        // code
    }
    ``` 

### Vòng đời của Component (Component Lifecycle)
- **Component Lifecycle** là chuỗi các bước diễn ra giữa quá trình khởi tạo và hủy component. Mỗi bước đại diện cho mỗi phần khác nhau của quy trình Angular để kết xuất các component và kiểm tra chúng để cập nhật theo thời gian

- Thứ tự diễn ra trong Component Lifecycle như sau:
    ```TS
    export class ComponentNameComponent {
        // Contructor
        ComponentNameComponent() {}

        ngOnChanges() {}

        ngOnInit() {}

        ngDoCheck() {}
        
        ngOnDestroy() {}
    
    } 
    ```

    + **ngOnInit** chạy sau khi Angular đã khởi tạo tất cả các đầu vào của component với các giá trị ban đầu của chúng. **ngOnInit** chạy đúng một lần.

    + **ngOnChanges** chạy sau khi bất kì đầu vào component nào thay đổi. Trong quá trình khởi tạo, **ngOnChanges** lần chạy đầu tiên trước **ngOnInit**

    + **ngOnDestroy** chạy một lần ngay trước khi một component bị hủy bỏ. Angular hủy một component khi nó không còn hiển thị trên trang nữa.

    + **ngDoCheck** chạy trước mỗi lần Angular kiểm tra template của component để tìm kiếm sự thay đổi. **ngDoCheck** lần chạy đầu tiên sau **ngDoInit**
    
## 🔹 Pipe

## 🔹 Một số lỗi thường gặp và cách khắc phục

### Không thể sử dụng command 'ng'
- Thông báo lỗi
    ``` 
    ng : File C:....Roaming\npm\ng.ps1 cannot be loaded because running scripts is disabled on this system.
    ```
- Xử lý
    ```
    set-ExecutionPolicy RemoteSigned -Scope CurrentUser
    Get-ExecutionPolicy
    Get-ExecutionPolicy -list
    ```
- Link chi tiết     
https://www.c-sharpcorner.com/article/how-to-fix-ps1-can-not-be-loaded-because-running-scripts-is-disabled-on-this-sys/

