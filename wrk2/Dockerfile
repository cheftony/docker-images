FROM alpine:3.8 as builder
RUN apk add alpine-sdk openssl-dev git \
      && git clone https://github.com/giltene/wrk2.git \
      && cd /wrk2 \
      && make

FROM alpine:3.8
COPY --from=builder /wrk2/wrk /bin
RUN apk add openssl-dev libgcc
CMD ["/bin/wrk"]
