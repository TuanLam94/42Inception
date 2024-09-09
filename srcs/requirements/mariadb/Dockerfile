FROM	debian:11.10

#common line
RUN	apt-get update && apt-get install -y nano wget tar

RUN	echo "deb http://ftp.debian.org/debian bookworm main contrib" > /etc/apt/sources.list.d/mariadb.list \
	&& echo "deb-src http://ftp.debian.org/debian bookworm main contrib" >> /etc/apt/sources.list.d/mariadb.list \
	&& echo "deb-src http://security.debian.org/debian-security bookworm-security main contrib" >> /etc/apt/sources.list.d/mariadb.list

RUN	apt-get update \
	&& apt build-dep mariadb-server -y

RUN	cd ~ \
	&& wget https://archive.mariadb.org/mariadb-11.3.2/source/mariadb-11.3.2.tar.gz \
	&& tar -xf mariadb-*.tar.gz \
	&& cd mariadb-11.3.2 \
	&& cmake . -DWITHOUT_DYNAMIC_PLUGINS=1 -DWITH_MARIABACKUP=0 -DPLUGIN_PERFSCHEMA=NO -DWIDTH_UNIT_TESTS=0 \
	&& cmake --build . \
	&& cmake --install .

EXPOSE	3306

