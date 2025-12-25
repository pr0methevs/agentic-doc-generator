These are the possible frontmatter fields for a custom agent:

| Field              | Description |
|--------------------|-------------|
| description        | A brief description of the custom agent, shown as placeholder text in the chat input field. |
| name               | The name of the custom agent. If not specified, the file name is used. |
| argument-hint      | Optional hint text shown in the chat input field to guide users on how to interact with the custom agent. |
| tools              | A list of tool or tool set names that are available for this custom agent. Can include built-in tools, tool sets, MCP tools, or tools contributed by extensions. To include all tools of an MCP server, use the `<server name>/*` format. |
| model              | The AI model to use when running the prompt. If not specified, the currently selected model in the model picker is used. |
| infer              | Optional boolean flag to enable use of the custom agent as a subagent (default is true). |
| target             | The target environment or context for the custom agent (`vscode` or `github-copilot`). |
| mcp-servers        | Optional list of Model Context Protocol (MCP) server config JSON to use with custom agents in GitHub Copilot (target: `github-copilot`). |
| handoffs           | Optional list of suggested next actions or prompts to transition between custom agents. Handoff buttons appear as interactive suggestions after a chat response completes. |
| handoffs.label     | The display text shown on the handoff button. |
| handoffs.agent     | The target agent identifier to switch to. |
| handoffs.prompt    | The prompt text to send to the target agent. |
| handoffs.send      | Optional boolean flag to auto-submit the prompt (default is false). |

Here are the list of tools that are available for use in the custom agent:
- https://code.visualstudio.com/docs/copilot/chat/chat-tools
- https://code.visualstudio.com/docs/copilot/reference/copilot-vscode-features#_chat-tools


Here is the definition of subagents :
https://code.visualstudio.com/docs/copilot/chat/chat-sessions#_subagents

they are called "handoffs" in the frontmatter or "#subagents {agent_name}" in the chat

Example Frontmatter that goes at the very top of the each agent file:

```
---
description: Generate an implementation plan
tools: ['search', 'fetch']
handoffs:
  - label: Start Implementation
    agent: implementation
    prompt: Now implement the plan outlined above.
    send: false
---
```