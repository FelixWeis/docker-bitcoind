FROM felixweis/buildpack-deps:bitcoind

RUN cd /root \
	&& curl -L https://github.com/bitcoin/bitcoin/archive/segwit.tar.gz | tar xzv \
	&& cd bitcoin-segwit/ \
	&& ./autogen.sh \
	&& ./configure --with-incompatible-bdb --disable-tests \
	&& make -j 2 \
	&& make install

EXPOSE 18333 18332

VOLUME /root/.bitcoin

ENTRYPOINT ["bitcoind"]

CMD ["-testnet", "-printtoconsole"]
