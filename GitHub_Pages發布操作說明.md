# AI啟程 GitHub Pages 發布操作說明

## 目前壓縮版內容

此資料夾已可作為 GitHub Pages 靜態網站根目錄：

```text
index.html
AI啟程_漫畫閱讀器.html
漫畫版內容/
.nojekyll
README.md
```

目前容量：
- WebP 圖片：270 張，約 109 MB
- PDF：17 份，約 99 MB
- 總容量：約 208 MB
- 最大單檔：約 7.95 MB

這個大小比原始版約 870 MB 小很多，比較適合放到 GitHub Pages。

## 方案 A：使用 GitHub 網頁操作

適合不想安裝 GitHub CLI 的情況。

1. 到 GitHub 建立新 repository。
2. 建議 repository 名稱：

```text
ai-comic-reader
```

3. 設定 repository 為 Public。
4. 上傳本資料夾內全部檔案。
5. 到 repository 的 `Settings` -> `Pages`。
6. Source 選擇 `Deploy from a branch`。
7. Branch 選擇 `main`，Folder 選擇 `/root`。
8. 儲存後等待 GitHub Pages 建置完成。
9. 取得網址，通常會像：

```text
https://你的GitHub帳號.github.io/ai-comic-reader/
```

## 方案 B：使用 Git + GitHub CLI

目前你的電腦已有：

```text
git
winget
python
node
```

目前尚未安裝：

```text
gh
```

如果要讓 Codex 協助建立 GitHub repo 並推送，建議先安裝 GitHub CLI：

```powershell
winget install --id GitHub.cli
```

安裝後登入：

```powershell
gh auth login
```

登入完成後，在本資料夾執行：

```powershell
git init
git add .
git commit -m "Publish AI comic reader"
gh repo create ai-comic-reader --public --source . --remote origin --push
gh api repos/:owner/ai-comic-reader/pages -X POST -f source.branch=main -f source.path=/
```

如果 GitHub Pages 已存在，最後一行可能會回報已建立，屬正常情況。

## 方案 C：Codex 協助操作

Codex 可以協助：
- 安裝 GitHub CLI
- 初始化 Git
- 建立 commit
- 建立 GitHub repo
- 推送到 GitHub
- 啟用 GitHub Pages

但需要你配合：
1. 同意安裝 `GitHub CLI`。
2. 在瀏覽器或 CLI 中完成 GitHub 登入。
3. 確認 repository 名稱、公開/私人設定。

建議 repository：

```text
ai-comic-reader
```

建議設定：
- Public repository
- GitHub Pages 從 `main` branch `/root` 發布

## 注意事項

- GitHub Pages 適合靜態網站，不需要後端伺服器。
- 檔案名稱含中文通常可以運作，但網址會自動轉成編碼；目前 HTML 使用相對路徑，正常情況可讀取。
- 如果未來要給大量外部人員觀看，建議再做更小的圖片版本，或改用 Cloudflare Pages / Netlify / 正式主機。
