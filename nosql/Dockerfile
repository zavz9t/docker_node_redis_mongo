FROM mongo:3.6

COPY mongo.conf /etc/mongo.conf
COPY init.sh /docker-entrypoint-initdb.d/

ARG USER_ID
ENV USER_ID $USER_ID
ARG GROUP_ID
ENV GROUP_ID $GROUP_ID

RUN [ -z $(getent group $GROUP_ID | cut -d: -f1) ] && groupmod -g $GROUP_ID mongodb || true
RUN usermod -u $USER_ID -g $GROUP_ID mongodb

EXPOSE 27017
CMD ["mongod", "--auth"]
