"#Postgresql ubuntu command-line" 
## Lệnh


- psql: đăng nhập vào Postgresql

- \q : Thoát khỏi postgres

### Tạo người dùng và cơ sở dữ liệu
- CREATE USER (yourusername) WITH PASSWORD 'yourpassword'; : Tạo người dùng mới
- CREATE DATABASE (yourdbname);
- GRANT ALL PRIVILEGES ON DATABASE yourdbname TO yourusername; : Cấp quyền cho người dùng đói với cơ sở dữ liệu
- DROP USER username; : Xóa người dùng


### Cấu hình kết nối từ xa: Mặc định Postgresql chỉ cho phép kết nối từ localhost, nếu cho truy cập từ máy khác cần sửa cấu hình
- sudo nano /etc/postgresql/15/main/postgresql.conf : Mở kết nối từ xa
- listen_addresses = '*' : tìm dòng này và thay đổi thành như vậy

### Xem cấu hình 
- /etc/postgresql/14/main/postgresql.conf

### xem tất cả các cấu hình hiện tại 
- SHOW ALL;
- SHOW max_connections:
- Các cấu hình liên quan đến kết nối: 
    SHOW listen_addresses;
    SHOW port;
    SHOW ssl;

#### Cấu hình liên quan đến hiệu suất và bộ nhớ
- SHOW shared_buffers;
- SHOW work_mem;
- SHOW maintenance_work_mem;
- SHOW effective_cache_size;

#### Cấu hình liên quan đến logging 
- SHOW log_destination;
- SHOW logging_collector;
- sSHOW log_statement;


## Lệnh liên quan đến database
- \l: xem danh sách các database
- \dt: xem thông tin trong bảng dữ liệu

- pg_dump your_database_name > backup_file.sql: backup
- psql your_database_name < backup_file.sql: restore
