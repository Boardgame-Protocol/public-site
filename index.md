---
layout: default
title: Boardgame Protocol
---

# Boardgame Protocol

The **Boardgame Protocol** is a JSON-based, extensible communication protocol designed to decouple the **game engine** from its **agents** (either human UIs or AIs). It is transport-agnostic but intended to work over **WebSockets** to support real-time multiplayer gameplay.

---

### 🔑 Key Goals:
- **Interoperability**: Designed to work across any board game by standardizing the way agents interact with the game server.
- **Extensibility**: Easily customizable to suit the specific needs of different games without modifying the core protocol.
- **Consistency**: Ensures that all communication between the game server and agents follows a consistent structure.


---

## ✨ Specifications

- Allow agents and engines to be developed independently.
- Support both human and AI players through the same interface.
- Ensure extensibility for any board game.
- Be fully based on **JSON** and **JSON Schema**, with layered validation.
- Be game-rule agnostic at the protocol level.
- Support real-time interaction using **WebSocket-only** communication.

---

## 🧩 Core Concepts

The protocol introduces a **generic match state** model, inspired by concepts from [boardgame.io](https://boardgame.io/), with support for:

- `phase`: the current high-level stage of the match  
- `turn`: the currently active agent's turn  
- `stage`: a per-agent sub-phase within a turn, allowing parallel or conditional actions

It also introduces the concept of **protocol-level versioning**, as well as optional **game-specific versioning** for the nested game state.

---

## 🧬 Double Protocol and Versioning

The protocol is built with a **two-layer structure**:

- A **generic protocol** that defines common message types and data formats.
- A **game-specific extension** that allows the game to define its unique state and actions, while still adhering to the core protocol.

Both layers have versioning to ensure backward compatibility and smooth upgrades across different versions of the protocol and games.
---

## 🚦 Match Status

The `status` field allows tracking of the lifecycle of a match:

- `waiting`: not all agents have joined yet  
- `started`: gameplay has begun  
- `ended`: the match is over  
- `abandoned`: if one or more agents abandoned the match

---

## 🔐 Authentication (Out of Scope)

Authentication and authorization are **not** handled by the protocol itself at this stage.  
It assumes that agents are already authenticated and authorized by the time they connect to a match.

> 🔸 Match access control, session management, and identity verification are left to the application layer.

---

## 🧠 Extensibility

The protocol is built for extension:

- Add new message types as needed  
- Extend the match state with custom metadata  
- Version changes independently at the protocol and game levels  

---

## 🔗 GitHub Organization

This protocol is maintained by the [Boardgame-Protocol GitHub organization](https://github.com/Boardgame-Protocol), where you’ll find:

- JSON schemas  
- Example games  
- SDKs  
- Tools and documentation  

---

## 📅 Roadmap

- [x] Define base schema structure  
- [ ] Add examples (e.g., Uno, Tic-Tac-Toe)  
- [ ] Create JS SDK for agents  
- [ ] Engine template project  
- [ ] Build UI reference implementation  

---

Feel free to contribute or open issues. Let’s make board game engines modular and interoperable!