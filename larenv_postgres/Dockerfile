FROM postgres:9.6.14
# ENV POSTGRES_DB=postgres
ENV POSTGRES_USER=postgres
ENV POSTGRES_PASSWORD=postgres
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
