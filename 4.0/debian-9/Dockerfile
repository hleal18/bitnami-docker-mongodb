FROM docker.io/bitnami/minideb:stretch
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV HOME="/" \
    OS_ARCH="amd64" \
    OS_FLAVOUR="debian-9" \
    OS_NAME="linux"

COPY prebuildfs /
# Install required system packages and dependencies
RUN install_packages acl ca-certificates curl gzip libc6 libcomerr2 libcurl3 libffi6 libgcc1 libgcrypt20 libgmp10 libgnutls30 libgpg-error0 libgssapi-krb5-2 libhogweed4 libidn11 libidn2-0 libk5crypto3 libkeyutils1 libkrb5-3 libkrb5support0 libldap-2.4-2 libnettle6 libnghttp2-14 libp11-kit0 libpcap0.8 libpsl5 librtmp1 libsasl2-2 libssh2-1 libssl1.0.2 libssl1.1 libtasn1-6 libunistring0 procps tar zlib1g
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "yq" "3.4.0-0" --checksum 18a36fe533b38d5d22e64aba99619ff0f32d22b04349f1c2ec678a91664cef23
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "wait-for-port" "1.0.0-1" --checksum 04cca3ba5204635108908eb8032b7b2f1882aba2f1636cc45fe3c70dfa0b498a
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "render-template" "1.0.0-0" --checksum 7defe2e6b6eabb3dd3a193e7d4e932f768b0188b6fb4ecd862bf10632e747f25
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "mongodb" "4.0.20-0" --checksum 2c611d6c9dd2d1f7fd3d943914e5b3f088fdeebb0aa8bd606c28f3452bc554c2
RUN . /opt/bitnami/scripts/libcomponent.sh && component_unpack "gosu" "1.12.0-0" --checksum b14e3fcbfe88c7a7421cb2adbf523c5a68ed0624651f9809190991906b531003
RUN chmod g+rwX /opt/bitnami

COPY rootfs /
RUN /opt/bitnami/scripts/mongodb/postunpack.sh
ENV BITNAMI_APP_NAME="mongodb" \
    BITNAMI_IMAGE_VERSION="4.0.20-debian-9-r59" \
    PATH="/opt/bitnami/common/bin:/opt/bitnami/mongodb/bin:$PATH"

EXPOSE 27017

USER 1001
ENTRYPOINT [ "/opt/bitnami/scripts/mongodb/entrypoint.sh" ]
CMD [ "/opt/bitnami/scripts/mongodb/run.sh" ]
