```mermaid
graph TB
    %% External Interfaces
    subgraph "User Interface"
        CLI[CLI Commands<br/>gluellm/cli/]
        API[Python API<br/>complete(), embed(), etc.]
    end

    %% Core Components
    subgraph "Core Layer"
        GlueLLM[GlueLLM Client<br/>Main API Class]
        Config[Configuration<br/>Settings & Environment]
        Models[Data Models<br/>Conversation, Prompt, etc.]
    end

    %% Execution Layer
    subgraph "Execution Layer"
        Executors[Executors<br/>SimpleExecutor, AgentExecutor]
        Agents[Agents<br/>GenericAgent, Custom Agents]
        Workflows[Workflows<br/>Pipeline, Iterative, RAG, etc.]
    end

    %% Supporting Services
    subgraph "Supporting Services"
        Embeddings[Embeddings<br/>Vector Generation]
        RateLimit[Rate Limiting<br/>API Key Pools, Algorithms]
        Guardrails[Guardrails<br/>Content Safety]
        Costing[Cost Tracking<br/>Pricing Data]
        Eval[Evaluation<br/>Recording & Metrics]
    end

    %% Infrastructure
    subgraph "Infrastructure"
        Runtime[Runtime<br/>Context, Shutdown]
        Observability[Observability<br/>Logging, Telemetry, Hooks]
        Providers[LLM Providers<br/>OpenAI, Anthropic, xAI]
    end

    %% Data Flow
    CLI --> GlueLLM
    API --> GlueLLM

    GlueLLM --> Config
    GlueLLM --> Models
    GlueLLM --> Executors
    GlueLLM --> Embeddings

    Executors --> Agents
    Executors --> Workflows

    GlueLLM --> RateLimit
    GlueLLM --> Guardrails
    GlueLLM --> Costing
    GlueLLM --> Eval

    GlueLLM --> Runtime
    GlueLLM --> Observability
    GlueLLM --> Providers

    %% Key Relationships
    Workflows -.-> Executors
    Agents -.-> Models
    Embeddings -.-> Providers
    Observability -.-> Runtime

    %% Styling
    classDef core fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef execution fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef support fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef infra fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef interface fill:#fce4ec,stroke:#880e4f,stroke-width:2px

    class CLI,API interface
    class GlueLLM,Config,Models core
    class Executors,Agents,Workflows execution
    class Embeddings,RateLimit,Guardrails,Costing,Eval support
    class Runtime,Observability,Providers infra
```

# GlueLLM Architecture Overview

## Core Architecture

**GlueLLM** is a high-level Python SDK that simplifies working with Large Language Models through a unified, provider-agnostic interface. The architecture follows a layered design with clear separation of concerns.

## Layer Breakdown

### 1. User Interface Layer
- **CLI Commands**: Command-line tools for testing and utilities
- **Python API**: Direct function calls (`complete()`, `embed()`, `structured_complete()`)

### 2. Core Layer
- **GlueLLM Client**: Main orchestration class that coordinates all functionality
- **Configuration**: Global settings management via environment variables and config files
- **Data Models**: Pydantic models for conversations, prompts, embeddings, and results

### 3. Execution Layer
- **Executors**: Different execution strategies (SimpleExecutor for direct calls, AgentExecutor for agent-based execution)
- **Agents**: Reusable agent definitions with system prompts, tools, and behavior
- **Workflows**: Multi-agent orchestration patterns (Pipeline, Iterative Refinement, RAG, Debate, etc.)

### 4. Supporting Services
- **Embeddings**: Vector generation for similarity search and RAG applications
- **Rate Limiting**: API rate limiting with multiple algorithms and key pools
- **Guardrails**: Content safety and input/output validation
- **Cost Tracking**: Automatic cost calculation and monitoring
- **Evaluation**: Request/response recording and performance metrics

### 5. Infrastructure Layer
- **Runtime**: Context management and graceful shutdown handling
- **Observability**: Comprehensive logging, telemetry, and hook system
- **LLM Providers**: Unified interface to OpenAI, Anthropic, xAI, and other providers

## Key Design Principles

1. **Provider Agnostic**: Single API works with multiple LLM providers
2. **Tool Integration**: Automatic tool calling with plain Python functions
3. **Error Resilience**: Built-in retries, rate limiting, and error classification
4. **Structured Outputs**: Pydantic model validation for reliable data extraction
5. **Extensible**: Plugin architecture for custom agents, workflows, and tools
6. **Observable**: Comprehensive logging, metrics, and debugging capabilities

## Data Flow

1. **Request Entry**: Via CLI or Python API calls
2. **Configuration**: Settings loaded and merged with defaults
3. **Execution**: Routed through appropriate executor (simple or agent-based)
4. **Provider Call**: Request sent to configured LLM provider
5. **Tool Execution**: If tools are called, they're executed with full error handling
6. **Response Processing**: Structured output validation and cost tracking
7. **Result Return**: Formatted response with metadata and observability data

## Key Features

- **Automatic Tool Execution**: LLMs can call Python functions as tools
- **Multi-turn Conversations**: Memory management across interactions
- **Batch Processing**: Concurrent processing with rate limiting
- **Streaming Support**: Real-time token streaming with structured output
- **Context Optimization**: Tool message condensing to reduce token usage
- **Dynamic Tool Routing**: Efficient tool selection for large toolsets</content>
<parameter name="filePath">/Users/shashwatsingh/Documents/glue-llm/ARCHITECTURE_DIAGRAM.md