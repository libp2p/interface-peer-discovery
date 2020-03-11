⛔️ DEPRECATED: interface-peer-discovery is now included in [libp2p-interfaces](https://github.com/libp2p/js-interfaces)
======

# interface-peer-discovery

[![](https://img.shields.io/badge/made%20by-Protocol%20Labs-blue.svg?style=flat-square)](http://protocol.ai)
[![](https://img.shields.io/badge/project-libp2p-yellow.svg?style=flat-square)](http://libp2p.io/)
[![](https://img.shields.io/badge/freenode-%23libp2p-yellow.svg?style=flat-square)](http://webchat.freenode.net/?channels=%23libp2p)
[![Discourse posts](https://img.shields.io/discourse/https/discuss.libp2p.io/posts.svg)](https://discuss.libp2p.io)

> A test suite and interface you can use to implement a Peer Discovery module for libp2p.

The primary goal of this module is to enable developers to pick and/or swap their Peer Discovery modules as they see fit for their application, without having to go through shims or compatibility issues. This module and test suite was heavily inspired by [abstract-blob-store](https://github.com/maxogden/abstract-blob-store).

Publishing a test suite as a module lets multiple modules all ensure compatibility since they use the same test suite.

The API is presented with both Node.js and Go primitives, however, there is not actual limitations for it to be extended for any other language, pushing forward the cross compatibility and interop through diferent stacks.

## Lead Maintainer

[Vasco Santos](https://github.com/vasco-santos).

## Modules that implement the interface

- [JavaScript libp2p-mdns](https://github.com/libp2p/js-libp2p-mdns)
- [JavaScript libp2p-bootstrap](https://github.com/libp2p/js-libp2p-bootstrap)
- [JavaScript libp2p-kad-dht](https://github.com/libp2p/js-libp2p-kad-dht)
- [JavaScript libp2p-webrtc-star](https://github.com/libp2p/js-libp2p-webrtc-star)
- [JavaScript libp2p-websocket-star](https://github.com/libp2p/js-libp2p-websocket-star)

Send a PR to add a new one if you happen to find or write one.

## Badge

Include this badge in your readme if you make a new module that uses interface-peer-discovery API.

![](/img/badge.png)

## Usage

### Node.js

Install `interface-discovery` as one of the dependencies of your project and as a test file. Then, using `mocha` (for JavaScript) or a test runner with compatible API, do:

```js
const test = require('interface-discovery')

const common = {
  setup () {
    return YourDiscovery
  },
  teardown () {
    // Clean up any resources created by setup()
  }
}

// use all of the test suits
test(common)
```

## API

A valid (read: that follows this abstraction) Peer Discovery module must implement the following API:

### `start` the service

- `await discovery.start()`

Start the discovery service.

It returns a `Promise`

### `stop` the service

- `await discovery.stop()`

Stop the discovery service.

It returns a `Promise`

### discoverying peers

- `discovery.on('peer', (peerInfo) => {})`

Everytime a peer is discovered by a discovery service, it emmits a `peer` event with the discover peer's [PeerInfo](https://github.com/libp2p/js-peer-info).
