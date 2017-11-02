FROM buildpack-deps:stretch-curl
MAINTAINER Felix Weis <mail@felixweis.com>

ENV BITCOIN_VERSION 0.15.0.1
ENV BITCOIN_DOWNLOAD_PATH https://bitcoin.org/bin/bitcoin-core-0.15.0.1
ENV BITCOIN_DOWNLOAD_FILENAME bitcoin-${BITCOIN_VERSION}-x86_64-linux-gnu.tar.gz
ENV BITCOIN_RELEASES_KEY 01EA5486DE18A882D4C2684590C8019E36C2E964

RUN wget $BITCOIN_DOWNLOAD_PATH/$BITCOIN_DOWNLOAD_FILENAME \
	&& wget $BITCOIN_DOWNLOAD_PATH/SHA256SUMS.asc \
	&& wget https://bitcoin.org/laanwj-releases.asc \
	&& gpg --import laanwj-releases.asc \
	&& gpg --fingerprint $BITCOIN_RELEASES_KEY \
	&& gpg --verify SHA256SUMS.asc \
	&& grep -o "$(sha256sum $BITCOIN_DOWNLOAD_FILENAME)" SHA256SUMS.asc \
	&& tar -xzvf $BITCOIN_DOWNLOAD_FILENAME \
	&& cd bitcoin-*/bin \
	&& mv bitcoin-cli bitcoin-tx bitcoind /usr/local/bin \
	&& cd / \
	&& rm -Rfv bitcoin-* *.asc

EXPOSE 8333 8332

VOLUME /root/.bitcoin

ENTRYPOINT ["bitcoind"]

CMD ["-printtoconsole", "-disablewallet"]
