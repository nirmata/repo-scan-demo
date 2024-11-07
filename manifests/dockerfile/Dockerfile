FROM golang:1.23 AS builder

WORKDIR .

COPY go.mod .
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /main

FROM scratch

ENV NPM_CONFIG_STRICT_SSL=true
ENV PYTHONHTTPSVERIFY 1
ENV NODE_TLS_REJECT_UNAUTHORIZED=1

COPY --from=builder /main /main

LABEL MAINTAINER="Nirmata"

ENTRYPOINT ["/main"]