FROM alpine:latest

# Define Mumble version
ENV MUMBLE_VERSION=1.3.2
ENV BZIP_URL=https://github.com/mumble-voip/mumble/releases/download/${MUMBLE_VERSION}/murmur-static_x86-${MUMBLE_VERSION}.tar.bz2

# Create Mumble directories
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories && \
    mkdir -pv /opt/mumble /etc/mumble && \
    adduser -DHs /sbin/nologin mumble && \
    apk add --update ca-certificates bzip2 su-exec tar tzdata wget \
    && wget -qO- ${BZIP_URL} | tar -xjv --strip-components=1 -C /opt/mumble \
    && apk del ca-certificates bzip2 tar wget && rm -rf /var/cache/apk/* \
    && chown -R mumble:mumble /etc/mumble /opt/mumble

# Set running user
USER mumble

# Default command
CMD ["/opt/mumble/murmur.x86", "-v", "-fg", "-ini", "/etc/murmur/murmur.ini"]