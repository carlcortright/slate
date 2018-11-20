# Websocket API

```javascript
// Example WS Request
{
    'version': '2.0'
    'type': 'request', 
    'target': 'endpoint', 
    'method': 'GET', 
    'api_key': '<your-api-key>',
    'sig': '<payload-signature>',
    'params': {},
    'message_id': 1, 
}

// Example WS Response
{
    'message_id': 1, 
    'version': '2.0',
    'status_code': '200',
    'content': {//Same as HTTP},
}
```

Our websocket API is a powerful way to trade in real-time. It offers all the same endpoints as HTTP over a secure websocket connection, allowing traders to connect once and send as many requests as they need. Websockets follow the same standards of security as the HTTP API. A websocket request is a HTTP request parameters encoded in JSON. All requests to the Paradex Websocket API are made to the following route:

`api.paradex.io/wsapi/v1`

All websocket requests will include a `type`. This identifies either a wrapped http request or a subscription request to one of our [feeds](https://developers.paradex.io/#feeds). The result will also contain a `type` field, making it easy to filter responses returned over the websocket. 

Security for the websocket API has the same levels as the regular HTTP API, the only difference is how authentication requests are sent. All basic access endpoints still require an API key, except on the websocket API the API key needs to be included in the payload under the name `api_key`. 

Account access request are also similar to the http version. The only difference is that instead of putting the signature in the header, we add the payload signature to the request under the name `sig`. When packing and signing, only pack and sign the params, not any of the other data associated with the message.

Throughout the rest of the documentation we will also be referencing examples for how to make websocket requests to each endpoint. 
