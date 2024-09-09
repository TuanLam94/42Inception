FROM	debian:11.10

RUN	apt update \
	# common
	&& apt-get install -y nano wget tar \
	&& apt dist-upgrade -y \
	&& apt install build-essential libpcre3-dev libssl-dev zlib1g-dev libgd-dev -y \
	&& wget http://nginx.org/download/nginx-1.26.0.tar.gz -y \
	&& tar -xzvf nginx-1.26.0.tar.gz \
	&& cd nginx-1.26.0
	
RUN	adduser --system --no-create-home --shell /bin/false --disabled-login --group nginx

RUN	./configure --prefix=/var/www/html --sbin-path=/usr/sbin/nginx --modules-path=/etc/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --pid-path=/etc/nginx/nginx.pid --lock-path=/etc/nginx/nginx.lock --user=nginx --group=nginx --with-threads --with-file-aio --with-http_ssl_module --with-http_v2_module --with-http_realip_module --with-http_addition_module --with-http_image_filter_module=dynamic --with-http_sub_module --with-http_mp4_module --with-http_gzip_static_module --with-http_auth_request_module --with-http_secure_link_module --with-http_slice_module --with-http_stub_status_module --http-log-path=/var/log/nginx/access.log --with-stream --with-stream_ssl_module --with-stream_realip_module --with-compat --with-pcre-jit

RUN	make -j4 \
	&& make install

RUN	echo "[Unit]" > /etc/systemd/system/nginx.service \
	&& echo "Description=The NGINX HTTP and reverse proxy server" > /etc/systemd/system/nginx.service \
	&& echo "After=syslog.target network-online.target remote-fs.target nss-lookup.target" > /etc/systemd/system/nginx.service \
	&& echo "Wants=network-online.target" > /etc/systemd/system/nginx.service \
	&& echo "[Service]" > /etc/systemd/system/nginx.service \
	&& echo "Type=forking" > /etc/systemd/system/nginx.service \
	&& echo "PIDFile=/etc/nginx/nginx.pid" > /etc/systemd/system/nginx.service \
	&& echo "ExecStartPre=/usr/sbin/nginx -t" > /etc/systemd/system/nginx.service \
	&& echo "ExecStart=/usr/sbin/nginx" > /etc/systemd/system/nginx.service \
	&& echo "ExecReload=/usr/sbin/nginx -s reload" > /etc/systemd/system/nginx.service \
	&& echo "ExecStop=/bin/kill -s QUIT $MAINPID" > /etc/systemd/system/nginx.service \
	&& echo "PrivateTmp=true" > /etc/systemd/system/nginx.service \
	&& echo "[Install]" > /etc/systemd/system/nginx.service \
	&& echo "WantedBy=multi-user.target" > /etc/systemd/system/nginx.service

EXPOSE 443

EXPOSE 9000
