FROM opensuse/leap:15.5

# 1. Base prerequisites
RUN zypper --non-interactive install -y \
      iptables iproute2 kmod curl \
      patterns-base-apparmor patterns-base-base \
      procps sudo systemd

# 2. Grommunio repo & key
ARG GROMMUNIO_REPO=community/openSUSE_Leap_15.5
RUN curl -fsSL https://download.grommunio.com/RPM-GPG-KEY-grommunio \
      -o /tmp/gr.key \
    && rpm --import /tmp/gr.key \
    && zypper --non-interactive --quiet ar -C \
         https://download.grommunio.com/${GROMMUNIO_REPO} grommunio \
    && zypper --gpg-auto-import-keys refresh grommunio

# 3. Install office service packages
RUN zypper --non-interactive install -y \
      vim \
      mariadb-client \
      gromox \
      grommunio-office \
      python3-dnspython

# 4. Copy office entry scripts & services
COPY gromox-office/scripts/entry.service /etc/systemd/system/entry.service
COPY gromox-office/scripts/enable.sh /home/scripts/enable.sh
RUN chmod +x /home/scripts/enable.sh

ENTRYPOINT [ "/usr/lib/systemd/systemd", "--log-level=err" ]
