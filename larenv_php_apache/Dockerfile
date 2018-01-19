#
# Para mais informaçoes vide link da documentaçao
# http://dockerfile.readthedocs.io/en/latest/content/DockerImages/dockerfiles/php-apache.html
#
#FROM "webdevops/php-apache:ubuntu-14.04"
FROM "webdevops/php-apache:ubuntu-17.04"
VOLUME /shared
RUN apt-get update
RUN apt-get install vim -y
RUN chown application /shared/
WORKDIR /app
