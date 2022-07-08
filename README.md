---  

### Registry

[AssetList](https://github.com/persistenceOne/assetlists)

[Cosmos](https://github.com/cosmos/chain-registry/tree/master/persistence)

[Directory](https://cosmos.directory/persistence)

[All That Node](https://www.allthatnode.com/persistence.dsrv)

### Endpoints

We provide following endpoints to help developers for integration

| Protocol | Endpoints |  
| :------: |:--------- |  
| RPC | `https://rpc.core.persistence.one`   |  
| REST | `https://rest.core.persistence.one`   |  
| GRPC | `grpc://grpc.core.persistence.one`  |  
| WSS | `wss://rpc.core.persistence.one:443/websocket`   |  

we also provide archival endpoints to retrieve historical data    

| Protocol | Endpoints |  
| :------: | :------- |  
| RPC | `https://rpc.persistence.audit.one`   |  
| REST | `https://rest.persistence.audit.one` |  
| WSS | `wss://rpc.persistence.audit.one:443/websocket`  |  


### Seeds Nodes

### State-Sync
to use statesync change the following under `config.toml`
```toml
[statesync]
enable = true
rpc_servers = "https://rpc.core.persistence.one:443,https://rpc.core.persistence.one:443"
trust_height = 0
trust_hash = ""
trust_period = "112h0m0s"
```

and use a trusted height from the rpc,(recent height will do)

```bash
curl -s https://rpc.core.persistence.one/status | jq '.result .sync_info | {trust_height: .latest_block_height, trust_hash: .latest_block_hash} | values'
```

### Snapshot

```  
https://tendermint-snapshots.s3.ap-southeast-1.amazonaws.com/persistence/data.tar.lz4  
```

Steps to use our backups
  * Install `aria2` and `lz4`
  * Download our backup with 
    ```bash  
    aria2c -x 4 -x 4 -c <url>
    ```
  * Extract the contents to persistenced home.   
    ```bash  
    tar -I lz4 -xf data.tar.lz4 -C <persistence home which defaults to ~/.persistenceCore/>
    ```

### Explorer

[Mintscan](https://www.mintscan.io/persistence)

[Persistence Explorer](https://explorer.persistence.one)

[Aneka](https://persistence.aneka.io/)


### Apps

[pStake](https://app.pstake.finance)

[Persistence Wallet](https://wallet.persistence.one/)

[Keplr App](https://wallet.keplr.app/#/core/stake)

[Ping.pub](https://ping.pub/persistence)

[Atomscan](https://atomscan.com/persistence)

[Persistence](https://persistence.thecodes.dev/)

[]()

### IBC

[IBCscan](https://ibcscan.net/)
