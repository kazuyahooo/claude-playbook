# 05. 環境事實與已知地雷

version: 1.0 ｜ last-updated: 2026-07-09 ｜ 本檔內容是**當日實測快照**，環境會變——發現不符時當場更新（L1），每季全面 re-probe（見 docs/04 第 3 節）。

## 環境事實（2026-07-09 實測）

- **平台**：Claude Cowork（桌面版），非 Claude Code。每個 session 獨立，無自動記憶。
- **持久化**：只靠本 repo（使用者手動 push/pull）。outputs 資料夾跨 session 不會被讀。
- **Agent tool**：`model` 參數接受 sonnet/opus/haiku；effort 不可逐次指定。agent types 含 claude、general-purpose、Explore（唯讀搜索）、Plan（規劃）、claude-code-guide（Claude 產品問答）。以 session 系統提示實列為準。
- **已連接可用的 MCP**：Notion（讀寫頁面/資料庫）、Gmail（讀信/草稿/標籤）、Google Drive（讀/建檔）、排程任務、artifacts、session transcript 讀取。
- **未授權（呼叫會失敗）**：engineering plugin 的 atlassian、datadog、linear、notion、slack；GitHub MCP 未連接。要用需使用者先在 connector 設定授權。注意：此處的「notion」是 engineering plugin 內建的另一套 Notion 工具，與上一行**已連接可用**的獨立 Notion MCP 是兩個不同整合，不要混淆。
- **排程任務**：兩個每日任務——Stock daily update（讀 Notion 交易記錄→查價→更新新聞頁與資產配置頁）、Daily learning digest（生成學習內容寫入 Notion＋更新 artifact）。相關 skill：stock-daily-update。
- **shell sandbox**：Ubuntu Linux，每次呼叫獨立（無 cwd/env 延續），用絕對路徑。sandbox 路徑與檔案工具路徑不同（mnt 對映，見 session 系統提示）。
- **網路**：web fetch/search 有網域限制；被擋的內容**禁止**用 curl/python 繞過（平台規則）。

## 已知地雷（教訓清單，格式見 docs/04 第 2 節）

- [2026-07-09] pip install 失敗：以為套件或網路問題 → sandbox 內要加 `--break-system-packages`。（來源：環境文件）
- [2026-07-09] 排程任務每天重查 Notion 歷史推導進度（學習進度、標籤去重 195+、本月快照存在性）→ 應建「狀態摘要區塊」開頭讀結尾寫；此改進屬 L2，**尚未實施**，待使用者同意。（來源：transcript 抽讀）
- [2026-07-09] 股票資料異常會被每日重新發現：VOO 交易均價(571.17)與市價(683.19)差距大待使用者確認；AMD 曾查無可靠收盤價。處理過就在此更新狀態，別再當新發現。（來源：Stock daily update 2026-07-09）
- [2026-07-09] 呼叫未授權 connector 的工具會直接失敗且無法在 session 內走 OAuth → 動手前先確認上方「未授權」清單，缺的請使用者去 connector 設定授權。（來源：本 session）
- [2026-07-09] Cowork 連接資料夾後 CLAUDE.md 是否自動載入未經實測確認 → 若開場行為顯示未載入，請使用者以「先讀 CLAUDE.md 再開始」開頭，並把實測結果更新到本條。（來源：本 session，未驗證）
