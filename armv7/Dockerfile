# This is an auto-generated file, please edit template/Dockerfile!
FROM arm32v7/ubuntu:bionic

COPY qemu/qemu-arm-static /usr/bin/qemu-arm-static

RUN \
    apt-get update \
    && apt-get install -y --no-install-recommends \
        python \
        python-pip \
        python-setuptools \
        python-pil \
        iputils-ping \
        git \
    && rm -rf \
        /tmp/* \
        /var/{cache,log}/* \
        /var/lib/apt/lists/*

COPY platformio.ini /opt/pio/

RUN \
    pip2 install --no-cache-dir --no-binary :all: platformio==3.6.7 \
    # Change some platformio settings
    && platformio settings set enable_telemetry No \
    && platformio settings set check_libraries_interval 1000000 \
    && platformio settings set check_platformio_interval 1000000 \
    && platformio settings set check_platforms_interval 1000000 \
    # Build an empty platformio project to force platformio to install all fw build dependencies
    # The return-code will be non-zero since there's nothing to build.
    && (platformio run -d /opt/pio; echo "Done") \
    && rm -rf /opt/pio/

VOLUME /config
WORKDIR /usr/src/app