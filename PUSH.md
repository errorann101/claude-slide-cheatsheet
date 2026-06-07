# 如何推到你自己的 GitHub

> 這個環境基於安全不會代你存取權杖，請在你自己的電腦執行以下指令。
> repo 名稱建議：`claude-slide-cheatsheet`（可自訂）。

## 步驟 1：在 GitHub 建立空 repo
到 https://github.com/new 建立新 repo（先不要勾 README）。

## 步驟 2：本機初始化並推送

```bash
cd 這個資料夾
git init
git add README.md PUSH.md .gitignore
git commit -m "用 Claude 做專業簡報懶人包：初版清單"
git branch -M main
git remote add origin https://github.com/<你的帳號>/claude-slide-cheatsheet.git
git push -u origin main
```

## 步驟 3（選用）：要連字型檔一起上傳

字型 OTF 每個約 16MB、6 個約 100MB。直接進 git 會讓 repo 變肥，建議用 **Git LFS**：

```bash
git lfs install
git lfs track "*.otf"
git add .gitattributes fonts/
git commit -m "新增思源黑體 OTF（透過 LFS）"
git push
```

> 若不想裝 LFS，更建議的做法：**不要把字型放進 repo**，改在 README 用 raw 連結讓人自行下載（連結已寫在 README.md 第 1 節）。
> 真要附檔，最乾淨的是把 OTF 當成 **GitHub Release 的附件**上傳，而非塞進原始碼。

## 認證提醒
push 時若要求帳密，密碼欄請貼 **Personal Access Token（PAT）**，不是 GitHub 登入密碼。
PAT 建立位置：GitHub → Settings → Developer settings → Personal access tokens。
