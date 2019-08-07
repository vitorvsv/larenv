#
# To read more, consult this link
# http://dockerfile.readthedocs.io/en/latest/content/DockerImages/dockerfiles/php-apache.html
#
#FROM "webdevops/php-apache:ubuntu-14.04" # PHP 5.5
#FROM "webdevops/php-apache:ubuntu-17.04" # PHP 7.0
# PHP 7.2
FROM webdevops/php-apache:ubuntu-18.04
VOLUME /shared
RUN apt-get update
RUN apt-get install vim -y
RUN chown application /shared/
WORKDIR /app
