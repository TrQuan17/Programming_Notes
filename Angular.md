# **Angular**

## 🔹 Tổng quan Angular

- **Angular**: là một platform và là một framework để xây dựng các ứng dụng single-page client sử dụng HTML và Typescript. Angular được viết bằng Typescript, nó được triển khai các chức năng cốt lỗi và tùy chọn dưới dạng một tập hợp các thư viện Typescript được import vào ứng dụng

- Kiến trúc của ứng dụng Angular dựa trên các khái niệm cơ bản nhất định. Các khối xây dựng cơ bản của Angular framework là Angular Components

## 🔹 Angular CLI

### Khái niệm
- **Angular CLI**: là một công cụ command line để khởi tạo, phát triển và duy trì các ứng dụng Angular trực tiếp từ shell lệnh

### Một số câu lệnh cơ bản
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
- **Component**: là một khối code trong 

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

