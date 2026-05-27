FROM alpine:3.20
ARG VERSION=0.14.0
RUN apk add --no-cache smartmontools wget ca-certificates && \
    case "$(uname -m)" in \
        x86_64)  ARCH=amd64 ;; \
        aarch64) ARCH=arm64 ;; \
        armv7l)  ARCH=armv7 ;; \
        *) echo "Unsupported arch: $(uname -m)" >&2; exit 1 ;; \
    esac && \
    wget -qO /tmp/smartctl_exporter.tar.gz \
        "https://github.com/prometheus-community/smartctl_exporter/releases/download/v${VERSION}/smartctl_exporter-${VERSION}.linux-${ARCH}.tar.gz" && \
    tar -xzf /tmp/smartctl_exporter.tar.gz -C /tmp && \
    mv "/tmp/smartctl_exporter-${VERSION}.linux-${ARCH}/smartctl_exporter" /usr/local/bin/smartctl_exporter && \
    chmod +x /usr/local/bin/smartctl_exporter && \
    rm -rf /tmp/smartctl_exporter*

EXPOSE 9633
ENTRYPOINT ["/usr/local/bin/smartctl_exporter"]
