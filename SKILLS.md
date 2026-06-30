# lab-drawer Skills Index

## humanizer

移除 AI 寫作模式，讓文字更自然。

- **功能**：偵測 33 種英文 AI 寫作模式 + 6 種中文特有模式，自動替換為自然寫法
- **適用**：Claude Code、OpenCode
- **版本**：3.0.0
- **License**：MIT
- **來源**：https://github.com/wolfgangyu/humanizer

## guardrail

修 CLAUDE.md 的結構病。先問「這段東西真的需要存在嗎？」——能刪就刪，能濃縮成一行就不留三段話。診斷分兩層：結構性問題（dead section、重複規則、過度描述）優先，格式檢查（行數、缺 section）跟進。發現問題會追根究柎，不是只說「太長了」，而是告訴你為什麼會變這麼長、怎麼修最省事。

- **功能**：lazy senior dev 精神的 CLAUDE.md 診斷工具，deletion-first、root-cause 分析
- **適用**：Claude Code
- **版本**：2.0.0
- **License**：MIT
- **來源**：https://github.com/wolfgangyu/project-guardrail

## talk-normal

反廢話 system prompt，讓 LLM 說人話。

- **功能**：注入常駐規則到 AGENTS.md，減少 56-73% 冗長輸出
- **適用**：OpenClaw、Hermes、ChatGPT、Claude、Gemini 等所有支援 system prompt 的 LLM
- **版本**：0.6.3
- **License**：MIT
- **來源**：https://github.com/wolfgangyu/talk-normal
