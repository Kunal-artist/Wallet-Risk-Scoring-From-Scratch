# 🧠 Wallet Risk Scoring from On-Chain Behavior

This project implements a custom **Wallet Risk Scoring model** that evaluates Ethereum wallets based on their historical interactions with the **Compound V2/V3 protocols**. The scoring system outputs a numerical risk score ranging from **0 (highest risk)** to **1000 (lowest risk)**, based on a wallet's financial behavior, protocol interactions, and technical reliability.

---

## 📌 Problem Statement

Given a list of Ethereum wallets, assess the **creditworthiness and risk profile** of each wallet solely from its **on-chain transaction history**. Specifically:

- Collect all relevant transactions with the Compound protocol
- Engineer meaningful features indicating financial and behavioral risk
- Output a score (0–1000) for each wallet that reflects its overall risk level

---

## 📊 Data Collection

Transaction data was collected using the **Etherscan API** and enriched with:

- **Normal transactions** (user-initiated)
- **Internal transactions** (contract-to-contract)
- **Protocol-specific contract filtering** (Compound cTokens, governance, markets)

This ensured a **comprehensive behavioral profile** for each wallet.

---

## 🔧 Feature Engineering

The model derives advanced features from raw transaction logs to quantify wallet risk:

| Feature Name                  | Description                                                            |
|------------------------------|------------------------------------------------------------------------|
| `borrow_to_supply_ratio`     | Proxy for leverage; higher means higher risk                           |
| `health_factor_proxy`        | Repayment behavior; higher implies lower liquidation risk              |
| `successful_tx_rate`         | Wallet's technical success rate                                        |
| `wallet_age_days`            | Time since first transaction                                           |
| `is_active_recently`         | Indicates current activity and engagement                              |
| `unique_contracts_interacted`| Measures user's DeFi ecosystem exposure                                |

All features were **normalized (Min-Max Scaling)** to prevent value bias and ensure uniform weighting.

---

## 🧮 Scoring Methodology

A **weighted linear model** was used to compute final risk scores:

- **Positive weights** for healthy behavior (e.g., successful transactions, repaying loans)
- **Negative weights** for risk-enhancing behavior (e.g., excessive borrowing)
- Highest negative weight assigned to `borrow_to_supply_ratio` as it indicates leverage risk
- The final score is scaled from raw value to a **0–1000** range

This ensures that wallets with risky behavior receive lower scores, and those with healthy, responsible usage patterns score higher.

---

## 📁 Output Format

Final risk scores are saved in a CSV file with the following format:

```csv
wallet_id,score
0xfaa0768bde629806739c3a4620656c5d26f44ef2,732
0x2a...c93,401
...
