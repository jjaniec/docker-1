FROM debian

ENV DEBIAN_FRONTEND noninteractive

EXPOSE 3000

RUN apt-get update -y && apt-get upgrade -y
RUN apt-get install git -y && apt-get install wget gcc mysql-server -y

RUN service mysql start && mysql -uroot -e "create database gogs"

RUN adduser --disabled-login --gecos 'Gogs' git && su - git
USER git

RUN mkdir -p /home/git/local
WORKDIR /home/git

RUN wget https://storage.googleapis.com/golang/go1.9.1.linux-amd64.tar.gz && tar -C /home/git/local -xvzf go1.9.1.linux-amd64.tar.gz && rm -rf go1.9.1.linux-amd64.tar.gz

ENV GOROOT=/home/git/local/go
ENV GOPATH=/home/git/go
ENV PATH=$PATH:$GOROOT/bin:$GOPATH/bin

RUN go get -u github.com/gogits/gogs
RUN go get -u -tags "sqlite" github.com/gogits/gogs

WORKDIR $GOPATH/src/github.com/gogits/gogs
ENV USER=git

RUN go build
RUN go build -tags "sqlite"

USER root

CMD service mysql start && ./gogs web

#docker build -t name path/to/dockerfile

#docker run -it --rm -p 3000:3000 name
