---
name: universal-english-song-worksheet
version: 3.0.0
author: RaeHo (azureplanet-spark) [Original Concept & Universal Refactoring] & hsinyuchi (Sylvia) [High School Refinement]
license: CC BY-NC-SA 4.0
description: >-
  打造通用進階版「英語歌曲互動網頁學習單 (Universal English Song Worksheet Pro)」。
  源自 RaeHo (azureplanet-spark) 最初的英語歌曲學習單發想，歷經 hsinyuchi (Sylvia) 老師針對高中職課堂的專業深化，
  再由 RaeHo 重新拆解、模組化重構為適用更多元對象（國小至成人、CEFR A1~B2）之通用進階版本。
  支援自訂本機存放資料夾、自訂教師/機構名稱、5/10 題彈性題數與三大題型（三選一、配合題、拼寫輸入），
  並支援 YouTube 與本機 MP3/MP4 雙播放引擎。
---

# 🎧 通用進階版英語歌曲互動學習單製作技能 (Universal English Song Worksheet Pro)

> 📜 **專案演進脈絡與著作權聲明 (Project Lineage & Attribution Notice)**：  
> 
> 本專案為教育社群開放共創之成果，歷經三個關鍵演進階段：
> 
> 1. **🌱 初代發想與原型構建 (v1.0 Concept & Prototype)**：  
>    由 **RaeHo (azureplanet-spark)** 最早發想並構建最初之「英語歌曲互動學習單」基礎架構與互動雛形。
> 2. **🏫 高中職課堂深化與教學鷹架 (v2.0 High School Refinement)**：  
>    由 **hsinyuchi (Sylvia)** 老師基於初代原型，針對臺灣高中職課堂教學標準、108 課綱學習歷程檔案與 CEFR A1~A2 學生需求進行深度教學優化，並建立《Count on Me》旗艦教學母版。
> 3. **🚀 通用進階版模組化重構 (v3.0 Universal Edition)**：  
>    由 **RaeHo (azureplanet-spark)** 吸收 Sylvia 老師的教學鷹架精華，進行全面核心拆解、參數化與模組化擴充（開放自訂教師/機構名稱、CEFR A1~B2 四級適配、三大題型切換、本機 MP3/MP4 雙播放引擎與彈性本機/雲端部署），升級為適用全年齡（國小至成人）與多元教學情境之通用版本。
> 
> 📜 **授權條款 (License)**：依據 [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) 國際授權條款發布（姓名標示—非商業性—相同方式分享）。歡迎各界教育夥伴進行非商業教學引用、共備與改編。

本 Skill 指導 Agent 為任意英語歌曲打造極致體驗的「單一獨立 HTML5 互動網頁學習單」，全面支援各級學校（國小高年級、國中、高中職、大專及成人教育）、補習班與個人自學，提供高度自訂化與零門檻本機/雲端部署。

---

## 🧭 開發前置對話精靈 (Interactive Setup Wizard)

在生成任何程式碼與教材之前，Agent **必須主動向使用者確認以下 8 大關鍵參數**：

```text
🎵 歡迎使用「通用進階版英語歌曲互動學習單」製作工具！
為了為您量身打造最佳學習體驗，請確認以下設定（可直接回覆序號或依序填寫）：

1. 📂 【本機存放路徑】：請提供您希望將成品（HTML、Zip 壓縮包）存放在本機的哪個資料夾路徑？（例如：D:\Teaching_Materials\Songs 或 C:\MySongs）
2. 🎤 【歌曲與歌手】：請提供歌曲名稱與歌手（例如：Bruno Mars - Count on Me）
3. 🏫 【教師與機構名稱】：請提供欲顯示的「教師姓名」與「學校/機構名稱」（例如：林老師 / 國立彰化高中；若想製作無特定個人標籤之通用版，可填寫「免標記」）
4. 📊 【學習者程度 (CEFR)】：請選擇適配程度：
   • A1（基礎入門：生活常用單字、極簡句型、完整繁中雙語輔助）
   • A2（初中級：日常情境單字、基礎文法、雙語鷹架）
   • B1（中級：進階字彙與片語、複合句、文化背景深度解析）
   • B2（中高級：文學修辭、抽象意境探討、全英/高階反思引導）
5. 🔢 【聽力題數】：請選擇題數：【 5 題 】 或 【 10 題 】（每題均分，總分 100 分）
6. 📝 【聽力題型】：請選擇一種主要的作答模式：
   • (A) 行內三選一 (Inline 3-Choice Popover - 含 2 個辨音干擾選項，最適合手機單手作答)
   • (B) 單字庫配合題 (Word Bank Matching - 單字庫點選/拖曳填空)
   • (C) 拼寫輸入題 (Spelling / Dictation Input - 鍵盤直接輸入單字，訓練拼字與精準聽力)
7. 🎬 【媒體來源】：
   • YouTube 官方影片（請提供 YouTube 連結，或由 Agent 自動搜尋純英文/無字幕官方版本）
   • 本機 MP3 / MP4 影音檔（網頁內建檔案選擇器與本機播放引擎，免開伺服器）
8. 🚀 【專案命名與部署】：
   • 專案英文代稱（Slug，例如：`count-on-me-a2`）
   • 是否需要指引連動至 Cloudflare Pages？（是 / 否，否則直接儲存至本機指定資料夾）
```

---

## 🎯 CEFR 四大等級適配準則 (Level Adaptation Matrix)

根據使用者選擇的 CEFR 等級，Agent 在設計單字、句型、賞析與反思題目時需進行難度分級：

| CEFR 等級 | 單字選取範圍 | 句型文法深度 | 歌曲賞析語調與深度 | 反思鷹架 (Sentence Starters) |
| :--- | :--- | :--- | :--- | :--- |
| **A1 (入門)** | 7000 單 Level 1~2、高頻日常名詞/動詞 | `S + V`、簡單祈使句、`can / want to` | 親切簡單、短篇對話式導讀，強調旋律好聽與基本情感 | 附完整雙語提示（如：`I like this song because... (我喜歡這首歌，因為...)`） |
| **A2 (初中級)** | 7000 單 Level 2~3、情緒/動作/描述形容詞 | 對等連接詞 (`and/but/so`)、時間子句 (`when/before`)、基礎比較級 | 結合青少年/學生校園生活、人際關係與自信建立 | 雙語鷹架，引導表達具體原因與感受 |
| **B1 (中級)** | 7000 單 Level 3~4、常用片語與動詞短語 | 條件句 (`if/unless`)、關係代名詞 (`who/which/that`)、使役動詞 | 深入創作背景、歌手生涯轉折、社會觀察或心理成長課題 | 半開放式英文引導句，鼓勵嘗試使用完整英文句子表達 |
| **B2 (中高級)** | 7000 單 Level 4~6、進階修辭/抽象概念字 | 倒裝句、虛擬語氣、分詞構句、名詞子句 | 文學意象解析、隱喻 (Metaphor)、當代文化與社會價值反思 | 全英鷹架（附進階詞彙提示庫），鼓勵批判性思考 (Critical Thinking) |

---

## 🛠️ 三大作答題型前端技術規格 (Question Mode Specifications)

網頁核心支援以下三種作答模式（依使用者選定套用）：

### 模式 A：行內三選一 (Inline 3-Choice Popover)
- **運作機制**：點擊歌詞中的空格 `[ 1. ____ ]`，立即在空格下方彈出 3 個選項按鈕（1 正解 + 2 個高質量辨音干擾項）。
- **辨音干擾項設計**：近音詞、押韻詞、同字首字根或形似詞（如 `sail` 配 `sale / tail`；`submission` 配 `commission / permission`）。
- **防遮擋 CSS**：
  ```css
  .lyric-line.active-line { z-index: 500; position: relative; }
  .cloze-blank.has-popover { z-index: 1000 !important; }
  ```
- **智慧翻轉**：靠近視窗底部時自動向上彈出 (`.pop-up`)。

### 模式 B：單字庫配合題 (Word Bank Matching)
- **運作機制**：在聽力區頂部或浮動面板展示隨機打亂的單字庫 (Word Chips)。
- **雙操作支援**：
  1. **滑鼠拖曳**：支援 HTML5 Drag & Drop，將單字卡拖至對應空格。
  2. **手機點擊**：點擊單字卡將其選中（高亮邊框），再點擊目標空格即可填入；點擊已填入空格可退回單字庫。
- **即時視覺狀態**：已被使用的單字卡呈現半透明或劃線狀態，可隨時點擊重置或更換。

### 模式 C：拼寫輸入題 (Spelling / Dictation Input)
- **運作機制**：空格直接呈現為行內輸入框 `<input type="text" class="spelling-input" maxlength="20" placeholder="Type here...">`。
- **智慧比對邏輯**：
  - 忽略前後空格 (`trim()`)。
  - 忽略英文字母大小寫 (`toLowerCase()`)。
  - 標點符號容錯（若單字含撇號如 `don't`，可允許使用者輸入 `dont` 或 `don't`）。
- **鍵盤優化**：按下 `Enter` 或 `Tab` 鍵自動聚焦 (focus) 到下一個挖空輸入框。

---

## 🎬 雙軌媒體播放引擎 (Dual Media Player Engine)

網頁同時支援 **YouTube 串流** 與 **本機檔案載入**：

### 1. YouTube 播放器 (線上串流模式)
- 使用 `https://www.youtube-nocookie.com/embed/{VIDEO_ID}?rel=0&enablejsapi=1` 嵌入。
- **嚴格審查標準**：
  - 優先挑選官方 MV、電影片段或動畫歌詞版（動態分鏡畫面）。
  - 純英文字幕或官方無字幕版本，嚴禁繁/簡中文字幕。
  - 右上角必備防版權限制跳轉按鈕：`▶️ 若無法直接播放，點此開啟 YouTube 觀看`。

### 2. 本機 MP3 / MP4 播放器 (離線/本機檔案模式)
- 網頁內建現代化 HTML5 `<audio>` / `<video>` 控制器，具備自定義波形/進度條、播放/暫停、前後快轉 5 秒、播放速度調整 (0.75x / 1.0x / 1.25x)。
- **即時本機載入器**：
  - 提供醒目的拖曳上傳區 (Dropzone) 與檔案選擇器 `<input type="file" accept="audio/*,video/*">`。
  - 使用 `URL.createObjectURL(file)` 進行即時串流播放，**100% 於瀏覽器前端本機解碼，無須連網、免開伺服器、保護個人版權隱私**。

---

## 📋 製作標準流程 (SOP 四大階段)

---

### Step 1：參數蒐集、素材審查與題目定位
1. 執行【前置對話精靈】，向使用者取得存放路徑、歌曲名稱、教師/機構資訊、CEFR 程度、題數 (5/10)、題型 (A/B/C)、媒體來源及專案代稱。
2. 搜尋並校對全曲 100% 完整歌詞，確保無缺行、無跳行、段落完整（主歌、副歌、過渡、合唱）。
3. 根據題數 (5 或 10 題) 精選關鍵聽力單字，並為題型 A 準備 2 個辨音干擾詞。
4. 挑選 3~5 個重點深究單字與 1~2 個句型。
5. 🛡️ **括號防衝突語法安全守則**：
   - 僅有要挖空的英文單字使用半形中括號 `[word]`。
   - 歌詞中的角色名、合唱標籤一律使用圓括號 `(Singer)` 或全形括號 `【合唱】`。

---

### Step 2：教學內容精細設計 (Pedagogical Content)
1. **單字深究區 (Vocabulary Study)**：
   - 單字、詞性、中文解釋、搭配詞 (Collocations)。
   - 程度友善例句（附 🔊 Web Speech API 原生朗讀按鈕與中文翻譯）。
2. **核心句型解析 (Target Sentence Structures)**：
   - 公式化拆解 (標示 S + V)。
   - 歌曲歌詞示範句（至少 2~3 句）。
   - 實用情境造句。
3. **歌曲賞析與背景文化 (Story & Youth Resonance)**：
   - 歌手檔案與亮眼紀錄（葛萊美、告示牌、串流紀錄等）。
   - 符合該 CEFR 等級口吻的對話式賞析短文（親切共感，拒絕上對下的教案說教口吻）。
   - 意境導讀與全曲雙語對照歌詞。
4. **學生反思鷹架問答 (Scaffolded Reflection)**：
   - **Q1 推薦星等**：1~5 星滑桿，動態文字反饋。
   - **Q2 推薦原因**：附對應等級之 `Sentence Starter` 雙語鷹架方塊與參考範例。
   - **Q3 打動歌詞與啟發**：附對應等級之 `Sentence Starter` 雙語鷹架方塊與參考範例。

---

### Step 3：單檔 HTML5 互動網頁開發

技術棧：`HTML5` + `Tailwind CSS (CDN)` + `Vanilla JavaScript` + `html2canvas (CDN)` + `canvas-confetti (CDN)`。

#### 網頁核心模組架構（自頂向下）：
1. **Header 品牌導覽區**：
   - 左側：學校/機構標籤、指導教師資訊（或通用學習標籤）、歌曲主副標題。
   - 右側鎖定計時器：`flex-shrink-0 min-w-[120px]`，防窄螢幕折行。
2. **影音播放器模組**：YouTube `iframe` 或本機 MP3/MP4 HTML5 Player。
3. **聽力挑戰區 (`#quiz-area`)**：
   - 吸頂黏性進度條 (Sticky Progress Bar)：題數計數器 (`0/5` 或 `0/10`)、得分進度。
   - 依使用者選擇套用題型 A（三選一 Popover）、B（單字庫配合）或 C（拼寫輸入）。
   - 聽力區底部快捷操作：`✅ 即時對答案` 與 `⬇️ 往下學習與填寫反思`。
4. **單字深究與語音朗讀區**（內建 Web Speech API TTS `en-US` 發音）。
5. **核心句型解析區**。
6. **歌曲深度賞析與全曲雙語歌詞區**。
7. **學生自我反思問答區 (`#reflection-section`)**。
8. **頁尾 Grand Submit 結算區**：
   - **Reflection Guard 守門員**：若未填寫反思，點擊結算時跳出 `confirm()` 友善提醒。
   - **4 級動態視覺特效 (Canvas Confetti)**：
     - 80 ~ 100 分：魔杖星光 + 全彩彩帶噴發 🧙‍♀️✨
     - 60 ~ 79 分：熱氣球升空飄浮 🎈☁️
     - 40 ~ 59 分：畫面搖晃提示 😬
     - < 40 分：灰階濾鏡 + 下雨雨滴動畫 🌧️
9. **學習成果認證卡 Modal 與 PNG 匯出**：
   - 包含自訂品牌/純淨標題、學生班級、座號、姓名、作答日期、總耗時、最終成績、評分星等與完整反思文字。
   - 點擊按鈕透過 `html2canvas` 一鍵匯出高解析度 PNG。
10. **頁尾非營利教育版權聲明**。

---

### Step 4：檔案自動儲存、打包與部署 (Delivery & Deployment)

1. **自動存檔至指定本機路徑**：
   - 將生成的 HTML 檔案寫入使用者指定的本機資料夾（例如：`{User_Target_Dir}/{Song_Slug}_網頁學習單.html`）。
   - 將網頁命名為 `index.html`，並打包為 `{User_Target_Dir}/{Song_Slug}_site.zip`。
2. **Cloudflare Pages 部署指引**：
   - 若使用者希望連動 Cloudflare Pages：
     - 指引使用者至 [Cloudflare Dashboard](https://dash.cloudflare.com/) ➜ `Workers & Pages` ➜ `Create application` ➜ `Pages` ➜ `Upload assets`。
     - 直接將產出的 `{Song_Slug}_site.zip` 或資料夾拖曳上傳即可獲得專屬網址（例如：`https://{Song_Slug}.pages.dev`）。
   - 若使用者無需連動，則告知使用者直接以瀏覽器雙擊開啟本機的 HTML 檔案即可完整離線使用。

---

## 💡 對話範例 (Example Interaction)

```text
User: 我想用 Taylor Swift 的 "Anti-Hero" 做一隻學習單。

Agent: 
太棒了！我們來為 Taylor Swift 的《Anti-Hero》製作通用進階版英語歌曲互動學習單。
請先協助確認以下 8 個基本設定：

1. 📂 成品存放路徑：請提供您電腦上的資料夾路徑（例如：C:\Users\USER\MusicWorksheets）
2. 🏫 教師/機構名稱：例如「黃老師 / 台北市立大同高中」（若想留空做通用版可回「免標記」）
3. 📊 CEFR 程度：A1 / A2 / B1 / B2 （建議本曲可選 B1 或 B2）
4. 🔢 題數：5 題 / 10 題
5. 📝 題型：(A) 三選一 Popover / (B) 單字庫配合題 / (C) 拼寫輸入題
6. 🎬 媒體來源：YouTube 官方影片 / 本機 MP3/MP4 檔案
7. 🚀 專案英文代稱：例如 anti-hero-b1
8. 🌐 是否需要 Cloudflare Pages 部署指引：是 / 否
```
