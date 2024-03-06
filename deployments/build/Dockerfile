# FROM golang:1.18-alpine3.17 as build
FROM golang:1.22-alpine3.19 as build

ENV GO111MODULE=on

WORKDIR /go/src/pinger

COPY ./go.mod .

COPY ./go.sum .

COPY ./cmd/pinger .

RUN go mod vendor

RUN CGO_ENABLED=0 GOOS=linux go build -mod vendor -a -installsuffix cgo -o pinger .

# FROM alpine:3.17
FROM alpine:3.19

COPY --from=build /go/src/pinger/pinger /app/

#COPY ./bin/pinger /app/pinger

ENTRYPOINT  ["/app/pinger"]
