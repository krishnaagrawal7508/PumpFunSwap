# PumpFunSwap

A simple and easy to use API to create transactions on pump.fun AMM.

## 📝 API Usage

### Endpoint
POST https://pumpfundex.onrender.com/api/buy - Buy a token on pump.fun AMM

GET https://pumpfundex.onrender.com/health - Check health of server

### Request Body
```javascript
{
    "amount": 1,                    // Amount in SOL
    "slippage": 0.01,               // Slippage percentage, for eg: (0.01 = 1%)
    "tokenMint": "token_address",   // Token mint address
    "walletAddress": "wallet",      // Buyer's wallet address
    "rpcUrl": "rpc_url"             // RPC URL to use
}
```

### Response
```json
{
    "success": true,
    "serializedTransaction": "base64_encoded_transaction"
}
```

### Example Usage

```javascript
// Create transaction
const response = await fetch('https://pumpfundex.onrender.com/api/buy', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        amount: "1000000",
        tokenMint: "token_address",
        walletAddress: "wallet",
        rpcUrl: "rpc_url"
    })
});

const { serializedTransaction } = await response.json();

// On client side:
const bufferData = Buffer.from(serializedTransaction, "base64");
const transaction = Transaction.from(bufferData);

// Sign and send
transaction.sign(userKeypair);
const txHash = await sendAndConfirmTransaction(
    connection, 
    transaction, 
    [userKeypair],
    { 
        skipPreflight: true, 
        preflightCommitment: 'confirmed' 
    }
);
```
## 📚 Error Responses

```json
{
    "success": false,
    "error": "Error message"
}
```
## 💰 Fees
- 1% fee on the buy amount is included in each buy transaction
- Fee is calculated based on the buy amount

## 📜 License

MIT License

## 🔗 Contact

- Twitter: [KrsnaAgr](https://x.com/KrsnaAgr)
- Telegram: [krishna123agrawal](https://t.me/krishna123agrawal)
