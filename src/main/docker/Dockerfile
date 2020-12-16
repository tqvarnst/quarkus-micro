FROM registry.access.redhat.com/ubi8/ubi AS ubi-micro-build
MAINTAINER Scott McCarty smccarty@redhat.com
RUN mkdir -p /mnt/rootfs
RUN yum install --installroot /mnt/rootfs coreutils-single zlib glibc-minimal-langpack --releasever 8 --setopt install_weak_deps=false --nodocs -y;yum clean all
RUN rm -rf /mnt/rootfs/var/cache/*
RUN rm -rf /mnt/rootfs/var/lib/rpm

FROM gruebel/upx:latest AS upx
COPY target/*-runner /tmp/application
RUN /usr/bin/upx --best --lzma -o /tmp/upx-compressed-application /tmp/application 

FROM scratch AS ubi8-micro
COPY --from=ubi-micro-build /mnt/rootfs/ /
COPY --from=ubi-micro-build /etc/yum.repos.d/ubi.repo /etc/yum.repos.d/ubi.repo
COPY --from=upx /tmp/upx-compressed-application /application
#COPY target/*-runner /application
EXPOSE 8080
CMD ["./application", "-Dquarkus.http.host=0.0.0.0"]