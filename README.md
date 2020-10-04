
# bitcoin-electrumx-docker

Running Bitcoin Core and Electrumx together in a docker-compose setup.

It builds upon existing docker images for [bitcoin_core](https://github.com/ruimarinho/docker-bitcoin-core) and [electrumx](https://github.com/lukechilds/docker-electrumx/).

## System requirements

It's basically the same system requirements as for running bitcoin core and electrumx separately. 
Most crucially, at the time of writing, it will occupy around 420 GB of disk space. 
I recommend you have at least 500 GB free.

You will need to install:

* Docker (version 18.06.0 or newer)
* Docker-Compose (version 1.22.0 or newer, see https://docs.docker.com/compose/install/)

## Use Cases

### Starting from scratch, I want to run an electrumx server

Great! Simply cloning this repository and (from its main directory) running 
```
docker-compose up -d
```
should be enough. If you want, you can customize the donation address in `docker-compose.yml` and the `volumes/elx_data/banner.txt` file first.

To stop, run `docker-compose down`.
All data is persisted to your hard drive. 
So you can just start again like above, and it will be up and running again almost instantly.  

### I also want to use `bitcoin-cli` with the running containers

Use
```
docker exec --user bitcoin bitcoin-core bitcoin-cli [command]
```

If you use it frequently, you might want to set an alias for `docker exec --user bitcoin bitcoin-core bitcoin-cli`.

### I want to use some different configuration

Feel free to adapt `bitcoin-core/bitcoin.conf` and `docker-compose.yml` as needed. Use 
```
docker-compose up --build -d
```
to make sure the containers got your changes.

### I want to run in testnet/regtest mode

* add `testnet=1` (resp. `regtest=1`) to `bitcoin-core/bitcoin.conf`
* adjust the port in the `DAEMON_URL` to `18332` for testnet or `18443` for regtest

### I want to use an existing SSL certificate

Copy or link your certificate files into the `volumes/ssl_certs` folder, and adjust the environment variables in `docker-compose.yml` to match your files.

## License

MIT © Ragtor