---
name: widelai
description: Use WidelAI to ask a specific non-default AI model, compare several models on one question, search or continue the user's WidelAI conversations, or check WidelAI credits. Use when the user mentions WidelAI, asks what Gemini, GPT, Kimi or GLM would say, or wants answers from several models side by side.
---

# Using WidelAI

WidelAI gives the user other AI models on their WidelAI account: Google Gemini, OpenAI GPT, Moonshot Kimi, Zhipu GLM and Anthropic Claude models. The `widelai` MCP server exposes them as tools.

## Choosing a tool

| The user wants | Tool |
| --- | --- |
| Which models are available, or an exact model id | `list_models` |
| One model's answer | `ask_model` |
| Two to four models on the same question | `compare_models` |
| To find an earlier WidelAI chat | `search_conversations`, then `get_conversation` |
| To continue a WidelAI chat | `ask_model` with its `conversationId` |
| Credits left or their plan | `get_account` |
| To change their default model | `settings_read`, then `settings_update` |

## Rules

- Each `ask_model` or `compare_models` call uses WidelAI credits. Do not use them to answer questions you can answer yourself.
- Write self-contained prompts. The other models only see the prompt you send, not this conversation or any files.
- Do not send secrets, credentials or private keys in prompts.
- Answers are saved to the user's WidelAI history. Mention the conversation link when one is returned.
- Present other models' answers as theirs. Do not merge them into your own answer without saying which model said what.
