# aztec-docker

## Overview

The Aztec Network is a privacy-focused blockchain platform designed to enable secure and private transactions. This guide provides instructions for setting up and running an Aztec sequencer node, a critical component of the network infrastructure.

## Prerequisites

Before starting, ensure you have the following:

- **Aztec CLI Tool**: Install the Aztec CLI tool and verify the correct version for the testnet using `aztec-up alpha-testnet`.
- **Operating System**: A Linux or macOS machine with terminal access.
- **Community Support**: Join the [Aztec Discord](https://discord.gg/aztec) for assistance and updates.

## Setting Up Your Sequencer

The `aztec start` command simplifies the process of running a sequencer node. It uses default configurations based on the `--network` flag and launches a Docker container with the sequencer software.

### Required Components

1. **RPC Endpoints**:
    - **L1 Execution Client**: Specify via `--l1-rpc-urls` or the `ETHEREUM_HOSTS` environment variable.
    - **L1 Consensus Client**: Specify via `--l1-consensus-host-urls` or the `L1_CONSENSUS_HOST_URLS` environment variable.

2. **Ethereum Keys**:
    - **Private Key**: Set using `--sequencer.validatorPrivateKey`.
    - **Public Address**: Specify using `--sequencer.coinbase`.

3. **Networking**:
    - Forward UDP and TCP traffic on port `40400` to your local IP.
    - Pass your external IP address to `--p2p.p2pIp`.

4. **Sepolia ETH**:
    - Obtain Sepolia ETH for gas costs via a faucet or the Aztec Discord.

### Starting the Sequencer

Run the following command to start your sequencer:

```bash
aztec start --node --archiver --sequencer \
  --network alpha-testnet \
  --l1-rpc-urls https://example.com \
  --l1-consensus-host-urls https://example.com \
  --sequencer.validatorPrivateKey 0xYourPrivateKey \
  --sequencer.coinbase 0xYourAddress \
  --p2p.p2pIp 999.99.999.99 \
  --p2p.maxTxPoolSize 1000000000
```

### Registering as a Validator

Once synced, register as a validator using:

```bash
aztec add-l1-validator \
  --l1-rpc-urls https://eth-sepolia.g.example.com/example/your-key \
  --private-key your-private-key \
  --attester your-validator-address \
  --proposer-eoa your-validator-address \
  --staking-asset-handler 0xF739D03e98e23A7B65940848aBA8921fF3bAc4b2 \
  --l1-chain-id 11155111
```

## Advanced Configuration

### Using Environment Variables

Create a `.env` file with configuration variables:

```env
ETHEREUM_HOSTS=https://example.com
L1_CONSENSUS_HOST_URLS=https://example.com
```

Source the file before running the command:

```bash
source .env
aztec start --network alpha-testnet --archiver --node --sequencer
```

### Using Docker Compose

For Docker Compose setups, use the following configuration:

```yaml
services:
  node:
     image: aztecprotocol/aztec:0.85.0-alpha-testnet.5
     environment:
        ETHEREUM_HOSTS: ""
        L1_CONSENSUS_HOST_URLS: ""
        VALIDATOR_PRIVATE_KEY: $VALIDATOR_PRIVATE_KEY
        P2P_IP: $P2P_IP
     ports:
        - 40400:40400/tcp
        - 40400:40400/udp
```

## Troubleshooting

- **L1 Access**: Use `host.docker.internal` for local RPC endpoints or configure `network_mode: "host"` in Docker Compose.
- **Public IP**: Retrieve your public IP using `curl ifconfig.me`.

For additional support, visit the [Aztec Discord](https://discord.gg/aztec).

Happy sequencing!