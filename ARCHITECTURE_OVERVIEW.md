# GlueLLM Architecture Components

## High-Level Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                    User Applications                        │
│  ┌─────────────────────────────────────────────────────┐    │
│  │                GlueLLM Python API                  │    │
│  │  ┌─────────────────────────────────────────────┐   │    │
│  │  │            GlueLLM Client (Main)           │   │    │
│  │  │  ┌─────────┬─────────┬─────────┬─────────┐  │   │    │
│  │  │  │ Config  │ Models  │Executors│Workflows│  │   │    │
│  │  │  └─────────┴─────────┴─────────┴─────────┘  │   │    │
│  │  └─────────────────────────────────────────────┘   │    │
│  └─────────────────────────────────────────────────────┘    │
└─────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────┐
│                 Supporting Services                         │
│  ┌─────────┬─────────┬─────────┬─────────┬─────────┐        │
│  │Embeddings│RateLimit│Guardrails│ Costing │  Eval  │        │
│  └─────────┴─────────┴─────────┴─────────┴─────────┘        │
└─────────────────────────────────────────────────────────────┘
                                   │
                                   ▼
┌─────────────────────────────────────────────────────────────┐
│                   Infrastructure Layer                       │
│  ┌─────────┬─────────┬─────────┬─────────┐                  │
│  │ Runtime │Observ-  │  CLI   │Providers│                  │
│  │         │ ability │         │(OpenAI, │                  │
│  │         │         │         │Anthropic│                  │
│  │         │         │         │  xAI)   │                  │
│  └─────────┴─────────┴─────────┴─────────┘                  │
└─────────────────────────────────────────────────────────────┘
```

## Component Relationships

### Core Components
- **GlueLLM Client**: Central orchestrator that coordinates all functionality
- **Configuration**: Manages settings from environment variables, config files, and defaults
- **Models**: Data structures for conversations, prompts, embeddings, and results
- **Executors**: Execution strategies (SimpleExecutor, AgentExecutor)
- **Agents**: Reusable agent definitions with prompts and tools
- **Workflows**: Multi-agent orchestration patterns

### Supporting Services
- **Embeddings**: Vector generation for RAG and similarity search
- **Rate Limiting**: Prevents API quota exhaustion with various algorithms
- **Guardrails**: Content safety and input/output validation
- **Cost Tracking**: Monitors API usage costs
- **Evaluation**: Records interactions for analysis and improvement

### Infrastructure
- **Runtime**: Manages execution context and graceful shutdown
- **Observability**: Logging, telemetry, and hook system for monitoring
- **CLI**: Command-line interface for testing and utilities
- **Providers**: Abstraction layer over different LLM APIs

## Data Flow Example

```
User Request → GlueLLM Client → Configuration → Executor → Agent → LLM Provider
                      ↓              ↓          ↓        ↓
                 Tool Execution ← Rate Limiting ← Guardrails ← Observability
                      ↓              ↓          ↓        ↓
                 Result Processing ← Cost Tracking ← Evaluation ← Logging
```

## Key Design Patterns

1. **Provider Agnostic**: Single API works with multiple LLM providers
2. **Tool Calling**: Automatic execution of Python functions by LLMs
3. **Structured Output**: Pydantic validation for reliable data extraction
4. **Error Resilience**: Comprehensive retry and error handling
5. **Extensibility**: Plugin architecture for custom components
6. **Observability**: Full request tracing and metrics collection</content>
<parameter name="filePath">/Users/shashwatsingh/Documents/glue-llm/ARCHITECTURE_OVERVIEW.md