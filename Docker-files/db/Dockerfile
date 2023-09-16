FROM mysql:8.0.33
LABEL "Project"="Vprofile"
LABEL "Author"="Michael"

ENV MYSQL_ROOT_PASSWORD="vprodbpass"
ENV MYSQL_DATABASE="accounts"

ADD dc-backup.sql /docker-entrypoint-initdb.d/db_backup.sql