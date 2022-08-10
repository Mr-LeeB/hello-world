# hello-world
my first repository
## **1.	Cài đặt container trên máy ảo linux.**
### **a.	Yêu cầu hệ điều hành.**
-	Để cài đặt Docker Engine, bạn cần phiên bản 64-bit của một trong các phiên bản Ubuntu sau:
    +	Ubuntu Jammy 22.04 (LTS) 
    +	Ubuntu Impish 21.10
    +	Ubuntu Focal 20.04 (LTS) 
    +	Ubuntu Bionic 18.04 (LTS)

### **b.	Gỡ cài đặt các phiên bản cũ.**
```
    $ sudo apt-get remove docker docker-engine docker.io containerd runc
```

### **c.	Thiết lập kho lưu trữ.**
-	Cập nhật apt chỉ mục gói và cài đặt các gói để cho phép apt sử dụng kho lưu trữ qua HTTPS:
```
$ sudo apt-get update
$ sudo apt-get install \ 
    ca-certificates \ 
    curl \ 
    gnupg \ 
    lsb-release
```
-	Thêm khóa GPG chính thức của Docker:
```go
$ sudo mkdir -p /etc/apt/keyrings 
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
-	Sử dụng lệnh sau để thiết lập kho lưu trữ:
```go
    echo \ 
    "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \ $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

### **d.	Cài đặt Docker Engine.**
-	Cập nhật aptchỉ mục gói và cài đặt phiên bản mới nhất của Docker Engine, containerd và Docker Compose hoặc chuyển sang bước tiếp theo để cài đặt một phiên bản cụ thể:
```go
    $ sudo apt-get update 
    $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin
```
-	_**Node:**_ Nhận lỗi GPG khi chạy apt-get update? Umask mặc định của bạn có thể không được đặt chính xác, khiến tệp khóa công khai cho repo không được phát hiện. Chạy lệnh sau và sau đó thử cập nhật lại repo của bạn
```
    $ sudo chmod a+r /etc/apt/keyrings/docker.gpg
```
-	Để cài đặt một phiên bản cụ thể của Docker Engine, hãy liệt kê các phiên bản có sẵn trong repo, sau đó chọn và cài đặt. Liệt kê các phiên bản có sẵn trong repo của bạn:
```
    $ apt-cache madison docker-ce
```
-	Ví dụ: cài đặt một phiên bản cụ thể bằng cách sử dụng chuỗi phiên bản từ cột thứ hai 5:20.10.16~3-0~ubuntu-jammy.
```go
    $ sudo apt-get install docker-ce=<VERSION_STRING> docker-ce-cli=<VERSION_STRING> containerd.io docker-compose-plugin
```
-	Xác minh rằng Docker Engine được cài đặt chính xác bằng cách chạy hello-world hình ảnh.
```
    $ sudo docker run hello-world
```
-	Nếu nó không hoạt động, có thể bạn chưa khởi động docker
( Usage: service docker {start|stop|restart|status} )
```
    $ sudo service docker start
```
