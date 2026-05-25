# Solana Token-2022 Tutorial

---

## 🧩 Step-by-Step Tutorial

---

### 1️⃣ For installation on Ubuntu Linux, follow the steps below:
Update the package lists to ensure all the packages are up-to-date:
```bash
sudo apt-get update
```

Install the following dependencies:
```bash
sudo apt-get install -y \
    build-essential \
    pkg-config \
    libudev-dev llvm libclang-dev \
    protobuf-compiler libssl-dev
```

### 2️⃣ Install Solana CLI & Dependencies (Official Solana Installer)
Enter the following command into your terminal to install all the necessary dependencies:
```bash
curl --proto '=https' --tlsv1.2 -sSfL https://solana-install.solana.workers.dev | bash
```
A successful installation will return output like the following:

Example output:
```
Installed Versions:
Rust: rustc 1.91.1 (ed61e7d7e 2025-11-07)
Solana CLI: solana-cli 3.0.10 (src:96c3a851; feat:3604001754, client:Agave)
Anchor CLI: anchor-cli 0.32.1
Surfpool CLI: surfpool 0.12.0
Node.js: v24.10.0
Yarn: 1.22.1
```
Verify a successful installation by checking the version of each installed dependency.
```bash
rustc --version && solana --version && anchor --version && surfpool --version && node --version && yarn --version
```

### 3️⃣ Solana config
Your Solana config specifies the following variables:
- Config file: The path to your config file
- RPC URL & Websocket URL: The Solana cluster to which the CLI makes requests
- Keypair path: The path to the default Solana wallet (keypair) used to pay transaction fees and deploy programs. By default, this file is stored at ~/.config/solana/id.json.

To see your current configuration settings, enter the follow command in your terminal.
```
solana config get
```
A successful command will return output similar to the following:
Example output
```
Config File: /Users/test/.config/solana/cli/config.yml
RPC URL: https://api.mainnet-beta.solana.com
WebSocket URL: wss://api.mainnet-beta.solana.com/ (computed)
Keypair Path: /Users/test/.config/solana/id.json
Commitment: confirmed
```
You can change the Solana CLI cluster with the following commands:
```
solana config set --url mainnet-beta
solana config set --url devnet
solana config set --url localhost
solana config set --url testnet
```
