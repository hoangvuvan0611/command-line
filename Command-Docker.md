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
```bash
docker run -d -p 8080:80 nginx