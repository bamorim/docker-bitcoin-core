# ruimarinho/bitcoin-core
A bitcoin-core docker image.

[![ruimarinho/bitcoin-core][docker-pulls-image]][docker-hub-url] [![ruimarinho/bitcoin-core][docker-stars-image]][docker-hub-url] [![ruimarinho/bitcoin-core][docker-size-image]][docker-hub-url] [![ruimarinho/bitcoin-core][docker-layers-image]][docker-hub-url]

## Supported tags and respective `Dockerfile` links

- `0.15.0.1-alpine`, `0.15-alpine` ([0.15/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.15/Dockerfile))
- `0.14.2-alpine`, `0.14-alpine` ([0.14/alpine/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.14/alpine/Dockerfile))
- `0.13.2-alpine`, `0.13-alpine` ([0.13/alpine/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.13/alpine/Dockerfile))
- `0.12.1-alpine`, `0.12-alpine` ([0.12/alpine/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.12/alpine/Dockerfile))
- `0.11.2-alpine`, `0.11-alpine` ([0.11/alpine/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.11/alpine/Dockerfile))

- `0.15.0.1`, `0.15`, `latest` ([0.15/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.15/Dockerfile))
- `0.14.2`, `0.14` ([0.14/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.14/Dockerfile))
- `0.13.2`, `0.13` ([0.13/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.13/Dockerfile))
- `0.12.1`, `0.12` ([0.12/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.12/Dockerfile))
- `0.11.2`, `0.11` ([0.11/Dockerfile](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/0.11/Dockerfile))

## What is Bitcoin Core?
_from [bitcoinwiki](https://en.bitcoin.it/wiki/Bitcoind)_

Bitcoin Core is a reference client that implements the Bitcoin protocol for remote procedure call (RPC) use. It is also the second Bitcoin client in the network's history.

## Usage
### How to use this image
This image contains the main binaries from the Bitcoin Core project - `bitcoind`, `bitcoin-cli` and `bitcoin-tx`. It behaves like a binary, so you can pass any arguments to the image and they will be forwarded to the `bitcoind` binary:

```sh
$ docker run --rm -it ruimarinho/bitcoin-core \
  -printtoconsole \
  -regtest=1 \
  -rpcallowip=172.17.0.0/16 \
  -rpcpassword=bar \
  -rpcuser=foo
```

By default, `bitcoind` will run as user `bitcoin` for security reasons and with its default data dir (`~/.bitcoin`). If you'd like to customize where `bitcoin-core` stores its data, you must use the `BITCOIN_DATA` environment variable. The directory will be automatically created with the correct permissions for the `bitcoin` user and `bitcoin-core` automatically configured to use it.

```sh
$ docker run --env BITCOIN_DATA=/var/lib/bitcoin-core --rm -it ruimarinho/bitcoin-core \
  -printtoconsole \
  -regtest=1
```

You can also mount a directory it in a volume under `/home/bitcoin/.bitcoin` in case you want to access it on the host:

```sh
$ docker run -v ${PWD}/data:/home/bitcoin/.bitcoin -it --rm ruimarinho/bitcoin-core \
  -printtoconsole \
  -regtest=1
```

You can optionally create a service using `docker-compose`:

```yml
bitcoin-core:
  image: ruimarinho/bitcoin-core
  command:
    -printtoconsole
    -regtest=1
```

## Image variants
The `ruimarinho/bitcoin-core` image comes in multiple flavors:

### `ruimarinho/bitcoin-core:latest`
Points to the latest release available of Bitcoin Core. Occasionally pre-release versions will be included.

### `ruimarinho/bitcoin-core:<version>`
Based on a slim Debian image, targets a specific version branch or release of Bitcoin Core.

### `ruimarinho/bitcoin-core:<version>-alpine`
Based on Alpine Linux with Berkeley DB 4.8 (cross-compatible build), targets a specific version branch or release of Bitcoin Core.

## Supported Docker versions
This image is officially supported on Docker version 1.12, with support for older versions provided on a best-effort basis.

## License
[License information](https://github.com/bitcoin/bitcoin/blob/master/COPYING) for the software contained in this image.

[License information](https://github.com/ruimarinho/docker-bitcoin-core/blob/master/LICENSE) for the [ruimarinho/docker-bitcoin-core](https://hub.docker.com/r/ruimarinho/bitcoin-core) docker project.

[docker-hub-url]: https://hub.docker.com/r/ruimarinho/bitcoin-core
[docker-layers-image]: https://img.shields.io/imagelayers/layers/ruimarinho/bitcoin-core/latest.svg?style=flat-square
[docker-pulls-image]: https://img.shields.io/docker/pulls/ruimarinho/bitcoin-core.svg?style=flat-square
[docker-size-image]: https://img.shields.io/imagelayers/image-size/ruimarinho/bitcoin-core/latest.svg?style=flat-square
[docker-stars-image]: https://img.shields.io/docker/stars/ruimarinho/bitcoin-core.svg?style=flat-square
