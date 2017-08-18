FROM debian:8.1
MAINTAINER @abdul <abdul.qabiz@gmail.com>

RUN apt-get update && apt-get -y dist-upgrade
RUN apt-get install -y golang git curl

ENV GOPATH /usr/go
RUN mkdir $GOPATH
ENV PATH $GOPATH/bin:$PATH

# RUN go get github.com/yudai/gotty
RUN mkdir /gotty 
WORKDIR /gotty
RUN curl -L https://github.com/yudai/gotty/releases/download/v1.0.1/gotty_linux_amd64.tar.gz | tar xz

# Install whatever program you want to run through gotty:
# RUN apt-get install -y bsdgames
# ENV PATH /usr/games/:$PATH

ENTRYPOINT ["/gotty/gotty"]
