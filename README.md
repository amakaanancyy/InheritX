
# Inheritx -Automated Will Execution Smart Contract**

### *Time-Locked Inheritance • Multi-Oracle Verification • NFT Distribution • Dispute Resolution*

---

## **Overview**

This project is a highly advanced **Clarity smart contract** for automated will execution on the Stacks blockchain.
It enables secure, decentralized inheritance processing without requiring a traditional executor or attorney.

The contract introduces:

* **Multi-oracle verification of death**
* **Time-locked inheritance payouts**
* **Automated STX distribution with tax handling**
* **NFT inheritance and on-chain ownership tracking**
* **Dispute reporting and multi-party resolution**
* **Support for phased inheritance release**
* **Flexible beneficiary configuration**
* **Updatable will-document hash**

This architecture ensures that inheritance is released **securely**, **transparently**, and **only under the correct conditions**, while keeping the system resistant to fraud or premature execution.

---

## **Key Features**

### ✅ **Multi-Oracle Death Confirmation**

Beneficiaries cannot claim inheritance until a quorum of trusted oracles confirms the owner’s passing.

* Oracles are added by the contract owner.
* Each oracle issues a `confirm-death` transaction.
* Once the required number of confirmations is met, the will is activated.

---

### ✅ **Time-Locked Distribution**

Each beneficiary can have a custom time-lock applied to their inheritance.

Examples:

* *Children receive inheritance at age 21.*
* *Funds are released 1 year after death.*

---

### ✅ **Automated STX Inheritance**

Upon claim:

* The contract calculates the beneficiary’s share.
* An **inheritance tax** (default 2%) is applied.
* STX is released to the claimant.
* Each beneficiary can claim *only once*.

---

### ✅ **NFT Inheritance**

Beneficiaries can inherit NFTs represented as token IDs.

* NFTs are tracked with the `nft-ownership` map.
* Ownership transfers automatically during inheritance claims.

---

### ✅ **Dispute Resolution System**

Any beneficiary can raise a dispute by submitting an evidence hash.

The contract stores:

* Evidence hash
* Resolution status
* Optional voting metadata (for oracle/jury decisions)

This helps prevent fraudulent claims, duplicate wills, or illegal executor behavior.

---

### ✅ **Phased Inheritance (Optional)**

A beneficiary may receive assets in multiple releases (e.g., 50% now, 50% later).

This helps support:

* Trust-style inheritance structures
* Controlled financial maturity
* Multi-stage disbursements

---

## **Contract Functions Summary**

### **Management**

| Function                        | Description                                         |
| ------------------------------- | --------------------------------------------------- |
| `initialize-contract`           | Registers oracles                                   |
| `add-beneficiary`               | Adds beneficiaries with shares, lock periods & NFTs |
| `update-will-hash`              | Updates the stored hash of the will                 |
| `update-required-confirmations` | Sets quorum (# of oracle votes)                     |
| `deactivate-contract`           | Emergency stop switch                               |

---

### **Inheritance**

| Function            | Description                                      |
| ------------------- | ------------------------------------------------ |
| `confirm-death`     | Oracle confirms owner's death                    |
| `claim-inheritance` | Beneficiary claims share + NFTs                  |
| `claim-phase-1`     | Claim first phased distribution (private helper) |

---

### **Dispute Handling**

| Function          | Description                       |
| ----------------- | --------------------------------- |
| `raise-dispute`   | Submit evidence to halt execution |
| `resolve-dispute` | Internal resolution function      |

---

### **Getters**

| Function               | Description                             |
| ---------------------- | --------------------------------------- |
| `get-beneficiary-info` | Returns share, lock, NFTs, claim status |
| `get-contract-status`  | Returns contract flags & metadata       |
| `get-nft-owner`        | Checks ownership of an NFT              |

---

## **Security Considerations**

* Multi-sig oracle requirement prevents unauthorized or early inheritance claims.
* Time-locks prevent funds from being released prematurely.
* Dispute system allows challenges before funds are irreversibly distributed.
* Contract owner cannot withdraw funds after death confirmation.
* Beneficiaries cannot claim more than once.
* NFTs transfer transparently using on-chain state.

---

## **Future Improvements (Optional)**

* Integration with SIP-009 NFT contracts for full inter-contract transfers.
* Full multi-party dispute voting logic.
* Add external oracle compatibility (e.g., Chainlink, Reality.eth-style).
* Gas optimization by consolidating storage writes.

---

## **License**

MIT — open and free for modification.

---

