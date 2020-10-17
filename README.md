# Algorithmic Trading on Equinix Metal

Imagine a machine learning model that can process a data stream, be it the live video stream of a product launch, financial earnings reports, a political speech, or general consumer sentiment gauged by processing a real-time Twitter feed, used to determine the execution of stock and equities trades. Such algorithmics (or algos) require a deep pool of computing resources to quickly process and execute upon identified trends. Equinix Metal provides the bare metal infrastrucure needed for such performance as well as the network interconnection capabilities to connect to upstream financial service providers.

This repo showcases uses Equinix Metal to deploy one such algo which communicates to the Alpaca stock trading API. Alpaca provides both a REST (pull) and streaming (push) API accessible via the programming language of your choice. For this repo, a sample algo written in Go is used. The deployed algo uses a "long/short" to continously monitor a basket of stocks identifying those to go long (purchase) and those to go short (sell). The algorithm runs continously with no human intervention and closes out all positions before the end of the trading day.

# Prerequisites

An account with Equinix Metal and with Alpaca are required to run this algo. Equinix Metal infrastructure is available on a per hour charge and the Alpaca services are free.

No financial outlay with Alpaca is required to run this demonstration as it uses a "paper trading" account. Paper trading uses live market data and while trades that are submitted are recorded and profits/loss are tracked, the gains (or losses) are purely fictional.

## Equinix Metal Account

Equinix Metal provides bare metal infrastructure (storage, processing, and networking). An Equinix Metal account can be self-provisioned at https://console.equinix.com/signup.

## Alpaca Account

Alpaca provides a trading API and access to the U.S. financial markets. An Alpaca account can be self-provisioned at https://app.alpaca.markets/signup.

# Deploying an Algo

Deploying an Algo requires underling compute infrastructure, Alpaca credentials, and the algorithm itself (source code or binary). The long-short algo is written in Go which will be run on an Ubuntu server deployed from Equinix Metal.

## Deploy Equinix Metal

Equinix Metal provides both an API and GUI to deploy infrastructure. This algo requires a single compute instance so the GUI will be used. Via the Equinix Metal console (https://console.equinix.com/), create a new project, and deploy an "on-demand", IAD 2, c3.medium.x86, Ubuntu 20.04 instance. Once it has started, via the Overview tab, copy the SSH root password and take note of the "Public IPv4" address.


## Server Software Dependencies

The algo has some software dependencies that must be satisfied through software updates. 

Start an SSH session, using a client such as Windows PuTTY, and connect to the instance as "root" using the root password saved from the Equinix Metal console.

Run the following commands to satisfy the software depenencies for the algo.

```
sudo add-apt-repository ppa:ubuntu-lxc/lxd-stable
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install golang git
```

## Setup Alpaca Credentials

Alpaca credentials (API Key & Secret) are required for the algo to talk to the Alpaca APIs.  An API key and corresponing key can be generated via the Alpaca console https://app.alpaca.markets/paper/dashboard/overview. The "paper" endpoint will be used for testing (not live) of the algo.

The API key and corresponding secret can be entered as environment variables using the commands below. The algo will read these environment variables when started and use them to authenticate to Alpaca

```
export APCA_API_KEY_ID="YOUR_KEY_ID_HERE"
export APCA_API_SECRET_KEY="CORRESPONDING_SECRET_HERE"
```

## Deploy Algo

With all the dependencies in place, the algo can be started up with the following command. The algo will connect to Alpaca, authenticate, and start streaming down trading inforation identifying trades to execute. If the U.S. stock market is closed, the algo will dutifully wait until it opens and then start trading. Approximately 15 minutes before the U.S markets close (3:45pm ET), the algo will start closing out positions to end the day with no positions open (long or short).

```
go run long-short.go
```

## Tear Down

The deployed metal should be torn down (released) when no longer needed as the resources are billed by the hour. Simply navigate back to the Equinix Console and "Delete" the deployed instance. It can be recreated at a later time to re-run the algo. 

## What's next?

This is a basic algo run across a single metal instance without any external data analysis. From here, an algorithm can processes other data sources, such as audio, video, press releases, Twitter, weather, etc to build its trading model. This will undoubtably require additional compute power requiring more larger and more complex infrastructure that can be provided via Equinix Metal.
