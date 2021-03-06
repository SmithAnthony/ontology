
<h1 align="center">Ontology </h1>
<h4 align="center">Version 1.0 </h4>

[![GoDoc](https://godoc.org/github.com/ontio/ontology?status.svg)](https://godoc.org/github.com/ontio/ontology)
[![Go Report Card](https://goreportcard.com/badge/github.com/ontio/ontology)](https://goreportcard.com/report/github.com/ontio/ontology)
[![Travis](https://travis-ci.org/ontio/ontology.svg?branch=master)](https://travis-ci.org/ontio/ontology)
[![Discord](https://img.shields.io/discord/102860784329052160.svg)](https://discord.gg/gDkuCAq)

English | [中文](README_CN.md)

Welcome to Ontology's source code repository!

Ontology is dedicated to creating a modularized, freely configurable, interoperable cross-chain, high-performance, and horizontally scalable blockchain infrastructure system. Ontology makes deploying and invoking decentralized applications easier.

The code is currently alpha quality, but it is in the process of rapid development. The master code may be unstable; stable versions can be downloaded in the release page.

The public test network is described below. We sincerely welcome and hope more developers join Ontology.

## Features

- Scalable lightweight universal smart contract
- Scalable WASM contract support
- Crosschain interactive protocol (processing)
- Multiple encryption algorithm support
- Highly optimized transaction processing speed
- P2P link layer encryption (optional module)
- Multiple consensus algorithm support (VBFT/DBFT/RBFT/SBFT/PoW)
- Quick block generation time


## Contents

- [Build development environment](#build-development-environment)
- [Get Ontology](#get-ontology)
    - [Get from release](#get-from-release)
    - [Get from source code](#get-from-source-code)
- [Run ontology](#run-ontology)
    - [Mainnet sync node](#mainnet-sync-node)
    - [Public test network Polaris sync node](#public-test-network-polaris-sync-node)
    - [Testmode](#testmode)
    - [Run in docker](#run-in-docker)
- [Some example](#some-example)
    - [ONT transfer sample](#ont-transfer-sample)
    - [Query transfer status sample](#query-transfer-status-sample)
    - [Query account balance sample](#query-account-balance-sample)
- [Contributions](#contributions)
- [Open source community](#open-source-community)
    - [Site](#site)
    - [Developer Discord Group](#developer-discord-group)
- [License](#license)

## Build development environment
The requirements to build Ontology are:

- Golang version 1.9 or later
- Glide (a third party package management tool)
- Properly configured Go language environment
- Golang supported operating system

## Get Ontology
### Get from release
- You can download latest ontology binary file with ` curl https://dev.ont.io/ontology_install | sh `.

- You can download other version at [release page](https://github.com/ontio/ontology/releases).

### Get from source code

Clone the Ontology repository into the appropriate $GOPATH/src/github.com/ontio directory.

```
$ git clone https://github.com/ontio/ontology.git
```
or
```
$ go get github.com/ontio/ontology
```
Fetch the dependent third party packages with glide.

```
$ cd $GOPATH/src/github.com/ontio/ontology
$ glide install
```

Build the source code with make.

```
$ make all
```

After building the source code sucessfully, you should see two executable programs:

- `ontology`: the node program/command line program for node control
- `tools/sigsvr`: (optional)Ontology Signature Server - sigsvr is a rpc server for signing transactions for some special requirement.detail docs can be reference at [link](./docs/specifications/sigsvr.md)

## Run ontology

### Mainnet sync node

Run ontology straightly

   ```
	./ontology
   ```
Then you can connect to ontology mainnet.

### Public test network Polaris sync node

Run ontology straightly

   ```
	./ontology --networkid 2
   ```
   
Then you can connect to ontology public test network.


### Testmode

Create a directory on the host and store the following files in the directory:
- Node program + Node control program  `ontology`
- Wallet file`wallet.dat` (`wallet.dat` can be generated by `./ontology account add`)

Run command `$ ./ontology --testmode` can start single-host test net.

Here's a example of single-host configuration:

- Directory structure

    ```shell
    $ tree
    └── ontology
        ├── ontology
        └── wallet.dat
    ```

### Run in docker

Please ensure there are docker environment in your machine.

1. make docker image

    - In the root directory of source code，run`make docker`, it will make ontology image in docker.

2. run ontology image

    - Use command `docker run ontio/ontology`to run ontology；

    - If you need to allow interactive keyboard input while the image is running, you can use the `docker run -ti ontio/ontology` command to start the image;

    - If you need to keep the data generated by image at runtime, you can refer to the data persistence function of docker (e.g. valume);

    - If you need to add ontology parameters, you can add them directly after `docker run ontio/ontology` such as `docker run ontio/ontology --networkid 2`.
     The parameters of ontology command line refer to [here](./docs/specifications/cli_user_guide.md).

## Some example

### ONT transfer sample
 -- from: transfer from； -- to: transfer to； -- amount: ont amount；
```shell
  ./ontology asset transfer  --to=AXkDGfr9thEqWmCKpTtQYaazJRwQzH48eC --amount=10
```
If transfer asset successd, the result will show as follow:

```
Transfer ONT
From:TA6edvwgNy3c1nBHgmFj8KrgQ1JCJNhM3o
To:TA4Xe9j8VbU4m3T1zEa1uRiMTauiAT88op
Amount:10
TxHash:10dede8b57ce0b272b4d51ab282aaf0988a4005e980d25bd49685005cc76ba7f
```
TxHash is the transfer transaction hash, we can query transfer result by txhash.
Because of generate block time, the transfer transaction will not execute befer at least generate one block.

### Query transfer status sample

--hash:transfer transaction hash
```shell
./ontology asset status --hash=10dede8b57ce0b272b4d51ab282aaf0988a4005e980d25bd49685005cc76ba7f
```
result：
```shell
Transaction:transfer success
From:AXkDGfr9thEqWmCKpTtQYaazJRwQzH48eC
To:AYiToLDT2yZuNs3PZieXcdTpyC5VWQmfaN
Amount:10
```

### Query account balance sample

--address: account address

```shell
./ontology asset balance --address=AYiToLDT2yZuNs3PZieXcdTpyC5VWQmfaN
```
result：
```shell
BalanceOf:AYiToLDT2yZuNs3PZieXcdTpyC5VWQmfaN
ONT:10
ONG:0
ONGApprove:0
```

Further examples you can reference at [documentation](https://ontio.github.io/documentation/)

## Contributions

Please open a pull request with a signed commit. We appreciate your help! You can also send your code as emails to the developer mailing list. You're welcome to join the Ontology mailing list or developer forum.

Please provide detailed submission information when you want to contribute code for this project. The format is as follows:

Header line: explain the commit in one line (use the imperative).

Body of commit message is a few lines of text, explaining things  in more detail, possibly giving some background about the issue  being fixed, etc.

The body of the commit message can be several paragraphs. Please do proper word-wrap and keep columns shorter than 74 characters or so. That way "git log" will show things  nicely even when it is indented.

Make sure you explain your solution and why you are doing what you are  doing, as opposed to describing what you are doing. Reviewers and your  future self can read the patch, but might not understand why a  particular solution was implemented.

Reported-by: whoever-reported-it &
Signed-off-by: Your Name [youremail@yourhost.com](mailto:youremail@yourhost.com)

## Open source community
### Site

- <https://ont.io/>

### Developer Discord Group

- <https://discord.gg/4TQujHj/>

## License

The Ontology library is licensed under the GNU Lesser General Public License v3.0, read the LICENSE file in the root directory of the project for details.
