FROM ekidd/rust-musl-builder:1.21.0 as builder  
  
ADD . .  
RUN sudo chmod -R 0777 *  
RUN cargo build --release  
  
FROM alpine:latest  
  
COPY \--from=builder \  
/home/rust/src/target/x86_64-unknown-linux-musl/release/falcon \  
/usr/local/bin/  
CMD /usr/local/bin/falcon

