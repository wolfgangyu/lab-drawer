# lab-drawer

Wolfgang's collection of Claude Code skills. Each skill is standalone — install all at once or pick and choose.

> Looking for 中文版？ Scroll down to [Chinese version](#lab-drawer（中文版）).

## Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [humanizer](humanizer/) | Removes 33 AI-writing patterns from English text, 39 from Traditional Chinese. | `ln -s $(pwd)/humanizer ~/.claude/skills/humanizer` |
| [guardrail](guardrail/) | Fixes structural rot in CLAUDE.md. Asks "does this need to exist?" first — deletes over edits, collapses over polishes. | `ln -s $(pwd)/guardrail ~/.claude/skills/guardrail` |
| [talk-normal](talk-normal/) | System prompt that reduces LLM verbosity by 56-73%. | `ln -s $(pwd)/talk-normal ~/.claude/skills/talk-normal && cd ~/.claude/skills/talk-normal && bash install.sh` |

## Quick Install All

```bash
git clone https://github.com/wolfgangyu/lab-drawer.git
cd lab-drawer
ln -s $(pwd)/humanizer ~/.claude/skills/humanizer
ln -s $(pwd)/guardrail ~/.claude/skills/guardrail
ln -s $(pwd)/talk-normal ~/.claude/skills/talk-normal
```

## Install Individual Skills

```bash
# humanizer
ln -s $(pwd)/humanizer ~/.claude/skills/humanizer

# guardrail
ln -s $(pwd)/guardrail ~/.claude/skills/guardrail

# talk-normal
ln -s $(pwd)/talk-normal ~/.claude/skills/talk-normal
cd ~/.claude/skills/talk-normal && bash install.sh
```

## License

See each skill's directory for its license.

---

# lab-drawer（中文版）

Wolfgang 的 Claude Code skills 集合。每個 skill 獨立可拆，可以一次安裝全部，也可以單獨下載。

## Skills

| Skill | 說明 | 安裝 |
|-------|------|------|
| [humanizer](humanizer/) | 移除 AI 寫作模式，讓文字更自然。支援英文（33 種模式）和繁體中文（39 種模式）。 | `ln -s $(pwd)/humanizer ~/.claude/skills/humanizer` |
| [guardrail](guardrail/) | 修 CLAUDE.md 的結構病。先問「這段東西真的需要存在嗎？」——能刪就刪，能濃縮成一行就不留三段話。 | `ln -s $(pwd)/guardrail ~/.claude/skills/guardrail` |
| [talk-normal](talk-normal/) | 反廢話 system prompt。讓 LLM 說人話，減少 56-73% 冗長輸出。 | `ln -s $(pwd)/talk-normal ~/.claude/skills/talk-normal && cd ~/.claude/skills/talk-normal && bash install.sh` |

## 快速安裝全部

```bash
git clone https://github.com/wolfgangyu/lab-drawer.git
cd lab-drawer
ln -s $(pwd)/humanizer ~/.claude/skills/humanizer
ln -s $(pwd)/guardrail ~/.claude/skills/guardrail
ln -s $(pwd)/talk-normal ~/.claude/skills/talk-normal
```

## 安裝單一 skill

```bash
# humanizer
ln -s $(pwd)/humanizer ~/.claude/skills/humanizer

# guardrail
ln -s $(pwd)/guardrail ~/.claude/skills/guardrail

# talk-normal
ln -s $(pwd)/talk-normal ~/.claude/skills/talk-normal
cd ~/.claude/skills/talk-normal && bash install.sh
```

## License

每個 skill 的 license 請參考其各自目錄下的說明。
