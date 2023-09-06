# **Angular**

## 🔹 Lý thuyết
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

