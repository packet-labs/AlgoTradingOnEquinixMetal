# Algorithmic Trading

Imagine a machine learning model that can process a data stream, be it the live video stream of a product launch, financial earnings reports, a political speech, or general consumer sentiment gauged by processing a real-time Twitter feed, used to determine the execution of stock and equities trades. Such algorithmics (or algos) require a deep pool of computing resources to quickly process and execute upon identified trends. Equinix Metal provides the bare metal infrastrucure needed for such performance as well as the network interconnection capabilities to connect to upstream financial service providers.

This repo showcases uses Equinix Metal to deploy one such algo which communicates to the Alpaca stock trading API. Alpaca provides both a REST (pull) and streaming (push) API accessible via the programming language of your choice. For this repo, a sample algo written in Go is used. The deployed algo uses a "high/low" to continously monitor a basket of stocks identifying those to go long (purchase) and those to go short (sell). The algorithm runs continously with no human intervention and closes out all positions before the end of the trading day.

# Algo on Equinix Metal


Algorithmic Trading  technical advances in financial techology (fintech), notably the general and free availability of financial trading APIs previously only available to the largest of companies, Algorithmic Trading is 

Algorithmic trading is the programmatic processing of data to determine the execution of stock and equities trades. Such
```
sudo add-apt-repository ppa:ubuntu-lxc/lxd-stable
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install golang git
```

```
mkdir long-short
cd log-short
wget https://raw.githubusercontent.com/alpacahq/alpaca-trade-api-go/master/examples/long-short/long-short.go
```

```
export APCA_API_KEY_ID=
export APCA_API_SECRET_KEY=
```


```
go run long-short.go
```
