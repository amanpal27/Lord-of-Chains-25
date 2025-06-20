# SupplyChainNFT

**SupplyChainNFT** is a simple way to see how products move in a supply chain right on the blockchain! Here’s how it works:

---

## What’s Inside

* **NFT Products:** Every product you create becomes a unique ERC‑721 token.
* **Four Stops:** Products go from *Created* → *AtWarehouse* → *InTransit* → *Completed*.
* **Roles You Play:** Pretend to be Seller, Warehouse staff, or Carrier by assigning yourself a role.
* **Checks & Balances:** Enforce cooling requirements, expiry dates, and log every step with a note.
* **Delivery Check:** When a product finishes, see if it was on time or late.

---

## Getting Started

Grab the `SupplyChainNFT.sol` file directly from GitHub:

1. **Open the contract** in your browser:

   ```
   https://github.com/yourusername/SupplyChainNFT/blob/main/SupplyChainNFT.sol
   ```
2. **Copy the code** and paste it into [Remix IDE](https://remix.ethereum.org/).
3. **Install OpenZeppelin** libraries in Remix via the plugin or using the import statements in the file.
4. **Compile & Deploy**:

   * Select Solidity 0.8.x.
   * In the “Deploy & Run Transactions” panel, enter your wallet address as `initialOwner`.
   * Click **Deploy**.

---

## How It Works

1. **Set Your Role**
   Call `assignRole(...)` to choose whether you’re the Seller, Warehouse, or Carrier.

2. **Mint a Product**
   As the Seller, call:

   ```js
   const productId = await contract.mintProduct(
     metadataURI,       // IPFS link to JSON metadata
     shelfLifeSeconds,  // shelf life in seconds
     deliverByTimestamp,
     needsCooling       // true/false
   );
   ```

3. **Move to Warehouse**
   When you’re in the Seller role:

   ```js
   await contract.moveToNext(
     productId,
     "Packed and sent to warehouse."
   );
   ```

4. **Confirm Storage**
   As Warehouse staff, if cooling is needed:

   ```js
   await contract.confirmColdStorage(productId);
   ```

5. **Ship It**
   Still in Warehouse role:

   ```js
   await contract.moveToNext(
     productId,
     "Picked up by carrier."
   );
   ```

6. **Deliver**
   Switch to Carrier role:

   ```js
   await contract.assignRole(Stage.InTransit);
   await contract.moveToNext(
     productId,
     "Delivered to customer."
   );
   ```

7. **Peek at History**
   See each step and comment:

   ```js
   const history = await contract.getHistory(productId);
   console.log(history);
   ```


