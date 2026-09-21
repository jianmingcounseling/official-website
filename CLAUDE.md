# 漸明諮商所官網 — 專案說明

## 與使用者溝通的原則

- 使用者是網站的**內容負責人**,沒有工程背景。
- 討論以**繁體中文**為準;遇到專業術語或使用者指定其他語言時才例外。
- 每次出現技術術語(例如 branch、commit、merge、push、repository),第一次提到時請用**一句白話**說明,例如:「branch(分支)= 一份獨立的草稿副本,改壞了也不影響正式網站」。
- 回覆保持精簡,先講結果,再講需要使用者決定的事。

## 修改流程(必須遵守)

1. **所有修改一律先建立新分支**,不可直接在 `main`(主線,也就是正式網站的版本)上修改。分支名稱用英文加簡述,例如 `update-about-text`。
2. 在分支上修改並 commit(存成一個版本紀錄)。
3. 請使用者在自己電腦預覽(見下方「本機預覽」),**使用者明確說「可以合併」後**,才把分支合併(merge = 把草稿併入正式版)回 `main`。
4. **未經使用者明確同意,不可 push(上傳)到 GitHub,也不可合併到 `main`。** push 到 `main` 之後網站就會公開更新。
5. 這台電腦的 `git` 不在系統 PATH 中,需使用 SourceTree 內建的 git:`C:\Users\User\AppData\Local\Atlassian\SourceTree\git_local\bin`(PowerShell 中先 `$env:Path += ";C:\Users\User\AppData\Local\Atlassian\SourceTree\git_local\bin"`)。
6. commit 訊息以繁體中文撰寫。

## 各頁面用途與內容

網站是純 HTML/CSS/JavaScript 的靜態網站(每個 .html 檔就是一個網頁,不需要後端或建置工具)。依《漸明品牌內容與社群參與規劃草案》,分為首頁加四大入口。

| 檔案 | 頁面 | 用途 | 目前主要內容 |
|---|---|---|---|
| `index.html` | 首頁 | 第一印象,並引導到四大入口 | 主標「漸漸地,你會看見自己的光」、副標(許明輝先生陪你走過情緒的幽谷…)、「預約諮詢」按鈕、四張入口卡片 |
| `about.html` | 認識我們 | 建立品牌辨識與專業可信度,定稿後少更新 | 關於漸明、我們如何看待心理工作、心理師介紹(目前僅許明輝)、漸明空間、漸明記事(時間軸) |
| `explore.html` | 探索理解 | 心理知識與專業觀點,心理師自願依專長產出 | 心理師觀點(專欄)、常見心理問題(可展開的 Q&A)、Podcast |
| `connect.html` | 參與連結 | 網站與實體活動的交會處 | 本月活動(含報名連結)、活動日曆、活動側記、合作企劃 |
| `services.html` | 心理服務 | 功能導向,協助判斷需求並完成預約 | 我需要諮商嗎、如何開始、如何選心理師、諮商流程、費用與取消規定、預約方式(聯絡資訊與表單) |

其他檔案:`css/style.css`(全站外觀:顏色、字體、間距)、`js/main.js`(手機版選單開關、頁尾年份)、`.gitignore`(告訴 git 哪些檔案不用追蹤)。

**目前狀態**:各頁大部分區塊仍是「待補」佔位文字;地址、電話、Email 尚未填入實際資料;聯絡表單目前**尚未接上任何收信服務**(按送出不會寄出任何東西)。

## 發布方式

- 程式碼放在 GitHub:`https://github.com/jianmingcounseling/official-website`(repository = 專案資料夾的線上備份與版本庫)。
- 專案內沒有 Vercel/Netlify 之類的設定檔,而 `https://jianmingcounseling.github.io/official-website/` 可以正常開啟,因此判斷是 **GitHub Pages**(GitHub 提供的免費靜態網站代管,把 `main` 上的檔案直接變成網站)。發布來源的分支設定需登入 GitHub 的 Settings → Pages 才能確認。
- 上線時間:push 到 `main` 後,GitHub Pages 通常約 **1–3 分鐘**更新(此為一般情況,非本專案實測);更新後若看不到變化,請強制重新整理(Ctrl+F5)。
- 提醒:本機 `main` 若比 `origin/main`(GitHub 上的版本)新,代表有改動尚未上線。

## 本機預覽

這台電腦沒有安裝 Node.js / Python,不能起本機伺服器,但網站是純靜態,不需要:

1. 在檔案總管開啟專案資料夾 `C:\Users\User\JianMing Website\official-website`。
2. 雙擊 `index.html`,會用瀏覽器開啟;頁面之間的連結可直接點擊切換。
3. 修改後在瀏覽器按 F5 重新整理即可看到結果。
4. 若正在某個分支上修改,資料夾內的檔案就是該分支的內容,預覽的就是草稿。

## 還原(改錯了怎麼辦)

先分辨情況(git 每個 commit = 一個可回頭的存檔點):

- **還沒 commit、想放棄某個檔案的修改**:`git restore <檔名>`(把檔案退回上次存檔的樣子,未存檔的修改會消失)。
- **已 commit 在分支上、尚未合併**:直接刪掉該分支即可,正式網站完全不受影響。
- **已合併並上線、想撤回**:用 `git revert <commit 代號>`(產生一個「反向修改」的新版本,歷史紀錄保留,最安全),再經使用者同意後 push。
- 不使用 `git reset --hard`、`git push --force` 這類會抹掉歷史的指令,除非使用者明確要求並已說明後果。
- 也可以用 SourceTree 圖形介面操作以上動作。
