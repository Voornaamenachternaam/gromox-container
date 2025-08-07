FROM opensuse/leap:15.5
RUN zypper --non-interactive refresh && zypper --non-interactive ar -C https://download.grommunio.com/community/openSUSE_Leap_15.5 grommunio && zypper --non-interactive --gpg-auto-import-keys refresh grommunio && zypper --non-interactive install -y iptables iproute2 kmod curl patterns-base-apparmor patterns-base-base procps sudo systemd vim mariadb-client gromox grommunio-office firewalld cyrus-sasl-saslauthd cyrus-sasl-plain jq python3-certbot python3-certbot-nginx
COPY gromox-office/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/entrypoint.sh"]
