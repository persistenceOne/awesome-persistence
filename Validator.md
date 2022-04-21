---

## Persistence Mainnet

### Managing Validator

While setting up a rudimentary validating node is easy, running a production-quality validator node with a robust architecture and security features requires an extensive setup.

The Persistence core is powered by the Tendermint consensus. Validators run full nodes, participate in consensus by broadcasting votes, commit new blocks to the blockchain, and participate in governance of the blockchain. Validators can cast votes on behalf of their delegators. A validator’s voting power is weighted according to their total stake. The top 75 validators make up the Active Validator Set and are the only validators that sign blocks and receive revenue.

Validators and their delegators earn the following fees:

Gas: Fees added on to each transaction to avoid spamming and pay for computing power. Validators set minimum gas prices and reject transactions that have implied gas prices below this threshold.

Validators can set commissions on the fees they receive as an additional incentive.

If validators double sign or frequently offline, their staked XPRT (including XPRT of users that delegated to them) can be slashed. Penalties can vary depending on the severity of the violation.  

---

### Joining Mainnet


#### System Requirements

- Four or more CPU cores
- At least 500 GB of disk storage
- At least 8 GB of memory
- At least 100 mbps of network bandwidth

** HDD not recommended **

#### Binaries

Download our binaries from [here](https://github.com/persistenceOne/persistenceCore/releases/tag/v0.2.3) and place it in your bin path

#### Generate keys
```bash
persistenceCore keys add [key_name]
```
or
```bash
persistenceCore keys add [key_name]   --recover  
```  
 to regenerate keys with your BIP39 mnemonic

#### Setting up a Node


Following steps  are  rudimentary way of setting up a validator, For production we advise your [sentry architecture](https://forum.cosmos.network/t/sentry-node-architecture-overview/454) to create well defined process

* [Install](####Binaries) persistence core application
* Initialize node
	```shell
	persistenceCore init {{NODE_NAME}} --chain-id core-1
	```
* Replace the contents of your `${HOME}/.persistenceCore/con, exchangesfig/genesis.json` with that of core-1/final_genesis.json from the `master` branch of [repository](https://github.com/persistenceOne/genesisTransactions).
* Verify checksum `jq -S -c -M "" genesis.json | sha256sum` matches `f90fb025e9b5b55c88730ab5ab762b121daa7808cde27d50f465e1fe3b3e5cad`
* Inside file `${HOME}/.persistenceCore/config/config.toml`, 
  * set `seeds` to `"08ab4552a74dd7e211fc79432918d35818a67189@52.69.58.231:26656,449a0f1b7dafc142cf23a1f6166bbbf035edfb10@13.232.85.66:26656,5b27a6d4cf33909c0e5b217789e7455e261941d1@15.222.29.207:26656"`.
  * If your node has a public ip, set it in `external_address = "tcp://<public-ip>:26656"`, else leave the filed empty.
* Set `minimum-gas-prices` in `${HOME}/.persistenceCore/config/app.toml` with the minimum price you want (example `0.005uxprt`) for the security of the network.
* [OPTOINAL] if you want to speed things up, you can use our [backup]( https://tendermint-snapshots.s3.ap-southeast-1.amazonaws.com/persistence/data.tar.lz4).
  * Install `aria2` and `lz4`
  * Download our backup with 
    ```bash  
    aria2c -x 4 -x 4 -c  
    ```
  * Extract the contents to persistenced home.   
    ```bash  
    tar -I lz4 -xf data.tar.lz4 -C (persistence home which defaults to ~/.persistenceCore/)
    ```
* Start node
	```bash
	persistenceCore start
	```
* Acquire $XPRT tokens to self delegate to your validator node. Minimum 1 XPRT is require to become a validator. You must send your XPRT to the address created in the Generate Keys step previosuly.
* Wait for the blockchain to sync. You can check the sync status using the command
	```bash
	curl http://localhost:26657/status sync_info "catching_up": false
	```
* Once `"catching_up"` is `false`, the sync is complete.

#### Architecture 

We recommend following ways to secure the validator setup

* Sentry Architecture to prevent slow startups and handle ddos on p2p
* Remote Signer to safeguard validator hotkey and 


#### Register the validator

Run the following command to register the validator  
```bash
persistenceCore tx staking create-validator \
--from {{KEY_NAME}} \
--amount XXXXXXXXuxprt \
--pubkey "$(persistenceCore tendermint show-validator)" \
--chain-id core-1 \
--moniker="{{VALIDATOR_NAME}}" \
--commission-max-change-rate=0.01 \
--commission-max-rate=1.0 \
--commission-rate=0.07 \
--min-self-delegation="1" \
```

---

### Maintain Delegation

Consider the following options to help improve your visibility and make yourself known to potential delegators.

#### Set up a website

Set up a website so that your delegators can find you. It is recommended that you make a custom section for XPRT delegators that instructs them how to delegate tokens.

#### Announce yourself on Discord

Join the [Persistence Validators Discord](https://discord.gg/qT4BtFnd) channel, and introduce yourself.

#### Setup a Metadata profile
To Improve  communication with community and core team, please add the following metadata to your validator. These  helps us  send security and chain upgrade announcement in a clear manner

```bash
persistenceCore tx staking edit-validator \
    --identity="keybase identity"
    --security-contact="XXXXXXXX" \
    --website="XXXXXXXX"
```
