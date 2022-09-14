# Modular Architecture
Below is a high-level description of the modular architecture of Fedimint
## Crates
We should aim to have the following crates:
- `core/api` - database and API encoding/decoding interfaces for the module types (txs, outcomes, consensus items, etc.) shared between the client and server
- `core/client` - client interfaces (creating txs, resolving outcomes, calls api)
- `core/server` - server interfaces (tx validation, consensus logic, serves api)
- `<module>/api` - api implementation (e.g. ln/mint/wallet)
- `<module>/client` - client implementation
- `<module>/server` - server implementation
- `crypto/tbs` - custom threshold cryptography
- `integrationtests` - tests
- `fedimint/server` - wiring the modules together to create a Fedimint server
- `fedimint/client` - wiring the modules together to create a Fedimint client

We separate the `client`, `server`, and `api` crates because:
- Clients need to compile to WASM and cannot use libraries such as `tokio`
- Servers need to minimize dependencies for security
- Clients and servers communicate via the API and share common types

## Module Dependency Tree
