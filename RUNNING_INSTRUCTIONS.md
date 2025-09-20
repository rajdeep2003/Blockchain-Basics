# Step-by-Step Running Instructions (for Windows)

This guide provides the exact commands to run the entire "Krypt" application on your local machine for development and testing. All commands are intended for the **PowerShell** terminal on Windows.

---

### **Part 1: Prerequisites (One-Time Setup)**

Before you begin, you need to have the following software installed.

1.  **Node.js and npm**: This project is built on Node.js, which includes the Node Package Manager (npm) for handling dependencies.
    *   **Install it from:** [nodejs.org](https://nodejs.org/en/download/)
    *   Download the "LTS" (Long-Term Support) version for your system. The installer will add `node` and `npm` to your command line path automatically.
    *   To verify the installation, open PowerShell and run `node -v` and `npm -v`. You should see version numbers for both.

2.  **MetaMask Browser Extension**: This will act as your wallet to interact with the application.
    *   **Install it from:** [metamask.io](https://metamask.io/)
    *   Add the extension to your preferred browser (Chrome, Firefox, Brave, or Edge).
    *   Complete the initial setup process to create a wallet. **Be sure to save your seed phrase somewhere secure and private.**

---

### **Part 2: Setting Up the Backend (Local Blockchain)**

First, we will start a local blockchain on your computer using Hardhat.

**Step 1: Open PowerShell**
*   Click the Start menu, type "PowerShell", and open it.

**Step 2: Navigate to the `smart_contract` Directory**
*   Use the `cd` command to change directories. Replace `C:\path\to\your\project` with the actual path where you saved the project.
    ```powershell
    cd C:\path\to\your\project\smart_contract
    ```

**Step 3: Install Dependencies**
*   Run the following command to install all the necessary packages for the backend, like Hardhat and Ethers.js.
    ```powershell
    npm install
    ```

**Step 4: Start the Local Blockchain**
*   This command starts a simulated Ethereum blockchain on your machine.
    ```powershell
    npx hardhat node
    ```
*   **IMPORTANT:** Leave this terminal running. It will print a list of 20 test accounts, each with a private key and 10000 fake ETH. This is your local blockchain.

---

### **Part 3: Deploying the Smart Contract**

Now, with the local blockchain running, we need to deploy our `Transactions.sol` contract to it.

**Step 1: Open a *Second* PowerShell Terminal**
*   Leave the first terminal running. Open a new, separate PowerShell window.

**Step 2: Navigate to the `smart_contract` Directory**
*   In this new terminal, go to the same directory as before.
    ```powershell
    cd C:\path\to\your\project\smart_contract
    ```

**Step 3: Deploy the Contract**
*   This command runs our deployment script and targets the local network we just started.
    ```powershell
    npx hardhat run scripts/deploy.js --network localhost
    ```
*   The output will show the address of the deployed contract. It will look like this:
    `Transactions deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3`
*   **Copy this address.** You will need it in the next step.

---

### **Part 4: Setting Up the Frontend (React App)**

Now we'll configure and run the user interface.

**Step 1: Update the Contract Address**
*   Open the project folder in a code editor like VS Code.
*   Navigate to the file: `client/src/utils/constants.js`.
*   You will see a line: `export const contractAddress = "0x...";`
*   **Paste the address you copied** from the previous step into the quotes. Save the file.

**Step 2: Open a *Third* PowerShell Terminal**
*   Leave the other two terminals open. Open a new, third PowerShell window.

**Step 3: Navigate to the `client` Directory**
    ```powershell
    cd C:\path\to\your\project\client
    ```

**Step 4: Install Frontend Dependencies**
*   This will install React, Ethers.js for the client, and other necessary libraries.
    ```powershell
    npm install
    ```

**Step 5: Run the Frontend Application**
*   This command starts the local development server for the React app.
    ```powershell
    npm run dev
    ```
*   The output will give you a local URL, typically `http://localhost:5173/`.

---

### **Part 5: Configuring MetaMask for Local Testing**

The final step is to tell MetaMask how to connect to our local blockchain and to import a test account.

**Step 1: Add the Hardhat Network to MetaMask**
1.  Open your browser and click the MetaMask extension icon.
2.  Click the network dropdown at the top (it will likely say "Ethereum Mainnet").
3.  Click **"Add network"**.
4.  On the new page, click **"Add a network manually"**.
5.  Fill in the form with these exact details:
    *   **Network Name:** `Hardhat Localhost`
    *   **New RPC URL:** `http://127.0.0.1:8545`
    *   **Chain ID:** `31337`
    *   **Currency Symbol:** `ETH`
6.  Click **"Save"**. MetaMask is now connected to your local blockchain.

**Step 2: Import a Test Account with Fake ETH**
1.  Go back to your **first terminal** (the one running `npx hardhat node`).
2.  Copy the **Private Key** for `Account #0` (or any other account from the list).
3.  In MetaMask, ensure you are on the "Hardhat Localhost" network.
4.  Click the colored circle icon at the top right, then click **"Import account"**.
5.  Paste the private key you copied and click **"Import"**.

Your MetaMask will now show a balance of 10000 ETH. This is fake Ether that you can use for testing within your local environment.

---

### **Conclusion**

You are all set!
*   **Terminal 1** is running your local blockchain.
*   **Terminal 3** is running your frontend server.
*   (Terminal 2 was only for deployment and can be closed).

Open the frontend URL (e.g., `http://localhost:5173/`) in your browser. You should see the Krypt application. Click "Connect Wallet" and you can now send test transactions using your imported account.
