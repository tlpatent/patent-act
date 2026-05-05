# 專利法閱讀器 · 部署指南（GitHub + Cloudflare Pages）

把這個閱讀器變成一個有網址的網頁，大約 15 分鐘完成。

---

## 📦 這個資料夾裡有什麼

```
deploy/
├── index.html      ← 主程式（370+ KB,包含全部條文、樣式、邏輯)
├── _headers        ← 安全設定檔(部署時自動套用)
└── README.md       ← 這份指南
```

部署後 README.md 可以保留也可以刪除,不影響網頁運作。

---

## 🚀 部署步驟總覽

1. **註冊 GitHub 帳號**(5 分鐘)
2. **把這三個檔案上傳到 GitHub**(5 分鐘)
3. **連到 Cloudflare Pages 自動部署**(5 分鐘)

---

## 階段 1:註冊 GitHub

1. 打開 <https://github.com>
2. 點右上角 **Sign up**
3. 填 Email、Password、Username(建議用簡單英文,例如 `tlpatent`,這會出現在網址中)
4. 完成 Email 驗證
5. 選 **Free** 方案
6. 看到首頁就完成了

---

## 階段 2:上傳檔案到 GitHub

### 2-1. 建立 Repository

1. GitHub 首頁點綠色 **Create repository** 按鈕
2. **Repository name**:`patent-act`
3. 選 **Public**(Cloudflare Pages 免費版才支援連 Public repo)
4. 其他選項全部不勾,點最下面 **Create repository**

### 2-2. 上傳三個檔案

1. 進到剛建立的 repository 頁面,找到並點 **uploading an existing file** 連結
2. **打開您的 deploy 資料夾**
3. **全選三個檔案**(index.html、_headers、README.md),**一起拖**到網頁的虛線框
   - ⚠️ 是拖**檔案**,不是拖整個資料夾
4. 滾到下方點綠色 **Commit changes** 按鈕
5. 看到三個檔案都在 repository 中即完成

記下您的 repository 網址,例如 `https://github.com/您的username/patent-act`

---

## 階段 3:連 Cloudflare Pages

### 3-1. 註冊 Cloudflare

1. 打開 <https://dash.cloudflare.com/sign-up>
2. 填 Email + Password 註冊
3. 完成 Email 驗證

### 3-2. 建立 Pages 專案

1. 登入後,左側選單點 **Workers & Pages**
2. 點 **Create application** → 切到 **Pages** 分頁 → 點 **Connect to Git**
3. 點 **GitHub** 圖示授權
4. GitHub 問「Where do you want to install Cloudflare Pages?」→ 選 **Only select repositories**
5. 下拉選您的 `patent-act` repository
6. 點 **Install & Authorize**

### 3-3. 設定部署參數

回到 Cloudflare 頁面後:

1. 選 `patent-act` repository
2. 點 **Begin setup**
3. **Project name**:可改成 `tlp-patent`(會變成網址前綴 `tlp-patent.pages.dev`)
4. **Production branch**:保持 `main`
5. **Build settings**:⚠️ 重要!
   - **Framework preset**:選 **None**
   - **Build command**:**留空**
   - **Build output directory**:**留空**
6. 點 **Save and Deploy**

### 3-4. 等部署完成

約 30 秒~1 分鐘,看到「Success! Your project is deployed.」就完成了。

Cloudflare 會給您一個網址,例如:

```
https://tlp-patent.pages.dev
```

---

## 🔐 預設密碼

**`tlpatent`**

第一次打開網頁,輸入此密碼即可進入。

⚠️ **請務必改掉預設密碼**,下面有完整步驟。

---

## 🔄 之後更新工具的方法

到您的 GitHub repository 編輯檔案,Cloudflare Pages 會**自動偵測並重新部署**。

**改檔案的步驟**:
1. 到 `github.com/您的username/patent-act`
2. 點要改的檔案(例如 `index.html`)
3. 點右上角的鉛筆圖示 ✏️
4. 編輯內容
5. 滾到最下方點 **Commit changes**
6. 等 1 分鐘,Cloudflare 自動重新部署

---

## 🔐 改密碼的具體步驟

### Step 1:產生新密碼的 SHA-256 雜湊

打開 <https://emn178.github.io/online-tools/sha256.html>

在輸入框打您的新密碼(例如 `tlp2026!`),下方會立刻顯示 64 個字元的雜湊值,**整串複製**。

### Step 2:在 GitHub 編輯 index.html

1. 到您的 repository
2. 點 **index.html**
3. 點右上角鉛筆圖示 ✏️
4. 用瀏覽器的尋找(Ctrl+F 或 Cmd+F)搜尋:
   ```
   36eae33544d7f9e4eaac31615a0377c865cd23ca21eb4e91dccd667540d02953
   ```
5. 把這串換成您剛複製的新雜湊值(**保持前後的單引號**)
6. 滾到最下方點 **Commit changes** 兩次確認
7. 等 1 分鐘 Cloudflare 自動部署完
8. 開新分頁測試新密碼

---

## 📱 把網頁加到手機桌面

### iPhone (Safari)
1. 用 Safari 打開您的網址
2. 點下方分享按鈕(方框 + 上箭頭)
3. 滑到「**加入主畫面**」
4. 取個名字(例如「專利法」)→ 加入

### Android (Chrome)
1. 用 Chrome 打開網址
2. 右上角三個點 → **加入主畫面**
3. 確認

之後點桌面圖示就能直接打開。

---

## 📦 跨裝置同步資料(手動方案)

工具裡的 **⚙ 備份** 按鈕可以匯出/匯入您的所有資料:

**從電腦同步到手機**:
1. 電腦:點 ⚙ 備份 → ⬇ 下載備份檔
2. 透過 LINE/Email 把檔案傳到手機
3. 手機打開網頁 → ⚙ 備份 → ⬆ 選擇備份檔還原

注意:還原會**覆蓋**該裝置目前的資料。建議先備份再還原。

---

## ⚠️ 關於密碼保護的真實能力

這是**前端密碼**,密碼檢查發生在使用者的瀏覽器裡。

**能擋下**:
- 不知道網址的人
- 知道網址但不知道密碼的人(99% 的隨意訪客)

**擋不下**:
- 懂技術的人「檢視原始碼」可以看到密碼雜湊(破解需要時間,但他們看得到所有程式碼)

**結論**:對於「不希望路人看到內容」的目的足夠。**不要用這個工具存放高度機密的客戶資料**。

---

## 🆘 卡關時的常見問題

**Q:Cloudflare 部署失敗,顯示「No build output found」**
A:重新檢查 Build settings:Framework preset 必須是 **None**,Build command 和 Build output directory 都要**留空**。

**Q:網頁打開是空白頁**
A:等 1-2 分鐘讓部署完成,或清除瀏覽器快取重試。

**Q:密碼忘了**
A:到 GitHub 編輯 index.html,產生新的雜湊值替換即可。

**Q:能不能連到自家網域 tlpatent.com?**
A:可以。Cloudflare Pages 支援自訂網域,到專案設定 → Custom domains 加上即可。需要時告訴 Claude 協助。

---

部署過程中卡關,**截圖給 Claude** 繼續詢問即可。
