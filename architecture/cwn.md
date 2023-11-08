### Overview
---
**C**lient **W**eb **N**ode - is an API for UI to send regular HTTP requests and use WebSockets to interact with p2p network and providers.
```WARN``` - this is local API, it does all encryptions and stores the keys.

CWN responsibilities:
- Give understandable HTTP API for UI.
- Pack incoming data to Event protobuf structure.
- Send packed Events to SWN to distribute their accross the network.
- Fetch coming events from SWN, decode them and pass to WS.