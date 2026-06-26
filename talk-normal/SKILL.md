---
name: talk-normal
slug: talk-normal
description: 讓任何 LLM 說人話。一段精煉的 system prompt，把囉嗦、客服腔的輸出減少 56-73%（已測量），同時保留所有有用資訊。雙語支援（英文 + 中文）。安裝到你的 AGENTS.md 作為常駐行為modifier。
version: 0.6.3
tags: [prompt, anti-slop, concise, system-prompt, chinese, bilingual, always-on]
homepage: https://github.com/wolfgangyu/talk-normal
license: MIT
---

# talk-normal

一段精煉的 system prompt，讓你的 LLM 不要再寫得像 LinkedIn 貼文。已測量：在 GPT-4o-mini 上減少 73% 字元數，GPT-5.4 上減少 72%，跨 10 個中英文提示詞，不遺漏任何有用資訊。

## 這個 skill 做什麼

安裝一次後，talk-normal 的規則會被注入你的 `AGENTS.md`，成為常駐的行為modifier。之後你的 agent 每次回覆都會遵循 `prompt.md` 裡的規則。這不是每次對話都要呼叫的 workflow skill——它是讓你永遠少一點廢話的一次性安裝工具。

## 如何安裝

在当前工作區安裝或更新 talk-normal：

```bash
bash install.sh
```

這個腳本是冪等的：重複執行只會替換 `AGENTS.md` 中已有的 talk-normal 區塊，不會碰到其他內容。

卸載：

```bash
bash install.sh --uninstall
```

## 安裝了什麼

`prompt.md` 的內容會被注入你的 `AGENTS.md`。規則針對讓 LLM 輸出變得囉嗦、客服腔的具體模式：

- **填充詞和假客套** — 禁止開場白（"Great question"、"讓我們一起來看看"），不重複問題
- **結構紀律** — 先給答案，深度匹配複雜度，只在內容真正平行時用列表
- **結尾模式** — 沒有「一句話總結」、沒有假性後續選項、沒有條件式菜單
- **修辭口癖** — 禁止「不是X，而是Y」的否定對比句式、禁止白話重述
- **比較的形狀** — 給建議加簡短理由，限制正反比較條數，不寫平衡式論文

確切規則列表在 `prompt.md` 中，每次提交都是消滅一個新的廢話模式。

## 更新到最新版本

```bash
bash install.sh
```

重新執行安裝器即可替換為最新規則。

## 相容性

適用於所有支援 system prompt 或自訂指示的 LLM：GPT-5.4、GPT-4o-mini、Claude 4.6、Gemini 2.5、Qwen 3、DeepSeek V3 等。OpenClaw 的整合透過 `AGENTS.md` 注入實現，agent 每次對話都會讀取。

## 測量效果

10 個提示詞的完整基準測試（temperature=0，按字元數統計）在 [TEST_RESULTS.md](TEST_RESULTS.md)。GPT-4o-mini 平均減少 73%，GPT-5.4 平均減少 72%，同時保留所有有用資訊。

## 規則迭代

每條規則都透過真實 LLM 輸出的漏網案例迭代。每次在實際使用中發現的規則漏洞都會記錄在 [regressions/](https://github.com/wolfgangyu/talk-normal/tree/main/regressions) 中，追蹤各版本的漏網次數、修復方式和觸發迭代的真實 LLM 輸出。

## Upstream 和貢獻

- 原始來源：https://github.com/hexiecs/talk-normal
- 問題和規則建議：https://github.com/wolfgangyu/talk-normal/issues
- 貢獻方式：參見 [CONTRIBUTING.md](CONTRIBUTING.md)

## License

MIT
