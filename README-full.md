# lets-social

[正體中文](#正體中文) | [English](#english)

## 正體中文

把一篇文章轉寫成符合 Instagram、Facebook、Threads 與 Telegram 平台特性的社群內容。

這是完整版說明。想先快速上手，請看[簡短版 README](README.md)。

`lets-social` 是 [Let's Write](https://www.letswrite.tw/) 推出的開源專案。名稱從 **Let's Write** 延伸為 **Let's Social**，但這個 Skill 適用於任何網站、作者與品牌。

### lets-social 是什麼？

`lets-social` 是純指令型 Agent Skill。你可以提供已完成的文章、Markdown、純文字、本機檔案，或 Agent 能讀取的網址。它會先建立一份內部 Source Brief，再針對每個指定平台獨立撰寫內容。Instagram 預設會附上 Nano Banana 2 與 ChatGPT Images 2.0 的可直接使用 prompt；Threads 只在圖片能補充內容時提供。

它不負責發佈、排程，也不替來源補上未經證實的資料。所有輸出都必須保留原文的事實、不確定性、立場與作者語氣。

### 為什麼需要 lets-social？

每個社群平台都有不同的閱讀方式。Facebook 適合補充背景，Threads 適合從一個明確觀察切入，Telegram 則重視資訊密度與掃讀效率。`lets-social` 會依平台重新判斷 Hook、資訊順序、語氣與 CTA，不會只把同一份文案改成不同長度。圖片也採用相同原則：Instagram 預設需要視覺素材，Threads 不會為了湊格式加入裝飾圖。

### 支援平台

| 平台 | 預設輸出 | 內容重點 |
| --- | --- | --- |
| Instagram | Caption、CTA、可選 Hashtag 或 Carousel、產圖 prompt | 手機閱讀、實用價值與配圖 |
| Facebook | Post、CTA | 背景、寫作動機與作者觀點 |
| Threads | 單篇貼文或適合的串文；必要時附產圖 prompt | 口語觀察與討論感 |
| Telegram | Message、連結位置建議 | 清楚、易掃讀與資訊密度 |

`1.0.0` 版尚未支援 LinkedIn、X、Bluesky 與 Mastodon。

### 運作方式

```text
來源文章
    -> 內部 Source Brief
        -> Instagram 草稿
        -> Facebook 草稿
        -> Threads 草稿
        -> Telegram 草稿
        -> Instagram Image Brief
        -> 可選的 Threads Image Brief
    -> 每份 Image Brief 產生兩個模型的完整 prompt
    -> 來源忠實度與平台差異檢查
    -> Markdown 輸出
```

每個平台都從同一份 Source Brief 出發，不會拿某個平台的草稿當成另一個平台的輸入。同一平台的兩份產圖 prompt 使用相同 Image Brief，因此主體、構圖與訊息保持一致。

### 安裝

Clone 或下載此 repository，再將完整的 `lets-social` 目錄放到 Agent 支援的 Skill 路徑。請保留 `SKILL.md`、`references/` 與 `examples/` 的相對位置。

若希望之後能更新，請使用 Git Clone，並直接 Clone 到下列 Skill 路徑；下載 ZIP 的安裝方式不會保留 Git 更新紀錄。

#### Claude Code

安裝為個人 Skill：

```bash
git clone https://github.com/letswritetw/lets-social.git ~/.claude/skills/lets-social
```

<details>
<summary>Windows 使用者請點這裡</summary>

Git Bash 可以直接用上面的指令。PowerShell 和 cmd 不會展開 `~`，會在當前目錄建一個名字叫 `~` 的資料夾，請改用下面的指令。

PowerShell：

```powershell
git clone https://github.com/letswritetw/lets-social.git "$HOME/.claude/skills/lets-social"
```

cmd：

```text
git clone https://github.com/letswritetw/lets-social.git "%USERPROFILE%/.claude/skills/lets-social"
```

</details>

或安裝在單一專案，在專案根目錄執行：

```bash
git clone https://github.com/letswritetw/lets-social.git .claude/skills/lets-social
```

Claude Code 可以依 description 自動選用，也可以用 `/lets-social` 明確呼叫。詳細規格請參考 [Claude Code Skills 官方文件](https://code.claude.com/docs/en/skills)。

```text
/lets-social 把 ./article.md 轉成 Instagram 與 Threads 貼文。
```

#### Codex

安裝為個人 Skill：

```bash
git clone https://github.com/letswritetw/lets-social.git ~/.agents/skills/lets-social
```

<details>
<summary>Windows 使用者請點這裡</summary>

Git Bash 可以直接用上面的指令。PowerShell 和 cmd 不會展開 `~`，請改用下面的指令。

PowerShell：

```powershell
git clone https://github.com/letswritetw/lets-social.git "$HOME/.agents/skills/lets-social"
```

cmd：

```text
git clone https://github.com/letswritetw/lets-social.git "%USERPROFILE%/.agents/skills/lets-social"
```

</details>

或安裝在單一 repository，在 repository 根目錄執行：

```bash
git clone https://github.com/letswritetw/lets-social.git .agents/skills/lets-social
```

Codex 可以依 description 自動選用，也可以用 `$lets-social` 明確呼叫。詳細規格請參考 [OpenAI Skills 官方文件](https://developers.openai.com/codex/skills)。

```text
$lets-social 把 ./article.md 轉成 Instagram 與 Threads 貼文。
```

#### 其他支援 Agent Skills 的工具

請依工具文件提供的安裝路徑，複製完整的 `lets-social` 目錄。此專案遵循 [Agent Skills 規格](https://agentskills.io/specification)，使用包含 `name` 與 `description` 的 YAML frontmatter、Markdown 指令本文，以及按需求讀取的 reference 檔案。

安裝後，可以從工具的 Skill 選單呼叫 `lets-social`，或在提示中直接指定：

```text
使用 lets-social，把這篇文章轉成 Facebook 與 Telegram 貼文。
```

Agent Skills 規格定義可攜的封裝格式，不負責統一各工具的安裝路徑，也不保證每個工具都支援相同的產品專屬功能。`lets-social` 只使用共通 frontmatter 欄位與一般 Markdown 相對連結，降低對單一工具的依賴。

### 版本與更新

目前版本記錄在 `SKILL.md` 的 `metadata.version`，各版本變更請參考 [CHANGELOG](CHANGELOG.md)。版本號遵循 [Semantic Versioning](https://semver.org/lang/zh-TW/)：修正增加 PATCH、向下相容功能增加 MINOR、不相容變更增加 MAJOR。

#### Git 更新（建議）

使用 Git Clone 安裝的使用者，可以依安裝位置執行：

```bash
# Claude Code 個人 Skill
git -C ~/.claude/skills/lets-social pull --ff-only

# Codex 個人 Skill
git -C ~/.agents/skills/lets-social pull --ff-only
```

<details>
<summary>Windows 使用者請點這裡</summary>

PowerShell 和 cmd 一樣不會展開 `~`。Git Bash 可直接使用上面的指令。

PowerShell，Claude Code：

```powershell
git -C "$HOME/.claude/skills/lets-social" pull --ff-only
```

PowerShell，Codex：

```powershell
git -C "$HOME/.agents/skills/lets-social" pull --ff-only
```

cmd，Claude Code：

```text
git -C "%USERPROFILE%/.claude/skills/lets-social" pull --ff-only
```

cmd，Codex：

```text
git -C "%USERPROFILE%/.agents/skills/lets-social" pull --ff-only
```

</details>

專案層級或其他 Agent 的安裝位置，請將上面的路徑替換為實際的 `lets-social` 目錄。`--ff-only` 會在本機內容與遠端版本分歧時停止，不會直接覆蓋使用者的修改。

下載 ZIP 或直接複製資料夾的使用者，請重新下載最新版，並以完整目錄取代舊版。若曾自訂 Skill，請先備份或保留差異。

#### 發布新版本（維護者）

1. 更新 `SKILL.md` 的 `metadata.version`。
2. 將版本內容與日期寫入 `CHANGELOG.md`。
3. Commit 後建立同版本 Git tag，推送 `main` 與 tag，再用該 tag 建立 GitHub Release。

```bash
VERSION="1.0.0"
git tag -a "v${VERSION}" -m "v${VERSION}"
git push origin main "v${VERSION}"
```

#### 使用 Skillshare 追蹤（選用）

[Skillshare](https://github.com/runkids/skillshare) 使用者可以用它安裝並更新：

```bash
skillshare install letswritetw/lets-social
skillshare sync
```

之後檢查與更新：

```bash
skillshare check lets-social
skillshare update lets-social
skillshare sync
```

請不要加 `--track`。這個 repository 把 `SKILL.md` 放在根目錄，`--track` 會改用追蹤模式，把它記成 `_lets-social` 並回報 `0 skills`，Skill 不會被 sync 到 Agent 的目錄。不加 `--track` 時 `skillshare update` 一樣可以更新。

Skillshare 是選用的第三方工具，不是執行 `lets-social` 的必要相依套件。

### 使用範例

```text
使用 lets-social，把 article.md 轉成 Instagram、Facebook、
Threads 與 Telegram 貼文。
```

```text
幫我宣傳這篇技術文章，只做 Threads 和 Telegram。Threads 口語一點，
Telegram 像頻道公告，所有平台都不要 Hashtag。
```

```text
把這篇文章改寫成 Facebook 宣傳文。保留作者的技術語氣，
CTA 要引導讀者閱讀完整文章。
```

```text
Instagram 不要產圖 prompt；Threads 這篇要一張配圖。
```

如果 Agent 無法讀取網址，Skill 會停止產生貼文，並要求你提供文章本文或 Markdown。它不會假裝已經讀過網頁。

### 支援的來源

- 已完成的純文字或 Markdown
- 可讀取的本機文章或文件
- 目前 Agent 具備網頁讀取能力時可使用網址
- 先前由 `lets-social` 產生的內容，可用於單一平台調整

來源必須包含足以支撐貼文的文章內容。只有標題或搜尋摘要並不足夠。

### 各平台規則

平台細節放在獨立 reference，Agent 只會讀取本次需要的平台：

- [Instagram](references/instagram.md)
- [Facebook](references/facebook.md)
- [Threads](references/threads.md)
- [Telegram](references/telegram.md)

共用規則請參考 [品牌語氣](references/brand-voice.md)、[產圖 prompt](references/image-prompts.md) 與 [輸出格式](references/output-format.md)。

### 產圖 prompt

Instagram 預設在文案後輸出 `Image Direction`、`Nano Banana 2 Prompt` 與 `ChatGPT Images 2.0 Prompt`。兩份 prompt 都是完整內容，可以分別貼進 Gemini 與 ChatGPT，不需要再補文章背景。

Threads 只有在圖片能說明比較、流程、具體物件、空間關係或文章支持的視覺概念時才輸出這三個欄位。純觀點與討論型貼文會保留文字形式。使用者可以明確要求加入或省略圖片 prompt。

每個平台各自建立 Image Brief。同一平台的兩份 prompt 必須使用相同主體、構圖、圖中文字與排除條件。

#### 視覺風格依文章挑選

不套用單一固定風格。Skill 會依文章實際內容選一個方向，在 Image Brief 說明選擇理由，並讓同一平台的所有圖片維持同一套風格。

| 方向 | 適合的文章 |
| --- | --- |
| 知識圖卡 | 檢查清單、評估條件、操作步驟 |
| 編輯式圖解 | 架構、資料流、請求生命週期、前後對照 |
| 大字海報 | 單一主張或一個反直覺的結論 |
| 終端機或藍圖 | 底層工程、工具、協定、除錯 |
| 插畫場景 | 團隊流程、職涯、決策 |

原文若指向更合適的方向，也可以改寫成自訂風格。使用者明確指定風格時以使用者為準。

#### 每份 prompt 都會包含的內容

- 至少四個具名顏色，並說明每個顏色負責什麼；使用者要求單色時例外。
- 來源支持的重點短句，直接寫在圖上。
- 閱讀層級：哪個元素先讀、其次、最後。
- 足夠的紋理、標註或結構細節，避免變成空泛的素材圖。
- 讓畫面活起來的具體條件：有個性的線條、刻意打破的格線、印刷或紙張紋理、動態記號，以及每張圖至少一個具體主體。prompt 中禁止出現 `flat vector`、`consistent stroke weight`、`generous whitespace` 這類會把個性抹平的字眼，除非使用者要的就是收斂或極簡。
- 來源有多個並列項目（四個平台、三個步驟）時，每一項要有各自的圖示、傾斜角度與主色，不畫成一模一樣的方塊。
- 不畫人的手、臉與人物。產圖模型畫手一定進恐怖谷，需要「指、推、擋、點」這類動作時改用箭頭、速度線、懸空的物件或印章。
- 箭頭要短、走直線或單一平緩弧線、桿身粗、箭頭是實心三角形。禁止扭曲、蛇行、多重彎曲或細長飄尾的箭頭，那會渲染成一撮頭髮。手感靠筆壓不均與輕微傾斜，不靠把路徑扭起來。
- 封面（單張或系列的第 1 張）要有一行識別文字，放在主標上方、字級小一號：原文標題夠短就用標題，太長則改用文章在講的那個名字（工具、產品或 skill 名），或不改變原意的縮短標題，上限 16 個中文字。系列的其他張不重複。

#### 圖中文字與字體規則

圖中文字預設為必要，不是選配。標題一句、重點三到五句、可選的結語一句，全部在 prompt 中逐字列出並指定位置，並要求模型不要輸出其他文字。每一句都必須是原文支持的說法，不能新增數字、結果或保證。

中文、日文、韓文一律指定清楚精確的粗體無襯線字，不使用手寫、毛筆、書法或做舊效果。產圖模型處理手寫 CJK 一定會糊，這條規則在所有風格下都成立。裝飾性手寫只用在兩到四個字的英文短語上，並且在 prompt 中明講這個分工。

#### 兩個模型的差別

Nano Banana 2 維持單張，對應 Instagram 的 4:5 封面。

ChatGPT Images 2.0 一次最多可產 10 張，且每張可以承載不同內容，所以它那份 prompt 是一組編號系列：第 1 張是封面，之後每個重點各一張，可選最後一張放結語或導讀 CTA。預設為封面加三到五個重點，也就是四到六張；輸出含 Carousel 大綱時改以大綱為準。整組共用同一個背景、色盤、字體規則與視覺語彙，只有內容改變。需要單張時，只取第 1 張。

Skill 只撰寫 prompt，不會連線到 Gemini 或 ChatGPT。實際產圖功能與費用依使用者的帳號方案而定。

### 自訂品牌語氣

預設語氣清楚、專業、容易親近，並以實用與易懂的方式表達技術內容。原文明確呈現的作者語氣擁有較高優先順序。

你可以直接用自然語言覆寫設定：

```text
語氣更像個人心得，不要 emoji，不要 Hashtag，技術名詞要精確。
```

使用者可以調整文風，但不能藉此改變來源事實或加入沒有根據的資訊。

### 只產生部分平台

只要指定需要的平台：

```text
只產生 Threads 與 Telegram。
```

後續也能只調整單一平台：

```text
Threads 再短一點，語氣更口語。
```

Skill 只會修改 Threads，不會重新產生其他平台內容。

### 專案結構

```text
lets-social/
├── .gitignore
├── SKILL.md
├── README.md
├── README-full.md
├── CHANGELOG.md
├── LICENSE
├── references/
│   ├── instagram.md
│   ├── facebook.md
│   ├── threads.md
│   ├── telegram.md
│   ├── brand-voice.md
│   ├── image-prompts.md
│   └── output-format.md
└── examples/
    ├── input-example.md
    └── output-example.md
```

此 repository 不需要 runtime、套件管理工具、建置系統或 API server。只有實際使用 prompt 產圖時才需要開啟外部產圖服務。

### 新增其他平台

1. 在 `references/` 新增一份專用文件，定義平台目標、內容判斷、輸出欄位與檢查項目。
2. 在 `SKILL.md` 加入平台路由，不要把詳細規則複製回主檔。
3. 在 `references/output-format.md` 加入最小且實用的輸出格式。
4. 補上範例，並確認 Hook、結構、資訊順序與 CTA 都和其他平台不同。

除非需要可重複且具確定性的工具操作，否則請維持純指令結構。

### 完整範例

內建範例使用以下問題：**Web Bluetooth 能不能用 JavaScript 直接連接公司的 Bluetooth 裝置？**

- [範例來源文章](examples/input-example.md)
- [四平台輸出與 Instagram 產圖 prompt 範例](examples/output-example.md)

這篇虛構來源不包含瀏覽器市占率或其他未經證實的精確數字。

### GitHub Repository Description 建議

> Repurpose articles into platform-native posts for Instagram, Facebook, Threads, and Telegram.

### 參與貢獻

請在 issue 或 pull request 中提供具體來源範例、未達預期的輸出，以及你期望的平台行為。變更應維持單一目標；若沒有明確需求，請勿增加 runtime dependency。規則若改變可觀察的輸出，也要更新範例。

送出前，請檢查來源忠實度、平台差異、Markdown 連結，以及 `lets-social` 名稱是否一致。

### 授權

[MIT](LICENSE) © 2026 Let's Write.

---

## English

Turn one article into platform-native social content for Instagram, Facebook, Threads, and Telegram.

This is the full documentation. For a quick start, see the [short README](README.md).

`lets-social` is an open-source project from [Let's Write](https://www.letswrite.tw/). The name extends **Let's Write** into **Let's Social**, but the skill works with any publication, author, or brand.

### What is lets-social?

`lets-social` is an instruction-only Agent Skill. Give it a completed article, Markdown, plain text, a readable local file, or a URL the agent can access. It builds one internal Source Brief, then writes each requested platform independently. Instagram includes copy-ready prompts for Nano Banana 2 and ChatGPT Images 2.0 by default. Threads includes them only when a visual supports the post.

It does not publish, schedule, or research claims for you. It preserves the source's facts, uncertainty, stance, and author voice.

### Why it exists

Readers do not approach every social platform in the same way. A Facebook post may need context, a Threads post may work best as one sharp observation, and a Telegram message may need a compact list. `lets-social` makes those decisions per platform instead of reformatting one master caption. It applies the same platform judgment to images: Instagram gets a visual by default, while Threads skips decorative media.

### Supported platforms

| Platform | Default output | Native emphasis |
| --- | --- | --- |
| Instagram | Caption, CTA, optional hashtags or carousel, and image prompts | Mobile scanning, practical value, and a visual |
| Facebook | Post and CTA | Context, motivation, and author perspective |
| Threads | Single post or justified thread; image prompts when useful | Conversational observation and discussion |
| Telegram | Message and link placement recommendation | Clarity, scanability, and information density |

LinkedIn, X, Bluesky, and Mastodon are not implemented in version `1.0.0`.

### How it works

```text
Source article
    -> Internal Source Brief
        -> Instagram draft
        -> Facebook draft
        -> Threads draft
        -> Telegram draft
        -> Instagram Image Brief
        -> Optional Threads Image Brief
    -> Two complete model prompts per Image Brief
    -> Fidelity and differentiation check
    -> Markdown output
```

Every platform starts from the same Source Brief. No platform draft becomes the input for another. Both model prompts for one platform use the same Image Brief, so they preserve the subject, composition, and message.

### Installation

Clone or download this repository, then place the complete `lets-social` directory in a skill location supported by your agent. Keep `SKILL.md`, `references/`, and `examples/` together.

To retain update history, use Git Clone and clone directly into one of the skill locations below. ZIP downloads do not retain Git update history.

#### Claude Code

Install as a personal skill:

```bash
git clone https://github.com/letswritetw/lets-social.git ~/.claude/skills/lets-social
```

<details>
<summary>On Windows, read this</summary>

Git Bash runs the command above as it is. PowerShell and cmd do not expand `~`, so they create a folder literally named `~` in the current directory. Use these instead.

PowerShell:

```powershell
git clone https://github.com/letswritetw/lets-social.git "$HOME/.claude/skills/lets-social"
```

cmd:

```text
git clone https://github.com/letswritetw/lets-social.git "%USERPROFILE%/.claude/skills/lets-social"
```

</details>

Or install inside one project, running this from the project root:

```bash
git clone https://github.com/letswritetw/lets-social.git .claude/skills/lets-social
```

Claude Code discovers both locations and can invoke the skill automatically from its description or explicitly as `/lets-social`. See the official [Claude Code skills documentation](https://code.claude.com/docs/en/skills).

```text
/lets-social Turn ./article.md into Instagram and Threads posts.
```

#### Codex

Install as a personal skill:

```bash
git clone https://github.com/letswritetw/lets-social.git ~/.agents/skills/lets-social
```

<details>
<summary>On Windows, read this</summary>

Git Bash runs the command above as it is. PowerShell and cmd do not expand `~`. Use these instead.

PowerShell:

```powershell
git clone https://github.com/letswritetw/lets-social.git "$HOME/.agents/skills/lets-social"
```

cmd:

```text
git clone https://github.com/letswritetw/lets-social.git "%USERPROFILE%/.agents/skills/lets-social"
```

</details>

Or install inside one repository, running this from the repository root:

```bash
git clone https://github.com/letswritetw/lets-social.git .agents/skills/lets-social
```

Codex can match the skill description automatically or invoke it explicitly with `$lets-social`. See the official [OpenAI skill documentation](https://developers.openai.com/codex/skills).

```text
$lets-social Turn ./article.md into Instagram and Threads posts.
```

#### Generic Agent Skills hosts

Use the installation path documented by your host and copy the entire directory there.

The package follows the [Agent Skills specification](https://agentskills.io/specification): YAML frontmatter with `name` and `description`, a Markdown instruction body, and on-demand supporting files.

After installation, invoke `lets-social` through the host's skill picker or ask the agent to use it by name:

```text
Use lets-social to create Facebook and Telegram posts from this article.
```

The Agent Skills specification defines a portable package format. It does not define one universal installation path or guarantee that every agent supports every host-specific feature. `lets-social` uses only shared frontmatter fields and plain Markdown references to reduce host-specific behavior.

### Versions and updates

The current version is stored in `metadata.version` inside `SKILL.md`. See the [changelog](CHANGELOG.md) for release notes. Versions follow [Semantic Versioning](https://semver.org/): PATCH for fixes, MINOR for backward-compatible features, and MAJOR for incompatible changes.

#### Update with Git (recommended)

If you installed with Git Clone, run the command matching the installation location:

```bash
# Personal Claude Code skill
git -C ~/.claude/skills/lets-social pull --ff-only

# Personal Codex skill
git -C ~/.agents/skills/lets-social pull --ff-only
```

<details>
<summary>On Windows, read this</summary>

PowerShell and cmd do not expand `~` here either. Git Bash runs the commands above as they are.

PowerShell, Claude Code:

```powershell
git -C "$HOME/.claude/skills/lets-social" pull --ff-only
```

PowerShell, Codex:

```powershell
git -C "$HOME/.agents/skills/lets-social" pull --ff-only
```

cmd, Claude Code:

```text
git -C "%USERPROFILE%/.claude/skills/lets-social" pull --ff-only
```

cmd, Codex:

```text
git -C "%USERPROFILE%/.agents/skills/lets-social" pull --ff-only
```

</details>

For a project-level or another agent installation, replace the path with the actual `lets-social` directory. `--ff-only` stops when local and remote histories have diverged instead of overwriting local changes.

If you downloaded a ZIP or copied the directory, download the latest version and replace the complete old directory. Back up or preserve your diff first if you customized the skill.

#### Publish a new version (maintainers)

1. Update `metadata.version` in `SKILL.md`.
2. Add the version contents and date to `CHANGELOG.md`.
3. Commit, create the matching Git tag, push `main` and the tag, then create a GitHub Release from that tag.

```bash
VERSION="1.0.0"
git tag -a "v${VERSION}" -m "v${VERSION}"
git push origin main "v${VERSION}"
```

#### Track with Skillshare (optional)

If you use [Skillshare](https://github.com/runkids/skillshare), install it with:

```bash
skillshare install letswritetw/lets-social
skillshare sync
```

To check for and apply updates later:

```bash
skillshare check lets-social
skillshare update lets-social
skillshare sync
```

Do not add `--track`. This repository keeps `SKILL.md` at its root, and `--track` switches to tracked-repo mode, which records it as `_lets-social`, reports `0 skills`, and never syncs the skill into your agent's directory. `skillshare update` works without `--track`.

Skillshare is an optional third-party tool, not a runtime dependency of `lets-social`.

### Usage examples

```text
Use lets-social to turn article.md into Instagram, Facebook, Threads,
and Telegram posts.
```

```text
Promote this technical article on Threads and Telegram only. Keep Threads
conversational, make Telegram read like a channel announcement, and skip
hashtags everywhere.
```

```text
Repurpose https://example.com/article for Facebook. Keep the author's
technical tone and make the CTA point readers to the full article.
```

```text
Skip image prompts for Instagram. Add one image concept for Threads.
```

If the agent cannot read a URL, the skill stops and asks for the article text or Markdown. It must not pretend that it read the page.

### Supported input

- Completed plain text or Markdown
- Readable local documents and article files
- URLs when the current agent has web-reading access
- A prior `lets-social` result for a scoped platform revision

The source must contain enough article content to ground the posts. A title or search snippet is not enough.

### Platform behavior

Platform rules live in separate reference files and load only when needed:

- [Instagram](references/instagram.md)
- [Facebook](references/facebook.md)
- [Threads](references/threads.md)
- [Telegram](references/telegram.md)

Shared behavior lives in [brand voice](references/brand-voice.md), [image prompts](references/image-prompts.md), and [output format](references/output-format.md).

### Image prompts

Instagram appends `Image Direction`, `Nano Banana 2 Prompt`, and `ChatGPT Images 2.0 Prompt` after the post copy by default. Each model prompt contains the full context needed for the user to paste it into Gemini or ChatGPT.

Threads adds the three fields only when an image clarifies a comparison, process, physical subject, spatial relationship, or source-grounded visual concept. Text-first observations and discussion prompts stay text only. The user can request or suppress image prompts.

Each platform gets its own Image Brief. Both prompts for that platform preserve the same subject, composition, on-image text, and exclusions.

#### The visual style is chosen per source

There is no single house style. The skill picks a direction from what the source actually is, states why in the Image Brief, and keeps that direction consistent across every image for the platform.

| Direction | Sources it fits |
| --- | --- |
| Handwritten-digital knowledge card | Checklists, evaluation criteria, how-to steps |
| Editorial diagram | Architecture, data flow, request lifecycles, before-and-after |
| Bold typographic poster | One strong opinion or a single counterintuitive claim |
| Retro terminal or blueprint | Low-level engineering, tooling, protocols, debugging |
| Soft illustrated scene | Team process, career, decision-making |

A source that suggests a better direction can get a custom one. An explicit user request wins over all of them.

#### What every prompt specifies

- At least four named colors, each with a stated job, unless the user asked for a monochrome look.
- The source-grounded key points, written on the image.
- Hierarchy: which element reads first, second, and last.
- Enough texture, markup, or structural detail that the image does not read as bare stock art.
- The concrete conditions that keep an image alive: line with character, a deliberately broken grid, print or paper texture, motion marks, and one concrete subject per image. Phrases like `flat vector`, `consistent stroke weight`, and `generous whitespace` are banned from prompts unless the user actually wants a restrained or minimal look.
- When the source has parallel items (four platforms, three steps), each gets its own icon, tilt, and accent color instead of an identical box.
- No human hands, faces, or figures. Image models render them into uncanny valley, so actions like pointing, pushing, blocking, or tapping are carried by arrows, speed lines, hovering objects, or stamps instead.
- Arrows are short, straight or on one gentle arc, thick-shafted, and end in a solid triangular head. Wobbly, squiggly, serpentine, and thin trailing arrows are banned because they render as strands of hair; hand feel comes from uneven pressure and slight tilt instead.
- The cover (the single image, or image 1 of a series) carries one identifying line above the headline in smaller type: the source title when short enough, otherwise the named subject or a faithful shortened title, capped at sixteen Chinese characters. It is never repeated on the other images in a series.

#### On-image text and the typography rule

On-image text is required by default, not optional. One headline, three to five key-point lines, and an optional closing takeaway are listed verbatim in the prompt with their placement, and the model is told to render no other lettering. Every string restates the source; none may add numbers, results, or guarantees the source does not state.

Every Chinese, Japanese, and Korean string is requested as clean, precise, bold sans-serif type. Never handwritten, brush, calligraphic, or distressed, because image models garble handwritten CJK. That rule holds across every style. Decorative handwriting is limited to short English phrases of two to four words, and both prompts state the split explicitly.

#### How the two models differ

Nano Banana 2 stays single-image and matches the Instagram 4:5 cover.

ChatGPT Images 2.0 returns up to ten images from one prompt and each can carry different content, so its prompt describes a numbered series: image 1 is the cover, each following image covers one key point, and an optional final image carries the takeaway or the call to read. The default is a cover plus three to five key points, so four to six images; when the Instagram output includes a carousel outline, the series follows that outline instead. The whole set shares one background, palette, font rule, and visual vocabulary, so only the content changes. Ask for a single image and only image 1 is requested.

The skill writes prompts and does not connect to Gemini or ChatGPT. Image availability and cost depend on the user's account plan.

### Brand voice customization

The default voice is clear, professional, approachable, practical, and technical without becoming hard to read. The source author's established voice takes priority.

You can override it in natural language:

```text
More personal, no emoji, no hashtags, and keep technical terms precise.
```

User preferences control style, but they cannot override source fidelity or authorize unsupported facts.

### Partial platform generation

Name only the platforms you need:

```text
Create Threads and Telegram versions only.
```

For a follow-up, ask for one scoped revision:

```text
Make Threads shorter and more conversational.
```

The skill changes only Threads and leaves the other platform drafts untouched.

### Project structure

```text
lets-social/
├── .gitignore
├── SKILL.md
├── README.md
├── README-full.md
├── CHANGELOG.md
├── LICENSE
├── references/
│   ├── instagram.md
│   ├── facebook.md
│   ├── threads.md
│   ├── telegram.md
│   ├── brand-voice.md
│   ├── image-prompts.md
│   └── output-format.md
└── examples/
    ├── input-example.md
    └── output-example.md
```

The repository has no runtime, dependency manager, build system, or API server. External image access is needed only when the user pastes a prompt into an image service.

### Adding another platform

1. Add one focused file under `references/` with native goals, decisions, output fields, and a pre-flight check.
2. Add the platform to the reference list in `SKILL.md` without copying its detailed rules there.
3. Extend `references/output-format.md` with the smallest useful output contract.
4. Add a platform version to the example and verify that it differs in hook, structure, information order, and CTA.

Keep new platform rules source-faithful and instruction-only unless deterministic tooling becomes necessary.

### Example

The included example uses the question: **Can JavaScript connect directly to a company's Bluetooth device with Web Bluetooth?**

- [Example source](examples/input-example.md)
- [Four platform-native outputs with Instagram image prompts](examples/output-example.md)

The fictional source avoids browser-share statistics and other unsupported precision.

### GitHub repository description

> Repurpose articles into platform-native posts for Instagram, Facebook, Threads, and Telegram.

### Contributing

Open an issue or pull request with a concrete source example, the output that failed, and the platform behavior you expected. Keep changes focused, avoid adding runtime dependencies without a demonstrated need, and update the example when a rule changes observable output.

Before submitting, verify source fidelity, platform differentiation, Markdown links, and consistency of the `lets-social` name.

### License

[MIT](LICENSE) © 2026 Let's Write.
