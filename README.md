# Wallet Risk Scoring From Scratch

## Project Overview

This project develops a risk scoring model for Ethereum wallets based on their on-chain transaction history with the Compound V2 & V3 protocols. The model analyzes various behavioral and financial metrics to assign each wallet a risk score from 0 (highest risk) to 1000 (lowest risk).

This is an end-to-end data science project that covers data collection, advanced feature engineering, normalization, and weighted scoring, demonstrating a deep understanding of DeFi lending protocol risks.

---

## Methodology

The risk assessment is based on a weighted model that considers both foundational on-chain activity and advanced, DeFi-specific financial behaviors.

#### Key Features Engineered:
* **Leverage Proxy (`borrow_to_supply_ratio`):** Measures how heavily a user is borrowing against their collateral. This is the most heavily weighted risk indicator.
* **Financial Health Proxy (`health_factor_proxy`):** Tracks if a user is responsibly repaying debt relative to their borrowing.
* **Behavioral Classification:** Transactions are classified into `supply`, `withdraw`, and `borrow/repay` to understand user intent.
* **Standard Health Indicators:** Includes `successful_tx_rate`, `wallet_age_days`, `is_active_recently`, and `unique_contracts_interacted`.

For a complete breakdown, please see the **[Methodology Report](Methodologies-Wallet Risk Scoring Model.docx)**.

---

## Results & Visualizations

The model successfully differentiates between low-risk, established users and higher-risk, speculative wallets.

#### Score Distribution
The final scores follow a normal distribution, with a majority of wallets clustering in the median-risk range, indicating a typical low-activity user profile.

![Score Distribution](score_distribution.png)

#### Feature Importance
The model's logic is driven primarily by DeFi-specific metrics, with `borrow_to_supply_ratio` having the most significant impact on the final score.

![Feature Importance](feature_importance.png)

---

## How to Run This Project

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/Kunal-artist/Wallet-Risk-Scoring-From-Scratch.git](https://github.com/Kunal-artist/Wallet-Risk-Scoring-From-Scratch.git)
    cd Wallet-Risk-Scoring-From-Scratch
    ```

2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Run the notebooks in order:**
    * `1_Data_Collection.ipynb`: Fetches the raw transaction data from the Etherscan API.
    * `2_Feature_Engineering_and_Scoring_Model.ipynb`: Processes the data, engineers features, calculates scores, and generates outputs.

