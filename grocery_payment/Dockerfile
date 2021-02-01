FROM centos:7

# Install Apache
RUN yum -y update
RUN yum -y install httpd httpd-tools



# Install EPEL Repo
RUN rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm \
 && rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm

# Install PHP
RUN yum -y install php72w php72w-bcmath php72w-cli php72w-common php72w-gd php72w-intl php72w-ldap php72w-mbstring \
    php72w-mysql php72w-pear php72w-soap php72w-xml php72w-xmlrpc

# Update Apache Configuration
RUN sed -E -i -e '/<Directory "\/var\/www\/html">/,/<\/Directory>/s/AllowOverride None/AllowOverride All/' /etc/httpd/conf/httpd.conf
RUN sed -E -i -e 's/DirectoryIndex (.*)$/DirectoryIndex index.php \1/g' /etc/httpd/conf/httpd.conf
RUN echo "ServerName localhost" >> /etc/httpd/conf/httpd.conf

EXPOSE 80

RUN mkdir /var/www/html; exit 0

WORKDIR /var/www/html

RUN yum -y install git

RUN git clone https://95d15a295546e6f22cf31e220350ae3614022ac8@github.com/vinodjain1/grocery_payment.git .

RUN chown -R apache:apache /var/www
# Start Apache
CMD ["/usr/sbin/httpd","-D","FOREGROUND"]
