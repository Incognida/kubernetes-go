FROM golang:alpine as builder

RUN apk --no-cache add git
WORKDIR /app/api

COPY go.mod .
COPY go.sum .
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux go build  -o api -a -installsuffix cgo main.go


FROM alpine:latest

RUN apk --no-cache add ca-certificates

RUN mkdir /app
WORKDIR /app

COPY --from=builder /app/api/api .
EXPOSE 8080
CMD ["./api"]


