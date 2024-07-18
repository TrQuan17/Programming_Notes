# **Docker**

## 🔷 Tổng quan Docker

### Docker
- **Docker** là nền tảng cho phép dựng, kiểm thử và triển khai ứng dụng một cách nhanh chóng
- Docker đóng gói phần mềm vào các đơn vị tiêu chuẩn hoá được gọi là container có mọi thứ mà phần mềm cần chạy, trong đó có thư viện, công cụ hệ thống, code và thời gian chạy
- Bằng cách sử dụng Docker, có thể nhanh chóng triển khai và thay đổi quy mô ứng dụng vào bất kì môi trường nào và biết chắc rằng code sẽ chạy được

### Container
- **Container** là các môi trường hoàn toàn cách ly. Trong chúng có thể chứa các quy trình hoặc service riêng, các netword, các mounts. Các container giống như các máy ảo ngoại trừ chúng đểu được chia sẻ cùng một nhân hệ điều hành
- Ưu điểm của Container:
    + **Linh hoạt**: Quản lý, cấp phát và chia sẻ tài nguyên hiệu quả hơn. Tài nguyên được chia sẻ linh hoặc giữa các container, không bị giới hạn tài nguyên **cứng** như Virtual Machine (VM)
    + **Tiết kiệm tài nguyên hệ thống** vì không phải lãng phí tài nguyên (CPU, RAM, Storage) cho Hypervisor và hệ điều hành như khi dùng VM
    +  **Hiệu năng**: Hoạt động nhanh và mượt mà hơn vì chạy trực tiếp trên cùng một nhân hệt điều hành. Không phải thông qua Hypervisor và hệ điều hành khách như hình thức ảo hoá phần cứng

- Nhược điểm của Container:
    +  **Kém ổn định**: Hiệu năng hoạt động của Container không ổn định nếu không quản lý hợp lý. Vì tài nguyên hệ thống được chia sẻ giữa các Container, không được phân chia **cứng** như trên VM. Nếu một container chiếm dụng quá nhiều tài nguyên sẽ ảnh hưởng đến các container khác trong cùng hệ thống
    +  **Hạn chế lựa chọn**: Không thể tạo ra container VM sử dụng hệ điều hành khác với hệ điều hành Host
