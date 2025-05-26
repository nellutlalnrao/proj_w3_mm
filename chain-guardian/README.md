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
ChainGuardian is architected with a modular, plug-and-play design that allows seamless integration of various Snaps, each focused on specific security tasks. The system operates in three main layers: 
1. Intercept Layer:
    Hooks into transaction requests made via MetaMask Flask, allowing ChainGuardian to intercept and parse them before they reach the signing stage. 
2. Analysis Layer:
    Executes a configurable chain of Snap modules, each performing a specific task such as: 
    -   Threat pattern matching
    -   ABI and bytecode inspection
    -   Address reputation checks (using threat intelligence feeds)
    -   Contract simulation with forked RPC environments
3. Feedback Layer:
    Displays the results of the analysis back to the user via MetaMask's UI, offering:
    -   Risk scores
    -   Human-readable diagnostics
    -   Suggested next actions (e.g., reject, proceed with caution)
This architecture ensures extensibility and composability—developers can write and publish new Snaps tailored for different security scenarios. 

## Developer Use-Case
When MetaMask Snap Store goes live, ChainGuardian can:
-   Be installed by users from a trusted registry.
-   Act as a **Modular Security Engine** like an antivirus for wallets.
-   Be extended by the community through open Snap plugins.

If you're building a dApp, you can integrate ChainGuardian to:
-   Scan all user-signed actions through Snap plugins
-   Show detailed diagnostics on risky contract behavior
-   Extend with custom plugins for compliance, token verification, etc.

## Limitations
-   **MetaMask Flask only:** Not compatible with the standard MetaMask browser extension.
-   **Snap permissions sandbox:** Limited APIs and no access to full blockchain state.
-   **No production deployment path yet:** Must wait for Snap Store.
-   **UX challenges:** Requires users to interpret security prompts correctly.


## Core Technologies
**MetaMask Flask:** Experimental MetaMask wallet that enables Snap installation.  
**MetaMask Snaps:** Isolated JavaScript environments for extending wallet functionality