#Cài đặt Web server sử dụng Tomcat 7 trên Ubuntu 14.04
##Mục Lục
[1. Giới thiệu](#Gioithieu)

[2. Các bước cài đặt Apache Tomcat](#Cacbuoccaidat)

[3. Một số cấu hình cơ bản trên Tomcat7](#Motsocauhinh)
<a name="Gioithieu"></a>
##1.Giới thiệu Apache Tomcat
Apache Tomcat là máy chủ web cho các ứng dụng Java được phát hành bởi Apache Software Foundation. Tomcat là một máy chủ web và cũng là một servlet container cho các ứng dụng web Java.

Để có một webserver đầy đủ (tức là hỗ trợ cả JSP, PHP , CGI...) thì  cần kết hợp Apache và TOMCAT

<a name="Cacbuoccaidat"></a>
##2.Các bước cài đặt Apache Tomcat
Trong bài này chúng ta sẽ cài JDK, Apache Tomcat 7, để bắt đầu chúng ta sẽ cài đặt JDK. Apache Tomcat 7 yêu cầu tối thiểu là java 1.6

**Bước 1: Cài đặt JDK**

Có thể bỏ qua bước này nếu đã cài phiên JDK tối thiểu mà Apache Tomcat 7 yêu cầu, sử dụng lệnh sau để cài JDK:

`$ sudo apt-get install openjdk-6-jdk`

**Bước 2: Thêm JAVA_HOME vào biến môi trường**

`$ sudo vi /etc/environment`

Sau đó thêm biến JAVA_HOME vào cuối file:

`JAVA_HOME=/usr/lib/jvm/java-6-openjdk-amd64`

**Bước 3: Cài đặt Apache Tomcat 7**

Cài đặt Tomcat 7 thông qua kho ứng dụng của Ubuntu với lệnh:

`$ sudo apt-get install tomcat7`

Sau đó kiểm tra kết quả bằng cách mở trình duyệt lên và truy cập vào địa chỉ
http://your_ip_address:8080

và xuất hiện trang với dòng “It works” là Tomcat đã hoạt động

**Bước 4: Cài đặt tài liệu Tomcat trực  tuyến, giao diện web (manager webapp) và một vài ví dụ ứng dụng web**

`$ sudo apt-get install tomcat7-docs tomcat7-admin tomcat7-examples`

**Bước 5: Cấu hình giao diện web Tomcat**

Mở file:
`$ sudo vi /etc/tomcat7/tomcat-users.xml`

Có thể thêm một người dùng có thể truy cập vào manager-gui và admin-gui (giao diện quản lý mà ta đã cài) bằng cách thêm các dòng sau:

```sh
<tomcat-users>
<user username=”admin” password=”admin” roles=”manager-gui,admin-gui”>
</tomcat-users>
```

Và chúng ta có thể thay đổi người dùng và password như ý muốn, sau đó khởi động lại dịch vụ Tomcat:

`$ sudo service tomcat7 restart`

Truy cập vào địa chỉ `http://your_ip_address:8080/manager/html`  để kiểm tra (điền user và password như cấu hình trên để đăng nhập) ta được giao diện web như sau:

<img src="http://i.imgur.com/T9SwdVi.png">

Có thể truy cấp để quản lý Virtual Host qua đường dẫn:

`http://your_ip_address:8080/ host-manager/html` ta được giao diện web như sau:

<img src="http://i.imgur.com/fMXCEcc.png">

Có thể xem tài liệu trực tuyến của Tomcat qua đường dẫn: 

`http://your_ip_address:8080/docs/`

<a name="Motsocauhinh"></a>
##3.Một số cấu hình cơ bản trên Tomcat 7
Một số thông số cấu hình cơ bản ở trong file server.xml, ta mở file này:

`$sudo vi /etc/tomcat7/server.xml`

Khai báo port kết nối như đoạn sau:

```sh
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
              URIEncoding="UTF-8"
               redirectPort="8443" />

```

Khai báo thư mục mặc định chứa code web:

```sh
<Host name="localhost"  appBase="webapps"
            unpackWARs="true" autoDeploy="true">
</Host>
```

Ở đây, thư mục mặc định là webapps và trang mặc định `index.html` nằm trong đường dẫn

`/var/lib/tomcat7/webapps/ROOT/index.html`

Chúng ta có thể sửa thư mục mặc định này bằng cách sửa `appBase=”webapps”` thành `appBase="/var/www/webapps"`

Khai báo trang web mặc định trong file `web.xml`

`$sudo vi /etc/tomcat7/web.xml` 

và chú ý đoạn sau:

```sh
 <welcome-file-list>
           <welcome-file>index.html</welcome-file>
           <welcome-file>index.htm</welcome-file>
           <welcome-file>index.jsp</welcome-file>
           </welcome-file-list>
```

Ở đây, các trang web `index.html`, `index.htm`, `index.jsp` là các trang web mặc định
	
**Ví dụ dựng 1 trang web đơn giản như sau:** 

- Tạo thư mục `/var/www/webapps/ROOT`:

`$ sudo mkdir -p /var/www/webapps/ROOT`

- Tạo file index.html với nội dung “DANG NHAP THANH CONG” để trong thư mục mới tạo ở trên

Sửa file cấu hình `/etc/tomcat7/server.xml`: sửa `appBase=”webapps”` thành  `appBase="/var/www/webapps"`

Khởi động lại dịch vụ: 

`$ sudo service tomcat7 restart`

- Vào trình duyệt theo đường dẫn  `http://your_ip_address:8080`
<ul>
Ta được giao diện web như sau là thành công:

<img src="http://i.imgur.com/FO7VQyk.png">
</ul>
