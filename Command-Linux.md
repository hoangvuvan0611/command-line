"# command-line" 
#Câu lệnh trong ubuntu Linux
## User
    •	Nhóm lệnh thực thi:
        o	sudo adduser (tennguoidung) : Thêm mới người dùng
        o	sudo usermod -aG sudo (tennguoidung) : Thêm mới người dùng vào nhóm sudo
        o	sudo useradd -m -s /bin/bash (username) : Tạo tài khoản không cần thông tin bổ sung
            	- m : Tạo thư mục home
            	- s : Chỉ định shell (mặc định là /bin/bash)
    o	sudo deluser (username) : xóa tài khoản
    o	sudo deluser --remove-home (username) : xóa tài khoản và thư mục home
    o	sudo usermod -l new_username old_username : đổi tên tài khoản
    	sudo usermod -d /home/new_username -m new_username : đổi cả thư mục home
    o	sudo usermod -s /bin/zsh (username) : Thay đổi shell đăng nhập
    o	Mở/Khóa tài khoản: 
    	sudo usermod -L (username) : Khóa tài khoản
    	sudo usermod -U (username) : Mở khóa tài khoản
    o	Thay đổi mật khẩu:
    	Passwd
    	sudo passwd username : thay đổi mật khẩu cho người khác
    o	Quản lý nhóm: 
    	sudo groupadd groupname: Tạo mới nhóm
    	sudo groupdel groupname : Xóa nhóm
    	sudo usermod -aG groupname username : Thêm người vào nhóm
    	groups username : Xem người dùng thuộc nhóm nào
    •	Nhóm lệnh tra cứu:
    o	awk -F: '$3 >= 1000 {print $1}' /etc/passwd : Danh sách người dùng thực không bao gồm hệ thống 
    o	cat /etc/passwd : Liệt kê danh sách người dùng
    o	su – (tennguoidung): Kiểm tra đăng nhập bằng tài khoản mới
    o	id (username) : xem quyền của user
    o	ls -l /path/to/file_or_directory : xem quyền truy cập tập tin 
    o	groups (username) : Xem thông tin về nhóm
    o	getent group sudo : kiểm tra quyền sudo
    o	who : kiểm tra người dùng hiện tại đang đăng nhập
    o	w : Hiển thị phiên đăng nhập đang hoạt động
    o	last : Lịch sử đăng nhập
    •	Cấu hình:
    o	Giới hạn thời gian đăng nhập: /etc/security/time.conf
    o	Hạn chế tài nguyên người dùng: /etc/security/limits.conf
    o	sudo chown username:groupname /path/to/directory : đổi chủ sỡ hữu đăng nhập
    o	sudo usermod -g $(id -g olduser) -G $(id -G olduser | tr ' ' ',') newuser : sao chép quyền của người khác
    o	sudo grep 'COMMAND=' /var/log/auth.log : Kiểm tra ai đang chạy lệnh sudo
## Nginx
    •	Sử dụng systemctl:
        o	sudo systemctl restart nginx : Khởi động lại 
        o	sudo systemctl status nginx : kiểm tra trạng thái
    Firewall (Cấu hình tường lửa – UFW)
        •	sudo apt install ufw: Cài đặt UFW
        •	sudo ufw allow OpenSSH: 3 câu lệnh chỉ cho phép các kết nối cần thiết
        •	sudo ufw enable
        •	sudo ufw status

## Cài đặt SSH (cấu hình SSH để an toàn hơn)
    •	sudo nano /etc/ssh/sshd_config : Mở cấy hình SSH cấu hình những thuộc tính sau 
        o	PermitRootLogin no : Chỉ cho phép đăng nhập bằng tài khoản không phải root
        o	PasswordAuthentication no : Cấm đăng nhập bằng mật khẩu nếu sử dụng (SSH Key)
        o	Port 2200 : Thay đổi cổng mặc định nếu cần
    •	sudo systemctl restart sshd : Lưu và khởi động lại SSH
    •	Tạo SSH Key trên máy cục bộ
        o	ssh-keygen
        o	ssh-copy-id -i ~/.ssh/id_rsa.pub tennguoidung@ip_server
    •	Tạo ssh-Key thủ công
        o	Sau khi dùng lệnh ssh-keygen
        o	Trên win:
            	cat ~/.ssh/id_rsa.pub : mở file chứa public key 
            	ssh username@your-server-ip : đăng nhập vào server
            	Tạo thư mục .ssh nếu chưa có
    •	mkdir -p ~/.ssh
    •	chmod 700 ~/.ssh
        	echo "your-public-key-content" >> ~/.ssh/authorized_keys : Thêm public key vào file authorized_keys
        	chmod 600 ~/.ssh/authorized_keys : đặt quyền cho authorized_keys

## Cài đặt Fail2Ban (Giúp bảo vệ server khỏi tấn công brute-force)
    •	sudo apt install fail2ban : Cài đặt
    •	Tùy chỉnh cấu hình: tạo file cấu hình tùy chỉnh
        o	sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
        o	sudo nano /etc/fail2ban/jail.local
    •	sudo systemctl enable --now fail2ban : Khởi động lại dịch vụ

## Vô hiệu hóa các dịch vụ không cần thiết
    •	sudo systemctl list-units --type=service : Kiểm tra các dịch vụ đang chạy
    •	Tắt các dịch vụ không sử dụng: 
        o	sudo systemctl disable ten_dich_vu
        o	sudo systemctl stop ten_dich_vu
    Bật cập nhật tự động: 
        •	sudo apt install unattended-upgrades
        •	sudo dpkg-reconfigure --priority=low unattended-upgrades

## Cài đặt phần mềm bảo mật bổ sung:
    •	sudo apt install clamav: ClamAV quest virut
    •	Kiểm tra rootkits: 
        o	sudo apt install rkhunter
        o	sudo rkhunter –checkall

## Theo dõi nhật ký hệ thống: 
    •	 sudo journalctl -xe : sử dụng journalctl để theo dõi nhật ký

## Kiểm tra trạng thái bảo mật: (sử dụng lynis)
    •	sudo apt install lynis : cài đặt
    •	sudo lynis audit system : chạy kiểm tra

## Backup dữ liệu định kỳ:
    •	Sử dụng rsync hoặc cron để tự động sao lưu



