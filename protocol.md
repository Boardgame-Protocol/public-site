---
layout: default
title: Protocol
permalink: /protocol/
---


# Protocol Overview

This page provides an overview of the **Boardgame Protocol**, with a focus on common use cases and structure. Each message in the protocol must always include these core fields:

- **version**: `"1.0.0"`
- **type**: `"perform_action"`
- **game**: `"game_code"`
- **match_id**: `"abc123"`
- **agent_id**: `"agent_2"`

These fields ensure that the messages remain consistent and structured for communication between game servers and agents.

---

## 1. Getting the State

This section explains how to retrieve the current state of the match.

### Request

To get the current match state, an agent sends a request message:

```json
{
  "version": "1.0.0",
  "type": "get_state",
  "game": "game_code",
  "match_id": "abc123",
  "agent_id": "agent_2"
}
```

### Response
```json
{
  "version": "1.0.0",
  "type": "get_state_response",
  "game": "game_code",
  "match_id": "abc123",
  "agent_id": "agent_2",
  "status": "started",
  "phase": "main",
  "turn": 1,
  "stage": "draw",
  "started_at": "2025-05-05T10:00:00Z",
  "ended_at": null,
  "active_agent_id": "agent_2",
  "agents": [
    { "id": "agent_1", "name": "Agent One", type: "human" },
    { "id": "agent_2", "name": "Agent Two", type: "ai" }
  ],
  "state": {
    "version": "1.0.0",
    "data": {
      "example_property": "example_value"
    }
  }
}
```

## Use Case 2: Perform Custom Action

Here’s an example of how a client sends an action to the server:

### Request

```json
{
  "version": "1.0.0",
  "type": "perform_action",
  "game": "game_code",
  "match_id": "abc123",
  "agent_id": "agent_2",
  "action": {
    "type": "some_action",
    "version": "1.0.0",
    "data": {
      "example_property": "example_value"
    }
  }
}
```

### Response

```json
{
  "version": "1.0.0",
  "type": "perform_action_response",
  "game": "game_code",
  "match_id": "abc123",
  "agent_id": "agent_2",
  "action_response": {
    "status": "success",
    "version": "1.0.0",
    "message": "Action performed successfully",
    "data": {
      "example_property": "example_value"
    }
  }
}
```

## Use Case 4: Async Push Message 

The server would send a response to inform agents of some asyncronous operation has performed.

### Response

```json
{
  "version": "1.0.0",
  "type": "push_message",
  "match_id": "abc123",
  "message_response": {
    "status": "success",
    "version": "1.0.0",
    "message": "Action performed successfully",
    "data": {
      "example_property": "example_value"
    }
  }
}
```