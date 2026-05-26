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
Install Rust
```
apt install rustc
```
**Reboot the system to update the PATH environment variable.**

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
### 4️⃣ Wallet setup
To generate a keypair at the keypair path, run the following command:
```
solana-keygen new --word-count 24
```
This command will not override an existing account at the default location, unless you use the --force flag.
**The generated this seed phrase is not saved by default!**

Recovering a Solana wallet using a seed phrase
```
solana-keygen recover
```
Set devnet.json as the default wallet:
```
solana config set --keypair ~/.config/solana/devnet.json
```

Check default wallet:
```
solana address
```
Check specific wallet file:
```
solana-keygen pubkey ~/.config/solana/devnet.json
```
Request an airdrop of Devnet SOL for testing:
```
solana airdrop 2
```
To check your wallet's SOL balance, run the following command:
```
solana balance
```
### 5️⃣ Create a New Token-2022
Token-2022 Program Account Address:
```
TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
```
To create a new token (mint account), run:
```
spl-token create-token --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb --enable-metadata --decimals 8
```
Default decimals: 9

It is possible to see all extensions on a mint or token account:
```
spl-token display <ACCOUNT_ADDRESS>
```
See raw data:
```
solana account <ACCOUNT_ADDRESS>
```
This command fetches the low-level blockchain data for any address, displaying its SOL balance, data length, and the owner Program ID (such as the Token-2022 program)

**Create Token Account**

A separate token account is required for each token (mint) in a wallet.

Create a token account:
```
spl-token create-account <TOKEN_ADDRESS> --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
```
To create a token account with a different owner:
```
spl-token create-account <TOKEN_ADDRESS> --owner <OWNER_ADDRESS> --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
```

**Mint Tokens**

To create new units of a token, mint tokens using the following command:
```
spl-token mint <TOKEN_ADDRESS> <TOKEN_AMOUNT> --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
```
To mint tokens to a different token account:
```
spl-token mint <TOKEN_ADDRESS> <TOKEN_AMOUNT> -- <RECIPIENT_TOKEN_ACCOUNT_ADDRESS> --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
```

Check token supply:
```
spl-token supply <TOKEN_ADDRESS>
```
Check account balance:
```
spl-token supply <TOKEN_ADDRESS>
```
**Transfer Tokens**

To send tokens from your wallet to another token account:
```
spl-token transfer <TOKEN_ADDRESS> <TOKEN_AMOUNT> <RECIPIENT_ADDRESS>
```
**Revoke Mint Authority (Disable Minting)**

To permanently disable minting and lock the total supply, use the following command:
```
spl-token authorize <TOKEN_ADDRESS> mint --disable --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
```

### 6️⃣  Create Token Metadata
The Token Extensions Program lets you store metadata directly on the Mint Account. 
The metadata extension is only available for mint accounts created with Token-2022. 
To create a token with the metadata extension, you must include the `--enable-metadata` flag.

To initialize the metadata:
```
spl-token initialize-metadata <TOKEN_ADDRESS> <YOUR_TOKEN_NAME> <YOUR_TOKEN_SYMBOL> <YOUR_TOKEN_URI>
```
**Updating metadata**

If the token mint was created using Token-2022 with the Metadata Extension (which includes the --enable-metadata flag) and already initialized via the spl-token initialize-metadata command, use the spl-token update-metadata command to modify its fields:
```
spl-token update-metadata <TOKEN_ADDRESS> <FIELD_NAME> <VALUE_STRING>
```
**Examples**
```
spl-token update-metadata <TOKEN_ADDRESS> name "MyToken"
```
```
spl-token update-metadata <TOKEN_ADDRESS> symbol "MTKN"
```
```
spl-token update-metadata <TOKEN_ADDRESS> uri "https://gateway.pinata.cloud/ipfs/<NEW_FOLDER_CID>/metadata.json"
```

**Revoke Metadata Update Authority**

Metadata update authority lets you change your Solana SPL Token name, symbol, logo, description, and links. Revoking it makes that data permanent: no one can alter it again. That gives holders and listing sites confidence that the token identity won't change.
```
spl-token authorize <TOKEN_ADDRESS> metadata --disable --program-id TokenzQdBNbLqP5VEhdkAS6EPFLC1PHnBqCXEpPxuEb
```
