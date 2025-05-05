---
layout: default
title: Boardgame Protocol
---

# Boardgame Protocol

The **Boardgame Protocol** is a JSON-based, extensible communication protocol designed to decouple the **game engine** from its **agents** (either human UIs or AIs). It is transport-agnostic but intended to work over **WebSockets** to support real-time multiplayer gameplay.

---

## ✨ Goals

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

## 📦 Protocol Message Types

1. `get_state`: request the current state of the match  
2. `perform_action`: submit an action from an agent  
3. `action_response`: acknowledge a valid action  
4. `push_event`: async updates for non-active agents  
5. `error`: in case of malformed input or invalid actions  

---

## 🧱 Match State Structure

A match state includes the following fields:

- `version`: protocol version
- `game`: identifier of the game type (e.g., "uno", "chess")
- `match_id`: unique identifier for the match
- `status`: match status (e.g., `waiting`, `started`, `ended`)
- `phase`, `turn`, `stage`: progress tracking
- `started_at`: timestamp when the match started
- `active_agent_id`: ID of the agent currently taking their turn
- `agents`: list of participating agents with metadata
- `state`: contains a `data` object that holds the game-specific state

> 🔹 The `version` field refers to the protocol schema, not the game logic. Game-specific state may carry its own version inside `state.data` if needed.

---

## 🧬 Schema Design

Schemas are organized into **two levels**:

1. **Protocol schema**: shared across all games, defines structure of messages and generic match state  
2. **Game-specific schema**: defines structure of the `state.data` object, actions, and rules  

This allows validation of both the protocol-level structure and the game logic independently.

---

## 🚦 Match Status

The `status` field allows tracking of the lifecycle of a match:

- `waiting`: not all agents have joined yet  
- `started`: gameplay has begun  
- `ended`: the match is over  

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