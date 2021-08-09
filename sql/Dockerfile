FROM alpine:latest
RUN apk add git
RUN git clone https://github.com/DiamondLightSource/ispyb-database.git /tmp/ispyb-database

FROM mariadb:10.4

COPY --from=0 /tmp/ispyb-database/schemas/ispyb/tables.sql /docker-entrypoint-initdb.d/1_tables.sql
COPY --from=0 /tmp/ispyb-database/schemas/ispyb/lookups.sql /docker-entrypoint-initdb.d/2_lookups.sql
COPY --from=0 /tmp/ispyb-database/schemas/ispyb/data.sql /docker-entrypoint-initdb.d/3_data.sql
COPY --from=0 /tmp/ispyb-database/schemas/ispyb/routines.sql /docker-entrypoint-initdb.d/4_routines.sql
# COPY --from=0 /tmp/ispyb-database/schema/routines.sql /docker-entrypoint-initdb.d/4_routines.sql

ENV MYSQL_DATABASE=ispyb
ENV MYSQL_RANDOM_ROOT_PASSWORD=1
ENV MYSQL_USER=ispyb
ENV MYSQL_PASSWORD=ispyb

# FROM alpine:latest

# RUN apk add mariadb mariadb-client git
# RUN mysql_install_db --user=mysql --datadir=/var/lib/mysql
# COPY build_db.sh /tmp/
# RUN sh -x /tmp/build_db.sh

