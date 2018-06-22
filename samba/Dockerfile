FROM alpine:3.7

ARG USER=clear10

RUN apk --update add \
    samba \
    samba-common-tools \
    && rm -rf /var/cache/apk/*

RUN mkdir /media/storage \
    && chmod 0777 /media/storage

RUN yes $(echo $USER | rev) | adduser ${USER} \
    && yes $(echo $USER | rev) | smbpasswd -a ${USER}

COPY smb.conf /etc/samba/smb.conf

EXPOSE 445/tcp

CMD ["sh", "-c", "smbd --foreground --log-stdout </dev/null"]
