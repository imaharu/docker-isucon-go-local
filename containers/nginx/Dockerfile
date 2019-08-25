FROM alpine AS build-dev

LABEL maintainer="imaharu"

ARG GIT_URL=https://github.com/isucon/isucon7-qualify.git

RUN git clone --depth=1 $GIT_URL /isubata

FROM nginx:1.10

COPY --from=build-dev /isubata /home/isucon/isubata
COPY isucon.conf /etc/nginx/conf.d/isucon.conf
