FROM centos:latest

ONBUILD RUN yum -y update

# Add the nginx and PHP dependent repository
ADD nginx.repo /etc/yum.repos.d/nginx.repo

# Install common packages
RUN yum -y install nginx

# RUN easy_install supervisor 

## CentOS 7 and Red Hat (RHEL) 7 ##
#RUN wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm && rpm -Uvh epel-release-latest-7.*.rpm
#RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

# Setting timezone to Rome
RUN unlink /etc/localtime
RUN ln -s /usr/share/zoneinfo/Europe/Rome /etc/localtime

# nginx config
#RUN sed -i -e"s/keepalive_timeout\s*65/keepalive_timeout 2/" /etc/nginx/nginx.conf
#RUN sed -i -e"s/keepalive_timeout 2/keepalive_timeout 2;\n\tclient_max_body_size 100m/" /etc/nginx/nginx.conf
RUN echo "daemon off;" >> /etc/nginx/nginx.conf

# Add the default virtual host configuration file
COPY ./default.conf /etc/nginx/conf.d/default.conf

# Adding the configuration file for Supervisor
#ADD supervisord.conf /etc/

# Add folder & permission to www
#RUN useradd yith
#RUN mkdir -p /var/www/vhosts
#RUN chown -R yith:nginx /var/www/vhosts

# Add folder & permission for sessions
#RUN mkdir -p /var/www/sessions
#RUN chown -R yith:nginx /var/www/sessions

# Set the port to 80
EXPOSE 80

# Executing supervisord
CMD ["nginx"]