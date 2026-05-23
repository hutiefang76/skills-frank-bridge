---
name: frank-ask-opencode
description: '把当前用户问题原话转发给 opencode CLI (Go 套餐, 默认 qwen3.6+), 拿回答原样返回. 触发: 用户输入 "/frank:ask:opencode <prompt>", "/frank-ask-opencode <prompt>", "/frank:ask:qwen <prompt>", "ask opencode", "问 qwen", "frank 转 opencode" 等明确指定要 opencode/qwen 回答的话.'
---

# frank-ask-opencode

用户**明确要 opencode / qwen 的视角**时, 用 Bash 工具调:

```bash
frank ai ask --to opencode --from claude --source-cwd "$PWD" "<用户的 prompt 原话>"
```

**约定**:
- 不修改 prompt
- 模型由 opencode CLI 自身配置决定 (用户已订 Go 套餐, 默认 qwen3.6+)
- prompt 含特殊字符用 heredoc

## Model 指定 (可选)

用户在 prompt 里明确说 "用 X 模型" 时, 加 `--model X`. 例:

- "用 haiku 模型告诉我..." → `frank ai ask --to claude --from claude --source-cwd "$PWD" --model haiku "告诉我..."`
- "用 gpt-5.4-mini 问..." → `frank ai ask --to gpt --from claude --source-cwd "$PWD" --model gpt-5.4-mini "..."`
- 没说就**不带** --model, 用 CLI 自家默认.

各家可用 model: 看 Web UI http://127.0.0.1:7780 的 ① CLI ② Model 下拉.
