FROM golang:1.21 as builder

WORKDIR /catgpt

ENV CGO_ENABLED=0

COPY go.mod go.sum ./
RUN go mod download && go mod verify

COPY . .
RUN go build -v -o main

FROM gcr.io/distroless/static-debian12:latest-amd64
EXPOSE 8080
EXPOSE 9090

COPY --from=builder catgpt/main compiled/main
CMD ["compiled/main"]

#Run: docker build -t catgpt .;
#docker run -d --publish 8080:8080 --publish 9090:9090 catgpt