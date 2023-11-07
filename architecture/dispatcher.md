### Overview
---
Dispatcher is a distributor of the events from SWN to [modules](/modules/README.md). In our implementation we use message broker [NATS](https://nats.io/), but dispatcher SHOULD be abstract from the used technologies.

Dispatcher responsibilities:
- Get requests from network and deliver to specific module, based on its [lexicon](/modules/README.md)
- Get responses from modules and send them to the network via [SWN](swn.md)
- Allow module-module request-response negotiations, without going outside nxp-node.

### How it works?
---
Dispatcher's role really consist in picking up a pubsub system and converting event uri to topic in this pubsub. So, if you have internal requests, you will only need your local provider message broker. Otherwise, there are cases when you need to use libp2p pubsub or just regular message brokers, but belonging to another provider.

**Incoming requests from network**:
1. Fetching event from network:
	1. SWN connects to specific dispatcher topic inside message broker (SWN and Dispatcher will be connected with both-side streaming).
	2. SWN gets event with ```eventbus``` protocol.
	3. SWN passes event to dispatcher via opened stream in message broker.
2. Distributing event to module:
	1. Dispatcher gets request from message broker
	2. Dispatcher looks on request's uri and decides how to pass request further (by default, it converts uri to topic and sends request to the same message broker). Other options, which require some additional management are: pass request over libp2p pubsub, pass request with external message broker.
3. After dispatcher gave event somewhere, module can take it and process.

**Requests among modules**:
1. Module1 wants to send some request to Module2. This functionality should be hardcoded inside the Module1, because it will need the scheme of request and specify the uri of the request.
2. Module1 packs request, forms the request body and, based on uri, goes to dispatcher and saids that it need to get response to request with specific uri.
3. Dispatcher then gets this request, checks where this module is located (picks needed pubsub) and sends request to specific topic.
	1. If your message broker supports request-response model and Module1 knows about it, it can just use this functionality
	2. If you do not have request-response model in message broker, then, Module1 should add field: ```req_id: uuid```, this should be unique identifier of the request. Now, after sending this request to the network, it then will parse responses and trying to find the responde with same ```req_id``` and will recognize the response to exact request.

**Internal requests among modules**:
it is a simplification of previous section.
- Module1 wants to send request to Module2. If it knows, that Module2 is presented in same local message broker, then it can just send request to required topic directly.
	- How does it know that Module2 is presented at the same provider? You can specify exact URI's that will be asked locally by using config, described in [/module setup guide](modules/setup.md)
	- Also, you can use any other functionality (e.g. hardcode behaviour on module-module requests in your module)

