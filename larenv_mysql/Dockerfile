FROM mariadb:10.1
ENV MYSQL_DATABASE=greenhouse
ENV MYSQL_ROOT_PASSWORD=root
VOLUME /shared
ADD bases /bases
ADD scripts /scripts
RUN chmod -R 777 /scripts
RUN chmod -R +x /scripts
RUN apt-get update
RUN apt-get install sshpass -y
RUN apt-get install vim -y
RUN cp -R /scripts /bin
RUN adduser --disabled-password --gecos '' application
RUN chown application /shared/
