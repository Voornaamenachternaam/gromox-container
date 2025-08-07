FROM opensuse/leap:15.5
RUN zypper --non-interactive refresh && zypper --non-interactive install -y iptables iproute2 kmod curl patterns-base-apparmor patterns-base-base procps sudo systemd python3-pip vim mariadb-client gromox grommunio-antispam grommunio-common grommunio-web grommunio-sync grommunio-dav postfix postfix-mysql grommunio-chat firewalld cyrus-sasl-saslauthd cyrus-sasl-plain jq python3-certbot python3-certbot-nginx
RUN pip3 install dnspython
RUN curl -fsSL https://download.grommunio.com/RPMS/grommunio-admin-api-1.17.10.5947394-lp155.11.1.noarch.rpm -o /tmp/admin-api.rpm && rpm -Uvh --nodeps /tmp/admin-api.rpm && rm /tmp/admin-api.rpm
RUN curl -fsSL https://download.grommunio.com/RPMS/grommunio-admin-web-1.17.10.5947394-lp155.11.1.noarch.rpm -o /tmp/admin-web.rpm && rpm -Uvh --nodeps /tmp/admin-web.rpm && rm /tmp/admin-web.rpm
COPY gromox-core/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
