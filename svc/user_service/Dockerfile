FROM circleci/golang AS builder
ADD ./main.go main.go
ADD ./service service
ADD /home/hui/Desktop/workspace/go/src/delinkcious/go.mod go.mod
# Fetch dependencies
ENV GOPROXY=https://goproxy.cn,direct
RUN go get -d -v ./...

# Build image as a truly static Go binary
RUN CGO_ENABLED=0 GOOS=linux go build -o /user_service -a -tags netgo -ldflags '-s -w' .

FROM scratch
MAINTAINER Gigi Sayfan <the.gigi@gmail.com>
COPY --from=builder /user_service /app/user_service
EXPOSE 7070
ENTRYPOINT ["/app/user_service"]
