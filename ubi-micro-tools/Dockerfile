## This dockerfile uses ubi8 image for multi-stage build
## Installs wget, curl, tar, gzip
## The final image size is just 88.9MB
## Docker image 
## docker.io/karansingh/ubi-tools
## quay.io/karansingh/ubi-tools

FROM registry.access.redhat.com/ubi8/ubi AS ubi-micro-build
RUN mkdir -p /mnt/rootfs
RUN yum install --installroot /mnt/rootfs wget curl tar gzip --releasever 8 --setopt install_weak_deps=false --nodocs -y; yum --installroot /mnt/rootfs clean all
RUN rm -rf /mnt/rootfs/var/cache/* /mnt/rootfs/var/log/dnf* /mnt/rootfs/var/log/yum.*

FROM scratch
LABEL maintainer="Red Hat, Inc."

LABEL com.redhat.component="ubi8-micro-container"
LABEL name="ubi8/ubi-micro"
LABEL version="8.4"

COPY --from=ubi-micro-build /mnt/rootfs/ /
COPY --from=ubi-micro-build /etc/yum.repos.d/ubi.repo /etc/yum.repos.d/ubi.repo
USER 1001

## Keep container running
ENTRYPOINT ["tail", "-f", "/dev/null"]
