# Enterprise AI Architecture Patterns 🚀

[![MIT License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Python 3.11+](https://img.shields.io/badge/python-3.11+-blue.svg)](https://www.python.org/)
[![MCP Spec Compliant](https://img.shields.io/badge/MCP-v1.0-orange.svg)](https://modelcontextprotocol.io)

A curated collection of production-grade reference architectures, design patterns, and benchmarks for building resilient, high-throughput AI agent systems and Model Context Protocol (MCP) servers.

Built with a focus on **distributed systems resilience, deterministic state management, and enterprise-grade observability**.

---

## 🏗️ Architecture Matrix & Modules

| Module | Core Technology | Architectural Pattern | Primary Concern Addressed |
| :--- | :--- | :--- | :--- |
| **`01-mcp-enterprise-servers/pg-query-optimizer`** | Python, MCP SDK, PostgreSQL | Agentic Tool Calling | Automated Query Optimization & Schema Analysis |
| **`02-agent-orchestration`** | LangGraph, Redis, FastAPI | Stateful Multi-Agent Loop | Fault-Tolerant Checkpointing & Human-in-the-Loop |
| **`03-hybrid-rag-pipelines`** | Qdrant, BM25, Cohere Rerank | Hybrid Sparse-Dense Retrieval | Hallucination Reduction & Sub-100ms Latency |

---

## 📜 Architecture Decision Records (ADRs)

| ADR | Title | Status | Primary Decision |
| :--- | :--- | :--- | :--- |
| [`0001`](./docs/adrs/0001-mcp-stdio-vs-sse-transport.md) | Model Context Protocol Transport Selection | Accepted | `stdio` for local IPC, Streamable HTTP for cloud/multi-tenant |

---

## 📐 System Architecture Overview

```mermaid
graph TD
    A[Client / Claude / Custom Agent] -->|MCP Protocol - stdio/SSE| B[Enterprise MCP Gateway]
    B --> C{Tool Router & Auth}
    C -->|Query Execution| D[PostgreSQL Read Replica]
    C -->|EXPLAIN ANALYZE| E[Query Plan Analyzer]
    E -->|Index Suggestion| F[Schema Advisory Engine]
    F -->|Structured JSON Response| A
