# Authentication

The Paradex API has four levels of authentication, public access, basic access, account access, and private key access. Most of the time you will be working with basic access and account access as these protect most of the endpoints. 

### Basic Access

```shell
# Make a request with your api key
curl "http://api.paradex.io/v2/nonce"
  -H "HTTP_API_KEY: <your-api-key>"
```

Basic access is used to any non-account endpoint. To query these endpoints you must include the `HTTP_API_KEY` header on your request that includes an API key generated for your account. Information about generating API keys can be found our our [API key page](https://paradex.io/developers). 

### Account Access

```shell
# First get a secret from the get_secret endpoint
curl "http://api.paradex.io/v2/get_secret"
 --data "nonce=<valid-nonce>"
 -H "HTTP_API_KEY: <your-api-key>"
 -H "HTTP_API_SIG: <payload-signature>"
```

Account access is required for any action that changes or queries the state of your account. We do this to add an extra layer of security to keep your data and trades safe. In order to access endpoints protected by basic access you must first request a secret from the generate secret endpoint. This secret is used to sign any data sent to the Paradex API to verify you are the sender. 

```shell
# Make a request using the secret retreived from the get secret endpoint
curl "http://api.paradex.io/v2/<account-access-endpoint>"
 --data "nonce=<valid-nonce>"
 -H "HTTP_API_KEY: <your-api-key>"
 -H "HTTP_API_SIG: <payload-signature-with-secret>"
```

Once you have your secret key you can use it to authorize requests to account access endpoints. This is done by hashing the packed payload and signing it, including that signature in the `HTTP_API_SIG` header. These signatures are the same as ethereum personal signatures in web3.


