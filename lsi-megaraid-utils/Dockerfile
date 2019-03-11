FROM centos:7.6.1810 as builder

ADD rpms /root/
RUN rpm -Uvh /root/*.rpm

FROM centos:7.6.1810

COPY --from=builder /opt /opt

RUN yum -y install \
  dmidecode \
  smartmontools \
  && yum clean all \
  && rm -rf /var/cache/yum \
  && /usr/sbin/update-smart-drivedb \
  && ln -s /opt/MegaRAID/MegaCli/MegaCli64 /usr/local/bin/megacli \
  && ln -s /opt/MegaRAID/MegaCli/MegaCli64 /usr/local/bin/MegaCli \
  && ln -s /opt/MegaRAID/storcli/storcli64 /usr/local/sbin/storcli

WORKDIR /root

CMD ["bash", "-l"]