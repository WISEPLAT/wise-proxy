# wise-proxy

Wiseplat mining proxy with web-interface.

**Proxy feature list:**

* Rigs availability monitoring
* Keep track of accepts, rejects, blocks stats
* Easy detection of sick rigs
* Daemon failover list

![Demo](https://raw.githubusercontent.com/wiseplat/wise-proxy/master/proxy.png)

### Building on Linux

Dependencies:

  * go >= 1.4
  * gwsh

Export GOPATH:

    export GOPATH=$HOME/go

Install required packages:

    go get github.com/wiseplat/wshash
    go get github.com/wiseplat/go-wiseplat/common
    go get github.com/goji/httpauth
    go get github.com/gorilla/mux
    go get github.com/yvasiyarov/gorelic

Compile:

    go build -o wise-proxy main.go

### Building on Windows

Follow [this wiki paragraph](https://github.com/wiseplat/go-wiseplat/wiki/Installation-instructions-for-Windows#building-from-source) in order to prepare your environment.
Install required packages (look at Linux install guide above). Then compile:

    go build -o wise-proxy.exe main.go

### Building on Mac OS X

If you didn't install [Brew](http://brew.sh/), do it. Then install Golang:

    brew install go

And follow Linux installation instructions because they are the same for OS X.

### Configuration

Configuration is self-describing, just copy *config.example.json* to *config.json* and specify endpoint URL and upstream URLs.

#### Example upstream section

```javascript
"upstream": [
  {
    "pool": true,
    "name": "EuroHash.net",
    "url": "http://wsh-eu.eurohash.net:8888/miner/0xc285f9dc21232fe887830234631adb9544e40d31/proxy",
    "timeout": "10s"
  },
  {
    "name": "backup-gwsh",
    "url": "http://127.0.0.1:8747",
    "timeout": "10s"
  }
],
```

In this example we specified [EuroHash.net](https://eurohash.net) mining pool as main mining target and a local gwsh node as backup for solo.

With <code>"submitHashrate": true|false</code> proxy will forward <code>wsh_submitHashrate</code> requests to upstream.

#### Running

    ./wise-proxy config.json

#### Mining

    wshminer -F http://x.x.x.x:8748/miner/5/gpu-rig -G
    wshminer -F http://x.x.x.x:8748/miner/0.1/cpu-rig -C

### Pools that work with this proxy

* [EuroHash.net](https://eurohash.net) EU Wiseplat mining pool
* [SuprNova.cc](https://wsh.suprnova.cc) SuprNova WSH Pool

Pool owners, apply for listing here. PM me for implementation details.

### TODO

**Currently it's solo-only solution.**

* Report block numbers
* Report luck per rig
* Maybe add more stats
* Maybe add charts

### Donations

* **WSH**: [0xc285f9dc21232fe887830234631adb9544e40d31](https://wisechain.org/account/0xc285f9dc21232fe887830234631adb9544e40d31)

* **BTC**: [1PqSFPTfKBat5w6oXvEzMcjMVgnUDUjJpk](https://blockchain.info/address/1PqSFPTfKBat5w6oXvEzMcjMVgnUDUjJpk)

Thanks to a couple of dudes who donated some Wise to me, I believe, you can do the same.

### License

The MIT License (MIT).
