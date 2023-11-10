Modules are microservices, which implement [lexicons](#lexicons), pinned to them. They are placed inside the NXP Node, get requests, send responses and communicate with each other with help of [dispatcher](/architecture/dispatcher.md).

### TODO
- [ ] Lexicons Specification, including data and URI standarts

### Lexicons
**Lexicon** - is a RPC, associated with uri, built by rules, dictated by specification.

**URI** schema - ```nxp:// AUTHORITY / path?query```
**Authority** is some identifier, **to whom** you send the request. It can be:
- DID - then you need to resolve DID Document to fetch network address of destination
- PeerID - p2p address of destination, check cash or go to DHT
- NNS - Neonyx Name Service address

Here is high-level list of paths, exact list of endpoints is listed inside following files:

[**/chat/***](chat.md)
Module, to provide functionality to private, public, group chats.

[**/account/***](account.md)
Manage your account inside provider.

[**/nip/***](account.md)
DID-auth, manage access tokens, control your identity/

[**/didman/***](didman.md)
Module, which allows UI to interact with DID's, extract and manage keys and data.