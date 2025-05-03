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
    ### Environment Configuration

    Before starting the sequencer, you need to configure your environment variables. Follow these steps:

    1. Copy the example environment file:
        ```bash
        cp example.env .env
        ```

    2. Open the `.env` file in a text editor and fill in the required values:
        ```bash
        # Environment Variables

        # Ethereum RPC URL for the L1 execution client
        ETHEREUM_HOSTS=https://eth-sepolia.g.alchemy.com/v2/

        # Ethereum RPC URL for the L1 consensus client
        L1_CONSENSUS_HOST_URLS=https://ethereum-sepolia.core.chainstack.com/beacon/

        # Ethereum private key for the sequencer
        VALIDATOR_PRIVATE_KEY=

        # Public address associated with your private key
        COINBASE_ADDRESS=0x95

        # Log level for debugging
        LOG_LEVEL=debug

        # Data directory for storing sequencer data
        DATA_DIRECTORY=/data
        ```

    3. Save the `.env` file after making the changes.