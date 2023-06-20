## Upgrade-to-v1.3.0
```
wget https://github.com/CosmWasm/wasmvm/releases/download/v1.2.3/libwasmvm.x86_64.so
sudo mv libwasmvm.x86_64.so /usr/lib/

rm -r ~/.paloma/data/wasm/cache
```

```
sudo systemctl stop palomad
sudo systemctl stop pigeond
```

### upgrade paloma
```
cd || return
rm -rf paloma
git clone https://github.com/palomachain/paloma.git
cd paloma || return
git checkout v1.3.0
make install
sudo mv -f $HOME/go/bin/palomad /usr/local/bin/palomad
palomad version # v1.3.0
```
### upgrade pigeon
```
git clone https://github.com/palomachain/pigeon.git
cd pigeon
git checkout v1.2.0
make build
sudo mv ./build/pigeon /usr/local/bin/pigeon
```
```
pigeon version
```
App version: 1.2.0
Build commit hash: bc1621644ff2220b315c263901b950bc5b243d95

```
sudo systemctl daemon-reload
sudo systemctl enable palomad
sudo systemctl enable pigeond
sudo systemctl start pigeond
sudo systemctl start palomad
```
### Check logs
```
sudo journalctl -u palomad -f --no-hostname -o cat
```
```
sudo journalctl -u pigeond -f --no-hostname -o cat
```
### Check synchronization
```
palomad status 2>&1 | jq .SyncInfo.catching_up
```
