# Digital Property Smart Contract – RWA

## Overview

The **Digital Property Smart Contract** is a blockchain-based solution designed for registering and managing ownership of digital or real-world assets (RWA). Built with **Solidity 0.8.24**, this contract ensures **transparency**, **security**, and **immutability** in property ownership and transfers.

The contract automatically manages property identifiers, assigns ownership on registration, and enforces strict access control for ownership transfers.

This project was developed and tested using **Remix IDE**, making it easy to deploy and interact with the smart contract directly from a web browser.

---

## Features

- **Asset Registration**  
  Allows users to register properties by providing a description. The contract automatically assigns a **unique, incremental ID** to each property.

- **Ownership Transfer**  
  Property owners can securely transfer ownership to another address.

- **Ownership Verification**  
  Anyone can verify the current owner and details of a registered property.

- **Access Control**  
  Ownership transfers are protected by an `onlyOwner` modifier.

- **Event Logging**  
  All important actions, such as registration and ownership transfer, emit blockchain events for transparency and traceability.

---

## Smart Contract Details

### Functions

#### `registerProperty(string calldata description)`

- Registers a new property.
- The property ID is **automatically generated** by the contract.
- The caller (`msg.sender`) becomes the initial owner.
- Emits the `PropertyRegistered` event.

---

#### `transferOwnership(uint256 id, address newOwner)`

- Transfers ownership of an existing property to a new address.
- Can only be called by the current owner.
- Prevents transfers to the zero address and self-transfers.
- Emits the `OwnershipTransferred` event.

---

#### `getProperty(uint256 id)`

- Retrieves the details of a registered property.
- Returns the property ID, description, and current owner.
- Reverts if the property does not exist.

---

### Events

- **`PropertyRegistered(uint256 id, string description, address owner)`**  
  Emitted when a new property is registered.

- **`OwnershipTransferred(uint256 id, address previousOwner, address newOwner)`**  
  Emitted when ownership of a property is transferred.

---

## How to Use

### Prerequisites

- **Remix IDE:** https://remix.ethereum.org

---

### Steps to Deploy and Test in Remix IDE

1. **Open Remix IDE**  
   Go to https://remix.ethereum.org

2. **Create the Smart Contract File**  
   - In the File Explorer, create a new file (e.g., `PropertyRegistry.sol`)
   - Copy and paste the smart contract code into the file

3. **Compile the Contract**  
   - Navigate to the **Solidity Compiler** tab  
   - Select compiler version **0.8.24**  
   - Click **Compile PropertyRegistry.sol**

4. **Deploy the Contract**  
   - Go to the **Deploy & Run Transactions** tab  
   - Select environment: **Remix VM (Cancun)**  
   - Click **Deploy**

5. **Interact with the Contract**  
   - Use the deployed contract interface to call:
     - `registerProperty`
     - `transferOwnership`
     - `getProperty`

---

## Testing the Contract

### Functional Tests

#### Basic Registration

- Call `registerProperty` with:
  - description = `"House in Marbella"`
- The property will be registered with ID `1`.
- Call `getProperty(1)` to confirm correct storage and ownership.

---

#### Ownership Transfer

- Call `transferOwnership` on a registered property.
- Verify ownership change using `getProperty`.

---

#### Automatic ID Increment

- Register multiple properties.
- Each new property receives a sequential ID (`1`, `2`, `3`, …).

---

### Security Tests

#### Unauthorized Access

- Attempt to call `transferOwnership` from a non-owner account.
- The transaction must revert with:
is not the Owner



---

#### Invalid Addresses

- Attempt to transfer ownership to the zero address (`0x000...000`).
- The transaction must revert with:
invalid address



---

#### Self Transfer

- Attempt to transfer ownership to the current owner.
- The transaction must revert with:
Cannot transfer to self



---

## Example Code Snippets

### Registering a Property

```solidity 
registerProperty("Apartment in Barcelona")
```

### Transferring Ownership
```solidity
transferOwnership(1, 0x123456789abcdef123456789abcdef123456789a);
```

### Checking Property Details
```solidity

getProperty(1);
```
---
## Future Enhancements
- **Extend the contract**:  to ERC-721 to represent properties as NFTs with external metadata.
- **Metadata Integration**: Add ERC-721 standards to include metadata for properties.
- **KYC System**: Introduce user verification before registering or transferring properties.
- **Multi-Signature Transfers**: Enable multi-signature approvals for high-value properties.
- **Property Enumeration**:Add functionality to list properties by owner or retrieve all registered property IDs.
- **Advanced Access Control**: Introduce admin roles or pausability for emergency situations.
---
## License
This project is licensed under the LGPL-3.0-only.

## Visual Representation
A **clear and interactive UI** could be built using frameworks like React.js to interact with this contract for enhanced user experience. For now, enjoy the simplicity and power of **Remix IDE**! 🚀
