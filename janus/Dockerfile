FROM golang:1.14-alpine

RUN apk add --no-cache make gcc musl-dev git

WORKDIR $GOPATH/src/github.com/qtumproject/janus
COPY ./ $GOPATH/src/github.com/qtumproject/janus

RUN go build \
        -ldflags \
            "-X 'github.com/qtumproject/janus/pkg/params.GitSha=`git rev-parse HEAD`'" \
        -o $GOPATH/bin $GOPATH/src/github.com/qtumproject/janus/... && \
    rm -fr $GOPATH/src/github.com/qtumproject/janus/.git

ENV QTUM_RPC=http://qtum:testpasswd@localhost:3889
ENV QTUM_NETWORK=auto

EXPOSE 23889

ENTRYPOINT [ "janus" ]