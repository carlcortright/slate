# Endpoints


## Get Nonce

```
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

```
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

```
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

```
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

```
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

```
curl "http://api.paradex.io/v2/ticker?market=weth-zrx"
  -H "HTTP_API_KEY: <your-api-key>"
```


```javascript
{
	'version': '2.0'
	'type': 'request', 
	'target': 'ticker', 
	'method': 'GET', 
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

```
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

## List Open Orders

```
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
    'params': [
      'market': 'rep-weth',
    ]

}
```

<b>Access Level:</b> Account Access

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
