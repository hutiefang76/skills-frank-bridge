# skills-frank-bridge

Frank 的 slash 命令 sub-skills — 让你在 Claude Code / codex / opencode 里用 `/frank:ask:gpt`、`/frank:mem:list` 等命令。

每个子目录是一个独立的 SKILL.md,内部 shell out 到 `frank` CLI(`frank ai ask`、`frank memory list` 等),所以**必须先装 frank**:

```bash
brew install hutiefang76/frank/frank
```

然后用 frank 自己装这些 skill 到三平台:

```bash
frank install frank-bridge           # 主桥, /frank:<provider> 模板触发
frank install frank-ask-gpt          # /frank:ask:gpt — 转发到 codex CLI (gpt-5.5 Plus)
frank install frank-ask-claude       # /frank:ask:claude — 转发到 claude CLI (Opus)
frank install frank-ask-opencode     # /frank:ask:opencode — 转发到 opencode (qwen3.6)
frank install frank-ask-gemini       # /frank:ask:gemini — 转发到 gemini CLI
frank install frank-mem-list         # /frank:mem:list — 列分布式记忆
frank install frank-mem-search       # /frank:mem:search — 语义检索记忆
```

frank 会 git clone 这个仓库到 `~/.frank/cache/<hash>/`,然后 `symlink` 每个子目录到 `~/.{claude,codex,opencode}/skills/<name>/`。

## 这些 skill 长啥样

每个目录就一个 `SKILL.md` (Claude 标准),含 description (触发关键词) + 短 prompt 模板告诉 AI 怎么调 `frank` CLI。零代码、零依赖,只是把"用户的自然语言"翻译成"frank 命令"。

## 为什么单独一个 repo

主仓 [skills-frank](https://github.com/hutiefang76/skills-frank) 是 Rust 代码 + binary 分发。这个仓只放配置文件 (SKILL.md),让 `frank install` 用标准 git+subpath 流程装 — 跟 `frank install nacos-ops` 等其他 skill 走同一条路径,代码统一。

## License

MIT
