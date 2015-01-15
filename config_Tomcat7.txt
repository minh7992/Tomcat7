
#!/bin/bash
#
echo "Config"
#Doi port
sed -i 's/8080/8888/g' /etc/tomcat7/server.xml

#Tao trang Index

echo "Tao trang Index"
echo "<h1> IT WORK !! </h1>" >> /var/lib/tomcat7/webapps/ROOT/index.htm
sed -i 's/<welcome-file>index.html<\/welcome-file>/<welcome-file>index.htm<\/welcome-file>'/ /etc/tomcat7/web.xml 
service tomcat7 restart

#Hien thi 

IP=`ip addr show eth1 | awk 'NR==3'{print} | awk '{print$2}' | sed 's/\/.*//'`
Port=`cat /etc/tomcat7/server.xml | awk 'NR==72{print$2}' | sed 's/\"//g' | sed 's/port=//'`

echo "Address: $IP"
echo "Port: $Port"

#Truy cap duong dan
echo "Truy cap web bang duong dan sau:"
echo "http://$IP:$Port"

