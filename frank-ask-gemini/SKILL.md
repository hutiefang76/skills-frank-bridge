---
name: frank-ask-gemini
description: '把当前用户问题原话转发给 gemini CLI (Google), 拿回答原样返回. 触发: 用户输入 "/frank:ask:gemini <prompt>", "/frank-ask-gemini <prompt>", "/frank:ask:google <prompt>", "ask gemini", "问 google", "frank 转 gemini" 等明确指定要 gemini/google 回答的话.'
---

# frank-ask-gemini

用户**明确要 gemini / google 的视角**时, 用 Bash 工具调:

```bash
frank ai ask --to gemini --from claude --source-cwd "$PWD" "<用户的 prompt 原话>"
```

**约定**: 不修改 prompt, 模型由 gemini CLI 自配置, prompt 含特殊字符 heredoc.

## Model 指定 (可选)

用户在 prompt 里明确说 "用 X 模型" 时, 加 `--model X`. 例:

- "用 haiku 模型告诉我..." → `frank ai ask --to claude --from claude --source-cwd "$PWD" --model haiku "告诉我..."`
- "用 gpt-5.4-mini 问..." → `frank ai ask --to gpt --from claude --source-cwd "$PWD" --model gpt-5.4-mini "..."`
- 没说就**不带** --model, 用 CLI 自家默认.

各家可用 model: 看 Web UI http://127.0.0.1:7780 的 ① CLI ② Model 下拉.
