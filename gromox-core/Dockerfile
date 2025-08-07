FROM opensuse/leap:15.5

# 1. Systemd setup prerequisites
RUN zypper --non-interactive install -y \
      iptables iproute2 kmod curl \
      patterns-base-apparmor patterns-base-base \
      procps sudo systemd

# 2. Add Grommunio repo and import GPG key
ARG GROMMUNIO_REPO=community/openSUSE_Leap_15.5
RUN curl -fsSL https://download.grommunio.com/RPM-GPG-KEY-grommunio \
      -o /tmp/gr.key \
    && rpm --import /tmp/gr.key \
    && zypper --non-interactive --quiet ar -C \
         https://download.grommunio.com/${GROMMUNIO_REPO} grommunio \
    && zypper --gpg-auto-import-keys refresh grommunio

# 3. Install all necessary packages (fixed names)
RUN zypper --non-interactive install -y \
      vim \
      mariadb-client \
      gromox \
      grommunio-admin-api \
      grommunio-admin-web \
      grommunio-antispam \
      grommunio-common \
      grommunio-web \
      grommunio-sync \
      grommunio-dav \
      postfix \
      postfix-mysql \
      grommunio-chat \
      firewalld \
      cyrus-sasl-saslauthd \
      cyrus-sasl-plain \
      jq \
      python3-dnspython \
      python3-certbot \
      python3-certbot-nginx

# 4. Copy service definitions & entrypoint
COPY gromox-core/scripts/db.service /etc/systemd/system/db.service
COPY gromox-core/scripts/entry.service /etc/systemd/system/entry.service
COPY gromox-core/entrypoint.sh /home/entrypoint.sh
RUN chmod +x /home/entrypoint.sh

# 5. Enable initial scripts
COPY gromox-core/scripts/enable.sh /home/scripts/enable.sh
RUN chmod +x /home/scripts/enable.sh \
 && /home/scripts/enable.sh

# 6. Final entrypoint: Systemd
ENTRYPOINT [ "/usr/lib/systemd/systemd", "--log-level=err" ]
