# 用 Claude 做專業簡報懶人包

> 整理者：鄭翔如 Ann ｜ 給非技術同仁與中高階主管的實用清單
> 目標：在 Claude（claude.ai / Claude Code / Cowork）裡，快速產出中文字體正確、版面專業的簡報、文件與圖表。

---

## 0. 這份懶人包解決什麼問題

AI 產出的 PPTX / SVG / Word 常見三大痛點：

1. **中文變成豆腐字（□□□）或亂套英文字型** → 缺中文字型，或沒指定字族。
2. 版面像「AI 味」很重 → 沒有固定的視覺系統（色票、字級、留白）。
3. 每次都要重講一遍需求 → 沒有把規格沉澱成可重用的 Skill / 範本。

懶人包的核心解法：**先裝好中文字型 → 固定一套視覺規格 → 用一句話下指令重複生成。**

---

## 1. 中文字型：思源黑體（Source Han Sans TC）

簡報能不能「看起來專業」，第一關就是中文字型。推薦 Adobe × Google 開源的**思源黑體**（Google 端名稱為 Noto Sans CJK），免費可商用。

### 1-1 官方來源

| 用途 | 網址 |
| --- | --- |
| 專案首頁 | https://github.com/adobe-fonts/source-han-sans |
| 繁中說明（README-TW） | https://github.com/adobe-fonts/source-han-sans/blob/master/README-TW.md |
| 發行頁（手動下載，最新 2.004R） | https://github.com/adobe-fonts/source-han-sans/releases |

### 1-2 raw 直連網址（指令稿 / 自動化可直接抓）

繁體中文 OTF，把結尾字重換掉即可（`Light` / `Normal` / `Regular` / `Medium` / `Bold` / `Heavy`）：

```
https://raw.githubusercontent.com/adobe-fonts/source-han-sans/release/OTF/TraditionalChinese/SourceHanSansTC-Regular.otf
```

> 註：GitHub Releases 的 zip 實際託管在 `objects.githubusercontent.com`，部分受限環境抓不到；改走 `raw.githubusercontent.com` 直連 OTF 一樣是官方檔。

### 1-3 一鍵安裝（Linux / Claude Code 環境）

```bash
mkdir -p ~/fonts && cd ~/fonts
for w in Light Normal Regular Medium Bold Heavy; do
  curl -sL -o "SourceHanSansTC-$w.otf" \
  "https://raw.githubusercontent.com/adobe-fonts/source-han-sans/release/OTF/TraditionalChinese/SourceHanSansTC-$w.otf"
done
sudo mkdir -p /usr/share/fonts/opentype/source-han-sans
sudo cp SourceHanSansTC-*.otf /usr/share/fonts/opentype/source-han-sans/
sudo fc-cache -f
fc-list | grep -i "source han sans tc"   # 驗證
```

字族名稱（在程式 / 簡報中指定用）：**`Source Han Sans TC`**（中文別名「思源黑體」）。

本 repo 的 `fonts/` 已附 6 個字重 OTF，可直接取用。

---

## 2. 固定一套視覺規格（範例：Ann 教學風）

把「色票 + 字型 + 版面」寫死成一份規格，每次叫 Claude 套用即可，產出才會一致。

| 項目 | 設定 |
| --- | --- |
| 底色 | 白底 |
| 主色（強調） | 橘 `#F05A1A` |
| 深色（標題） | 深藍 `#1E2761` |
| 中文字型 | Source Han Sans TC（思源黑體）/ 微軟正黑體 |
| 頁尾 | 橘色名牌「鄭翔如 Ann」 |

> 你可以把上表換成你自己的品牌色與字型，原則不變：**先定規格，再生成。**

---

## 3. 在 Claude 裡產簡報的三條路

| 工具 | 適合情境 | 產出 |
| --- | --- | --- |
| **claude.ai 對話** | 單份簡報、快速產出 | 直接下載 PPTX / PDF / SVG |
| **Claude Code** | 要自訂字型、跑腳本、批次處理 | 用 pptxgenjs / python-pptx 程式化生成 |
| **Claude Cowork** | 非技術同仁、桌面操作 | 圖形化操作，可掛 Skill |

---

## 4. 進階：把規格沉澱成 Skill

重複性高的簡報，建議做成 **Skill**，下一句「用我的風格做一份關於 X 的簡報」就能重現。

常用做法：
- 把色票、字型、版型寫進 `SKILL.md`
- 附上可重用的 pptxgenjs 元件庫
- 加上輸出前的視覺 QA 檢查清單（中文不爆框、色票一致、頁尾正確）

---

## 5. 快速指令範本（複製即用）

```
請用「思源黑體 / Source Han Sans TC」當中文字型，
白底、橘色 #F05A1A 強調、深藍 #1E2761 標題，
幫我做一份關於【主題】的專業簡報，
每頁含標題 + 3 個重點，頁尾放名牌「鄭翔如 Ann」，
輸出成可下載的 PPTX。
```

---

## 授權

- 思源黑體 / Source Han Sans：SIL Open Font License 1.1（免費商用）。
- 本懶人包文字：自由取用、修改、分享。
