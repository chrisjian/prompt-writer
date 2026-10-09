# Anthropic API Reference

Status: official-source verified 2026-10-09

## Official sources

- https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5
- https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-fable-5-1
- https://platform.claude.com/docs/en/models/fable-5-1/overview
- https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5-5
- https://platform.claude.com/docs/en/models/opus-5-5/overview
- https://platform.claude.com/docs/en/models/opus-5-5/migration-guide

## Claude Opus 5.5

- Model ID: `claude-opus-5-5`. Adaptive thinking is always on; the default effort is `medium`. Tune effort using real workload results, not inherited Opus 5 settings.
- Remove unsupported thinking-disabled and explicit thinking-budget requests on migration; do not use forced tool-choice modes rejected by Opus 5.5.
- Preserved thinking blocks depend on the model and conversation history; keep required blocks intact rather than attempting to repair them with prompt text.
- Progress notes between tool calls are returned as thinking blocks. The default display omits their text; clients that must show updates need the documented `thinking.display` and rendering flow.

## Effort

- Anthropic describes effort as the main intelligence/latency/cost control for Fable 5-family workloads.
- For Fable 5, current guidance uses `high` as a default starting point for many tasks, with higher/lower levels evaluated against the workload rather than assumed better.
- For Fable 5.1, re-evaluate all effort levels on the target task; same-named effort levels do not imply the same amount of thinking across model generations.
- At low effort, Fable 5.1 may call search/retrieval tools less often. For current-fact workflows already configured at low effort, an explicit search trigger can be useful when the harness actually provides such a tool.

## Thinking and conversation state

- Thinking visibility and preserved thinking blocks depend on the supported Anthropic API/harness mechanisms; do not request private chain-of-thought as ordinary response text.
- Fable 5.1 has stricter considerations around preserved thinking and append-only conversation histories. Editing earlier turns can invalidate the expected state/caching behavior.
- Compaction, tool batching, progress-update mechanisms and long-running state are runtime/API features, not abilities created by prompt wording.

## Integration boundary

- Host-managed subagents, memory, async communication and UI progress mechanisms are not guaranteed by the model API alone.
- When runnable integration details are requested, verify the current Anthropic API/model docs for the exact endpoint and supported fields.

## Prompt boundary

Keep model-visible instructions focused on task, scope, completion, style and tool-use behavior. Keep effort values, thinking/history protocol and state-management mechanics in the API/harness configuration.
