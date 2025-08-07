FROM opensuse/leap:15.5

RUN zypper --non-interactive refresh && zypper --non-interactive install -y iptables iproute2 kmod curl patterns-base-apparmor patterns-base-base procps sudo systemd

ARG GROMMUNIO_REPO=community/openSUSE_Leap_15.5
RUN curl -fsSL https://download.grommunio.com/RPM-GPG-KEY-grommunio -o /tmp/gr.key && rpm --import /tmp/gr.key && zypper --non-interactive ar -C https://download.grommunio.com/${GROMMUNIO_REPO} grommunio && zypper --non-interactive --gpg-auto-import-keys refresh grommunio

RUN zypper --non-interactive ar https://download.opensuse.org/repositories/devel:/languages:/python/openSUSE_Leap_15.5/ python-python && zypper --non-interactive ref

RUN zypper --non-interactive install -y vim mariadb-client python3-dns gromox grommunio-archive python3-certbot python3-certbot-nginx

COPY gromox-archive/entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
