FROM golang:alpine AS builder  
MAINTAINER "Cuong Manh Le <cuong.manhle.vn@gmail.com>"  
RUN apk update && \  
apk add git build-base && \  
rm -rf /var/cache/apk/* && \  
mkdir -p "$GOPATH/src/github.com/skippbox/kubewatch"  
  
ADD . "$GOPATH/src/github.com/skippbox/kubewatch"  
  
RUN cd "$GOPATH/src/github.com/skippbox/kubewatch" && \  
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -a --installsuffix cgo
--ldflags="-s" -o /kubewatch  
  
# --- Builder end ---  
FROM alpine:3.4  
RUN apk add --update ca-certificates  
  
COPY \--from=builder /kubewatch /bin/kubewatch  
  
ENTRYPOINT ["/bin/kubewatch"]  
  

