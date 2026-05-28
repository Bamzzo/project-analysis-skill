# Agent Project Analysis

Use this reference when the project involves LLMs, agents, tool calling, workflows, automation, multi-agent systems, RAG, computer use, or external action execution.

## Agent-Specific Questions

- What is the agent's goal?
- Is it chat-only, tool-using, workflow-based, autonomous, or human-in-the-loop?
- What model(s) does it call?
- Where are model providers configured?
- How are prompts constructed?
- Where are tools registered?
- How does the agent choose tools?
- Where are tool calls executed?
- What observation is returned to the model?
- How is state/memory stored?
- What stops infinite loops?
- Which actions are read-only vs destructive?
- What requires user confirmation?

## Common Agent Layers

```text
User input
-> Intent/task parsing
-> Planner
-> Tool selection
-> Tool call serialization
-> Executor/router
-> External system/tool
-> Observation/state update
-> Evaluation
-> Replan or finish
```

## Components to Locate

- Model client / adapter
- Prompt templates
- Planner / orchestrator / graph runner
- Tool schema definitions
- Tool registry
- Tool executor
- State store / memory
- Observation builder
- Event stream / callback handling
- Safety checks / approvals
- Evaluation or loop detection
- Logs and traces

## Tool-Calling Contract

For each important tool, capture:

- Tool name
- Description exposed to the model
- Input schema
- Output schema
- Side effects
- Error format
- Required preconditions
- Whether result includes ids needed by later steps
- Whether the tool is safe to retry

## Observation Quality

Good observations should:

- Be structured.
- Include the state change or relevant current state.
- Include stable ids/handles needed for later actions.
- Include warnings.
- Be small enough for the model to use.
- Avoid hiding key data inside huge payloads.

## Agent Failure Modes

- Wrong model/provider route
- Missing API key or base URL
- Prompt does not expose needed tools
- Too many tools exposed at once
- Tool schema too vague
- Tool result lacks next-step ids
- Model loops on same tool
- Model ignores observation
- Executor silently swallows errors
- External action succeeds but observation is stale
- Destructive action lacks preview/approval

## Safety and Control

Look for:

- Read-only vs write tools
- Human approval gates
- Dry-run / preview mode
- Max step limits
- Timeout and retry behavior
- Tool allowlists
- Secret redaction
- Audit logs
- Rollback or checkpoint strategy

## Recommended Output Additions

When analyzing an Agent project, add sections for:

1. Agent Loop
2. Model Routing
3. Tool Registry and Action Space
4. State / Memory / Observation
5. Safety and Human-in-the-Loop
6. Evaluation and Loop Control
7. Agent-Specific Risks
