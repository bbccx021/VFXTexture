# FX Sprite Lab

程序化生成的遊戲特效貼圖產生器（單檔網頁，無需安裝）。獨立於 NoiseGenerator 噪波產生器。

A procedural game-VFX sprite texture generator. Single self-contained HTML file, no build step.

## 特效類型 / Effect types

**打擊 Strike** — Slash 斬擊月牙、Bolt 閃電束、CrossSlash 交叉斬痕、Glint 銳利閃點

**光暈 Glow** — Glow 柔光、StarGlow 星芒、RingGlow 光環、Anamorphic 橫向光斑

**煙霧 Smoke** — CelSmoke 卡通煙團（平滑聯集法線兩色調、頂亮底暗如真實雲團、2× 超取樣抗鋸齒）

**石頭 Rock** — Rock 程序化石頭（有稜有角巨石輪廓、三調卡通面、底部坐地）

**火焰 Fire** — Flame 程序化火焰（團塊堆疊圓潤火焰、亮核暗焰兩色調、負空間洞）

## 功能 / Features

- 10 種色彩映射：灰階 / **卡通雙色** / **卡通三色** / 金 / Plasma / 火焰 / 冰 / 電 / 毒 / 熔岩 gradient + cel mapping
- 背景切換：黑 / 白 / 透明（透明輸出帶 alpha 通道，可直接放進引擎）background: black / white / alpha
- 後處理鏈：色階、對比、Gamma、亮度、反轉 + 亮度直方圖 + 一鍵自動色階
- 手繪 / 賽璐璐：色塊階數（posterize）、墨線描邊、外框線（日系深色 silhouette 輪廓）；cel 開啟時自動 2× 超取樣消除邊緣鋸齒 hand-drawn / cel-shading + SSAA
- 溶解預覽
- 批次 ZIP 下載、URL 參數分享
- 中文 / English 語言切換
- seed / octaves / 縮放 參數控制，適合批次生成命中幀變體

## 使用 / Usage

直接開 `index.html`，或部署到 GitHub Pages。
Open `index.html` directly, or deploy via GitHub Pages.
