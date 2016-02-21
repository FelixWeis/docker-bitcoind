FROM felixweis/buildpack-deps:bitcoind

RUN cd /root \
	&& curl -L https://github.com/bitcoin/bitcoin/archive/master.tar.gz | tar xzv \
	&& cd bitcoin-master/ \
	&& ./autogen.sh \
	&& ./configure --with-incompatible-bdb --disable-tests \
	&& make -j 2 \
	&& make install

EXPOSE 18333 18332

VOLUME /root/.bitcoin

ENTRYPOINT ["bitcoind"]

CMD ["-testnet", "-printtoconsole"]
