1. Get aptos-cli (https://github.com/aptos-labs/aptos-core/releases/tag/aptos-cli-0.2.0)
2. Clone this repository https://github.com/Krishnacore/aptos-localtestnet
3. Generate key pair for root/faucet account :
```bash
aptos key generate --output-file root
```
4. Generate key pair for validator
```bash
aptos genesis generate-keys --output-dir .
```
    
This will create two files: `private-keys.yaml`, `validator-identity.yaml`
    
5. Configure validator information:
```bash
aptos genesis set-validator-configuration \
--keys-dir . --local-repository-dir . \
--username localtestnet \
--validator-host 127.0.0.1:6180
```
6. This will create a validator config file, like `localtestnet.yaml`
7. Open `layout.yaml` file, edit `root_key` (copy it from your `root.pub` file). You can also change other network/genesis parameters here.
8. Compile genesis blob and waypoint:
```bash
aptos genesis generate-genesis --local-repository-dir . --output-dir .
```
9. Copy `.env.example` file to `.env` . Set the value of the `FAUCET_PRIVATE_KEY` variable from the `root` file
10. Start your local testnet:
```bash
docker-compose up -d
```

REST: 127.0.0.1:8080

FAUCET 127.0.0.1:8000