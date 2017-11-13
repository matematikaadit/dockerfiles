# Based on:
# - https://raw.githubusercontent.com/tomsik68/docker-xampp/master/Dockerfile
# - https://raw.githubusercontent.com/fuyuanli/Dockerfile-XAMPP/master/Dockerfile

FROM ubuntu:16.04
RUN apt-get update

# net-tools for /bin/netstat, needed by xampp
RUN apt-get -y install wget net-tools

# download and install xampp
RUN wget -O xampp-installer.run \
    "https://www.apachefriends.org/xampp-files/7.1.11/xampp-linux-x64-7.1.11-0-installer.run"
RUN chmod +x xampp-installer.run
RUN ./xampp-installer.run
RUN rm xampp-installer.run

# soft link lampp executable to /usr/bin/lampp
RUN ln -s /opt/lampp/lampp /usr/bin/lampp

# expose PHPMyAdmin
RUN sed -i.bak s'/Require local/Require all granted/g' /opt/lampp/etc/extra/httpd-xampp.conf

# Prepare /www as mount point
RUN mkdir /www && ln -s /www /opt/lampp/htdocs
VOLUME ["/www"]

EXPOSE 3306 443 80
CMD ["/opt/lampp/lampp", "start"]
