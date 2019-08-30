FROM ubuntu:18.04 as build-dev

LABEL maintainer="imaharu"
ARG GIT_URL

RUN mkdir -p /home/isucon/isubata
WORKDIR /home/isucon/isubata

RUN apt-get update -qq && \
	apt-get install -y software-properties-common git && \
	add-apt-repository ppa:longsleep/golang-backports && \
	apt-get install -y golang-go && \
	git clone --depth=1 "$GIT_URL" /home/isucon/isubata

## ベンチマーカーの準備 ##
ENV HOME /root
ENV PATH $HOME/local/go/bin:/root/go/bin:$PATH
RUN go get github.com/constabulary/gb/...
## cd bench ##
WORKDIR /home/isucon/isubata/bench
RUN gb vendor restore && \
	make && \
	./bin/gen-initial-dataset

FROM mysql:5.7

ENV MYSQL_ALLOW_EMPTY_PASSWORD=yes MYSQL_DATABASE=isubata MYSQL_USER=isucon MYSQL_PASSWORD=isucon

COPY --from=build-dev /home/isucon/isubata/db /home/db
COPY --from=build-dev /home/isucon/isubata/bench/isucon7q-initial-dataset.sql.gz /home/db/init.sql.gz

## データベース初期化 ##
WORKDIR /home
COPY setToInsertData.txt setToInsertData.txt
