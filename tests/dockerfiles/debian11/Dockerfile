FROM debian:11

RUN apt-get update \
	&& apt-get install -y \
		curl \
		gpg \
		procps \
		python \
		sudo \
		systemd \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN true \
  && groupadd deploy \
  && groupadd ruud \
  && useradd -ms /bin/bash deploy -g deploy \
  && useradd -ms /bin/bash ruud -g ruud \
  && echo 'deploy ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers \
  && echo 'ruud ALL=(ALL) NOPASSWD: ALL' >> /etc/sudoers \
  && mkdir /data \
  && chgrp ruud /data \
  && chmod 0775 /data

CMD ["/lib/systemd/systemd"]
