# Hướng dẫn chạy script cài đặt Apache Tomcat7

##1. Cài đặt Apache Tomcat7

###B1. Tải các gói, các script
Truy cập vào tài khoản root của máy chủ và tải các gói, script chuẩn bị cho quá trình cài đặt

```sh
apt-get update
apt-get install git -y
git clone https://github.com/minh7992/Tomcat7.git
cd Tomcat7
chmod +x *.sh
```

###B2. Tiến hành chạy script để cài đặt

`bash setup_Tomcat7.sh`

Sau khi thực hiện script trên, máy sẽ cài đặt JDK và Apache Tomcat7, khi nào xuất hiện dòng "Finish" là quá trình cài đặt kết thúc

###B3. Tiến chạy script để thiết lập thông số cơ bản

`bash config_Tomcat7.sh`

Sau khi thực hiện script trên, máy sẽ đổi port mặc định của Tomcat7 là 8080 thành 8888, thay đổi trang web mặc định thành trang web khác, đồng thời hiện thị địa chỉ ip của máy, port, và đường dẫn để truy cập tới trang web mặc định của web server
