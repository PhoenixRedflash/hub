# Build tern
FROM golang:1.24.5-alpine3.22 AS tern
RUN apk --no-cache add git
RUN go install github.com/jackc/tern@latest

# Build final image
FROM alpine:3.22.0
RUN addgroup -S db-migrator -g 1000 && adduser -S db-migrator -u 1000 -G db-migrator
USER 1000
WORKDIR /home/db-migrator
COPY --from=tern /go/bin/tern /usr/local/bin
COPY database/migrations .
