**Neonyx Protocol Layer**:
- **Services**: Are components, which are hidden from end-user and used as a connector between Neonyx modules.
	- [Sovereign Web Node](/services/swn.md) - main networking unit, part of NXP-node, used to exchange events in p2p layer
	- [Dispatcher](/services/dispatcher.md) - service, which parses Events from SWN and directs it to functional modules or to end-user
	- [Client Web Node](/services/cwn.md) - same as API, mainly is a connection between frontend and p2p layer (with help of SWN)
- **Modules**: Are part of Neonyx messenger ecosystem, it could be chats, voice calls, accounts and other extensions, which build the messenger functionality.

**Neonyx Self Sovereign Identity Layer**:
- DID - Decentralized Identifiers, as described in our contracts [README](https://github.com/neonyxhub/neonyx-contracts/blob/main/src/contracts/did/README.md)

