## This dockerfile uses alpine as base image and installs vegeta (https://github.com/tsenart/vegeta)
## A few dependencies that needs to be installed are wget tar gzip
## The final image size is just 94.1MB

FROM registry.access.redhat.com/ubi8/ubi AS ubi-micro-build
RUN mkdir -p /mnt/rootfs
RUN yum install --installroot /mnt/rootfs wget tar gzip --releasever 8 --setopt install_weak_deps=false --nodocs -y; yum --installroot /mnt/rootfs clean all
RUN rm -rf /mnt/rootfs/var/cache/* /mnt/rootfs/var/log/dnf* /mnt/rootfs/var/log/yum.*

FROM scratch
ENV VEGETA_VERSION 12.8.4

LABEL \
    maintainer="Karan Singh <karan.singh731987@gmail.com>" \
    com.redhat.component="ubi8-micro-container" \
    name="karansingh/vegeta-ubi" \
    version="12.8.4" \
    org.opencontainers.image.title="vegeta" \
    org.opencontainers.image.description="Docker image for the Vegeta HTTP load testing tool." \
    org.opencontainers.image.authors="Karan Singh <karan.singh731987@gmail.com>" \
    org.opencontainers.image.url="https://github.com/peter-evans/vegeta-docker" 

COPY --from=ubi-micro-build /mnt/rootfs/ /
COPY --from=ubi-micro-build /etc/yum.repos.d/ubi.repo /etc/yum.repos.d/ubi.repo

RUN /usr/bin/wget "https://github.com/tsenart/vegeta/releases/download/v${VEGETA_VERSION}/vegeta_${VEGETA_VERSION}_linux_amd64.tar.gz" -O /tmp/vegeta.tar.gz \
    && cd bin \
    && /usr/bin/tar xzf /tmp/vegeta.tar.gz \
    && rm /tmp/vegeta.tar.gz 

USER 1001
CMD [ "/bin/vegeta", "-help" ]