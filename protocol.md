---
title: Protocol
permalink: /protocol/
nav_order: 2
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
  "agent_id": "agent_2",
  "state": {
    "version:: "1.0.0"
  }
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
    { "id": "agent_1", "name": "Agent One", "type": "human" },
    { "id": "agent_2", "name": "Agent Two", "type": "ai" }
  ],
  "state": {
    "version": "1.0.0",
    "data": {
      "example_property": "example_value"
    }
  }
}
```

## Perform Custom Action

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
    "version": "1.0.0",
    "type": "some_action",
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
    "version": "1.0.0",
    "status": "success",
    "message": "Action performed successfully",
    "data": {
      "example_property": "example_value"
    }
  }
}
```

## Async Push Message 

The server would send a response to inform agents of some asyncronous operation has performed.

### Response

```json
{
  "version": "1.0.0",
  "type": "push_message",
  "game": "game_code",
  "match_id": "abc123",
  "agent_id": "agent_2",
  "message_response": {
    "version": "1.0.0",
    "message": "Agent 1 drew a card",
    "data": {
      "example_property": "example_value"
    }
  }
}
```

## Error Response

The server would send a response to inform agents that some errors occurred.

### Response

```json
{
  "version": "1.0.0",
  "type": "error",
  "game": "game_code",
  "match_id": "abc123",
  "agent_id": "agent_2",
  "error": {
    "version": "1.0.0",
    "message": "Unauthorized action",
    "data": {
      "example_property": "example_value"
    }
  }
}
```
