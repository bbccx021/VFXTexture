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

**光暈 Glow（新增）** — Beam 能量光束、Rays 放射光芒（聖光 / nova）

**液體 Liquid** — Splatter 飛濺液滴、Bubble 泡泡（薄殼＋高光）、Ripple 水面漣漪、Caustics 水下焦散（雙尺度 Voronoi 光網）

**魔法 Magic** — InkRing 手繪墨圈、Vortex 漩渦、Snowflake 雪花冰晶（六重對稱＋側枝）、ArcRing 電弧環（環狀閃電＋外放弧枝）、Orb 能量球（fresnel 亮邊＋內旋紋）

**拖尾 Trail** — TrailRamp 拖尾漸層（亮頭淡尾，配 2:1／4:1 比例＋左錨）

## 功能 / Features

- **🧱 組合堆疊（差異性核心）**：基底特效之後可疊任意層 —— 29 種特效層（加法／乘法／減去／最大／最小／濾色混合 + 不透明度／縮放／獨立 seed）與 9 種運算節點（Warp 扭曲／模糊／銳化／色階／Threshold 二值化／反轉／鏡像／放射遮罩／旋轉），可排序、可刪除；**31 組一鍵範例**（能量煙、雷光斬、冰霜法陣、雷電護盾、聖光爆發、雷電法球、煙火綻放、霜凍領域、焦散漩渦…）；堆疊進分享連結，全程 Worker 運算 composite stack (linear node chain)
- **每型專屬參數面板**：每種特效宣告自己的參數（名稱／範圍對齊實際行為，滑桿無死區），選特效自動切換 per-type param schema
- **動畫 / 序列幀**：時間 t 演化（煙消散、衝擊波擴張、碎片炸開、泡泡爆破…），t 滑桿預覽單幀、**▶ 一鍵烘焙循環播放（FPS 4–30 可調）**，匯出 **flipbook Sheet** / 各幀 ZIP / **🎬 循環 GIF**（內建零依賴 GIF89a 編碼器）
- **配方存檔**：完整外觀（特效＋參數＋堆疊＋調色＋風格＋發光）存進瀏覽器，可載入／刪除／**JSON 匯出匯入**（團隊共享配方庫）
- **漸進式預覽**：拖桿時 1× 快速回饋，放手 260ms 自動 2× SSAA 精修
- **節點 bypass／複製**：堆疊層可 👁 暫時停用、⧉ 一鍵複製
- **區塊狀態徽章**：堆疊層數、賽璐璐、Glow%、動畫狀態顯示在區塊標題 —— 收合也一目了然
- **Web Worker 渲染**：生成運算在背景執行緒，拖滑桿與批次匯出 UI 不凍結（不支援環境自動 fallback）
- **全域 2× 超取樣**：所有特效、所有模式一致抗鋸齒（不再只看賽璐璐開關）
- **Add / Multiply 成對匯出**：勾選後同時輸出 `_a`（黑底加法版）與 `_m`（白底反轉乘法版），對齊引擎雙貼圖慣例
- **非方形尺寸**：1:1 / 2:1 / 4:1 比例（trail、beam 貼圖格式），內容自動壓縮拉伸
- **錨點控制**：中 / 左 / 右 / 上 / 下 —— 內容往邊緣靠（槍口火光靠左、拖尾靠底，配合引擎 pivot）
- **HDR 匯出**：Radiance `.hdr`（RGBE、線性光），Glow 超過 1 的能量保留，引擎 bloom 有真實餘量
- **線性空間 ramp 混色**：漸層在線性光插值再轉回 sRGB，亮度均勻無暗帶
- **manifest.json 參數側錄**：批次 ZIP 內附完整生成參數（可重現、可追溯）
- 11 種色彩映射：灰階 / **卡通雙色** / **卡通三色** / **自訂雙色（color picker 暗色＋亮色）** / 金 / Plasma / 火焰 / 冰 / 電 / 毒 / 熔岩
- 背景切換：黑 / 白 / 透明；透明模式帶 **去黑邊修正**（straight-alpha 引擎混合不出暗色 fringing）
- 後處理鏈：色階、對比、Gamma、亮度、反轉、**Glow 發光（bloom）** + 亮度直方圖 + 一鍵自動色階
- 卡通風格：**賽璐璐** 一鍵預設（色塊階數、墨線描邊、外框線、邊緣抖動可微調）
- Op 層：Cells（Voronoi）、Warp、Blend 等運算為共用積木，generator 組合使用
- 溶解預覽、批次 ZIP、URL 參數分享（含每型參數）、中文 / English

## 使用 / Usage

直接開 `index.html`，或部署到 GitHub Pages。
Open `index.html` directly, or deploy via GitHub Pages.
