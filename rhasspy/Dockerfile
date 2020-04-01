FROM synesthesiam/rhasspy-server:latest
LABEL maintainer="Michael Hansen <hansen.mike@gmail.com>"

ENV LANG C.UTF-8

# Copy script to run
COPY docker/run.sh /run.sh
RUN chmod a+x /run.sh
RUN apt-get install -y libasound2-plugins

ENV CONFIG_PATH /data/options.json

ENTRYPOINT ["/run.sh"]
