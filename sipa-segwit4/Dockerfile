FROM felixweis/buildpack-deps:bitcoind

ENV BITCOIN_REPOSITORY sipa
ENV BITCOIN_BRANCH segwit4

RUN cd /root \
	&& curl -L https://github.com/$BITCOIN_REPOSITORY/bitcoin/archive/$BITCOIN_BRANCH.tar.gz | tar xzv \
	&& cd bitcoin-$BITCOIN_BRANCH/ \
	&& ./autogen.sh \
	&& ./configure --with-incompatible-bdb --disable-tests \
	&& make \
	&& make install \
	&& cd .. \
	&& rm -Rfv bitcoin-$BITCOIN_BRANCH/

EXPOSE 28901 28901

VOLUME /root/.bitcoin

ENTRYPOINT ["bitcoind"]

CMD ["-segnet", "-printtoconsole"]
