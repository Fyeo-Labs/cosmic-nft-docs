# Hook for minting

## Triggers
This should be triggered when a payment is received in a wallet with a memo called `CosmicMintingRequest`

## Inputs
`MintPrice`: String - Minting price. This will be passed to the hook when installed in an account per collection. Every time collection creator wants to change the mint price, they will have to reinstall the hook.
`URITokens`: String[] - List of URIToken that are available in this collection. This will be passed to the hook when installed in an accout per collection. Everyt time collection creator wants to change the mint price, they will have to reinstall the hook.

## Implementation details
- Validate that payment amount is aleast the minting price and greater than 5 XAH
- URITokens are passed as parameter. If URITokens are not in the hook state, first get it from the parameter and set it in hook state
- Mint an URIToken and make sure the issuer is `issuerAddress` and destination is `destinationAddress`. Randomly pick an URIToken from hook state
- Transfer the minted token to `destinationAddress`
- Wait for minted transaction to be validated - Do we need that?
- Transfer 5% of mint price to ComicXahau

## For cosmic backend
- Watch for transactions on chain
- Check if the transactions are for our collection creators (check the memo)
- Update our database with the new information, like NFTId, TxnId, etc
- Think about other verification that should be done to avoid attacks
