FROM ubuntu:18.04

LABEL maintainer="imaharu"
ARG GIT_URL

RUN mkdir -p /home/isucon/isubata
WORKDIR /home/isucon/isubata

RUN apt-get update -qq && \
  apt-get install -y curl software-properties-common git sudo vim && \
  add-apt-repository ppa:longsleep/golang-backports && \
  apt-get install -y golang-go && \
  git clone --depth=1 "$GIT_URL" /home/isucon/isubata

## ベンチマーカーの準備 ##
ENV HOME /root
ENV PATH $HOME/local/go/bin:/root/go/bin:$PATH

RUN go get github.com/constabulary/gb/...
# cd bench ##
WORKDIR /home/isucon/isubata/bench
RUN gb vendor restore && \
  make && \
  ./bin/gen-initial-dataset
