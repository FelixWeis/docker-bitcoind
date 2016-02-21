Automated Bitcoin Core / bitcoind docker builds
===============================================

This repository contains the `Dockerfile` sources used on [docker hub](https://hub.docker.com/) for automated builds of [bitcoin core](https://bitcoincore.org/). Always run the latest version of bitcoin core with a single command.


Quick Guide
-----------

To run the latest release version of bitcoin core with a persistent blockchain storage on the docker host and open p2p-port run the following command.

    $ docker run -i -t --rm --name bitcoind \
        -v $HOME/bitcoin-data:/root/.bitcoin \
        -p 8333:8333 \
        felixweis/bitcoind

After a successful start you are can detach docker's pseudo-TTY with `Ctrl+P` + `Ctrl+Q`.

To follow the daemon's output logs:

    $ docker logs -f bitcoind

To test the bitcoin-cli

    $ docker exec bitcoind bitcoin-cli getinfo

At https://bitnodes.21.co/ you can verify that your node is reachable to the world and supporting the p2p network.


Custom arguments / running testnet
----------------------------------

The `:latest` image uses `bitcoind` as ENTRYPOINT and `-printtoconsole -disablewallet` for CMD. Thus it uses `STDOUT` instead of `debug.log` and the wallet is disabled by default because this may require additional security measures.

Custom command line arguments appended to the docker image will replace the default CMD arguments. E.g. to run a testnet instance with wallet:

    $ docker run -i -t --rm --name bitcoind_testnet \
        -v $HOME/bitcoin-data:/root/.bitcoin \
        -p 18333:18333 \
        felixweis/bitcoind \
        -printtoconsole \
        -testnet \
