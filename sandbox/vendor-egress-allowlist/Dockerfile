FROM debian:bookworm-slim

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
    ca-certificates \
    curl \
    dnsutils \
    iproute2 \
    iptables \
    python3 \
  && rm -rf /var/lib/apt/lists/*

COPY allowlist.txt /opt/riela-sandbox/allowlist.txt
COPY bin/entrypoint.sh /usr/local/bin/riela-vendor-egress-entrypoint
COPY bin/sandbox-check.py /usr/local/bin/riela-sandbox-check

RUN chmod +x \
  /usr/local/bin/riela-vendor-egress-entrypoint \
  /usr/local/bin/riela-sandbox-check

ENV RIELA_VENDOR_ALLOWLIST=/opt/riela-sandbox/allowlist.txt
ENTRYPOINT ["riela-vendor-egress-entrypoint"]
CMD ["riela-sandbox-check", "/package"]
