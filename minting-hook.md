# Hook for minting

## Triggers
This should be triggered when a payment is received in a wallet with a specific parameter called `CosmicMinting`

## Inputs
`URIToken`: String - Token to be minted \
`IssuerAddress`: String - Address who is issuing the token \
`DestinationAddress`: String - Address who would own the token \

## Output
`NFTId`: String\
`TxnId`: String

## Implementation details
- Mint an URIToken and make sure the issuer is `issuerAddress` and destination is `destinationAddress`
- Wait for minted transaction to be validated - Do we need that?
- Deduct -> 5% for cosmic + 2 * network fees + 2 XAH reserve for NFT (Remit)
- Transfer the balance to issuer after deducting above amount

## Questions
- Is there any timeout for hooks to finish their execution?
- Can we do all the above steps in one transaction?


## For cosmic backend
- Watch for transactions on chain
- Check if the transactions are for our collection creators
- Check if the transactions was done by our hook
- Update our database with the new information, like NFTId, TxnId, etc
- Keep minting open to other wallets while a specific wallet is minting a specific URIToken
