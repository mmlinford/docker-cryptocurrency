FROM debian:stretch-20181112-slim

# install dependencies
RUN apt-get update
RUN apt-get install --assume-yes git make curl lbzip2 gcc g++ autoconf libtool pkg-config bsdmainutils

# fetch source
RUN git clone -b 'v0.16.3' https://github.com/litecoin-project/litecoin.git

# build remaining dependencies
WORKDIR /litecoin/depends
ENV NO_QT 1
RUN make

# build dogecoind
WORKDIR /litecoin
RUN ./autogen.sh
RUN ./configure --disable-tests --disable-bench --without-gui --prefix=/litecoin/depends/x86_64-pc-linux-gnu
RUN make

# container configuration
# mainnet p2p, mainnet json-rpc, testnet p2p, testnet json-rpc
EXPOSE 9333 9332 19335 19332
ENTRYPOINT ["/litecoin/src/litecoind"]
