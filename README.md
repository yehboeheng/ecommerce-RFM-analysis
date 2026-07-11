# 電商顧客分群分析 | E-commerce Customer Segmentation (RFM)

**問題：行銷資源有限，該把預算花在哪些客戶身上？**

以 RFM 模型（Recency、Frequency、Monetary）對線上零售顧客進行分群，
並透過 Pareto 分析找出高價值客群，作為行銷資源分配的依據。

## 📊 核心發現 (Core Findings)

- **Pareto 法則驗證**：前 20% 的顧客貢獻了 **77.2%** 的總營收。
- **最佳客戶** 僅佔 25.2% 的顧客人數，卻貢獻了 **69.3%** 的總營收。
- **重點召回** 客群佔 14%，平均購買 4.9 次，是最值得投放召回資源的一群。
- **快流失/已流失** 客群佔 25.9%，平均僅購買 1.3 次，貢獻營收不到 4%。

---

## 🗂️ 顧客分群結果 (Segmentation Results)

| 客群 | 客戶數 | 人數占比 | 營收占比 |
|---|---|---|---|
| 最佳客戶 | 1,481 | 25.2% | 69.3% |
| 穩定回購 | 1,222 | 20.8% | 14.4% |
| 重點召回 | 824 | 14.0% | 9.2% |
| 快流失/已流失 | 1,523 | 25.9% | 3.8% |
| 新客戶 | 443 | 7.5% | 2.2% |
| 有潛力培養 | 385 | 6.5% | 1.2% |

---

## 🛠️ 技術棧 (Tech Stack)

- **Python**：Pandas、NumPy、Matplotlib
- **分析方法**：RFM 模型、Pareto 分析（Lorenz 曲線）
- **視覺化**：Tableau Public

---

## 📈 互動式儀表板 (Interactive Dashboard)

👉 [點此查看 Tableau Dashboard](https://public.tableau.com/app/profile/.25094516/viz/RFMCustomerSegmentationAnalysis_17832676637400/1)

---

## 🔍 分析方法 (Methodology)

1. **資料清理**：篩選 Quantity > 0、Price > 0、Customer ID 非空；排除退貨發票（Invoice 'C'）與測試代碼（StockCode 'TEST'），最終保留 **805,539 筆**交易。
2. **RFM 計算**：以 `max(InvoiceDate) + 1 天` 為快照日，計算 Recency（距最近購買天數）、Frequency（不重複發票數）、Monetary（總消費金額）。
3. **評分**：使用 `pd.qcut` 五分位數評分；Frequency 以 `.rank(method='first')` 處理重複值。
4. **分群**：綜合 RFM 分數，共分為 6 個客群（最佳客戶、穩定回購、重點召回、快流失/已流失、新客戶、有潛力培養）。
