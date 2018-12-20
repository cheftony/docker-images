FROM alpine:3.8 as builder

RUN apk add alpine-sdk openssl-dev git \
      && git clone https://github.com/giltene/wrk2.git \
      && cd /wrk2 \
      && make

FROM alpine:3.8

COPY --from=builder /wrk2/wrk /bin

RUN addgroup -g 1000 wrk \
    && adduser -D -u 1000 wrk -G wrk -s /bin/sh \
    && apk add openssl-dev libgcc

USER wrk

CMD ["/bin/wrk"]
