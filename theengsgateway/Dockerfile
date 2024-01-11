ARG BUILD_FROM
FROM $BUILD_FROM
LABEL io.hass.version="1.9.0" io.hass.type="addon" io.hass.arch="armv7|armhf|aarch64|i386|amd64"
RUN apt-get update && apt-get upgrade -y && \
    apt-get install --no-install-recommends -y build-essential bluez python3-pip python3-dev git
RUN git clone https://github.com/theengs/gateway.git
RUN python3 -m pip install --upgrade pip -y && \
    pip install setuptools-scm --upgrade -y  && \
    pip install wheel --upgrade -y
ENV current /root/gateway
WORKDIR $current
RUN git submodule init && git submodule update
RUN pip install . --upgrade
ENV current /root
ENV HOME $current
WORKDIR $current
COPY run.sh /root
COPY entrypoint.sh /root
RUN chmod a+x /root/run.sh
RUN chmod a+x /root/entrypoint.sh
ENTRYPOINT ["/root/entrypoint.sh"]
CMD [ "/root/run.sh" ]
