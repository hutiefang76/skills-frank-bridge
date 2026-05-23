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

## 共享上下文 (v0.8+, 可选)

用户**明确指代上一次问答**时, 加 `--context-from default`:
- "review 下刚才的代码" → `frank ai ask --to gpt --from claude --source-cwd "$PWD" --context-from default "review 下刚才的代码"`
- "那段还有什么改进空间" → 同上,加 `--context-from default`
- "继续上次的讨论" → 同上
- 没指代就**不加**, 避免污染独立问题的上下文.

加 `--context-from <tag>` 后, frank 自动: ask 前查 memory top-3 相关注入前缀; ask 完异步存 Q+A 到 memory. 跨 agent 共享 (同 tag scope), claude 写代码 codex review 真能拿到上下文.
