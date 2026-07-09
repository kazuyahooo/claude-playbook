# claude-playbook

wei 的 Claude 工作制度。目的：讓每一個接手的模型（Sonnet / Opus / Haiku）都按同一套經過驗證的規則工作，並把踩過的坑累積下來。

由 Claude Fable 5 於 2026-07-09 建立。規則的權威來自其附帶的理由，不來自建立者——理由失效的規則就該改（見 docs/04）。

## 結構

```
CLAUDE.md              入口路由檔（每個 session 先讀這個）
docs/00-diagnosis.md   本環境三大失效模式與修法（其他檔案的依據）
docs/01-dispatch.md    模型調度守則：何時派 subagent、怎麼派、怎麼驗收
docs/02-judgment.md    判斷 rubric：升級/完成/停下問人/換路/品質底線
docs/03-templates.md   派工 prompt 模板（搜尋/實作/重構/研究/審查）
docs/04-maintenance.md 維護協議＋給未來 session 的交接信
docs/05-environment.md 環境事實與已知地雷（教訓寫回這裡）
PROMPT-revised.md      本制度的建立 prompt 修訂版（留存用）
```

## 部署（使用者 wei 操作，一次性）

1. 在 GitHub 建 repo（如 `claude-playbook`），把本資料夾全部內容 push 上去。
2. 在本機 clone 到固定位置（如 `~/claude-playbook`）。
3. 每次開 Cowork session 時，連接（mount）`~/claude-playbook` 這個資料夾。
4. 若 session 沒有自動載入 CLAUDE.md，第一句話輸入：「先讀 CLAUDE.md 再開始」。

## 更新流程

- 模型在 session 中修改檔案 → 依 docs/04 的權限分級決定是否先問使用者 → session 結尾提醒使用者：「playbook 有更新，記得 push」。
- 使用者 push；下次 session pull 到最新版。
- 注意：Cowork 的 outputs 資料夾不會被下一個 session 自動讀到。持久化**只有**這個 repo 這一條路。

## 已知限制（誠實條款）

這套制度能補的是執行品質：拆解、驗證、多樣本評審。補不了模糊題與品味判斷——遇到時的處理方式寫在 docs/02 第 6 節，選項是：升級模型、要使用者第二意見、或明說做不到。
