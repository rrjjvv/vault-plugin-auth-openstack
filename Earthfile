VERSION 0.6

FROM golang:1.13-alpine

ENV CGO_ENABLED=0
ENV GOOS=linux
ENV GOARCH=amd64

plugin:
    BUILD +test
    FROM +dep
    RUN go build .
    SAVE ARTIFACT vault-plugin-auth-openstack

test:
    FROM +dep
    RUN go vet ./... && \
        go test ./...

dep:
    WORKDIR /src
    COPY go.mod go.sum ./
    RUN go mod download && go mod verify
    COPY . .
