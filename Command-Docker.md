"# Command-Docker"


Lợi ích:
- Có thể xem file Markdown trực tiếp trên GitHub, Visual Studio Code, hoặc bất kỳ trình xem Markdown nào.
- Dễ dàng cập nhật và chỉnh sửa.

---

## **2. Lưu trong file Excel hoặc Google Sheets**
Tạo một bảng để tổ chức các câu lệnh Docker, chia cột thành các phần như sau:

| **Nhóm**          | **Câu lệnh**                 | **Mô tả**                                          |
|--------------------|------------------------------|--------------------------------------------------|
| Thông tin hệ thống | `docker info`               | Hiển thị thông tin Docker                        |
| Quản lý container  | `docker ps`                 | Liệt kê các container đang chạy                  |
| Quản lý container  | `docker run -d nginx`       | Chạy container Nginx trong chế độ nền            |
| Quản lý image      | `docker images`             | Liệt kê các image có trên hệ thống               |
| Quản lý image      | `docker pull <image-name>`  | Tải image từ Docker Hub                          |

# Các cờ quan trọng 
-d : chạy lệnh ở chế độ nền
-i : Nó giữ STDIN mở ngay cả khi không được gắn vào
-e : thiết lập các biến môi trường

```plaintext
# Thông tin hệ thống
docker --version
docker info

# Quản lý container
docker ps
docker ps -a
docker run -d -p 8080:80 nginx
docker stop <container-id>
docker rm <container-id>


# Quản lý image
docker images
docker pull <image-name>
docker rmi <image-id> : Xóa image

# Docker Commands Cheat Sheet

## 1. Thông tin hệ thống
- `docker --version`: Kiểm tra phiên bản Docker.
- `docker info`: Hiển thị thông tin tổng quan.

## 2. Quản lý Container
### Chạy container
- docker run -d -p 8080:80 nginx
    + Trong đó: 80 là cổng chạy trong container (server port trong file yaml)
    + Cổng 8080: sẽ là cổng được dùng ở host 

- docker run -dp 8081:8080 --name spring-container -v "$(pwd):/app" vuvanhoang/spring-docker:v1.0.0 
    + Khi docker đang run mà có thay đổi thì sẽ tự update vào docker

### Tạo task cho image
- Docker tag (name-image):latest (name-image):newTag

### Push to Docker Hub
- docker push vuvanhoang/vnua-test-app:tagname

# Lưu ý khi build docker local
- Khi sử dụng database thì không thể sử dụng path localhost do localhost khi build trên docker thì nó sẽ không trỏ đến host của máy tính mà nó trỏ đến container của docker, vì vậy cần sửa cấu hình của db về host docker
vd: spring.datasource.url=jdbc:postgresql://host.docker.internal:5432/your_database
