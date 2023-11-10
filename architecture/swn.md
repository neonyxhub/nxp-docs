### Overview

**S**overeign **W**eb **N**ode is main networking unit in Neonyx Node.

On client side, SWN is used to send events from user to network and fetch incoming events from network for further process of delivering this action directly to user interface.

SWN stands for:
- Opening and managing libp2p connections with other SWNs by [multiaddresses](https://docs.libp2p.io/concepts/fundamentals/addressing/)
- Manage [stream multiplexing](https://docs.libp2p.io/concepts/multiplex/overview/) over libp2p connections
- Support [required protocols](#protocols) to build the core of Neonyx Functional Layer.

### Protocols

List of libp2p protocols, supported by SWN additionaly to regular libp2p node.

```/swn/eventbus/%v``` - protocol to exchange events accross p2p network

```/swn/auth/%v``` - protocol to perform challenge-response on SWN network level

### TODO
- [ ] Add API explanation
- [ ] Describe how SWN setup looks like