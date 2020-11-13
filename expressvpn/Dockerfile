
# Run expressvpn in a container
FROM arm32v7/debian:buster-slim
COPY qemu-arm-static /usr/bin
LABEL maintainer="awillems@matchbase.tech"

ENV ACTIVATION_CODE Code
ENV LOCATION smart
ARG APP=expressvpn_3.2.1.2-1_armhf.deb

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates wget expect iproute2 curl \
    && rm -rf /var/lib/apt/lists/* \
    && wget -q "https://www.expressvpn.works/clients/linux/${APP}" -O /tmp/${APP} \
    && dpkg -i /tmp/${APP} \
    && rm -rf /tmp/*.deb \
    && apt-get purge -y --auto-remove wget

COPY entrypoint.sh /tmp/entrypoint.sh
COPY expressvpnActivate.sh /tmp/expressvpnActivate.sh

ENTRYPOINT ["/bin/bash", "/tmp/entrypoint.sh"]
