# Skills

A collection of skills I built. Some are part of the
[LLAssemblyCLI](https://github.com/electronick1/LLAssemblyCLI) workflow, some work standalone.

## Status labels

Every skill carries one of three statuses:

| Status | Meaning |
| --- | --- |
| `draft` | First version. Not well tested — no evals run against it yet. |
| `in-use` | Ready to use day to day, but has not gone through the evaluation process. |
| `stable` | Passed the evaluation process. |

The end goal is for every skill to go through multiple rounds of evals.

## Available skills

| Skill | Description | Blog post | LLAssemblyCLI workflow | Status |
| --- | --- | --- | --- | --- |
| [prompt-confusion-table](skills/prompt-confusion-table/) | Reads the reasoning traces of a run and builds a confusion table: every row pins an exact phrase of the prompt, skill, rule file, tool description or agent definition to the reasoning quote where it cost the model attention, typed and split into artifact-caused and task-caused. | [Mining Qwen3.8 reasoning trace for prompt/skill evaluation](https://olegivye.com/#/article/confusion-evaluation) | false | `in-use` |

## About LLAssemblyCLI

[LLAssemblyCLI](https://github.com/electronick1/LLAssemblyCLI) is a skill for agent orchestration:
it takes a control-flow plan — a Mermaid diagram, Python, pydantic-monty or assembly DSL — and
walks it deterministically, spawning one sub-agent per node, so branches, retries and loops are
decided by the plan instead of improvised by a model each turn. Skills marked `true` in the table
above carry such a plan inside their `SKILL.md`, which LLAssemblyCLI runs exactly as defined in any
dev tool — OpenCode, Claude Code, Codex, Pi or Claude Dynamic Workflows.
