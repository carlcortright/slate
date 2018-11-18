# Authentication

The Paradex API has four levels of authentication, public access, basic access, account access, and private key access. Most of the time you will be working with basic access and account access as these protect most of the endpoints. 

### Basic Access

```shell
curl "http://api.paradex.io/v2/nonce"
  -H "HTTP_API_KEY: <your-api-key>"
```

Basic access is used to any non-account endpoint. To query these endpoints you must include the `HTTP_API_KEY` header on your request that includes an API key generated for your account. Information about generating API keys can be found our our [API key page](https://paradex.io/developers). 

### Account Access

```
 # TODO: Curl request that get's secret
```

Account access is required for any action that changes or queries the state of your account. We do this to add an extra layer of security to keep your data and trades safe. In order to access endpoints protected by basic access you must first request a secret from the generate secret endpoint. This secret is used to sign any data sent to the Paradex API to verify you are the sender. 

```
# TODO: Example account access request signature
```

Once you have your secret key you can use it to authorize requests to account access endpoints. This is done by signing a string containing the current nonce and including that signature in the request under the header `paradex_request_sig` along with the `paradex_request_nonce` header so the api knows which nonce was signed. These signatures are the same as ethereum personal signatures in web3 so hopefully no extra imports are necessary in your code.
