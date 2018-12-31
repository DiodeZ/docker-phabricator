FROM arm32v6/alpine:3.8
RUN apk add --no-cache mariadb mariadb-client
ARG UID=1000
ARG GID=1000
RUN sed -i "s@^mysql.*@mysql:x:$UID:$GID:mysql:/var/lib/mysql:/sbin/nologin@" /etc/passwd && \
    sed -i "s@^mysql.*@mysql:x:$GID:mysql@" /etc/group && \
    install -o mysql -g mysql -d /run/mysqld && \
    install -o mysql -g mysql -d /etc/mysql/conf.d && \
    chown -R mysql:mysql /etc/mysql /var/lib/mysql && \
    echo "!includedir /etc/mysql/conf.d/" >> /etc/mysql/my.cnf
COPY start.sh /start.sh
RUN chmod +x /start.sh
USER mysql
WORKDIR /var/lib/mysql
EXPOSE 3306/tcp
CMD ["/start.sh"]
