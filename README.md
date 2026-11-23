# WidelAI for Claude

Ask other AI models from Claude using your [WidelAI](https://www.widelai.com) account. This plugin connects Claude Code to the WidelAI MCP server so Claude can ask Google Gemini, OpenAI GPT, Moonshot Kimi, Zhipu GLM or another Claude model for a second opinion, compare two to four models side by side, and search or continue your WidelAI conversations.

## What it adds

- **MCP connector** `widelai`: a remote server at `https://api.widelai.com/mcp/claude/widelai`.
- **Skill** `second-opinion`: asks another model to review the current plan, diff or answer, then reports where the models agree and disagree.
- **Skill** `widelai`: guidance on which WidelAI tool to use and how to write self-contained prompts.

The plugin contains no executable code, hooks or local servers. It is configuration and Markdown only.

## Requirements

A WidelAI account with an active plan. Each model answer uses WidelAI credits at the per-model rates on [widelai.com/pricing/transparency](https://www.widelai.com/pricing/transparency). Listing models, reading history and checking credits use none.

## Install

```
/plugin marketplace add LushBinary/widelai-claude-plugin
/plugin install widelai@widelai
```

Then run `/mcp`, select `widelai`, and sign in with your WidelAI account. Sign-in uses OAuth 2.1 with PKCE in your browser; WidelAI issues a token that only works for this server, and the plugin stores no credentials.

To use the connector without the plugin:

```
claude mcp add --transport http widelai https://api.widelai.com/mcp/claude/widelai
```

## Try it

- "Get a second opinion from Gemini on this plan."
- "Ask GPT and Kimi to review the diff for bugs and compare what they find."
- "Find my WidelAI chat about the pitch deck and summarize it."
- "How many WidelAI credits do I have left?"

## Tools

| Tool | What it does | Changes data |
| --- | --- | --- |
| `list_models` | Lists the models you can use | No |
| `ask_model` | Sends one prompt to one model and returns its answer | Saves a conversation, uses credits |
| `compare_models` | Sends one prompt to 2 to 4 models in parallel | Saves conversations, uses credits |
| `show_answers` | Displays returned answers side by side | No |
| `search_conversations` | Searches your WidelAI conversations | No |
| `get_conversation` | Reads one WidelAI conversation | No |
| `get_account` | Your credits and plan | No |
| `get_profile` | Which WidelAI account is connected | No |
| `open_widelai` | Recent conversations and an ask box | No |
| `second_opinion` | A panel to pick models and ask them | Only when you send |
| `settings_read` | Your WidelAI defaults | No |
| `settings_update` | Changes your default models | Yes |

## Data handling

- **What is sent:** only what Claude passes to a tool: the prompt for a model, a search query, a conversation id, or a setting. The plugin does not read or send your Claude conversation, memory, files or repository on its own; the `second-opinion` skill tells Claude to include only the plan or diff you are reviewing and to strip secrets first.
- **Where it goes:** to WidelAI's API at `api.widelai.com` (operated by LushBinary), which forwards prompts to the model provider you choose (Google, OpenAI, Moonshot, Zhipu or Anthropic).
- **What is kept:** each answer is saved as a conversation in your WidelAI history until you delete it or your account. See the [privacy policy](https://www.widelai.com/privacy) and [terms](https://www.widelai.com/terms).
- **Disconnect:** run `/mcp` and clear authentication for `widelai`, or uninstall the plugin.

## Support

Documentation: [widelai.com/integrations/claude](https://www.widelai.com/integrations/claude). Help: [widelai.com/contact](https://www.widelai.com/contact) or connect@lushbinary.com.

## License

MIT. See [LICENSE](LICENSE). WidelAI itself is a commercial service governed by its own terms.
