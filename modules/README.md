### Overview
---
Modules are microservices, which implement [lexicons](#lexicons), pinned to them. They are placed inside the NXP Node, get requests, send responses and communicate with each other with help of [dispatcher](/architecture/dispatcher.md).

### Lexicons
---
Lexicon - is a uri, built by rules, dictated by specification. Here is high-level list, exact list of endpoints is listed inside following files:

[**nxp:/chat/***](chat.md)
Module, to provide functionality to private, public, group chats.

[**nxp:/account/***](account.md)
DID-auth, manage access tokens, perform login and register inside the provider.

[**nxp:/didman/***](didman.md)
Module, which allows UI to interact with DID's, extract and manage keys and data.