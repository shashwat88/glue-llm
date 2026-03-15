# GlueLLM Architecture Documentation

This directory contains comprehensive architecture documentation for the GlueLLM repository.

## Architecture Diagrams

### 1. [ARCHITECTURE_DIAGRAM.md](ARCHITECTURE_DIAGRAM.md)
Complete Mermaid diagram showing the layered architecture with all major components and their relationships.

### 2. [ARCHITECTURE_OVERVIEW.md](ARCHITECTURE_OVERVIEW.md)
High-level overview with ASCII diagrams and component descriptions.

### 3. [MODULE_ARCHITECTURE.md](MODULE_ARCHITECTURE.md)
Detailed module structure showing the file organization and relationships.

### 4. [REQUEST_FLOWS.md](REQUEST_FLOWS.md)
Sequence diagrams showing how requests flow through the system for different use cases.

## Architecture Summary

GlueLLM is a high-level Python SDK for Large Language Models that provides:

- **Provider-agnostic API** supporting OpenAI, Anthropic, xAI, and others
- **Automatic tool execution** with plain Python functions
- **Structured outputs** using Pydantic models
- **Multi-agent workflows** for complex tasks
- **Built-in error handling** and retries
- **Comprehensive observability** and monitoring

## Key Design Principles

1. **Unified Interface**: Single API regardless of underlying LLM provider
2. **Tool Integration**: Seamless calling of Python functions by LLMs
3. **Error Resilience**: Automatic retries, rate limiting, and error classification
4. **Extensibility**: Plugin architecture for custom agents and workflows
5. **Observability**: Full request tracing, metrics, and debugging
6. **Type Safety**: Pydantic models throughout for reliable data handling

## Core Components

- **API Layer**: Main entry points (`complete()`, `embed()`, `GlueLLM` class)
- **Execution Layer**: Executors, agents, and workflow orchestration
- **Supporting Services**: Embeddings, rate limiting, guardrails, costing
- **Infrastructure**: Runtime management, observability, provider abstraction

## Usage Examples

```python
# Simple completion
result = await complete("What is Python?")

# With tools
def get_weather(city: str) -> str:
    return f"Weather in {city}: 72°F, sunny"

result = await complete("What's the weather in Paris?", tools=[get_weather])

# Agent-based execution
agent = GenericAgent(tools=[get_weather])
executor = AgentExecutor(agent)
result = await executor.execute("Plan my Paris trip")

# RAG workflow
workflow = RAGWorkflow(retriever=my_retriever, generator=executor)
result = await workflow.execute("What does the documentation say about X?")
```

## Architecture Benefits

- **Reduced Boilerplate**: Handles common LLM integration patterns
- **Production Ready**: Built-in error handling, retries, and monitoring
- **Scalable**: Batch processing, rate limiting, and cost tracking
- **Maintainable**: Clear separation of concerns and modular design
- **Extensible**: Easy to add new providers, workflows, and tools</content>
<parameter name="filePath">/Users/shashwatsingh/Documents/glue-llm/ARCHITECTURE_README.md