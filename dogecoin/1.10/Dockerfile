FROM debian:stretch-20181112-slim

# install dependencies
RUN apt-get update
RUN apt-get install --assume-yes git make wget lbzip2 gcc g++ autoconf libtool pkg-config bsdmainutils

# fetch source
RUN git clone -b 'v1.10.0' https://github.com/dogecoin/dogecoin.git

# build remaining dependencies
WORKDIR /dogecoin/depends
ENV NO_QT 1
RUN make

# build dogecoind
WORKDIR /dogecoin
RUN ./autogen.sh
RUN ./configure --without-gui --prefix=/dogecoin/depends/x86_64-unknown-linux-gnu
RUN make

# container configuration
# mainnet p2p, mainnet json-rpc, testnet p2p, testnet json-rpc
EXPOSE 22556 22555 44556 44555
ENTRYPOINT ["/dogecoin/src/dogecoind"]
