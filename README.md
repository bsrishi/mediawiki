# Use the CentOS 7 base image
FROM centos:7

# Disable the fastestmirror plugin
RUN sed -i 's/enabled=1/enabled=0/' /etc/yum/pluginconf.d/fastestmirror.conf

# Install required packages
RUN yum update -y && \
    yum install -y epel-release && \
    yum install -y http://rpms.remirepo.net/enterprise/remi-release-7.rpm

# Enable the Remi repository for PHP 7.4
RUN yum-config-manager --enable remi-php74

# Install PHP and required extensions
RUN yum install -y httpd php php-mysql php-mbstring php-gd php-xml

# Download and extract MediaWiki
RUN curl -L -o mediawiki.tar.gz https://releases.wikimedia.org/mediawiki/1.36/mediawiki-1.36.2.tar.gz && \
    tar -xzf mediawiki.tar.gz && \
    rm -f mediawiki.tar.gz && \
    mv mediawiki-1.36.2/* /var/www/html/

# Set the working directory
WORKDIR /var/www/html/

# Expose port 80
EXPOSE 80

# Start Apache web server
CMD ["/usr/sbin/httpd", "-DFOREGROUND"]
