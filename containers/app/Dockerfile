FROM ubuntu:18.04

LABEL maintainer="imaharu"

RUN mkdir docker-go-isucon
ENV DGI docker-go-isucon

WORKDIR $DGI

RUN apt-get update -qq && \
		apt-get install -y curl software-properties-common git && \
		add-apt-repository ppa:longsleep/golang-backports && \
		apt-get install -y golang-go && \
		git clone https://github.com/isucon/isucon7-qualify.git isubata

