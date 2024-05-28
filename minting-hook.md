# Hook for minting

## Triggers
This should be triggered when a payment is received in a wallet with a memo called `CosmicMintingRequest`

## Inputs
`MintPrice`: String - Minting price. This will be passed to the hook when installed in an account per collection. Every time collection creator wants to change the mint price, they will have to reinstall the hook.

## Implementation details
- Validate that payment amount is aleast the minting price and greater than 5 XAH
- Mint an URIToken and make sure the issuer is `issuerAddress` and destination is `destinationAddress`. Randomly pick an URIToken from hook state
- Transfer the minted token to `destinationAddress`
- Wait for minted transaction to be validated - Do we need that?
- Transfer 5% of mint price to ComicXahau

## Questions
- Is there any timeout for hooks to finish their execution?
- Can we do all the above steps in one transaction?
- What about concurrency? Will the state of hook be updated in single threaded approach?

## For cosmic backend
- Watch for transactions on chain
- Check if the transactions are for our collection creators
- Check if the transactions was done by our hook
- Update our database with the new information, like NFTId, TxnId, etc
- Keep minting open to other wallets while a wallet is minting a specific URIToken
