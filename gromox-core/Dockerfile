FROM opensuse/leap:15.5

RUN zypper --non-interactive refresh && zypper --non-interactive install -y iptables iproute2 kmod curl patterns-base-apparmor patterns-base-base procps sudo systemd

ARG GROMMUNIO_REPO=community/openSUSE_Leap_15.5
RUN curl -fsSL https://download.grommunio.com/RPM-GPG-KEY-grommunio -o /tmp/gr.key && rpm --import /tmp/gr.key && zypper --non-interactive ar -C https://download.grommunio.com/${GROMMUNIO_REPO} grommunio && zypper --non-interactive --gpg-auto-import-keys refresh grommunio

RUN zypper --non-interactive install -y vim mariadb-client gromox grommunio-admin-api grommunio-admin-web grommunio-antispam grommunio-common grommunio-web grommunio-sync grommunio-dav postfix postfix-mysql grommunio-chat firewalld cyrus-sasl-saslauthd cyrus-sasl-plain jq python3-py3dns python3-certbot python3-certbot-nginx

COPY gromox-core/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
