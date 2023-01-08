# Local Projects node-eventsource-http2 Fork

## Overview

Forked from [capturetechnologies/node-eventsource-http2](https://github.com/capturetechnologies/node-eventsource-http2) with modifications merged from [bobheadlabs/node-eventsource-http2](https://github.com/bobheadlabs/node-eventsource-http2).

## Modifications

Modified to implement a few missing constructor options from the [eventsource](https://github.com/EventSource/eventsource) package on which this library was modeled:

Additional constructor option parameters include:
- `ca: string | Buffer | Array<string | Buffer> | undefined;`  
Pass a certificate to optionally override the trusted CA certificates.

  Example:
  ```ts
  // Specify a trusted certificate authority
  const sse = new EventSource('https://example.com', { ca: fs.readFileSync("./ca.crt") });
  ```

- `rejectUnauthorized: boolean`  
Allow connections even with an invalid certificate . The HTTP2 documentation asserts that this option only applies to servers, but testing indicates that it has an affect on clients as well. This is unsafe and should not be used in production (or possibly ever).

  Example:
  ```ts
  // Connects to servers with self-signed certificates, unsafe in production
  const sse = new EventSource('https://example.com', { rejectUnathorized: false });
  ```

---

## Original Readme:

## why
Eventsource nodejs client https://github.com/EventSource/eventsource
doesn't support http/2.

This package fixes it build on top of `http2`, so it fully supports it

## install
```
npm install node-eventsource-http2
```

## usage

**[Spec](https://developer.mozilla.org/en-US/docs/Web/API/EventSource)**
```js
const EventSource = require('node-eventsource')
const sse = new EventSource('your.endpoint/sse');
sse.addEventListener('type', (event) => {
  // your code goes here
})
```

