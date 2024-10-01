#bitcoin #bitcoin-book 

This chapter will talk about the compilation process, installation and use of the bitcoin core.

## Preparations

- First clone the repository.
- Select the release.
- Configuring the core build.

Generate a set of building scripts with `autogen.sh`.

The `autogen.sh` script creates a set of automatic configuration scripts that will interrogate your system to discover the correct settings and ensure you have all the necessary libraries to compile the code. The most important of these is the configure script that offers a number of different options to customize the build process. Use the `./configure --help` to see the various options.

The configure script allows you to enable or disable certain features of bitcoind through the use of flags.

The command `./configure <flags here>` creates a customized build script.

- Build the Bitcoin Core Executable

Use the command `make` to compile the source code.

- Check the compilation

Use the command `make check` to verify that the linked libraries are not broken in obvious ways.

- Install the Executable

Use the command `make install`.
The default installation of bitcoind puts it in `/usr/local/bin`.
You can check the path where it was installed using the command `which bitcoind`.

## Running a Bitcoin Core Node

- By running a node you don't have to rely on a third party to validate a transaction.
- By running a full node you contribute to the Bitcoin network an help make it more robust.
- Running a node by **default** requires downloading and processing over 500 GB of data initially (all the history of bitcoin blockchain) and about 400 MB of bitcoin transactions per day.
- Bitcoin Core will not be able to process transactions or update account balances until the full blockchain dataset is downloaded.

#### Why run a node?

- You do not want to rely on any third party to validate the transactions you receive.
- You do not want to disclose to third parties which transactions belong to your wallet.
- You are developing Bitcoin software and need to rely on a Bitcoin node for programmable (API) access to the network and blockchain.
- You are building applications that must validate transactions according to Bitcoin’s consensus rules. Typically, Bitcoin software companies run several nodes.
- You want to support Bitcoin. Running a node that you use to validate the transactions you receive to your wallet makes the network more robust.


## Configuring the Bitcoin Core Node

- Bitcoin Core will look for a configuration file in its data directory on every start.
- To locate the configuration file, run bitcoind -printtoconsole in your terminal and look for the first couple of lines.
- Usually the configuration file is inside `.bitcoin` data directory under your home directory.
- To se a list of configuration options run `bitcoind --help`

###  Some of the most important options

#### alertnotify

Run a specified command or script to send emergency alerts to the owner of this node.

#### conf

An alternative location for the configuration file. This only makes sense as a command-line parameter to bitcoind, as it can’t be inside the configuration file it refers to.

#### datadir

Select the directory and filesystem in which to put all the blockchain data. By default this is the _.bitcoin_ subdirectory of your home directory. Depending on your configuration, this can use from about 10 GB to almost 1 TB as of this writing, with the maximum size expected to increase by several hundred gigabytes per year.

#### prune

Reduce the blockchain disk space requirements to this many megabytes by deleting old blocks. Use this on a resource-constrained node that can’t fit the full blockchain. Other parts of the system will use other disk space that can’t currently be pruned, so you will still need at least the minimum amount of space mentioned in the datadir option.

#### txindex

Maintain an index of all transactions. This allows you to programmatically retrieve any transaction by its ID provided that the block containing that transaction hasn’t been pruned.

#### dbcache

The size of the UTXO cache. The default is 450 mebibytes (MiB). Increase this size on high-end hardware to read and write from your disk less often, or reduce the size on low-end hardware to save memory at the expense of using your disk more frequently.

#### blocksonly

Minimize your bandwidth usage by only accepting blocks of confirmed transactions from your peers instead of relaying unconfirmed transactions.

#### maxmempool

Limit the transaction memory pool to this many megabytes. Use it to reduce memory use on memory-constrained nodes.


###

- By default Bitcoin Core builds a data base containing **only** the transactions related to the **user's wallet**.
- If you want to be able to access _any_ transaction with commands like `getrawtransaction`you need to configura Bitcoin Core to build a complete transaction index.

#### Sample of a full-index node configuration file
```
alertnotify=myemailscript.sh "Alert: %s"
datadir=/lotsofspace/bitcoin
txindex=1
```

#### Sample configuration of a resource-constrained system
```
alertnotify=myemailscript.sh "Alert: %s"
blocksonly=1
prune=5000
dbcache=150
maxmempool=150
```

###

- To run Bitcoin Core in the background as a process, start it with the daemon option, as `bitcoind -daemon`
- To monitor the progress and runtime status:
	- Start in daemon mode
	- Use the command `bitcoin-cli getblockchaininfo`

```json
{
  "chain": "main",
  "blocks": 0,
  "headers": 83999,
  "bestblockhash": "[...]19d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f",
  "difficulty": 1,
  "time": 1673379796,
  "mediantime": 1231006505,
  "verificationprogress": 3.783041623201835e-09,
  "initialblockdownload": true,
  "chainwork": "[...]000000000000000000000000000000000000000000000100010001",
  "size_on_disk": 89087,
  "pruned": false,
  "warnings": ""
}	
```

- This shows a node with a blockchain height of 0 blocks and 83,999 headers. The node first fetches the block headers from its peers in order to find the blockchain with the most proof of work and afterward continues to download the full blocks, validating them as it goes.

## Bitcoin Core API

- Bitcoin Core implements a JSON-RCP interface.
- RCP: Remote Procedure Call.
- Can be accessed using the command-line `bitcoin-cli`
- Use the command `bitcoin-cli help` to see a list of Bitcoin Core RCP commands.
- To get help with an specific command use `bitcoin-cli help <command>`

### Get Information on Bitcoin Core's Status

- Bitcoin Core provides status reports on different modules through the JSON-RPC interface.

Example:
```
bitcoin-cli getnetworkinfo
```

```json
{
  "version": 240001,
  "subversion": "/Satoshi:24.0.1/",
  "protocolversion": 70016,
  "localservices": "0000000000000409",
  "localservicesnames": [
    "NETWORK",
    "WITNESS",
    "NETWORK_LIMITED"
  ],
  "localrelay": true,
  "timeoffset": -1,
  "networkactive": true,
  "connections": 10,
  "connections_in": 0,
  "connections_out": 10,
  "networks": [
    "...detailed information about all networks..."
  ],
  "relayfee": 0.00001000,
  "incrementalfee": 0.00001000,
  "localaddresses": [
  ],
  "warnings": ""
}
```

### Exploring and Decoding Transactions

Get a transaction passing the transaction ID (txid):

```
bitcoin-cli getrawtransaction <txid>
```

The command `getrawtransaction` returns a serialized transaction in hexadecimal notation.

```
01000000000101eb3ae38f27191aa5f3850dc9cad00492b88b72404f9da13569
8679268041c54a0100000000ffffffff02204e0000000000002251203b41daba
4c9ace578369740f15e5ec880c28279ee7f51b07dca69c7061e07068f8240100
000000001600147752c165ea7be772b2c0acb7f4d6047ae6f4768e0141cf5efe
2d8ef13ed0af21d4f4cb82422d6252d70324f6f4576b727b7d918e521c00b51b
e739df2f899c49dc267c0ad280aca6dab0d2fa2b42a45182fc83e81713010000
0000
```

Decoding transaction hexadecimal notation:

```
bitcoin-cli decoderawtransaction 01000000000101eb3ae38f27191aa5f3850dc9cad00492b88b72404f9da13569
8679268041c54a0100000000ffffffff02204e0000000000002251203b41daba
4c9ace578369740f15e5ec880c28279ee7f51b07dca69c7061e07068f8240100
000000001600147752c165ea7be772b2c0acb7f4d6047ae6f4768e0141cf5efe
2d8ef13ed0af21d4f4cb82422d6252d70324f6f4576b727b7d918e521c00b51b
e739df2f899c49dc267c0ad280aca6dab0d2fa2b42a45182fc83e81713010000
0000
```

Transaction decoded:

```json
{
  "txid": "466200308696215bbc949d5141a49a4138ecdfdfaa2a8029c1f9bcecd1f96177",
  "hash": "f7cdbc7cf8b910d35cc69962e791138624e4eae7901010a6da4c02e7d238cdac",
  "version": 1,
  "size": 194,
  "vsize": 143,
  "weight": 569,
  "locktime": 0,
  "vin": [
    {
      "txid": "4ac541802679866935a19d4f40728bb89204d0cac90d85f3a51a19...aeb",
      "vout": 1,
      "scriptSig": {
        "asm": "",
        "hex": ""
      },
      "txinwitness": [
        "cf5efe2d8ef13ed0af21d4f4cb82422d6252d70324f6f4576b727b7d918e5...301"
      ],
      "sequence": 4294967295
    }
  ],
  "vout": [
    {
      "value": 0.00020000,
      "n": 0,
      "scriptPubKey": {
        "asm": "1 3b41daba4c9ace578369740f15e5ec880c28279ee7f51b07dca...068",
        "desc": "rawtr(3b41daba4c9ace578369740f15e5ec880c28279ee7f51b...6ev",
        "hex": "51203b41daba4c9ace578369740f15e5ec880c28279ee7f51b07d...068",
        "address": "bc1p8dqa4wjvnt890qmfws83te0v3qxzsfu7ul63kp7u56w8q...5qn",
        "type": "witness_v1_taproot"
      }
    },
    {
      "value": 0.00075000,
      "n": 1,
      "scriptPubKey": {
        "asm": "0 7752c165ea7be772b2c0acb7f4d6047ae6f4768e",
        "desc": "addr(bc1qwafvze0200nh9vkq4jmlf4sy0tn0ga5w0zpkpg)#qq404gts",
        "hex": "00147752c165ea7be772b2c0acb7f4d6047ae6f4768e",
        "address": "bc1qwafvze0200nh9vkq4jmlf4sy0tn0ga5w0zpkpg",
        "type": "witness_v0_keyhash"
      }
    }
  ]
}
```

### Exploring Blocks

Exploring blocks is similar to exploring transactions.

- Blocks can be referenced either by the block **height** or **hash**.

Get block by height:
```
bitcoin-cli getblockhash <block height>
```

The result is the block **header**:
```
0000000000002917ed80650c6174aac8dfc46f5fe36480aaef682ff6cd83c3ca
```

Getting a block info:
```
bitcoin-cli getblock <block header>
```

Block info:
```json
{
  "hash": "0000000000002917ed80650c6174aac8dfc46f5fe36480aaef682ff6cd83c3ca",
  "confirmations": 651742,
  "height": 123456,
  "version": 1,
  "versionHex": "00000001",
  "merkleroot": "0e60651a9934e8f0decd1c[...]48fca0cd1c84a21ddfde95033762d86c",
  "time": 1305200806,
  "mediantime": 1305197900,
  "nonce": 2436437219,
  "bits": "1a6a93b3",
  "difficulty": 157416.4018436489,
  "chainwork": "[...]00000000000000000000000000000000000000541788211ac227bc",
  "nTx": 13,
  "previousblockhash": "[...]60bc96a44724fd72daf9b92cf8ad00510b5224c6253ac40095",
  "nextblockhash": "[...]00129f5f02be247070bf7334d3753e4ddee502780c2acaecec6d66",
  "strippedsize": 4179,
  "size": 4179,
  "weight": 16716,
  "tx": [
    "5b75086dafeede555fc8f9a810d8b10df57c46f9f176ccc3dd8d2fa20edd685b",
    "e3d0425ab346dd5b76f44c222a4bb5d16640a4247050ef82462ab17e229c83b4",
    "137d247eca8b99dee58e1e9232014183a5c5a9e338001a0109df32794cdcc92e",
    "5fd167f7b8c417e59106ef5acfe181b09d71b8353a61a55a2f01aa266af5412d",
    "60925f1948b71f429d514ead7ae7391e0edf965bf5a60331398dae24c6964774",
    "d4d5fc1529487527e9873256934dfb1e4cdcb39f4c0509577ca19bfad6c5d28f",
    "7b29d65e5018c56a33652085dbb13f2df39a1a9942bfe1f7e78e97919a6bdea2",
    "0b89e120efd0a4674c127a76ff5f7590ca304e6a064fbc51adffbd7ce3a3deef",
    "603f2044da9656084174cfb5812feaf510f862d3addcf70cacce3dc55dab446e",
    "9a4ed892b43a4df916a7a1213b78e83cd83f5695f635d535c94b2b65ffb144d3",
    "dda726e3dad9504dce5098dfab5064ecd4a7650bfe854bb2606da3152b60e427",
    "e46ea8b4d68719b65ead930f07f1f3804cb3701014f8e6d76c4bdbc390893b94",
    "864a102aeedf53dd9b2baab4eeb898c5083fde6141113e0606b664c41fe15e1f"
  ]
}
```

The **confirmations** tells us the **depth** of this block. Indicating the difficulty of changing any of the transaction in this block.

### Alternative Clients, Libraries, and Toolkits


#### C/C++

[Bitcoin Core](https://oreil.ly/BdOwl)

The reference implementation of Bitcoin

#### JavaScript

[bcoin](https://bcoin.io/)

A modular and scalable full-node implementation with API

[Bitcore](https://bitcore.io/)

Full node, API, and library by Bitpay

[BitcoinJS](https://oreil.ly/4iqf2)

A pure JavaScript Bitcoin library for node.js and browsers

#### Java

[bitcoinj](https://bitcoinj.github.io/)

A Java full-node client library

#### Python

[python-bitcoinlib](https://oreil.ly/xn_rg)

A Python bitcoin library, consensus library, and node by Peter Todd

[pycoin](https://oreil.ly/wcpXP)

A Python bitcoin library by Richard Kiss

#### Go

[btcd](https://oreil.ly/h5MEI)

A Go language, full-node Bitcoin client

#### Rust

[rust-bitcoin](https://oreil.ly/me6gf)

Rust bitcoin library for serialization, parsing, and API calls

#### Scala

[bitcoin-s](https://bitcoin-s.org/)

A Bitcoin implementation in Scala

#### C#

[NBitcoin](https://oreil.ly/Qfjgq)

Comprehensive bitcoin library for the .NET framework