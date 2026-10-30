# Avoid Overkill

**Model-agnostic engineering guidance for coding agents.** Deliver the smallest complete solution that meets real requirements, while retaining necessary safeguards and meaningful verification.

Use this skill to avoid **overengineering** during implementation, bug fixes, refactoring, and **code review**. Aim for a **minimal complete solution**, not merely fewer lines of code. It also guides agents to give concise, non-repetitive answers and distinguish reversible implementation choices from decisions that require clarification. The full instructions are in Traditional Chinese, with an English discovery description; they are not tied to a specific model or vendor.

適用於各種 coding agent 的繁體中文技能：避免過度工程，讓實作、修復、重構及程式碼審查的複雜度與需求、契約和實際風險成比例。

## 核心原則

- 完成最小完整方案，不把簡單當成省略需求或必要驗證的理由。
- 新增抽象、依賴、校驗、重試、回退前，必須有具體需求或風險依據。
- 修正根因，沿用既有慣例，不順便擴大重構範圍。
- 保留授權、信任邊界、資料完整性等必要防護。
- 驗證公開行為與實際回歸，不堆疊只照抄實作的測試。
- 需求與必要驗證完成後停止。
- 一次說清楚每項發現，不以表格、逐項展開及總結重複相同內容。
- 低風險可逆細節依慣例繼續；行為、契約或授權不明時才提出必要問題。

完整規則見 [SKILL.md](SKILL.md)。本技能聚焦軟體開發，不處理論文寫作，也不取代專門的安全稽核。

## 使用方式

使用 [Skills CLI](https://github.com/vercel-labs/skills) 從 GitHub 安裝，並依提示選擇目標 agent：

```bash
npx skills add 5Gswatergod/avoid-overkill --skill avoid-overkill
```

此指令預設安裝至目前專案。技能不綁定單一 agent；安裝位置與支援範圍由 Skills CLI 及目標產品決定。

從 [Releases](https://github.com/5Gswatergod/avoid-overkill/releases) 下載 ZIP 並解壓縮，或下載本儲存庫。

| Agent 能力 | 載入方式 |
| --- | --- |
| 支援 `SKILL.md` 技能 | 依該產品的技能安裝方式加入包含 `SKILL.md` 與 `LICENSE` 的資料夾。 |
| 支援專案指令 | 將 `SKILL.md` 正文（不含開頭 YAML 中繼資料）加入既有專案指令；保留原有規則與來源授權。 |
| 只有聊天介面 | 貼上技能正文，再提供程式碼、需求與契約。 |

範例任務：

> 請使用 Avoid Overkill 審查以下程式。僅列出有具體依據的問題與最小必要修正，不修改檔案。

> 請依 Avoid Overkill 完成以下功能，沿用既有慣例，執行與變更直接相關的必要檢查，交代未驗證部分。

## 相容性與能力邊界

技能不綁定模型、供應商、IDE、CLI、MCP 或特定工具名稱，也沒有額外執行依賴。

有工具且已獲授權的 agent 可修改檔案與執行檢查；純對話助理則提供可套用的程式碼與驗證步驟，必須區分建議和已執行工作。所在環境的指令優先序、專案規範與權限仍然適用。

「模型無關」指規則可移植，不代表所有產品共用同一安裝機制，也不保證不同模型的遵循程度相同。本版本未逐一完成所有 coding agent 的實機驗證。

ChatGPT 外掛是另一種平台封裝；本儲存庫提供可獨立使用的通用技能，不需要先安裝 ChatGPT 外掛。

## 驗證

在 v1.1.0 的一次 ChatGPT 外掛對話中，曾觀察到以下四項審查行為符合預期：

| 測試情境 | 預期行為 |
| --- | --- |
| `first(xs)` 誤用 `xs[1]`，輸入契約為 `number[]` | 建議改為 `xs[0]`，空陣列回傳 `undefined`；不新增 Factory 或驗證依賴。 |
| 前端已隱藏管理員按鈕 | 保留後端授權檢查，不將前端當成安全邊界。 |
| 付款逾時且結果不明、沒有冪等鍵 | 不無限重送；先核對交易結果與安全重送條件。 |
| 驗收與必要檢查完成，無具體未解問題 | 停止工作，不新增萬用框架或大量 mock 測試。 |

該回覆亦明確表示未修改檔案、未執行測試、未檢查完整專案。這是有限的對話行為驗證，不是跨模型測試或實際付款系統驗證。可在其他 agent 載入技能後重用這些情境。

v1.2.0 新增規則已做文字與套件檢查，尚未完成模型行為驗收。驗收時可補測以下情境：

- 要求以表格簡短審查三項問題：判斷、理由與建議應集中在表格，不再逐項重述同一內容。
- 已授權修復函式，僅缺內部區域變數命名偏好：沿用附近慣例繼續，不新增確認關卡。
- 同一 API 有兩種互斥的空值行為，契約與文件均未指定：詢問預期行為，再做相依修改。
- 資料遷移未說明是否可刪除現有資料：不推定刪除授權；只繼續不依賴該決定的工作。

## 來源與授權

本版本參考並改寫自 [6Kmfi6HP/avoid-overkill](https://github.com/6Kmfi6HP/avoid-overkill)，不是上游的官方版本。改寫重點包括繁體中文、必要防護、驗證與停止條件，以及跨 agent 的能力邊界。

依 [MIT License](LICENSE) 發布，保留上游版權與授權聲明。
