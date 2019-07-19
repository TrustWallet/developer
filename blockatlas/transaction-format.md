# Formats

## Transactions

### Base

`id` - transaction hash

```
{
   "id": "12345678"
   "from": "123",
   "to": "123",
   "fee": "1234"
   "coin": 60,
   "block": 1
}

```

### Transfer

Type: `transfer`

```
{
   "type": "transfer",
   "metadata: {
       "name": "Viktor Coin",
       "symbol": "VIK",
       "decimals": 18,
       "value": "12312312"
   }
}
```

### Token Transfer

Type: `token_transfer`

```
{
   "type": "token_transfer",
   "metadata: {
       "name": "Viktor Coin",
       "symbol": "VIK",
       "token_id" : "0x123",
       "decimals": 18,
       "value": "12312312",
       "from": "123",
       "to": "123",
   }
}
```

### Native Token Transfer

Type: `native_token_transfer`

```
{
   "type": "native_token_transfer",
   "metadata: {
       "name": "Bittorent",
       "symbol": "BTT",
       "token_id" : "1002000",
       "decimals": 8,
       "value": "12312312"
   }
}
```

### Collectible Transfer

Type: `collectible_transfer`

```
{
   "type": "collectible_transfer",
   "metadata: {
       "name": "Viktor Kittie",
       "contract" : "0x123",
       "image_url": "https://google.com/img.png",
       "from": "0x123",
       "to": "0x123",
   }
}
```

### Token Swap

Type: `token_swap`

```
{
   "type": "token_swap"
   "metadata: {
       "input" : {
           "coin": 60,
           "token_id": "0x123" - optional
           "symbol": "BNB",
           "value": "123",
           "decimals": 8,
       },
       "output": {
           "coin": 60,
           "token_id": "0x123" - optional
           "symbol": "BTT",
           "value": "123",
           "decimals": 8,
       }
   }
}
```

### Any Action

Type: `any_action`

```
{
    "type": "any_action",
    "metadata": {
       "coin": 60,  
       "title": "Place Order",
       "key":  "place_order",     
       "token_id": "0x123" - optional
       "name": "Viktor Coin",
       "symbol": "VIK",
       "decimals": 18,
       "value": "12312312"
    }
}
```

#### Keys

- `place_order` - Placer Order
- `cancel_order` - Cancel order
- `issue_token` - Issue Token
- `burn_token` - Burn Token
- `mint_token` - Mint Token
- `approve_token` - Approve Token

will continue... Keys mostly used to provide localized version on the clients by key

#### Transaction Status
- `completed` - completed and settled in the ledger
- `pending` - pending in the mempool
- `error` - smart contract failed to execute transaction or failed for any reason in the ledger

## Staking

### Validators

```json
{
   "rank": 1,
   "name":"Polychain Labs",
   "description":"Secure staking with Polychain Labs, the most experienced institutional grade staking team.",
   "status":"online/offline",
   "uptime": 100,
   "rate": 0.2,
   "address":"cosmos14k4pzckkre6uxxyd2lnhnpp8sngys9m6jtwwnd",
   "operator_address":"cosmosvaloper14k4pzckkre6uxxyd2lnhnpp8sngys9m6hl6ml7",
   "pubkey":"cosmosvalconspub1zcjduepquhlqdhjw4qp2c2t6qh5z7tfk52qc72623f0etc8f3n7hy8uuh25ql34fvu",
   "info": {
      "website":"https://google.com",
      "image":"https://google.com/placeholder.png"
   },
}
```

