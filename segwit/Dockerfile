FROM felixweis/buildpack-deps:bitcoind

RUN cd /root \
	&& curl -L https://github.com/sipa/bitcoin/archive/segwit.tar.gz | tar xzv \
	&& cd bitcoin-segwit/ \
	&& ./autogen.sh \
	&& ./configure --with-incompatible-bdb --disable-tests \
	&& make -j 2 \
	&& make install

EXPOSE 28333 28332

VOLUME /root/.bitcoin

ENTRYPOINT ["bitcoind"]

CMD ["-segwit", "-printtoconsole"]
