# Cross Chain Bridge with Lit Protocol

## Goal:

How can I build a cross-chain bridge using Lit Protocol's Programmable Key Pairs(PKPs) with SDK v3 version?

## Overview

1. Building a cross-chain bridge using Lit Protocol's Programmable Key Pairs (PKPs) with the version 3 of the SDK involves several key steps:

2. Understand the SDK and PKPs: The `Lit SDK v3` introduces additional permission scoping requirements when working with Programmable Key Pairs (PKPs). These scopes determine the kinds of data that individual Programmable Key Pairs (PKPs) are allowed to sign and are required when creating session signatures​​.

3. Install Required Packages: Begin by installing the necessary packages from the Lit SDK. For SDK version `3.0.21`, you would typically use the following commands:

   `yarn add @lit-protocol/lit-auth-client@cayenne`

   `yarn add @lit-protocol/contracts-sdk@cayenne​​`

4. Initialize the LitContract Instance: Import LitContracts from `@lit-protocol/contracts-sdk` and create a new LitContracts instance. This instance will attempt to use `window.etheruem` if no signer is provided​​.

5. Create and Assign Scopes to PKPs: For new PKPs, generate them with the: `contracts-sdk`, specifying the required scopes (e.g., `AuthMethodScope`.`SignAnything`, `AuthMethodScope.OnlySignMessages`).

6. This is done through the `mintWithAuth` method of the contractClient​​. For existing Programmable Key Pairs (PKPs), verify and set the scopes using pkpPermissionsContract methods from the `LitContracts SDK​`​.

7. Developing Cross-Chain Bridges: Lit Protocol uses threshold cryptography for its PKPs, allowing for decentralized key management. This functionality is crucial for developing cross-chain bridges. Programmable Key Pairs (PKPs) can execute JavaScript code, enabling cross-chain interactions. For instance, you can develop an escrow service where two parties send assets to a PKP address, and upon verification of the required balance, the Lit network facilitates a swap of assets between the chains​​.

8. Write and Deploy Lit Action Code: To create and use a PKP, you need to write the Lit Action JavaScript code associated with the key pair. This code can then be uploaded to IPFS, creating a decentralized record for execution with your key pair. The PKPs, managed by NFTs, are minted, associated with the JavaScript function, and then burned to ensure they function as intended without being altered​​.

9. Integration with Applications: Utilize the open-source SDK developed for integrating these exchanges within applications. This SDK helps in determining whether users have sent their tokens to the PKP address and implementing the logic within your application. Knowing the counterparty beforehand is necessary for creating the Lit Action code for swap transactions​​.

10. These steps outline the process of building a crosschain bridge using Lit Protocol's PKPs with the v3 version of the SDK. It involves a combination of programming, understanding of blockchain technologies, and the specific functionalities provided by Lit Protocol.

## Integration a cross-chain exchanges into apps using Lit Protocol's SDK

The integration of cross-chain exchanges into applications using Lit Protocol's SDK involves a few key steps:

1. Write Lit Action Code: First, you need to write the JavaScript code for the Lit Action that will be associated with your PKP. This code specifies the conditions under which the PKP will sign transactions.

2. Upload Code to IPFS: After writing and testing your Lit Action code, upload it to IPFS. This step creates a decentralized record of the code, which dictates the actions your PKP can execute.

3. Minting the PKP: PKPs are essentially key pairs managed by NFTs. After uploading your code to IPFS, you can mint a PKP. This process associates the key pair with your JavaScript function and then "burns" the PKP, meaning it no longer has an owner and can't run arbitrary JavaScript. It's bound to function exactly as programmed.

4. Verifying Trustless and Verifiable Operations: With the PKP minted, you can verify that only your specific JavaScript code can be executed by this key pair. You can also confirm that the PKP has no owner, ensuring its single function is to facilitate cross-chain exchanges.

5. SDK for Application Integration: Lit Protocol offers an open-source SDK to integrate these functionalities within your application. The SDK assists in verifying if users have sent tokens to the PKP address and implementing the corresponding logic.

6. Potential Future Developments: The SDK currently requires you to know the other counterparty for creating the Lit Action code. In future iterations, it could support a cross-chain order book, enabling users to swap tokens without needing to find a counterparty themselves.

7. These steps demonstrate how you can use Lit Protocol's tools and SDK to create decentralized, trustless cross-chain exchanges within your applications.

## Triggering Cross Chain State Changes

Q: What code should I use to read a state change on one chain and have the trigger a signature that changes state on another?

A: To implement a system that reads a state change on one blockchain and triggers a signature to change state on another, you'll need to use a combination of blockchain listeners, smart contracts, and possibly a middleware to orchestrate the process.

Here's a basic outline in pseudocode:

### Listening for State Change on Chain A

Set up an Event Listener:

```
// Assuming you're using a JavaScript library
// like web3.js or ethers.js
const contractA = new web3.eth.Contract(abi, contractAddress);
contractA.events.StateChanged({
    fromBlock: 'latest'
}, function(error, event){
    if (!error) {
        handleStateChange(event.returnValues);
    }
});
```

### Handle State Change Event:

```
function handleStateChange(data) {
    // Check if the state change meets your criteria
    if (isRelevantChange(data)) {
        triggerCrossChainAction(data);
    }
}
```

### Triggering State Change on Chain B

Trigger Cross Chain Action:

```
async function triggerCrossChainAction(data) {
    // Prepare data or transaction for Chain B
    const preparedData = prepareDataForChainB(data);

    // Use Lit Protocol PKP for signing transaction for Chain B
    const signature = await signWithLitPKP(preparedData);

    // Send transaction to Chain B
    sendTransactionToChainB(preparedData, signature);
}
```

### Sign with Lit Protocol PKP:

```
async function signWithLitPKP(data) {
    // This would involve interacting with the Lit Protocol
    // to get the PKP to sign your transaction or data.
    // Exact implementation depends on Lit Protocol SDK.
    // Return the signed data or transaction
}
```

### Send Transaction to Chain B:

```
async function sendTransactionToChainB(data, signature) {
    // Using a smart contract or API to send the signed transaction to Chain B.
    // This might involve calling a function on a smart contract on Chain B
    // with the signed data and any other necessary parameters.
}
```

## Note:

The above code is a high-level pseudocode representation and will need to be adapted to your specific blockchain platforms and use case.
The interaction with Lit Protocol PKP would depend on the specific features and methods provided by the Lit Protocol SDK.

Ensure that the smart contracts on both chains are designed to handle the cross-chain interaction securely and efficiently.

Testing and security audits are crucial for cross-chain operations to ensure the integrity and security of the transactions.
