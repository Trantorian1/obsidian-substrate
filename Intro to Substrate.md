> 📚 **Substrate** is a *modular blockchain library* used as a ready-made base to deploy custom nodes or chains.

Substrate guarantees it's flexibility through the use of it's FRAME libraries.

> ⚠️ Do not think of Substrate in analogy to linear program execution. Do not even think of it in term of a `main` program execution structure! Substrate is much closer to a DSL / Domain-Specific-Framework: it is best though of in terms of interoperable modules which communicate with each other to achieve multiple functionalities, such as block signing and creation, consensus mechanisms, p2p... When trying to modify a part of Deoxys, do not look for a single unified source of execution, but rather for the module providing that functionality.

---
## Architecture

Substrate splits it's architecture into two main components components:

- **a core client**, which handles network and blockchain infrastructure events.
- **a runtime**, responsible for handling the blockchain mutation logic, such as transactions, votes...

> 💡Substrate's runtime is compiled to [webassembly](https://webassembly.org/) and directly hosted on-chain. This allows for a single source of truth which can easily be updated, as an alternative to more traditional forks on a blockchain.

![Substrate Architecture](https://docs.substrate.io/static/dae77f7ece855ad265b5c93651f4881b/5c636/libraries.avif)

---
# FRAME

> 📚 The **F**ramework for **R**untime **A**ggregation of **M**odularized **E**ntities is a set of Substrate libraries used to define the runtime and transactions functionality

FRAMES are compose of pre-built modules, or *pallets*, which each represent a specific set of functionalities, such as adding cryptocurrency or voting support.\

---
# Naming conventions: 

> ℹ️ Substrate libraries use a naming convention to indicate whether a library is part of the Substrate core client, FRAME and the runtime, or a Substrate primitive.

| naming convention | belongs to            |
| ----------------- | --------------------- |
| `sc_*`            | Substrate core client |
| `frame_*`         | FRAME                 |
| `pallet_*`        | Substrate runtime     |
| `sp_*`                  | Substrate primitive                      |
