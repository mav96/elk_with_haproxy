FROM haproxy

RUN set -x	&& \
	apt-get update					&&  \
	apt-get install -y rsyslog  dnsutils iputils-ping &&  \
	mkdir -p /etc/rsyslog.d/				&&  \
	touch /var/log/haproxy.log				&&  \
	ln -sf /dev/stdout /var/log/haproxy.log

# Include our custom entrypoint that will the the job of lifting
# rsyslog alongside haproxy.
ADD entrypoint.sh /usr/local/bin/entrypoint
ADD rsyslog.d /etc/rsyslog.d
RUN chmod +x /usr/local/bin/entrypoint

# Set our custom entrypoint as the image's default entrypoint
ENTRYPOINT [ "entrypoint" ]

ADD haproxy.cfg /etc/haproxy/haproxy.cfg
CMD [ "-f", "/etc/haproxy/haproxy.cfg" ]

