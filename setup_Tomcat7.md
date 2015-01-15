#!/bin/bash

#Update for Ubuntu

apt-get update
sleep 3

#Setup JDK

echo "Setup JDK"
apt-get install openjdk-6-jdk
sleep 2
echo "JAVA_HOME=/usr/lib/jvm/java-6-openjdk-amd64" >> /etc/environment

#Setup Apache Tomcat7

echo "Setup Apache Tomcat7"
apt-get install tomcat7
sleep 3
echo "Finish"