# Endpoints


## Get Nonce

```shell
curl "http://api.paradex.io/v2/nonce"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'nonce', 
	'method': 'GET', 
	'id': 1,
  'api_key': '<your-api-key>' 
}
```

<b>Access Level:</b> Basic Access

Gets the current nonce associated with the API key. Used for debugging nonce-related issues.

<aside class="notice">
The recommended nonce is a unix timestamp at the current moment the request is sent. 
</aside>

### HTTP Request 

`GET http://api.paradex.io/v2/nonce`

### Query Parameters

None

### Returns

<pre class="center-column-code">
{
  'nonce': your-nonce
}
</pre>

## Get Order Expiration Times

```shell
curl "http://api.paradex.io/v2/expirations"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'expirations', 
	'method': 'GET', 
	'id': 1,
  'api_key': '<your-api-key>'
}
```

<b>Access Level:</b> Basic Access

Gets the order expiration times min and max.

### HTTP Request 

`GET http://api.paradex.io/v2/expirations` 

### Query Parameters

None

### Returns


<pre class="center-column-code">
{
  'minExpirationMinutes': min-expiration,
  'maxExpirationMinutes': max-expiration
}
</pre>

## Get Tokens

```shell
curl "http://api.paradex.io/v2/tokens"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'tokens', 
	'method': 'GET', 
	'id': 1, 
  'api_key': '<your-api-key>'
}
```

<b>Access Level:</b> Basic Access

Get all of the tokens listed on paradex. Returns a list of objects with the name symbol and address of each token

### HTTP Request 

`GET http://api.paradex.io/v2/tokens` 

### Query Parameters

None

### Returns

<pre class="center-column-code">
[
  {
    name: 'Wrapped Ether',
    symbol: 'WETH',
    address: '0xd0a1e359811322d97991e03f863a0c30c2cf029c'
  },
  ...
]
</pre>

## Get Markets

```shell
curl "http://api.paradex.io/v2/markets"
  -H "HTTP_API_KEY: <your-api-key>"
```

```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'markets', 
	'method': 'GET', 
	'id': 1, 
  'api_key': '<your-api-key>'
}
```

<b>Access Level:</b> Basic Access

Get all of the markets listed on paradex. Returns a list of markets and their key parameters.

### HTTP Request 

`GET http://api.paradex.io/v2/markets` 

### Query Parameters

None

### Returns

<pre class="center-column-code">
[
  {
    id: '1',
    symbol: 'ZRX/WETH',
    baseToken: 'ZRX',
    quoteToken: 'WETH',
    minOrderSize: '0.001',
    maxOrderSize: '10000',
    priceMaxDecimals: 5,
    amountMaxDecimals: 6
  },
  ...
]
</pre>

## Get OHLCV

```shell
curl "http://api.paradex.io/v2/ohlcv?market=weth-zrx&period=1d&amount=100"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'ohlcv', 
	'method': 'GET', 
	'id': 1, 
  'api_key': '<your-api-key>',
    'params': [
      'market': 'weth-zrx',
      'period': '1d',
      'amount': 100
    ]

}
```

<b>Access Level:</b> Basic Access

Get open, high, low, close, and volume data for a market. 

### HTTP Request 

`GET http://api.paradex.io/v2/ohlcv` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market
period  | '1m' '5m' '15m' '1h' '6h' '1d' | time period to fetch ohlcv data
amount  | int | how many candles to be returned

### Returns

<pre class="center-column-code">
[
  {
    id: '1',
    symbol: 'ZRX/WETH',
    baseToken: 'ZRX',
    quoteToken: 'WETH',
    minOrderSize: '0.001',
    maxOrderSize: '10000',
    priceMaxDecimals: 5,
    amountMaxDecimals: 6
  },
  ...
]
</pre>


## Get Ticker Snapshot

```shell
curl "http://api.paradex.io/v2/ticker?market=weth-zrx"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'ticker', 
	'method': 'GET', 
  'api_key': '<your-api-key>',
	'id': 1, 
    'params': [
      'market': 'weth-zrx',
    ]
}
```

<b>Access Level:</b> Basic Access

Gets a ticker snapshot of the specified market 

### HTTP Request 

`GET http://api.paradex.io/v2/ticker` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Returns

<pre class="center-column-code">
{
  'bid': '0.004',
  'ask': '0.005',
  'last': '0.0045'
}
</pre>

## View Orderbook

```shell
curl "http://api.paradex.io/v2/orderbook?market=rep-weth"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'orderbook', 
	'method': 'GET', 
	'id': 1, 
  'api_key': '<your-api-key>',
    'params': [
      'market': 'rep-weth',
    ]

}
```

<b>Access Level:</b> Basic Access

Gets a snapshot of the order book of the given market

### HTTP Request 

`GET http://api.paradex.io/v2/orderbook` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Returns

<pre class="center-column-code">
{
    marketId: 1,
    marketSymbol: 'REP-WETH',
    bids:[
        { amount: '300', price: '0.004' },
        { amount: '440', price: '0.003' },
        { amount: '500', price: '0.002' },
        ...
    ],
    asks:[
        { amount: '200', price: '0.005' },
        { amount: '360', price: '0.006' },
        { amount: '445', price: '0.007' },
        ...
    ]
}
</pre>

## Trade History

```shell
curl "http://api.paradex.io/v2/trade_history?market=rep-weth"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'trade_history', 
	'method': 'GET', 
	'id': 1, 
  'api_key': '<your-api-key>',
    'params': [
      'market': 'REP-WETH',
    ]

}
```

<b>Access Level:</b> Basic Access

Get the trade history of a market

### HTTP Request 

`GET http://api.paradex.io/v2/trade_history` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Returns

<pre class="center-column-code">
{
	'id': 1, 
  'version': '2.0',
	'result': [
      {
            id: 2, 
            state: 'pending',
            type: 'buy'|'sell',
            amount: '10.236319460000000000',
            price: '0.073249280000000000',
            baseToken: 'REP',
            quoteToken: 'ETH',
            txHash: None,
            createdAt: "2018-03-09T02:50:27Z"
            completedAt: None,
            baseFee: '',
            tradingFee: '',
            netAmount: '10.236319460000000000',
            priceAdjustments: []
        },
      ...
    ]
}

</pre>


## List Orders

```shell
curl "http://api.paradex.io/v2/orders"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'orders', 
	'method': 'POST', 
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
	'id': 1, 
    'params': [
      'market': 'rep-weth',
      'state': 'all'
    ]

}
```

<b>Access Level:</b> Account Access

List orders for your account based on market and order state

### HTTP Request 

`GET http://api.paradex.io/v2/orders` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market
state |  'all' 'unknown' 'open' 'expired' 'filled' 'unfunded' 'cancelled' | order state

### Returns

<pre class="center-column-code">
[
    {
        orderParams: {
            ...
        },
        id: 3423,
        price: '0.078',
        amount: '100',
        type: 'buy'|'sell',
        market: 'REP/WETH',
        orderHash: 'b41664ebbb46b42fbf32fdce8be3c8df66f354a93dd272e62421e4573a8945d8',
        state: 'unknown'|'open'|'expired'|'filled'|'unfunded'|'cancelled',
        amountRemaining: '75',
        closedAt: None,
        expiresAt: '2017-11-01T21:24:20Z'
    },
    ...
]
</pre>

## Get Order by ID

```shell
curl "http://api.paradex.io/v2/get_order/<order-id>"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'get_order/<order_id>', 
	'method': 'POST', 
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
	'id': 1, 
    'params': [
      'market': 'REP-WETH'
      'state': 'all'
    ]

}
```

<b>Access Level:</b> Account Access

Get an order by its ID

### HTTP Request 

`GET http://api.paradex.io/v2/get_order` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market
state |  'all' 'unknown' 'open' 'expired' 'filled' 'unfunded' 'cancelled' | order state

### Returns

<pre class="center-column-code">
[
    {
        orderParams: {
            ...
        },
        id: 3423,
        price: '0.078',
        amount: '100',
        type: 'buy'|'sell',
        market: 'REP-WETH',
        orderHash: 'b41664ebbb46b42fbf32fdce8be3c8df66f354a93dd272e62421e4573a8945d8',
        state: 'unknown'|'open'|'expired'|'filled'|'unfunded'|'cancelled',
        amountRemaining: '75',
        closedAt: None,
        expiresAt: '2017-11-01T21:24:20Z'
    },
    ...
]
</pre>

## List Order Trades

```shell
curl "http://api.paradex.io/v2/get_order/<order-id>/trades"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'get_order/<order_id>/trades', 
	'method': 'POST', 
	'id': 1,
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
  'params': []
}
```

<b>Access Level:</b> Account Access

List all of the trades associated with a given order

### HTTP Request 

`GET http://api.paradex.io/v2/get_order` 

### Query Parameters

None

### Returns

<pre class="center-column-code">
[
    {
        id: 1, 
        state: 'confirmed',
        type: 'buy'|'sell',
        amount: '0.011986460000000000', 
        price: '0.073249280000000000', 
        market: 'REP-WETH'
        txHash: '0x1234567891234567891234567890000',
        completedAt: '2017-11-14T23:15:18Z',
        baseFee: '',
        tradingFee: '',
        netAmount: '0.011986460000000000',
        priceAdjustments: [
            {
                id: 2, 
                state: 'pending', 
                token: 'REP', 
                amount: '2.000000000000000000', 
                completedAt: None, 
                txHash: '0x234',
                feeAdjustment: '0E-18',
                netAmount: '2.000000000000000000'
            },
            ...
        ]
    }
]
</pre>

## List My Trades

```shell
curl "http://api.paradex.io/v2/get_trades"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'get_trades', 
	'method': 'POST', 
	'id': 1,
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
  'params': [
    'market': 'REP-WETH'
  ]
}
```

<b>Access Level:</b> Account Access

Get all of the trades associated with an API key on a given market

### HTTP Request 

`GET http://api.paradex.io/v2/get_trades` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Returns

<pre class="center-column-code">
[
  {
      id: 1, 
      state: 'confirmed',
      type: 'buy'|'sell',
      amount: '0.011986460000000000', 
      price: '0.073249280000000000', 
      market: 'REP-WETH', 
      txHash: '0x1234567891234567891234567890000',
      createdAt: "2018-03-09T02:50:27Z"
      completedAt: '2017-11-14T23:15:18Z',
      baseFee: '',
      tradingFee: '',
      netAmount: '0.011986460000000000',
      priceAdjustments: [
        {
            id: 2, 
            state: 'pending', 
            token: 'REP', 
            amount: '2.000000000000000000', 
            completedAt: None, 
            txHash: '0x234'
            feeAdjustment: '0E-18',
            netAmount: '12.000000000000000000'
        },
        ...
    ]
  },
  ...
]
</pre>

## Balances

```shell
curl "http://api.paradex.io/v2/balances"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'balances', 
	'method': 'POST', 
	'id': 1,
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
  'params': []
}
```

<b>Access Level:</b> Account Access

Get all of the token balances associated with an API key

### HTTP Request 

`GET http://api.paradex.io/v2/balances` 

### Query Parameters

None

### Returns

<pre class="center-column-code">
[
    {
        id: 1
        name: 'REP'
        symbol: 'REP'
        balance: '1234'
        allowance: '1201'
    }
    ...
]
</pre>

## Get Order Parameters

```shell
curl "http://api.paradex.io/v2/order_params"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'order_params', 
	'method': 'POST', 
	'id': 1,
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
  'params': [
    'market': 'REP-WETH',
    'orderType': 'buy',
    'price': 0.1
    'amount': 10
    'expirationDate': '2017-11-14T23:15:18Z'
  ]
}
```

<b>Access Level:</b> Account Access

Get parameters for a zrx order to be signed

### HTTP Request 

`GET http://api.paradex.io/v2/order_params` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market
orderType | 'buy' 'sell' | type of order
price | float | price in quote currency
amount | float | amount of base currency
expirationDate | ISO 8601 time | expiration date and time of order

### Returns

<pre class="center-column-code">
{
  fee: { 
      id: 'b046140686d052fff581f63f8136cce1',
      baseFeeDecimal: '1.697552694864903098033668128',
      tradingFeeDecimal: '21.21940868581128872542085161',
      secundsUntilPrune: 60,
      pruneUnixTimeStamp: 2017-11-21T18:00:00Z
  },
  zrxOrder: {
      exchangeContractAddress: '0x12459c951127e0c374ff9105dda097662a027093',
      expirationUnixTimestampSec: '1518124088',
      feeRecipient: '0x0000000000000000000000000000000000000000',
      maker: '0x9e56625509c2f60af937f23b7b532600390e8c8b',
      makerFee: '0',
      makerTokenAddress: '0xef7fff64389b814a946f3e92105513705ca6b990',
      makerTokenAmount: '22000000000000000',
      salt: '54515451557974875123697849345751275676157243756715784155226239582178',
      taker: '0xa2b31dacf30a9c50ca473337c01d8a201ae33e32',
      takerFee: '0',
      takerTokenAddress: '0x323b5d4c32345ced77393b3530b1eed0f346429d',
      takerTokenAmount: '10000000000000000',
  }
}

</pre>


## Place an Order

```shell
curl "http://api.paradex.io/v2/order"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'order', 
	'method': 'POST', 
	'id': 1,
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
  'params': [
    'order': { signed zrx order }
  ]
}
```

<b>Access Level:</b> Account Access

Submit a signed order to the orderbook

### HTTP Request 

`GET http://api.paradex.io/v2/order` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
order  | signed zrx order | signed order to place on the orderbook

### Returns

<pre class="center-column-code">
{
	'id': 1, 
  'version': '2.0',
	'result': {
      'status': True,
      'id': 23425
	}
}
</pre>

## Cancel Orders

```shell
curl "http://api.paradex.io/v2/cancel_orders"
  -X POST
  -H "Content-Type: application/json"
  -H "HTTP_API_KEY: <your-api-key>"
  -H "HTTP_API_SIG: <payload-signature>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'cancel_orders', 
	'method': 'POST', 
	'id': 1,
  'api_key': '<your-api-key>',
  'sig': '<payload-signature>',
  'params': [
    'all': true
  ]
}
```

<b>Access Level:</b> Account Access

Cancel either all orders, orders based on market, or by id

### HTTP Request 

`GET http://api.paradex.io/v2/cancel_orders` 

### Query Parameters

Parameter | Options | Description
-------------- | -------------- | --------------
all  | boolean (optional) | cancel all orders
markets | list(market_ids) | list of market symbols to cancel all orders for 
orderIds | list(order_ids) | order ids to cancel

### Returns

<pre class="center-column-code">
{
	'id': 1, 
  'version': '2.0',
	'result': { 'cancelled': [1,2...] }
}
</pre>

