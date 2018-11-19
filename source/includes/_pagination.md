# Pagination

```shell
curl "http://api.paradex.io/v2/orderbook?market=rep-weth&cursor=2018-03-09T02:50:27Z&per_page=75"
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
      'cursor': '2018-03-09T02:50:27Z',
      'per_page': 75
    ]

}
```


Several endpoints on the Paradex API are paginated over both HTTP and websocket. Pagination on Paradex works by ordering all records descending based on when the records were created. This means all orders are returned in the order they were placed on the orderbook etc. 

Each time a request is made to a pagination endpoint, an optional `per_page` and `cursor` can be included. This specifies how many records to include and where in the sequence to start. The maximum page limit for each request is `100` objects. 

When a request is made to one of these endpoints the response will includes a `next_cursor` field. When this cursor is passed to the `cursor` field in the next request it returns the next page. When all of the records have been traversed, the api will return `-1` for the next cursor. If this is passed back into the next request, the API will start from the beginning. 
