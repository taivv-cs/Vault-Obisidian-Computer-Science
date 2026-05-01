# Đề bài

Đăng nhập trò chơi bằng `ssh`. Máy chủ cần kết nối là _bandit.labs.overthewire.org_ trên cổng 2220. Tên đăng nhập là **bandit0** và mật khẩu là **bandit0**. Sau khi đăng nhập thành công, đi đến [[Level 1]].

## Lệnh ssh

**SSH** hay còn gọi là giao thức ssh ..., có các option sau đây

## Hướng dẫn sử dụng

Số cổng `ssh` mặc định là 22, mỗi khi sử dụng `ssh user@IP` nó sẽ cố gắng kết nối vào cổng mặc định là 22, nhưng nếu máy chủ từ xa cung cấp cổng khác cho `ssh`. Ta truyền tham số cổng vào như sau

```bash
ssh -p port_number user@IP
```

## Lời giải

> ssh bandit0@bandit.labs.overthewire.org -p 2220

## Cấu hình 
	
```config
Host bandit
  Hostname bandit.labs.overthewire.org
  Port 2220
  User bandit0
  Compression yes
  AddressFamily inet
```