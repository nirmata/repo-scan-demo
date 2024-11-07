FROM golang:1.23 AS builder

WORKDIR .

COPY go.mod .
RUN go mod download

COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o /main

FROM scratch

COPY --from=builder /main /main

ENTRYPOINT ["/main"]