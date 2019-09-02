FROM alpine AS build-dev

LABEL maintainer="imaharu"

ARG GIT_URL

RUN apk update && \
  apk upgrade && \
  apk add --no-cache \
  git && \
  git clone --depth=1 "$GIT_URL" isubata

FROM nginx:1.10

COPY --from=build-dev /isubata /home/isucon/isubata
COPY isucon.conf /etc/nginx/conf.d/isucon.conf
