# AlgoTradingOnEquinixMetal

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
