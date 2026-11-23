---
name: second-opinion
description: Get a second opinion from another AI model (Gemini, GPT, Kimi, GLM or another Claude model) on the current plan, design, diff or answer through the user's WidelAI account. Use when the user asks for a second opinion, a cross-check, another model's review, or to compare what different models think.
---

# Second opinion with WidelAI

Use the `widelai` MCP tools to ask other models to review work from this session. Every model call uses the user's WidelAI credits, so only ask when the user wants another model's view.

## Steps

1. Decide what to review: the plan you just wrote, a diff (`git diff`, or the files the user names), an error and your proposed fix, or an answer you gave.
2. Pick models. If the user named some, call `list_models` and match the names to exact ids. If they did not, use one strong model from a provider other than Anthropic (for example the newest Gemini or GPT model) for a single opinion, or two or three different providers for a comparison.
3. Write one self-contained prompt. The other models cannot see this conversation or the repository, so include:
   - the goal in one or two sentences,
   - the material itself (plan text, diff or code excerpt; trim unrelated files and keep it under about 15,000 characters),
   - what you want back, for example "List concrete bugs, risks and missing cases, most serious first. Say 'no issues' if there are none."
   Never include secrets, credentials, `.env` contents or tokens. Strip them from diffs before sending.
4. Call `ask_model` for one model or `compare_models` for two to four.
5. Report back:
   - what each model flagged, merged and de-duplicated,
   - where they agree or disagree with each other and with you,
   - which points you think are valid and what you would change, before changing anything.
   Link the saved WidelAI conversation when the tool returns one.

## Notes

- If the tools ask the user to sign in, tell them to run `/mcp`, select `widelai` and authenticate.
- If a model fails or the account is out of credits, say so plainly and continue with the answers you did get.
