FROM golang:alpine as build-env

WORKDIR /src
# Get source and compile
COPY go.* ./
RUN go mod download

COPY ../client/proto proto
COPY main.go .

RUN go build -o /server main.go

# Create small image to copy executable only
FROM alpine:3.12.3

WORKDIR /src
COPY --from=build-env /server .

ENTRYPOINT ["/src/server"]