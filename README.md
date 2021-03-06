# Sockethub Client

This library handles all the nitty-gritty details of talking to your
[sockethub](http://sockethub.org/).

[![Build Status](https://secure.travis-ci.org/sockethub/sockethub-client.png)](http://travis-ci.org/sockethub/sockethub-client)

## Getting started

Include [sockethub-client.js](https://github.com/nilclass/sockethub-client/raw/master/sockethub-client.js) script:

```html
  <script src="sockethub-client.js"></script>
```

Create a client and wait for the "registered" event to fire:
```javascript

var sockethubClient = SockethubClient.connect({
  host: 'localhost',
  register: {
    secret: '1234567890'
  }
})

sockethubClient.on('registered', function() {
  // done!
  // you can start calling verbs now, such as...

  console.log('ping');
  sockethubClient.ping().then(function() {
    console.log('pong');
  });
});
```

You may also want to set up some error handlers:
```javascript
sockethubClient.on('failed', function() {
  console.error("Connection to sockethub failed!");
});

sockethubClient.on('disconnected', function() {
  console.error("Sockethub got disconnected!");
});
```

for more information, see:
[Quickstart](https://github.com/sockethub/sockethub-client/raw/master/doc/quickstart.md) (FIXME: may be outdated/deprecated)


### Events

Out of the box, `SockethubClient` implements these events:
* `connected` - Fired once the WebSocket connection is established (i.e. socket.onopen has been called)
* `close` - Fired in case the WebSocket connection is closed (i.e. socket.onclose has been called)
* `error` - Fired when the client encounters an error of some sort.
* `message` - Fired when the hub sends a message that isn't associated to a specific request.
* `response` - Fired when the hub sends a message that looks like a response (i.e. has a "rid" attribute), but can't be associated with any known request.


## Using sockethub-client with an AMD loader, such as [RequireJS](requirejs.org)

Currently the AMD module and the simple client are separate code-bases. For more info on using Sockethub with AMD see the doc here: [AMD](https://github.com/sockethub/sockethub-client/raw/master/doc/amd.md)
