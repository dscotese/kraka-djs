Node Kraken
===========

NodeJS Client Library for the Kraken (kraken.com) API

This is an asynchronous node js client for the kraken.com API. It exposes all the API methods found here: https://www.kraken.com/help/api through the ```api``` method.

Please note that when you make more than one API call and correctly set the nonce so that it is always larger than the previous nonce, the requests might arrive to Kraken out of order, which guarantees that Kraken will seen an "Invalid Nonce".  You can fix this by allowing your nonces to go backwards during [a small "Nonce Window"](https://support.kraken.com/hc/en-us/articles/360001148023-What-is-a-nonce-window-), which uses milliseconds as units.  I had to set mine to 5000.

### Installation

```bash
npm install kraka-djs
```

### Example Usage:

```javascript
const key          = '...'; // API Key
const secret       = '...'; // API Private Key
const KrakenClient = require('kraken-api');
const kraken       = new KrakenClient(key, secret);

(async () => {
	// Display user's balance
	console.log(await kraken.api('Balance'));

	// Get Ticker Info
	console.log(await kraken.api('Ticker', { pair : 'XXBTZUSD' }));
})();
```

### Updates:

#### 1.0.3:
- Added CancelOrderBatch to private methods.
- Allows parameter Object to contain a property ctr which is added to the nonce to differentiate same-ms requests.

#### 1.0.2 (Imported):
- Removes any added nonce to prevent reuse [nothingisdead #77](https://github.com/nothingisdead/npm-kraken-api/pull/77)
- Added CancelAll to private methods [nothingisdead #73](https://github.com/nothingisdead/npm-kraken-api/pull/73)

#### 1.0.1 (links here and below are all to nothingisdead's repo):
- Update dependencies
- Update required NodeJS version: [#42](https://github.com/nothingisdead/npm-kraken-api/pull/42)
- Add GetWebSocketsToken private method: [#65](https://github.com/nothingisdead/npm-kraken-api/pull/65)
- Update README: [#44](https://github.com/nothingisdead/npm-kraken-api/pull/44)

#### 1.0.0:

- All methods return a promise.
- The second argument (parameters) can be omitted.
- The third argument to the constructor can be an object (configuration) or a string (OTP), for backwards compatibility.

#### 0.1.0:

The callback passed to the ```api``` function conforms to the Node.js standard of

```javascript
function(error, data) {
	// ...
}
```

Thanks to @tehsenaus and @petermrg for pointing this out.

### Credit:

I used the example php implementation at https://github.com/payward/kraken-api-client and the python implementation at https://github.com/veox/python3-krakenex as references.

BTC donation address: 12X8GyUpfYxEP7sh1QaU4ngWYpzXJByQn5
