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

### 1️2️⃣ Install Solana CLI & Dependencies (Official Solana Installer)

Run the official installer from the Solana documentation:

```bash
curl --proto '=https' --tlsv1.2 -sSfL https://solana-install.solana.workers.dev | bash
```

Example successful output:

```
Installed Versions:
Rust: rustc 1.86.0 (05f9846f8 2025-03-31)
Solana CLI: solana-cli 2.2.12 (src:0315eb6a; feat:1522022101, client:Agave)
Anchor CLI: anchor-cli 0.31.1
Node.js: v23.11.0
Yarn: 1.22.1
```

Verify installation:

```bash
rustc --version && solana --version && anchor --version && node --version && yarn --version
```

---
