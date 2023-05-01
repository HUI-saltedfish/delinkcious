FROM circleci/golang AS builder
ADD ./main.go main.go
ADD ./service service
COPY /home/hui/Desktop/workspace/go/src/delinkcious/go.mod go.mod
COPY /home/hui/Desktop/workspace/go/src/delinkcious/go.sum go.sum
# Fetch dependencies
ENV GOPROXY=https://goproxy.cn,direct
RUN go get -d -v

# Build image as a truly static Go binary
RUN CGO_ENABLED=0 GOOS=linux go build -o /link_service -a -tags netgo -ldflags '-s -w' .

FROM scratch
MAINTAINER Gigi Sayfan <the.gigi@gmail.com>
COPY --from=builder /link_service /app/link_service
EXPOSE 7070
ENTRYPOINT ["/app/link_service"]
