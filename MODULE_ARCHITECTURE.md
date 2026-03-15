# GlueLLM Module Architecture

```
gluellm/
├── api.py                 # Main API (GlueLLM class, complete(), embed())
├── config.py              # Configuration management
├── embeddings.py          # Embedding generation
├── __init__.py            # Package exports
│
├── models/                # Data models
│   ├── agent.py          # Agent definitions
│   ├── conversation.py   # Conversation management
│   ├── embedding.py      # Embedding results
│   ├── prompt.py         # System/user prompts
│   ├── workflow.py       # Workflow configurations
│   └── ...
│
├── executors/            # Execution strategies
│   ├── _base.py         # Base Executor class
│   ├── __init__.py      # SimpleExecutor, AgentExecutor
│   └── ...
│
├── agents/               # Agent implementations
│   ├── generic.py       # GenericAgent class
│   └── ...
│
├── workflows/            # Multi-agent patterns
│   ├── _base.py         # Base Workflow class
│   ├── rag.py           # RAG workflow
│   ├── pipeline.py      # Pipeline workflow
│   ├── iterative.py     # Iterative refinement
│   └── ... (15+ workflow types)
│
├── runtime/              # Execution context
│   ├── context.py       # Correlation IDs, context
│   └── shutdown.py      # Graceful shutdown
│
├── rate_limiting/        # Rate limiting
│   ├── rate_limiter.py  # Rate limiting logic
│   └── api_key_pool.py  # API key management
│
├── observability/        # Monitoring & logging
│   ├── logging_config.py # Logging setup
│   └── logging_utils.py  # Logging utilities
│
├── guardrails/           # Content safety
│   ├── runner.py        # Guardrail execution
│   └── config.py        # Guardrail configuration
│
├── eval/                 # Evaluation & recording
│   ├── store.py         # Base evaluation store
│   ├── jsonl_store.py   # JSONL file storage
│   └── callback_store.py # Callback-based storage
│
├── hooks/                # Extensibility system
│   ├── manager.py       # Hook management
│   └── utils.py         # Hook utilities
│
├── costing/              # Cost tracking
│   ├── cost_tracker.py  # Cost calculation
│   └── pricing_data.py  # Provider pricing
│
├── tool_router.py        # Dynamic tool routing
├── telemetry.py          # Telemetry collection
├── events.py             # Event system
├── provider_params.py    # Provider-specific parameters
├── rate_limit_types.py   # Rate limiting types
├── schema.py             # Data schemas
│
└── cli/                  # Command line interface
    ├── __init__.py
    ├── utils.py
    └── commands/
        └── ...           # CLI commands
```

## Key Module Relationships

### Core Flow
```
User → api.py → executors/ → agents/ → workflows/ → api.py → LLM Providers
```

### Supporting Infrastructure
```
api.py → config.py (settings)
api.py → embeddings.py (vectors)
api.py → rate_limiting/ (quotas)
api.py → guardrails/ (safety)
api.py → costing/ (costs)
api.py → eval/ (recording)
api.py → observability/ (monitoring)
api.py → runtime/ (context)
```

### Data Models
```
models/ ← Used by all modules for type safety and data structure
```

### Extensibility
```
hooks/ ← Pluggable system used throughout for customization
```

## Module Categories

- **API Layer**: `api.py`, `embeddings.py`
- **Configuration**: `config.py`
- **Data Models**: `models/`
- **Execution**: `executors/`, `agents/`, `workflows/`
- **Infrastructure**: `runtime/`, `rate_limiting/`, `observability/`
- **Safety & Quality**: `guardrails/`, `eval/`
- **Business Logic**: `costing/`, `tool_router.py`
- **User Interface**: `cli/`, `__init__.py`</content>
<parameter name="filePath">/Users/shashwatsingh/Documents/glue-llm/MODULE_ARCHITECTURE.md