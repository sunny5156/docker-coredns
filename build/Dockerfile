# go build
FROM golang:1.18.6-alpine as builder

WORKDIR /go/src
ENV GO111MODULE=on

RUN apk add --no-cache alpine-sdk 

COPY ./ /go/src/coredns-api/

RUN cd coredns-api \
    && go get -u github.com/swaggo/swag/cmd/swag \
    && sh scripts/code_build.sh

# image build
FROM alpine:3.12

COPY --from=builder /go/src/coredns-api /coredns-api

CMD ["/coredns-api/build/coredns-api"]
