# ADR 0001: Model Context Protocol (MCP) Transport Selection — stdio vs. Streamable HTTP / SSE

- **Status:** Accepted
- **Date:** 2026-10-15
- **Context:** Enterprise AI Systems & Tool Integration

---

## Context & Problem Statement

When exposing tools and database query analyzers to LLM clients (such as Claude Desktop, IDE extensions, or custom agent gateways), selecting the correct transport layer dictates security boundaries, latency, and deployment topology.

We need to decide when to use **stdio** versus **Streamable HTTP (with SSE)** for enterprise MCP server implementations.

---

## Decision Drivers

1. **Process Boundary & Security:** Where does the client execute relative to the database/tool credentials?
2. **Network & Multi-Tenancy:** Does the tool serve a single local developer session or shared remote services?
3. **Transport Overhead:** Sub-millisecond IPC requirement vs. HTTP network hop.

---

## Options Considered

1. **`stdio` (Standard Input/Output):** JSON-RPC 2.0 messages over standard process streams (`stdin`/`stdout`).
2. **`Streamable HTTP` / `SSE`:** Network transport over HTTP/HTTPS with event streaming endpoints.

---

## Decision & Rationale

* **Local Developer Workflows:** Use **`stdio`**. Spawns as a child process with zero network overhead (~0ms latency) and stays isolated to the local user session.
* **Remote & Enterprise Deployment:** Use **`Streamable HTTP`**. Required for horizontal scaling, central authentication (Bearer/OAuth), and multi-tenant audit logging.

---

## Consequences

- **Positive:** Clear architectural boundary between local workstation tools (`stdio`) and shared cloud tools (`HTTP`).
- **Negative:** Transport logic must be decoupled using the MCP SDK transport adapter layer to allow effortless protocol swaps.
