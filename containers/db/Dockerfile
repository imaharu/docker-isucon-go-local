FROM ubuntu:18.04 AS build-dev

LABEL maintainer="imaharu"

ARG GIT_URL=https://github.com/isucon/isucon7-qualify.git

RUN apt-get update -qq && \
		apt-get install -y software-properties-common && \
		add-apt-repository ppa:longsleep/golang-backports && \
		apt-get install -y golang-go && \
		git clone --depth=1 $GIT_URL /home/isucon/isubata && \
		cd /home/isucon/isubata/bench && \
		go get github.com/constabulary/gb/... && \
		gb vendor restore && \
		make && \
		bin/gen-initial-dataset

FROM mysql:5.7

COPY --from=build-dev /home/isucon/isubata/db /home/db
COPY --from=build-dev /home/isucon/isubata/bench/isucon7q-initial-dataset.sql.gz /home/db/init.sql.gz
