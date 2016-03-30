FROM felixweis/buildpack-deps:bitcoind

ENV BITCOIN_REPOSITORY bitcoin
ENV BITCOIN_BRANCH master

RUN cd /root \
	&& curl -L https://github.com/$BITCOIN_REPOSITORY/bitcoin/archive/$BITCOIN_BRANCH.tar.gz | tar xzv \
	&& cd bitcoin-$BITCOIN_BRANCH/ \
	&& ./autogen.sh \
	&& ./configure --with-incompatible-bdb --disable-tests \
	&& make \
	&& make install \
	&& cd .. \
	&& rm -Rfv bitcoin-$BITCOIN_BRANCH/

EXPOSE 18333 18332

VOLUME /root/.bitcoin

ENTRYPOINT ["bitcoind"]

CMD ["-testnet", "-printtoconsole"]
