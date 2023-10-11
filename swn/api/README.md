### Overview
---
SWN is a networking service and it still needs reasons to exist. That is why there is a way to pass and receive events from Neonyx network using the gRPC API.

Methods above speak about event distribution.
### How to pass events
---
Use method below taken from swn bus api. It opens a client-side streaming, where you need just to specify the destination for SWN and it will do all the networking stuff.
```protobuf
rpc LocalDistributeEvents(stream Event) returns (StreamEventsResponse) {};
```

### How to collect events
---
Use method below taken from swn bus api. Opens a server-side streaming, giving the requester all the events, coming from the p2p network. 
```protobuf
rpc LocalFunnelEvents(ListenEventsRequest) returns (stream Event) {};
```

### TODO:
- [ ] Add some SWN managment as an example and enrich the API description