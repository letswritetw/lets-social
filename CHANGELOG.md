# Changelog

[正體中文](#正體中文) | [English](#english)

## 正體中文

`lets-social` 的所有重要變更都記錄在這份文件。

版本號遵循 [Semantic Versioning](https://semver.org/lang/zh-TW/)。

### [1.0.0] - 2026-09-01

#### 新增

- 純指令型 Agent Skill，支援 Instagram、Facebook、Threads 與 Telegram，各平台從同一份 Source Brief 獨立撰寫。
- 共用的來源忠實度、品牌語氣與輸出格式 reference。
- Instagram 預設提供 Nano Banana 2 與 ChatGPT Images 2.0 的可直接使用產圖 prompt。
- Threads 只在圖片能補充貼文角度時提供產圖 prompt。
- 每個平台各自建立 Image Brief，同一平台的兩份 prompt 共用主體、構圖與訊息。
- 產圖 prompt 依文章內容挑選視覺風格，提供知識圖卡、編輯式圖解、大字海報、終端機或藍圖、插畫場景等方向，並在 Image Brief 說明選擇理由。
- 每份 prompt 指定至少四個具名顏色、圖片的閱讀層級，以及足以避免變成素材圖的結構細節。
- 每份 prompt 指定線條個性、打破格線的排版、印刷紋理與動態記號，並列出會讓畫面僵硬的禁用字眼，避免產出制式的企業簡報風格。
- 禁止在 prompt 中要求人的手、臉與人物，改用箭頭、速度線或物件承擔動作，避免產圖模型的恐怖谷結果。
- 明確規範箭頭畫法：短、直線或單一弧線、粗桿、實心三角頭，禁止扭曲與細長飄尾的線條。
- 封面固定帶一行識別文字（標題或文章在講的那個名字），系列的其他張不重複。
- 圖中預設寫上來源支持的重點短句，中文一律指定清楚的粗體無襯線字，裝飾性手寫只用於英文短語，並在 prompt 逐字列出文字與位置。
- ChatGPT Images 2.0 的 prompt 預設要求一組編號系列，封面加三到五個重點各一張，上限 10 張；Nano Banana 2 維持單張封面。
- 版本 metadata，以及 Git 與 Skillshare 更新流程說明。

---

## English

All notable changes to `lets-social` are documented in this file.

The project follows [Semantic Versioning](https://semver.org/).

### [1.0.0] - 2026-09-01

#### Added

- Instruction-only Agent Skill for Instagram, Facebook, Threads, and Telegram, with every platform written independently from one shared Source Brief.
- Shared source-fidelity, brand-voice, and output-format references.
- Copy-ready Nano Banana 2 and ChatGPT Images 2.0 prompts for Instagram by default.
- Conditional Threads image prompts when a visual supports the selected angle.
- One Image Brief per platform, so both model prompts share the subject, composition, and message.
- Source-driven visual style selection across knowledge card, editorial diagram, typographic poster, terminal or blueprint, and illustrated scene directions, with the choice justified in the Image Brief.
- Every prompt names at least four colors with stated jobs, the image's reading hierarchy, and enough structural detail to avoid bare stock art.
- Every prompt specifies line character, a broken grid, print texture, and motion marks, with a banned-phrase list that keeps output from collapsing into sterile corporate infographics.
- Human hands, faces, and figures are banned from prompts, with arrows, speed lines, and objects carrying the action instead, avoiding uncanny-valley renders.
- Arrow anatomy is specified: short, straight or single-arc, thick-shafted, solid triangular head, with squiggly and thin trailing lines banned.
- The cover image carries one identifying line, the source title or the named subject, and a series never repeats it on later images.
- Source-grounded key points written on the image, with CJK pinned to clean bold sans-serif, decorative handwriting limited to short English phrases, and every string and its placement quoted verbatim in the prompt.
- ChatGPT Images 2.0 prompts request a numbered series where each image covers a different key point, four to six images by default and ten at most, while Nano Banana 2 stays single-image.
- Version metadata and documented Git and Skillshare update workflows.
