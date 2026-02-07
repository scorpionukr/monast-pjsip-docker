FROM rgielen/monast-pymon-docker

USER root

ADD monast-pymon.zip /
RUN unzip monast-pymon.zip \
      && rm -rf /pymon \
      && mv monast-pymon /pymon \
      && rm monast-pymon.zip

RUN mkdir /pymon/config && chown monast.monast /pymon/config
ADD monast.conf.template /pymon/
ADD entrypoint.sh /pymon/
RUN chown monast.monast /pymon/ -R && chmod +x /pymon/monast.py

ENV BIND_HOST=0.0.0.0
ENV BIND_PORT=5039
ENV ASTERISK_HOST=localhost
ENV ASTERISK_PORT=5038
ENV AMI_USERNAME=admin
ENV AMI_PASSWORD=admin
ENV DEFAULT_CONTEXT=default
ENV TRANSFER_CONTEXT=default
ENV MEETME_CONTEXT=default
ENV USER_ADMIN_SECRET=qwerty-01
ENV USER_AGENT_SECRET=agent
ENV ADDITIONAL_CONFIG_LINES=""

EXPOSE ${BIND_PORT}

USER monast

ENTRYPOINT ["/pymon/entrypoint.sh"]