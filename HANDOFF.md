# Handoff — P010 穿越跳石陣・猜旋律模式（v3.8）

- 更新時間：2026-10-18T03:25+08:00
- 更新者：Claude（逐檔讀原始碼，撰寫專案交接）
- 倉庫：https://github.com/jackeytw886/Melody
- 分支：main
- 本次基準 SHA：`eecb4ec1f7185897f2522954daedb4f5ceb7b9f2`（Codex 管理整理提交）
- 核對層級：已讀全部原始碼；已執行語法檢查與無頭瀏覽器冒煙測試（見 docs/VERIFICATION.md）；**未接實體跳石陣、未核對實體 SD 卡音檔**。

## 1. 這是什麼

「穿越跳石陣」網頁模擬器的 v3.8「猜旋律挑戰」版。玩法與 P009（v3.5 環形燈條版）相同：10 排 × 3 列共 30 顆跳石，90 秒內只踩亮藍色的路線。差別是**每踩對一步就彈出一個音，整條路線踩完剛好是一首兒歌**，玩家邊踩邊猜歌名，結算時揭曉答案。另外加入 **CF9510M 語音模組模擬層**，把網頁說的每句話換算成實體 MP3 的資料夾與檔號。

- 線上網址：https://jackeytw886.github.io/Melody/ （GitHub Pages）
- 相關：P009（Champagne，v3.5 基礎版）、P026（同時段建立的空倉庫）。實體韌體（Arduino Mega 30 通道）**不在此倉庫**。

## 2. 檔案

- `index.html`（約 86 KB、2,733 行），無外部程式庫、可離線。行號索引見 docs/FILE-MAP.md。
- `docs/PROTOCOL.md`：CF9510M 語音檔對照表（本次由程式整理）。

## 3. 與 P009 相同的部分

設定（`ROWS`、`COLS`、`TOTAL_TIME=90`…）、`PATH_THEMES` 8 條路線、`GAME` 狀態、`setStoneRing()` 單一繪製入口、flowId 流程取消、`speak()` 語音、16 種燈效與結算規則都與 P009 一致，說明見 P009 的 HANDOFF.md。

## 4. v3.8 新增的部分

| 功能 | 位置／名稱 | 說明 |
| --- | --- | --- |
| 隱藏旋律 | `PATH_THEMES[].melody`、`tuneName`、`timbre` | 每條路線綁一首歌：銀河漫遊＝小星星、神龍擺尾＝兩隻老虎、渡海尋寶＝倫敦鐵橋、閃電快線＝火車快飛、森林小徑＝小蜜蜂、月影折返＝點仔膠、雙峰攀登＝生日快樂、螢火蟲迴路＝王老先生有塊地。`melody` 是 10 個音的簡譜級數（1＝Do） |
| 踩踏出聲 | `SFX.melodyNote(stepIndex, theme, interval)`、`SCALE_FREQ`、`SCALE_NAME` | 依踩對的順序播下一個音；兩步間隔越短，音越短越大聲（< 300 ms、< 600 ms、< 1200 ms、其他 四級） |
| 音名提示 | `flashNoteHint()` | 字幕旁閃出 Do／Re／Mi |
| 提示按鈕 | `showTuneHint()` | 遊戲中可講出歌名第一個字 |
| 揭曉 | `endGame()` 內 | 結算前語音「答案揭曉！這首旋律是…」 |
| 踩錯語音 | `WRONG_VOICE_LINES`、`SFX.wrongStep()` | 四句輪流＋錯誤次數 |
| CF9510M 模擬 | `CF_FILE_MAP`、`textToCfSequence()`、`appendCfLog()`、`#cfLog` | 每次 `speak()` 同時列出實體應播放的檔案序列，對照表見 docs/PROTOCOL.md |

## 5. 已知問題與待辦

- CF9510M 對照只存在網頁端，實體 SD 卡是否照此排列、韌體是否用相同檔號**都未核對**。
- 旋律只有 10 個音（路線長度 10），歌曲只到前段；若路線長度改變，`stepIndex % melody.length` 會循環播放。
- 與 P009 為複製後各自修改，修 bug 時要考慮兩邊同步。

## 6. 測試方式

直接開 `index.html`。可在頁面中讀 `GAME.phase`、`GAME.theme.tuneName`、`GAME.melodyIndex`，或檢查 `#cfLog` 的紀錄數量；點 `.stone`（`data-r`、`data-c`）模擬踩踏。

## 7. 修改時注意

- 新增語音句子時，同步在 `CF_FILE_MAP` 加檔號，並更新 docs/PROTOCOL.md 與 SD 卡清單。
- 調整 `PATH_THEMES` 順序會改變資料夾 2 的檔號。

## 8. 版本沿革

- 2026-05-16：經 EZPage 部署 v3.8。
- 2026-10-17：Codex 管理整理（代號 P010、AI 入口文件）。
- 2026-10-18：Claude 補寫本交接與 docs/PROTOCOL.md。

## 版本定位

基準 SHA 定位本次文件修改前的程式；本次文件提交由此檔所在的 Git 提交與倉庫歷史定位，不預填同一提交自己的 SHA。
