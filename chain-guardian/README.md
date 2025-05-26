# ChainGuardian – Modular Security Snaps for MetaMask

## Overview
ChainGuardian is an experimental security framework built with **MetaMask Flask** and **Snaps**. It allows users and developers to intercept, analyze and assess any blockchain transactions that a user is about to sign via MetaMask (particularly **EVM-compatible blockchain transactions** - before the wallet processes the signature), using plugin-like modules called **Snaps**. These Snaps can scan for threats, simulate contracts, or validate cross-chain interactions in real-time.  

ChainGuardian acts like a **security middleware** between MetaMask and the blockchain, powered by Snaps, which are plugin-like scripts running in a secure sandboxed environment inside MetaMask Flask.
It allows:
-   **Custom threat detection** on transactions.
-   **Contract simulation** before sending funds.
-   **Cross-chain validation** (e.g., warning users when interacting with unverified bridges).
-   **Plugin-based modularity**, so anyone can write their own security Snap.

## Architecture
**ChainGuardian** is architected with a modular, plug-and-play design that allows seamless integration of various Snaps, each focused on specific security tasks. The system operates in three main layers: 
1. **Intercept Layer:**
    Hooks into transaction requests made via MetaMask Flask, allowing ChainGuardian to intercept and parse them before they reach the signing stage. 
2. **Analysis Layer:**
    Executes a configurable chain of Snap modules, each performing a specific task such as: 
    -   Threat pattern matching
    -   ABI and bytecode inspection
    -   Address reputation checks (using threat intelligence feeds)
    -   Contract simulation with forked RPC environments
3. **Feedback Layer:**
    Displays the results of the analysis back to the user via MetaMask's UI, offering:
    -   Risk scores
    -   Human-readable diagnostics
    -   Suggested next actions (e.g., reject, proceed with caution)
This architecture ensures extensibility and composability—developers can write and publish new Snaps tailored for different security scenarios. 

## Custom Snaps Integration
**ChainGuardian** supports and encourages the creation of custom Snaps. Here are some potential Snaps included in the framework:
-   **Phishing Detector Snap:**
    Checks if the target contract address appears in known phishing or scam address lists.
-   **Contract Simulation Snap:**
    Simulates the transaction using an EVM fork (e.g., via Tenderly or Anvil) and predicts the token or asset transfers.
-   **Bridge Validator Snap:**
    Verifies the credibility of cross-chain bridges by checking for audits, chain IDs, and supported token mappings.
-   **Stablecoin Verifier Snap:**
    Validates whether a stablecoin contract adheres to standards like ERC-20, includes mint/burn logic, and maintains peg audits.
Each Snap runs independently in a sandbox and communicates results back to ChainGuardian for aggregation and display. 

## Security Philosophy
ChainGuardian operates on the principle of **user-informed consent** and **transaction transparency**. Instead of silently blocking actions, it aims to educate users and provide them with clear, interpretable insights. 
**Key principles:**
-   **Informed Decision-Making:** Users should understand the risk before approving a transaction. 
-   **Transparent Analysis:** Snaps reveal what the transaction actually does, not just what it appears to do. 
-   **Least Privilege:** Snaps run with minimal permissions and do not have access to wallet keys or signing functions. 
-   **Composable Security:** Security logic is modular, allowing different perspectives on a single transaction.

## Developer Use-Case
When MetaMask Snap Store goes live, ChainGuardian can:
-   Be installed by users from a trusted registry.
-   Act as a **Modular Security Engine** like an antivirus for wallets.
-   Be extended by the community through open Snap plugins.

If you're building a dApp, you can integrate ChainGuardian to:
-   Scan all user-signed actions through Snap plugins
-   Show detailed diagnostics on risky contract behavior
-   Extend with custom plugins for compliance, token verification, etc.

## Project Use Cases
-   **For Developers**
    -   Integrate security validation into dApps to reduce liability and build user trust.
    -   Provide assurance to institutions or enterprise clients about contract safety.
-   **For DeFi Users**
    -   Prevent approval of malicious tokens or contracts that drain wallets.
    -   Detect honeypot tokens or fake liquidity pools.
-   **For Bridge Users**
    -   Get alerted when interacting with suspicious or unaudited bridges.
    -   Prevent accidental cross-chain swaps to scam destinations.

## Future Integrations
ChainGuardian is designed with extensibility in mind. Planned future integrations:
-   **On-chain reputation systems** (e.g., Forta, Chainalysis, WalletGuard)
-   **AI-based contract summarization** (e.g., using LLMs to explain code)
-   **Live EVM simulation via Anvil or Tenderly** with real-time token flow charts
-   **Multichain support** including non-EVM chains via Snap adapters
-   **Browser plug-in for dApp scanning** before MetaMask interaction
-   **Mobile compatibility** once MetaMask Flask support arrives on mobile

## Limitations
-   **MetaMask Flask only:** Not compatible with the standard MetaMask browser extension.
-   **Snap permissions sandbox:** Limited APIs and no access to full blockchain state.
-   **No production deployment path yet:** Must wait for Snap Store.
-   **UX challenges:** Requires users to interpret security prompts correctly.


## Core Technologies
**MetaMask Flask:** Experimental MetaMask wallet that enables Snap installation.  
**MetaMask Snaps:** Isolated JavaScript environments for extending wallet functionality