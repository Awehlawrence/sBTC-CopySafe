
# sBTC-CopySafe – Intellectual Property Protection on Blockchain

## Overview

**sBTC-CopySafe** is a Clarity smart contract for the **Stacks blockchain** that enables creators, inventors, and organizations to register, verify, and manage **intellectual property (IP)** assets in a **trustless, immutable, and transparent** way.

The contract provides mechanisms for IP ownership registration, hash verification, secure ownership transfer, expiration-based validity, and updates to IP metadata.

---

## ✨ Features

* **IP Registration**

  * Register IP with a unique hash (32 bytes).
  * Optional expiration block height for time-limited protections.
  * Prevents duplicate or zero-value hashes.

* **Ownership Verification**

  * Query current owner of a registered IP ID.
  * Verify if a given hash corresponds to a registered IP.

* **Ownership Transfer**

  * Transfer ownership of IP to another principal.
  * Ensures only the current owner can transfer.

* **Expiration Management**

  * Register IPs with optional expiration dates.
  * Extend IP validity beyond the original expiration.
  * Expired IPs cannot be updated.

* **Metadata Update**

  * Owners can update the registered hash for an IP.
  * Old hash is removed from the registry before storing the new one.

* **Hash Registry**

  * Global tracking of registered hashes to prevent collisions.
  * Query to check if a hash is already registered.

---

## 🔑 Error Codes

| Code    | Description              |
| ------- | ------------------------ |
| `u1000` | Not authorized           |
| `u1001` | Invalid hash length      |
| `u1002` | Hash cannot be all zeros |
| `u1003` | Hash already registered  |
| `u1004` | IP not found             |
| `u1005` | Invalid IP ID            |
| `u1006` | IP ID out of range       |
| `u1007` | IP expired               |
| `u1008` | Invalid expiration       |
| `u1009` | No expiration set        |

---

## 📚 Key Functions

### Public

* **`register-ip(ip-hash, expiration-block)`** → Register a new IP with hash and optional expiration.
* **`transfer-ip(ip-id, new-owner)`** → Transfer ownership to a new principal.
* **`extend-ip-registration(ip-id, new-expiration)`** → Extend expiration of an existing IP.
* **`update-ip-metadata(ip-id, new-hash)`** → Update the hash metadata for an IP.

### Read-Only

* **`check-ip-ownership(ip-id)`** → Returns the current owner of the IP.
* **`verify-ip-hash(ip-id, hash-to-verify)`** → Checks if a given hash matches the registered hash.
* **`is-hash-registered(ip-hash)`** → Returns true if the hash is already registered.

---

## ⚙️ Constants

* **Hash length**: Must be exactly 32 bytes.
* **Zero hash**: Not allowed (all zeros).
* **Expiration**: Must be a future block height.

---

## 🛠️ Example Usage

```clarity
;; Register an IP with expiration at block 20000
(contract-call? .ip-guard register-ip 0x1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd1234abcd (some u20000))

;; Verify ownership
(contract-call? .ip-guard check-ip-ownership u1)

;; Transfer ownership
(contract-call? .ip-guard transfer-ip u1 'ST3ABCDXYZ1234ABCDEXAMPLE5678)

;; Extend expiration
(contract-call? .ip-guard extend-ip-registration u1 u25000)

;; Update IP metadata (hash change)
(contract-call? .ip-guard update-ip-metadata u1 0x9876abcd9876abcd9876abcd9876abcd9876abcd9876abcd9876abcd9876abcd)
```

---
