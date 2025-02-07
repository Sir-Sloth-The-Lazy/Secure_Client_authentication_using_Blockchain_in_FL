# Secure Client Authentication using Blockchain in Federated Learning

## Overview
The objective of this phase is to implement a federated learning framework where model updates from clients are submitted to a blockchain. The blockchain ensures the integrity and transparency of the updates before they are aggregated to form a global model.

This phase builds upon:
- **Phase 1**: Centralized Logistic Regression.
- **Phase 2**: Federated Learning.

Refer to previous phases for more details on dataset preprocessing (SMOTE, cross-validation) and federated learning concepts.

## Background
Financial institutions currently use centralized models to analyze and predict financial outcomes like fraud detection and credit risk assessment. However, these models have limitations:
- Limited data diversity.
- Biased or inaccurate predictions.
- Restricted collaboration due to privacy concerns.

Federated learning allows institutions to collaboratively train machine learning models while keeping data private. However, ensuring transparency and trust in model updates remains a challenge. **Blockchain integration** addresses this by providing:
- **Data integrity**: Ensuring that model updates remain untampered.
- **Transparency**: Enabling auditability of model updates.
- **Decentralized trust**: Eliminating the need for a central authority.
- **Immutability**: Preventing alterations or deletions of recorded updates.

## Proposed Solution
This project integrates **Federated Learning (FL) with Ethereum Blockchain**, inspired by **JPMorgan's FedSyn paper**. The goal is to build a **global logistic regression model** without sharing private data.

**Key Features:**
- **Clients (financial institutions) train local models** on their private datasets.
- **Model parameters are encrypted and submitted to a blockchain** instead of sharing raw data.
- **Federated Learning Coordinator aggregates these parameters** to create a robust global model.

This approach enhances privacy while fostering collaboration, ensuring a **more accurate and comprehensive predictive model**.

## Results and Interpretation
The **global model** achieved the following test set performance:
- **Accuracy**: 99.17% (high, but not the best metric due to class imbalance).
- **Precision**: 15.75% (indicating false positives are a challenge).
- **Recall**: 87.76% (captures fraudulent transactions well).
- **F1 Score**: 0.2671 (balancing precision and recall).
- **ROC AUC Score**: 0.9547 (excellent at distinguishing fraud vs. non-fraud).
- **AUPRC**: 0.7133 (useful metric for imbalanced datasets).

### **Significance & Benefits**
- **Enhanced Data Integrity and Security**: Blockchain prevents tampering of model updates.
- **Transparency and Traceability**: Maintains a transparent record of model contributions.
- **Decentralized Trust**: Eliminates reliance on a central authority.
- **Immutability**: Ensures that recorded updates remain consistent over time.

## Dataset Description
- **Dataset**: Credit Card Fraud Detection (Kaggle).
- **Transactions**: 284,807 total (492 fraud, 284,315 non-fraud).
- **Features**:
  - **Time**: Time elapsed since the first transaction.
  - **V1-V28**: Principal components obtained via PCA.
  - **Amount**: Transaction amount.
  - **Class**: 1 (fraudulent), 0 (non-fraudulent).

### **How the Dataset Was Used**
1. **Split into local training and global test sets**.
2. **Divided into 5 subsets**, each representing a financial institution.
3. **Stratification ensured adequate fraudulent transaction representation**.
4. **Local models were trained, updates submitted on-chain, and aggregated into a global model**.

## Blockchain Technologies Used
- **Truffle**: Ethereum development framework for smart contract management.
- **Ganache**: Personal blockchain for contract deployment and testing.

## Execution Steps
### **1. Setting Up the Blockchain**
- Deploy a smart contract using **Truffle** and **Ganache**.

### **2. Data Preparation**
- Load and preprocess dataset.
- Split data into **5 subsets** simulating different financial institutions.

### **3. Local Model Training**
- Train local models with **SMOTE** to handle class imbalance.

### **4. Submit Model Updates to Blockchain**
- **Only 5 permissioned clients** can submit updates to the **FederatedLearning smart contract**.
- **Only encrypted model parameters** are shared, preserving privacy.

### **5. Aggregate Models from Blockchain**
- **Validator nodes** ensure compliance with submission protocols.
- **Federated Averaging (FedAvg)** aggregates model updates.
- Institutions verify the **aggregated model** before receiving the global model.

### **6. Evaluate Global Model**
- Evaluate **accuracy, precision, recall, AUPRC**, and other key metrics.
- Restart the process periodically for continuous model updates.

## Code Execution Steps
### **Prerequisites**
- **Python (3.12.3)**
- **Virtual Environment** setup
- **Ganache** installed and running

### **1. Setting Up Ganache**
- Start Ganache, create a new workspace.
- Ensure settings match **truffle-config.js** (host: 127.0.0.1, port: 7545).

### **2. Setting Up Python Environment**
```sh
# Create Virtual Environment
python -m venv venv-fraudbusters

# Activate Virtual Environment
# Windows
.\venv-fraudbusters\Scripts\activate
# macOS/Linux
source venv-fraudbusters/bin/activate

# Install Dependencies
pip install -r requirements.txt
```

### **3. Deploy Smart Contract**
```sh
cd phase3a-federated_learning_with_blockchain

# Compile the Smart Contract
truffle compile

# Migrate the Smart Contract
truffle migrate --network development
```

### **4. Run Project Scripts (in order)**
```sh
python src/data_preparation.py
python src/local_training.py
python src/submit_updates.py
python src/aggregate_models.py
python src/evaluate_global_model.py
```

## Appendix
### **Overview of Project Phases**
#### **Phase 1: Centralized Model using Logistic Regression**
- Baseline logistic regression model for fraud detection.
- Data preprocessing and exploratory analysis.
- Model training and evaluation.

#### **Phase 2: Federated Learning using Logistic Regression**
- Distributed training across multiple institutions.
- Implemented **Federated Averaging (FedAvg)** algorithm.
- Aggregation and evaluation of global model.

#### **Phase 3A: Federated Learning with Blockchain**
- **Integrates blockchain for secure model updates.**
- **Implements transparency, trust, and decentralized verification.**
- **Ensures integrity and traceability of updates.**

#### **Phase 3B: Federated Learning with Zero-Knowledge Proofs (ZKPs)**
- Uses **ZKML (Zero-Knowledge Machine Learning)** for privacy-enhanced updates.
- Allows institutions to **verify correctness without revealing data**.
- Implements **PyZPK** for secure model verification.

### **Overview of Technology Concepts**
- **Logistic Regression**: Used for binary classification (fraud detection).
- **Federated Learning**: Enables multiple clients to train models collaboratively while maintaining data privacy.
- **Blockchain**: Ensures secure, transparent, and tamper-proof model updates.

---

This **README** provides a comprehensive overview of Secure Client Authentication using Blockchain in Federated Learning, detailing background, execution steps, and results.
