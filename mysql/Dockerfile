FROM centos:7
LABEL author xuexingdong 
ENV RPM_NAME mysql80-community-release-el7-1.noarch.rpm
ENV YUM_REPO_URL https://dev.mysql.com/get/${RPM_NAME}
RUN yum -y install wget
RUN wget ${YUM_REPO_URL} \
    && yum localinstall ${RPM_NAME} \
    && yum -y install mysql-community-server \
    && rm ${RPM_NAME}
RUN systemctl start mysqld.service
# modify password
RUN password=$(cat /var/log/mysqld.log | grep "temporary password" | tail -1 | sed -n 's/.*root@localhost: //p') \
    && mysql -uroot -p$password
ENV GROUP mysql
ENV USER mysql
RUN groupadd ${GROUP} \
    && useradd -M -s /sbin/nologin -g ${GROUP} ${USER}

