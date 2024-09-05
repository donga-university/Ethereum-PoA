# Ethereum PoA private network

Build your own Ethereum Proof of Authority private network (devnet)


## ⚠️ This repo is outdated

**Recommended to install Go-ethereum version `1.13`**

*Since geth v1.14 Clique has been deprecated. By now Geth is not able to seal Ethash or Clique blocks. It only works in PoS mode and in concert with a consensus client.*


## How to run

### Run node 1

*Open a new terminal and follow the steps below.*

**Step 1:** Change the current working directory to `node1`

```bash
cd node1
```

**Step 2:** Initialize genesis block 

```bash
geth --datadir ./ init ../genesis.json
```

**Step 3:** Run Ethereum protocol

```bash
geth --datadir ./ --networkid 3355 --unlock 0x8a710e458b2782ae3105a77b6cdb6a491901f64f --mine --miner.etherbase=0x8a710e458b2782ae3105a77b6cdb6a491901f64f --password ./password.txt --allow-insecure-unlock --nodiscover --syncmode full --ipcdisable --ws --ws.port 8510 --ws.api eth,net,web3,personal,admin,miner --ws.origins "*" --http --http.api admin,debug,web3,eth,txpool,personal,miner,net --http.corsdomain "*" --http.port 8511 --http.addr 127.0.0.1 --authrpc.port 8610 --port 30010
```


### Run node 2

*Open a new terminal and follow the steps below.*

**Step 1:** Change the current working directory to `node2`

```bash
cd node2
```

**Step 2:** Initialize genesis block 

```bash
geth --datadir ./ init ../genesis.json
```

**Step 3:** Run Ethereum protocol

```bash
geth --datadir ./ --networkid 3355 --unlock 0x41017ef54bb3be28cb5b869375d6eef883824efe --mine --miner.etherbase=0x41017ef54bb3be28cb5b869375d6eef883824efe --password ./password.txt --allow-insecure-unlock --nodiscover --syncmode full --ipcdisable --ws --ws.port 8520 --ws.api eth,net,web3,personal,admin,miner --ws.origins "*" --http --http.api admin,web3,eth,txpool,personal,miner,net --http.corsdomain "*" --http.port 8521 --http.addr 127.0.0.1 --authrpc.port 8620 --port 30020
```

## Add peers

### Get info of node1

*Open a new terminal and follow the steps below.*

**Step 1:** Attach to `node1` using HTTP

```bash
geth attach http://127.0.0.1:8511
```

**Step 2:** Show `enode` of node1

```bash
admin.nodeInfo.enode
```

Example output of `Step 2`:
```bash
"enode://e6ab2cb96ec264c3b12b95aea457479a2aa845adfac572107a92688a9fee6aa12a64ed500206be4ca0cb1b33ffc6741703755992b3071667c903886b8e74b7a3@127.0.0.1:30010?discport=0"
```

**Step 3:** Copy enode output from `Step 2` to your clipboard.

### Add peer from node2

*Open a new terminal and follow the steps below.*

**Step 1:** Attach to `node2` using HTTP

```bash
geth attach http://127.0.0.1:8521
```

**Step 2:** Add node1 to node 2 peers by paste enode of node1 from your clipboard.

```bash
admin.addPeer("enode://e6ab2cb96ec264c3b12b95aea457479a2aa845adfac572107a92688a9fee6aa12a64ed500206be4ca0cb1b33ffc6741703755992b3071667c903886b8e74b7a3@127.0.0.1:30010?discport=0")
```
