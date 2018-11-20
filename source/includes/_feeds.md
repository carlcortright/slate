# Feeds

Included in the Paradex API is a set of powerful feeds for processing trade data for each market, watching the orderbook, and getting a ticker. For each feed once you subscribe you will receive a stream of real-time data from Paradex. 

## Authentication

Authentication for all feeds is the same as normal websocket authentication. The same `api_key` and/or `sig` keys are required in the body of the message depending if the feed is basic or account access. See [websocket authentication](https://developers.paradex.io/#websocket-api) for more details.

## Handling Subscriptions

### New Subscriptions

```javascript
// Subscription
{
    "type": "subscribe",
    "target": "market_trades",
    "params": {
        "marketIds": ["ZRX-WETH", "TACO-BELL", ...]
    }
    "messageId": 123
}
```

All feeds are subscribed to by making a subscribe request. Subscribe request are the same as any other websocket request except the `type` of the request is `subscribe` and the `target` is the feed we are subscribing. 

<aside class="notice">
All feeds time out after 24 hours. If you need to keep the connection open longer, please send a second subscription message.
</aside>

After subscribing to a feed, a message will be returned with the same message id either confirming or listing errors creating the subscription. When subscribing to multiple feeds some subscriptions might be created successfully while others might fail in the same request. It's important for clients to handle this behavior accordingly.

### Unsubscribing

```javascript
// Unsubscribe
{
    "type": "unsubscribe",
    "target": "market_trades",
    "params": {
        "marketIds": ["ZRX-WETH"]
    }
    "messageId": 123
}

// Unsubscribe all
{
    "type": "unsubscribe_all",
    "target": "market_trades",
    "params": {}
    "messageId": 123
}
```

Unsubscribing is similar to making a subscription, the only real difference is the `type` of the message is now either `unsubscribe` or `unsubscribe_all`. Unsubscribe specifies the feeds that we are unsubscribing from and unsubscribe all is a catchall that removes all subscriptions. When using the `unsubscribe` command, specific groups can be included in the parameters (i.e. market ids to unsubscribe from). 

After the unsubscribe command executes the API will return a message with the same id and a key `success: true | false` determining whether the operation was successful. 

### Listing Active Subscriptions

```javascript
{
    "type": "subscriptions",
    "messageId": 123
}
```

Along with subscribe and unsubscribe, we also include a function to list subscriptions. This will return all subscriptions going to the current client making it simple to manage all active subscriptions. This endpoint returns the target key and description for each of the subsciptions. This result is first sorted by the key and then by the description. They type of message being returned is `subscription_result`. 

## Avaliable Feeds

### Ticker

```javascript
{
    "type": "subscribe",
    "target": "ticker",
    'api_key': '<your-api-key>',
    "params": {
        "market": "ZRX-WETH"
    }
    "messageId": 123
}
```

<b>Access Level:</b> Basic Access

Subscribe to the ticker for an individual market or all markets

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market or `all` for all markets

### Orderbook

```javascript
{
    "type": "subscribe",
    "target": "orderbook",
    'api_key': '<your-api-key>',
    "params": {
        "market": "ZRX-WETH"
    }
    "messageId": 123
}
```

<b>Access Level:</b> Basic Access

Subscribe to the orderbook for a given market

Parameter | Options | Description
-------------- | -------------- | --------------
market  | string | symbol of the market

### Account Trades

```javascript
{
    "type": "subscribe",
    "target": "account_trades",
    'api_key': '<your-api-key>',
    'sig': '<payload-signature>',
    "params": {}
    "messageId": 123
}
```

<b>Access Level:</b> Account Access

Subscribe to all of the trades coming from your account. Get updates for when state changes.

Parameters: `None`

### Account Orders

```javascript
{
    "type": "subscribe",
    "target": "account_orders",
    'api_key': '<your-api-key>',
    'sig': '<payload-signature>',
    "params": {}
    "messageId": 123
}
```

<b>Access Level:</b> Account Access

Subscribe to all of the orders coming from your account. Get updates for when state changes.

Parameters: `None`

### Market Trades

```javascript
{
    "type": "unsubscribe",
    "target": "market_trades",
    'api_key': '<your-api-key>',
    'sig': '<payload-signature>',
    "params": {
        "marketIds": ["ZRX-WETH"]
    }
    "messageId": 123
}
```

<b>Access Level:</b> Account Access

Subscribe to all of the trades happening on a market or multiple markets.

Parameter | Options | Description
-------------- | -------------- | --------------
markets  | list(string) | list of markets to subscribe
