ARG BUILD_FROM
# hadolint ignore=DL3006
FROM ${BUILD_FROM}

# Set shell
SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN apt-get update
RUN apt-get install -y software-properties-common 
RUN add-apt-repository ppa:ondrej/php
RUN apt-get install -y git iptables iproute2 iw wpasupplicant net-tools
RUN apt-get install -y hostapd qrencode dnsmasq lighttpd vnstat
RUN apt-get install -y dhcpcd5
RUN apt-get install -y php7.3-cgi

RUN rm -Rf /var/www/html
RUN git clone --branch 2.6.2 https://github.com/RaspAP/raspap-webgui /var/www/html 
 
COPY /rootfs / 
# TODO wpa_supplicant -Dnl80211 -i wlan0 -c/etc/wpa_supplicant/wpa_supplicant.conf

RUN cp /var/www/html/config/50-raspap-router.conf /etc/lighttpd/conf-available
RUN ln -s /etc/lighttpd/conf-available/50-raspap-router.conf /etc/lighttpd/conf-enabled/50-raspap-router.conf

# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_REF
ARG BUILD_VERSION

# Labels
LABEL \
    io.hass.name="hotspot_wifi" \
    io.hass.description="hotspot_wifi" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="ArminasTV <arminas.stream@gmail.com>" \
    org.label-schema.description="hotspot_wifi" \
    org.label-schema.build-date=${BUILD_DATE} \
    org.label-schema.name="hotspot_wifi" \
    org.label-schema.schema-version="1.0" \
    org.label-schema.url="https://github.com/ArminasTV/Hassio-addons/" \
    org.label-schema.usage="https://github.com/ArminasTV/Hassio-addons/tree/master/hotspot_wifi/tree/master/README.md" \
    org.label-schema.vcs-ref=${BUILD_REF} \
    org.label-schema.vcs-url="https://github.com/ArminasTV/Hassio-addons/tree/master/hotspot_wifi" \
    org.label-schema.vendor="ArminasTV"

