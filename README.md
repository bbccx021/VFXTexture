# FX Sprite Lab

程序化生成的遊戲特效貼圖產生器（單檔網頁，無需安裝）。獨立於 NoiseGenerator 噪波產生器。

A procedural game-VFX sprite texture generator. Single self-contained HTML file, no build step.

## 特效類型 / Effect types

**打擊 Strike** — Slash 斬擊月牙、Bolt 閃電束、CrossSlash 交叉斬痕、Glint 銳利閃點

**光暈 Glow** — Glow 柔光、StarGlow 星芒、RingGlow 光環、Anamorphic 橫向光斑

**煙霧 Smoke** — CelSmoke 卡通煙團（平滑聯集法線兩色調、頂亮底暗如真實雲團、2× 超取樣抗鋸齒）

**石頭 Rock** — Rock 程序化石頭（有稜有角巨石輪廓、三調卡通面、底部坐地）

**火焰 Fire** — Flame 程序化火焰（寬圓潤多瓣身體 + 雙尖火舌、自帶尖端的內焰亮部；缺口數量／大小滑桿 + 🎲 一鍵換位）

**爆發 Burst** — Shockwave 衝擊波環、MuzzleFlash 槍口火光、Sparks 星形火花、GroundCrack 地裂裂紋、CellCrack 細胞地裂（Voronoi 邊界 + Perlin Warp）、StylizedImpact 風格化衝擊（SD 思路：三角碎片減圓弧 + Splatter 環狀 + Cells 切碎 + Warp 波浪邊，搭 Glow 出 bloom）

**液體 Liquid** — Splatter 飛濺液滴（血 / 毒 / 黏液通用，配 ramp 換色）

**魔法 Magic** — InkRing 手繪墨圈（debuff 圈 / 印記）

## 功能 / Features

- **每型專屬參數面板**：每種特效宣告自己的參數（名稱／範圍對齊實際行為，滑桿無死區），選特效自動切換 per-type param schema
- **動畫 / 序列幀**：時間 t 演化（煙消散、衝擊波擴張、碎片炸開、火焰搖曳…），t 滑桿即時預覽單幀，一鍵匯出 **flipbook Sheet**（單張網格）或各幀 ZIP
- **Web Worker 渲染**：生成運算在背景執行緒，拖滑桿與批次匯出 UI 不凍結（不支援環境自動 fallback）
- **全域 2× 超取樣**：所有特效、所有模式一致抗鋸齒（不再只看賽璐璐開關）
- **Add / Multiply 成對匯出**：勾選後同時輸出 `_a`（黑底加法版）與 `_m`（白底反轉乘法版），對齊引擎雙貼圖慣例
- 11 種色彩映射：灰階 / **卡通雙色** / **卡通三色** / **自訂雙色（color picker 暗色＋亮色）** / 金 / Plasma / 火焰 / 冰 / 電 / 毒 / 熔岩
- 背景切換：黑 / 白 / 透明；透明模式帶 **去黑邊修正**（straight-alpha 引擎混合不出暗色 fringing）
- 後處理鏈：色階、對比、Gamma、亮度、反轉、**Glow 發光（bloom）** + 亮度直方圖 + 一鍵自動色階
- 卡通風格：**賽璐璐** 一鍵預設（色塊階數、墨線描邊、外框線、邊緣抖動可微調）
- Op 層：Cells（Voronoi）、Warp、Blend 等運算為共用積木，generator 組合使用
- 溶解預覽、批次 ZIP、URL 參數分享（含每型參數）、中文 / English

## 使用 / Usage

直接開 `index.html`，或部署到 GitHub Pages。
Open `index.html` directly, or deploy via GitHub Pages.
