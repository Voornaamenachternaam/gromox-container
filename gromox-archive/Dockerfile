FROM opensuse/leap:15.5

# (Repeat same setup steps as core)
RUN zypper --non-interactive install -y \
      iptables iproute2 kmod curl \
      patterns-base-apparmor patterns-base-base \
      procps sudo systemd

ARG GROMMUNIO_REPO=community/openSUSE_Leap_15.5
RUN curl -fsSL https://download.grommunio.com/RPM-GPG-KEY-grommunio \
      -o /tmp/gr.key \
    && rpm --import /tmp/gr.key \
    && zypper --non-interactive --quiet ar -C \
         https://download.grommunio.com/${GROMMUNIO_REPO} grommunio \
    && zypper --gpg-auto-import-keys refresh grommunio

RUN zypper --non-interactive install -y \
      vim \
      mariadb-client \
      gromox \
      grommunio-archive \
      # (other archive-specific Grommunio packages…)
      python3-dnspython

# Copy archive-specific service files
COPY gromox-archive/scripts/firewall.sh /home/scripts/firewall.sh
COPY gromox-archive/scripts/entry.service /etc/systemd/system/entry.service
COPY gromox-archive/scripts/enable.sh /home/scripts/enable.sh
RUN chmod +x /home/scripts/*.sh

ENTRYPOINT [ "/usr/lib/systemd/systemd", "--log-level=err" ]
