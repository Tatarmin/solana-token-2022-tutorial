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
```bash

Verify a successful installation by checking the version of each installed dependency.
```bash
rustc --version && solana --version && anchor --version && surfpool --version && node --version && yarn --version
```
