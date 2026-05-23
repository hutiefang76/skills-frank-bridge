---
name: frank-ask-claude
description: '把当前用户问题原话转发给 claude CLI (Pro/Max 订阅 opus 默认), 拿回答原样返回. 触发: 用户输入 "/frank:ask:claude <prompt>", "/frank-ask-claude <prompt>", "ask claude:", "问 claude", "frank 转 claude", "用 opus 看下" 等明确指定要 claude/opus 回答的话.'
---

# frank-ask-claude

用户**明确要 claude / opus 的视角**时, 用 Bash 工具调:

```bash
frank ai ask --to claude --from claude --source-cwd "$PWD" "<用户的 prompt 原话>"
```

**约定**:
- 不修改 prompt
- 模型由 claude CLI 自身配置决定 (用户已配 opus/sonnet/haiku 默认)
- 失败常见原因: `claude` CLI 没登录 (跑 `claude setup-token` 一次)
- prompt 含特殊字符用 heredoc

**变体识别**: 用户说 "用 opus / sonnet / haiku" 时也走这条 — claude CLI 自己路由到对应模型, frank 不动 CLI 参数.

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
