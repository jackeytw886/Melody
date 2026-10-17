# File Map — P010 檔案地圖

核對基準：`7ce5843abe0e20435c7187177c9a56ca0d5533b1`。下表列出整理前檔案，大小來自 Git tree；新增管理文件另列於文末。

| 路徑 | 大小（bytes） | 類型 |
| --- | ---: | --- |
| [README.md](../README.md) | 57 | md |
| [index.html](../index.html) | 86115 | html |

## 管理入口

README.md、AGENTS.md、HANDOFF.md、PROJECT.json、CLAUDE.md、GEMINI.md、.github/copilot-instructions.md、docs/VERIFICATION.md。

## 檔內結構（行號索引，2026-10-18 Claude 依基準 `eecb4ec` 整理）

只讀需要的段落；標 ⚠️ 的是超長單行資料，不要整行載入。

| 約略行號 | 內容 |
| ---: | --- |
| 7–592 | `<style>` |
| 594–746 | HTML 介面（含右側 CF9510M 播放紀錄 `#cfLog`、旋律提示） |
| 747–2730 | 主程式 `<script>` |
| 766–779 | 設定（同 P009） |
| 780–877 | 語音 `speak()`（同時寫入 CF9510M 紀錄） |
| 878–967 | 音效 `SFX`（含 `melodyNote`、`wrongStep`） |
| 968–1125 | CF9510M 模擬層：`CF_FILE_MAP`、數字對照、`textToCfSequence()`、紀錄面板 |
| 1126–1158 | 倒數字型、`SCALE_FREQ`／`SCALE_NAME` 音階 |
| 1159–1258 | `PATH_THEMES`：8 條路線＋隱藏旋律 `melody`、`tuneName` |
| 1259–1356 | 踩錯語音、`GAME` 狀態、DOM 參照 |
| 1357–1641 | 格子、呼吸迴圈、流程控制、字幕、旋律狀態與提示、路線生成 |
| 1642–2309 | 16 種燈效 |
| 2310–2349 | `demoEffect()`、`setPhase()` |
| 2350–2484 | `startGame()`（含「猜猜這是什麼旋律」開場）與計時 |
| 2485–2582 | `onStoneClick()`：旋律音符、音名提示、踩錯語音 |
| 2583–2730 | `endGame()`（揭曉歌名）與重設 |

## 2026-10-18 新增文件

- [docs/PROTOCOL.md](PROTOCOL.md)：CF9510M 語音檔資料夾與檔號對照（依網頁 `CF_FILE_MAP` 整理）。
