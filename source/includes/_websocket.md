# Websocket API

```javascript
// Example WS Request
{
    'version': '2.0'
    'type': 'request', 
    'target': 'endpoint', 
    'method': 'GET', 
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

Our websocket API is a powerful way to trade in real-time. It offers all the same endpoints as HTTP over a secure websocket connection, allowing traders to connect once and send as many requests as they need. Websockets follow the same standards of security as the HTTP API. A websocket request is a HTTP request parameters encoded in JSON. 

Security for the websocket API is the same as the regular HTTP API, the only difference is how authentication requests are sent. 

```
TODO: Document security for WS
```
