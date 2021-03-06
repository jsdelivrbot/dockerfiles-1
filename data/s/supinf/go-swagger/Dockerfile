# go-swagger  
#  
# docker run --rm -v $(pwd):/go/src supinf/go-swagger validate ./swagger.yml  
# docker run --rm -v $GOPATH/src:/go/src -w /go/src/github.com/your-
account/project supinf/go-swagger generate server -A sample -f ./swagger.yml  
# docker run --rm -v $GOPATH/src:/go/src -w /go/src/github.com/your-
account/project supinf/go-swagger generate client -A sample -f ./swagger.yml  
  
FROM alpine:3.7  
  
ENV SWAGGER_VERSION=0.14.0 \  
GOPATH=/go  
  
RUN apk --no-cache add \--virtual build-dependencies bash gcc musl-dev openssl
go git \  
  
# Install go 1.10  
&& GOLANG_VERSION=1.10.2 \  
&& GOLANG_SRC_URL=https://golang.org/dl/go$GOLANG_VERSION.src.tar.gz \  
&&
GOLANG_SRC_SHA256=6264609c6b9cd8ed8e02ca84605d727ce1898d74efa79841660b2e3e985a98bd
\  
&& export GOROOT_BOOTSTRAP="$(go env GOROOT)" \  
&& wget -q "$GOLANG_SRC_URL" -O golang.tar.gz \  
&& echo "$GOLANG_SRC_SHA256 golang.tar.gz" | sha256sum -c \- \  
&& tar -C /usr/local -xzf golang.tar.gz \  
&& cd /usr/local/go/src \  
&& ./make.bash \  
&& mkdir -p /go/src \  
&& chmod -R 777 /go \  
  
# Install go-swagger  
&& go get -u github.com/go-swagger/go-swagger/cmd/swagger \  
&& cd /go/src/github.com/go-swagger/go-swagger \  
&& git checkout ${SWAGGER_VERSION} \  
&& go get -u github.com/mitchellh/gox \  
&& /go/bin/gox --osarch "linux/amd64" -ldflags "-s -w" -output /swagger \  
github.com/go-swagger/go-swagger/cmd/swagger \  
&& mv /swagger /usr/bin/ \  
  
# Clean up  
&& apk del --purge -r build-dependencies \  
&& rm -rf /usr/local/go /usr/lib/go /go /var/cache/* /var/lib/apk*
/golang.tar.gz  
  
WORKDIR /go/src  
  
ENTRYPOINT ["swagger"]  
CMD ["-h"]  

