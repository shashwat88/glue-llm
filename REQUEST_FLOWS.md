# GlueLLM Request Flow

## Typical Completion Request Sequence

```mermaid
sequenceDiagram
    participant User
    participant API as api.py
    participant Config as config.py
    participant Executor as executors/
    participant Agent as agents/
    participant Provider as LLM Provider
    participant Tools as Tool Functions
    participant Observ as observability/

    User->>API: complete("Hello", tools=[func])
    API->>Config: Load settings
    Config-->>API: Configuration
    API->>Executor: Create execution context
    Executor->>Agent: Initialize agent
    Agent-->>Executor: Agent ready

    loop Tool Execution Loop
        Executor->>Provider: Send prompt to LLM
        Provider-->>Executor: Response with tool calls
        Executor->>Tools: Execute tool functions
        Tools-->>Executor: Tool results
        Executor->>Observ: Log execution
    end

    Executor->>API: Final response
    API->>Observ: Record metrics/costs
    API-->>User: ExecutionResult
```

## RAG Workflow Sequence

```mermaid
sequenceDiagram
    participant User
    participant Workflow as workflows/rag.py
    participant Retriever as Custom Retriever
    participant Generator as AgentExecutor
    participant Embeddings as embeddings.py
    participant VectorDB as External Vector DB

    User->>Workflow: execute("Query")
    Workflow->>Embeddings: Generate query embedding
    Embeddings-->>Workflow: Query vector
    Workflow->>VectorDB: Similarity search
    VectorDB-->>Workflow: Relevant documents
    Workflow->>Retriever: Format context
    Retriever-->>Workflow: Context chunks
    Workflow->>Generator: Generate with context
    Generator-->>Workflow: Final response
    Workflow-->>User: RAG result
```

## Key Flow Patterns

### 1. Simple Completion
```
User → complete() → GlueLLM → Provider → Response
```

### 2. Completion with Tools
```
User → complete() → GlueLLM → Provider → Tool Calls → Tool Execution → Provider → Response
```

### 3. Agent-Based Execution
```
User → AgentExecutor → Agent → GlueLLM → Provider → Tools → Response
```

### 4. Workflow Execution
```
User → Workflow → Multiple Agents → Executors → Providers → Coordinated Response
```

### 5. Batch Processing
```
User → BatchProcessor → Concurrent Executors → Rate Limiting → Results
```

## Error Handling Flow

```mermaid
sequenceDiagram
    participant API
    participant Retry as Retry Logic
    participant RateLimit as Rate Limiting
    participant Error as Error Classification
    participant Provider

    API->>Provider: Request
    Provider-->>API: Error response

    alt Retriable Error
        API->>Retry: Check retry policy
        Retry->>RateLimit: Check rate limits
        RateLimit-->>Retry: OK to retry
        Retry->>API: Retry request
    else Non-retriable
        API->>Error: Classify error
        Error-->>API: Error type
        API-->>User: Formatted error
    end
```

## Configuration Flow

```mermaid
sequenceDiagram
    participant User
    participant Config
    participant Env as Environment
    participant Defaults

    User->>Config: Request setting
    Config->>Env: Check environment variables
    Env-->>Config: GLUELLM_* values
    Config->>Defaults: Fallback to defaults
    Defaults-->>Config: Default values
    Config-->>User: Resolved configuration
```

## Observability Flow

```mermaid
sequenceDiagram
    participant Component
    participant Hooks as Hook System
    participant Logger as Logging
    participant Telemetry as Telemetry
    participant Storage as Eval Storage

    Component->>Hooks: Pre-execution hook
    Hooks-->>Component: Continue
    Component->>Logger: Log operation start
    Component->>Component: Execute operation
    Component->>Telemetry: Record metrics
    Component->>Storage: Store evaluation data
    Component->>Hooks: Post-execution hook
    Component->>Logger: Log completion
```</content>
<parameter name="filePath">/Users/shashwatsingh/Documents/glue-llm/REQUEST_FLOWS.md