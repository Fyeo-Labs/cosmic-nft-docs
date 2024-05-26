# Hook for minting

## Inputs
URIToken: String - Token to be minted
IssuerAddress: String - Address who is issuing the token
DestinationAddress: String - Address who would own the token

## Output
NFTId: String
TxnId: String

## Implementation details
- Mint an URIToken and make sure the issuer is `issuerAddress` and destination is `destinationAddress`
- Wait for minted transaction to be validated - Do we need that?
- Deduct -> 5% for cosmic + 2 * network fees + 2 XAH reserve for NFT (Remit)
- Transfer the balance to issuer after deducting above amount

## Questions
- Is there any timeout for hooks to finish their execution?
- Can we do all the above steps in one transaction?