### Overview
---
Dispatcher is a distributor of the events from SWN to [modules](/modules/README.md). In our implementation we use message broker [NATS](https://nats.io/), but dispatcher SHOULD be abstract from the used technologies.

Dispatcher responsibilities:
- Get requests from network and deliver to specific module, based on its [lexicon](/modules/README.md)
- Get responses from modules and send them to the network via [SWN](swn.md)
- Allow module-module request-response negotiations, without going outside nxp-node.

### How it works?
---
Dispatcher's role really consists in passing events to the destination in face of module. So, our choice by now is regular pubsub and developing something else will be just re-creating message brokers with some upgrades.

**Incoming requests from network:**
1. Fetching event from network:
	1. SWN gets event with ```eventbus``` protocol.
	2. SWN converts its uri to pubsub topic.
	3. SWN passes event to dispatcher via opened stream in message broker.
2. Distributing event to module:
	1. Module is subscribed to required topics, like ```chat.*``` and just fetches all the events.

**Requests among modules:**
1. Module1 wants to send some request to Module2. This functionality should be hardcoded inside the Module1, because it will need the scheme of request and specify the uri of the request.
2. Module1 packs request, forms the request body and, based on uri, goes to dispatcher and saids that it need to get response to request with specific uri.
3. Module2 just takes this request from dispatcher, which is being a pubsub system

**Request-response model:**
If you pick regular pubsub, like Nats, then it has request-response model from source. Another way to support req-resp in such an asynchronous architecture, is to use our routing system:
- Instance1 gets request and need to address it to Instance2. I1 can add some unique ```request_id: uuid``` and store this request locally. Then, it updates request and adds field request_id to it and passes to I2.
- Now, I2 got some request and that I1 waits for the response with id, specified in request_id field.
- I2 processes the request and, again, asynchronously sends response to I1, marking response with same uuid.
- I1 gets response, maps same request_id. Profit!

**External requests among modules:**
Sending requests among different modules is not really currently supported. We focus on this usage in case of apps development, as described in [developers guide](/app-development/README.md)
