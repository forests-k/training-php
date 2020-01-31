FROM mysql:8.0

# 指定の場所にログを記録するディレクトリを作る
RUN mkdir -p /var/log/mysql
# 指定の場所にログを記録するファイルを作る
RUN touch /var/log/mysql/mysqld.log

# 設定ファイルの配置
ADD ./conf.d/my.cnf /etc/mysql/conf.d
RUN chmod 644 /etc/mysql/conf.d/my.cnf