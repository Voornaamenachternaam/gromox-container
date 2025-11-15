FROM opensuse/leap:15.6
RUN rpm --import https://download.grommunio.com/RPM-GPG-KEY-grommunio; zypper --non-interactive refresh; zypper --non-interactive ar -f --no-gpgcheck https://download.grommunio.com/community/openSUSE_Leap_15.6 grommunio; zypper --non-interactive refresh; zypper --non-interactive install -y iptables iproute2 kmod curl patterns-base-apparmor patterns-base-base procps sudo systemd vim mariadb-client gromox grommunio-antispam grommunio-common grommunio-web grommunio-sync grommunio-dav postfix postfix-mysql grommunio-chat firewalld cyrus-sasl-saslauthd cyrus-sasl-plain jq python3-certbot python3-certbot-nginx
COPY gromox-core/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
