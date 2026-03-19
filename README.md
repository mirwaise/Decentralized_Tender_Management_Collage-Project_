<div align="center">
  <h1>🛡️ Secure Smart Tender Management System</h1>
  <p><b>Hybrid Web3 Procurement Architecture with Off-Chain AES Encryption</b></p>

  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" />
  <img src="https://img.shields.io/badge/Django-092E20?style=for-the-badge&logo=django&logoColor=white" />
  <img src="https://img.shields.io/badge/Web3-Ethereum-3C3C3D?style=for-the-badge&logo=ethereum&logoColor=white" />
  <img src="https://img.shields.io/badge/Security-AES%20Encryption-red?style=for-the-badge" />
</div>

<br/>

> **The Problem:** Standard public blockchains operate on an "open ledger" system. In government or corporate procurement, placing bids directly on-chain exposes sensitive financial data to competitors before the tender closes.
>
> **The Solution:** A Hybrid Decentralized Application (DApp) that prioritizes Data Privacy by implementing off-chain AES-256 encryption. Bid details remain mathematically confidential and tamper-proof until the tender is officially closed and the decryption keys are released.

## 🏗️ Architecture

The system utilizes a **Hybrid Architecture** to balance privacy with immutable trust:
1.  **Frontend/Backend:** Django (Python) handles user authentication, views, and data processing.
2.  **Security Layer:** Custom Python implementation (`pyaes`) encrypts sensitive data locally.
3.  **Blockchain Layer:** Solidity Smart Contracts store the *encrypted* ciphertext, ensuring immutability without sacrificing privacy.
4.  **Connector:** `Web3.py` acts as the bridge between the Django backend and the EVM network.

## ✨ Key Features

* **AES-256 Data Encryption:** All tender and bid data is encrypted using `pyaes` (CTR Mode) before ever reaching the blockchain.
* **Tamper-Proof Bidding:** Once a bid is placed, it is cryptographically signed and stored on Ethereum; it cannot be altered by admins, competitors, or node operators.
* **Role-Based Access Control (RBAC):**
    * **Admin/Government:** Create tenders, decrypt bids after deadline, declare winners.
    * **Bidder:** View active tenders, place encrypted bids.
* **Automated Evaluation:** Python logic parses decrypted blockchain data to automatically calculate the lowest qualifying bid, removing human bias.

## 🔐 Security Deep Dive

To ensure absolute bid confidentiality, the system executes the following cryptographic flow:
1.  **Input:** User enters the bid amount.
2.  **Key Generation:** A session-based key is derived using `PBKDF2`.
3.  **Encryption:** `pyaes.AESModeOfOperationCTR` encrypts the data string.
4.  **Encoding:** The ciphertext is Base64 encoded for transport.
5.  **Immutability:** The Base64 string is written to the Smart Contract via `contract.functions.createTender()`.

## 🛠️ Technology Stack

* **Backend Framework:** Django (Python)
* **Blockchain Interface:** Web3.py
* **Smart Contract:** Solidity (Deployed on local Ganache/Anvil node)
* **Cryptography:** `pyaes` (AES-CTR mode), `pbkdf2` (Key derivation)

## 🚀 Local Deployment

### Prerequisites
* Python 3.9+
* Local EVM Node (Ganache / Foundry Anvil) running on `http://127.0.0.1:7545`

### Initialization
```bash
git clone [https://github.com/mirwaise/smart-tender-system.git](https://github.com/mirwaise/smart-tender-system.git)
cd smart-tender-system
pip install django web3 pyaes pbkdf2 numpy
