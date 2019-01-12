FROM node:10.6

RUN apt-get update && apt-get install -y \
        git \
        netcat \
        mc \
    && rm -rf /var/lib/apt/lists/*

RUN mkdir -p /home/node \
    && mkdir -p /home/node/.ssh \
    && echo "\tHost *\n\tStrictHostKeyChecking no\n" >> /home/node/.ssh/config \
    && echo "\tIdentityFile /home/node/.ssh/id_rsa\n" >> /etc/ssh/ssh_config

ARG USER_ID
ENV USER_ID $USER_ID
ARG GROUP_ID
ENV GROUP_ID $GROUP_ID

RUN [ -z $(getent group $GROUP_ID | cut -d: -f1) ] && groupmod -g $GROUP_ID node || true
RUN usermod -u $USER_ID -g $GROUP_ID node

WORKDIR /var/www

COPY docker-entrypoint.sh /
RUN chmod +x /docker-entrypoint.sh

CMD ["/docker-entrypoint.sh"]
