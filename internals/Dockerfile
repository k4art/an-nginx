# syntax=docker/dockerfile:1

FROM ubuntu:22.04 AS builder

COPY deps_delivery build-nginx .

ARG NGINX_VERSION=1.25.1

RUN : \
  && apt-get update && apt-get install -y build-essential wget perl \
  && rm -f /usr/bin/pod2man \
  && ./build-nginx $NGINX_VERSION \
  && wget -O /nginx-tests.tar.gz https://github.com/nginx/nginx-tests/archive/refs/heads/master.tar.gz \
  && tar xf /nginx-tests.tar.gz && mv /nginx-tests-master /nginx-tests

FROM ubuntu:22.04
COPY --from=builder /usr/local/nginx /usr/local/nginx
COPY --from=builder /nginx-tests /nginx-tests

RUN apt-get update -y && apt install -y perl

EXPOSE 80

ENV TEST_NGINX_BINARY=/usr/local/nginx/sbin/nginx

WORKDIR /nginx-tests
RUN : \
  && adduser tester --disabled-password --no-create-home --gecos "" \
  && chown tester . -R && su -c "prove ." tester \
  && deluser tester

CMD ["/usr/local/nginx/sbin/nginx", "-g", "daemon off;"]
