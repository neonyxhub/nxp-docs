**Neonyx Protocol Layer**:
- **Services**: Are components, which are hidden from end-user and used as a connector between Neonyx modules.
	- Sovereign Web Node - main networking unit, used to exchange events in p2p layer
	- Dispatcher - service, which parses Events from SWN and directs it to functional modules or to end-user
	- Client Web Node - same as API, mainly is a connection between frontend and p2p layer (with help of SWN)
- **Modules**: Are part of Neonyx messenger ecosystem, it could be chats, voice calls, accounts and other extensions, which build the messenger functionality.