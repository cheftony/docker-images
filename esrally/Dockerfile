FROM alpine:3.8

ENV ESRALLY_VERSION=1.0.2

RUN addgroup -g 1000 esrally \
    && adduser -D -u 1000 esrally -G esrally -s /bin/sh \
    && apk --no-cache add python3 git build-base linux-headers python3-dev openjdk8 \
    && pip3 install --upgrade esrally==${ESRALLY_VERSION} \
    && rm -rf /root/.cache

COPY rally.ini /root/.rally/

USER esrally

CMD ["esrally"]
