SWN uses a libp2p node for networking. This document describes SWN features, but for better suggestion we strongly recommend you to refer to [libp2p](libp2p.io)

### SWN communication
---
SWN-SWN communication is based on libp2p handlers, which respond for events exchanging, methods invoking, performing authorizations, etc.

To perform iteractions SWN MUST:
- Know other SWN p2p multiaddr. (in future release DHT support will be added)
- Establish connection (by libp2p rules: [libp2p spec](github.com/libp2p/specs/tree/master/connections))
- Open stream with specified [protocol](../protocol/README.md) 
- Negotiate using this protocol!