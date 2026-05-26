# Agent Reference: FatBlog Writing & Publishing Rules

## 1. English-in-Chinese Usage Rules

When writing Chinese blog posts, follow these rules for English loanwords:

### KEEP in English (do not translate)
- **Brand / model names**: Hanhart, Tutima, Venus 175, ST1901, NH35, Miyota, Seiko, Sea-Gull, Oris, Jaeger-LeCoultre, Rolex, Blancpain, Zenith, Girard-Perregaux, Cestrian, Casio, etc.
- **Technical horology terms**: ébauche, guilloché, COSC, column wheel, hairspring, balance assembly, escapement, rotor, bridge, calibre
- **Platform / proper nouns**: AliExpress, Taobao, eBay, Amazon, Carousell, GitHub, Jekyll, Bitcoin, Ethereum, Litecoin, Kaspa, BSV
- **Historical / military references**: Dirty Dozen, Luftwaffe
- **Literal caseback / dial text** (when quoting): "HAND WINDING", "POWER RESERVE", "SAPPHIRE", etc.
- **Movement / calibre numbers**: ST2527, ST1901, ST16, ST36, Unitas 6497, ETA 2824
- **Specific product names**: F-91W, MRW-200H, Duro, 6202G

### ALWAYS LOCALIZE to Chinese
- **Common adjectives**: vintage → 复古/老, eccentric → 古怪/离经叛道, maximalist → 极繁主义, utilitarian → 实用主义, hypnotic → 催眠感
- **Common adverbs**: collectively → 总体而言/综合来看, unmistakably → 无可置疑地/ unmistakably 地
- **Colours in descriptions**: tan → 黄褐色/棕褐色, salmon → 三文鱼色, burgundy → 酒红色, khaki → 卡其色
- **Engineered / designed**: engineered → 设计精良的/精工细作的
- **Concepts with natural Chinese equivalents**: cosplay (only keep if used as internet slang verb; otherwise → 扮演/模仿)
- **Avoid**: "vintage 机芯", "engineered 旅行表", "tan 色皮表带", "collectively 代表了", "eccentric 正装表"

### CONTEXTUAL JUDGMENT
- **Cosplay**: keep as loanword when used metaphorically ("这块表 cosplay 成军表"). Use 角色扮演 only if literal.
- **Heritage**: can stay as loanword in watch contexts ("military heritage") if it feels more natural than 传承/遗产 in that sentence.
- **Vibe / mood**: acceptable as casual internet slang in light passages. Use 氛围/情调 in formal description.
- **Enthusiasm / energy**: localize to 气息/活力 unless used in specific art-critical sense.

---

## 2. What to Post & Where

### Blog Structure
- **Jekyll** static site hosted on GitHub Pages at `https://vfxowlsyvh.github.io`
- **Theme**: minima
- **Posts directory**: `/_posts/`
- **Images directory**: `/assets/images/`
- **Categories**: `watch`, `gem`, `art`, `proof-of-work`, `chokin`, `thangka`

### Bilingual Post Format
Every topic must have **two separate files**:
```
_posts/YYYY-MM-DD-title-slug-en.md
_posts/YYYY-MM-DD-title-slug-zh.md
```

Front matter template:
```yaml
---
layout: post
title: "English Title Here"
date: YYYY-MM-DD 00:00:00 +0000
categories: watch
lang: en
---
```

Chinese version:
```yaml
---
layout: post
title: "中文标题"
date: YYYY-MM-DD 00:00:00 +0000
categories: watch
lang: zh
---
```

### Image References
Use relative paths:
```markdown
![Alt text](/assets/images/filename.jpg)
```

### Image Naming Convention
Use descriptive, kebab-case filenames:
```
red-star-zhenghe-front.jpg
red-star-blue-back.jpg
kaspa-teal-dial-detail.jpg
```

Avoid spaces and special characters in filenames.

---

## 3. Writing Style Reference

### Voice
- Informal, witty, observational, slightly cynical but appreciative
- Essay-like personal voice, not Wikipedia-neutral
- Use vivid metaphors and contradictions ("a traffic accident between a pilot's watch and an annual calendar")
- Willing to mock marketing copy while defending the product's charm
- First-person implied ("you are buying someone's judgment")

### Structure
- Lead with a strong, slightly provocative opening
- One main image near the top
- 3–6 sections per post, separated by `---`
- Mix technical specs with cultural/personal commentary
- End with a compact spec line in italics: `*Movement: X. Case: Y. Price: Z.*`

### Tone by Category
- **Watch posts**: knowledgeable about movements, dismissive of brand snobbery, fond of microbrand quirks
- **Gem/mineral posts**: geological + aesthetic appreciation, origin stories
- **Crypto posts**: skeptical of hype, respectful of technical fundamentals, historically informed
- **Art posts**: material-focused, process-oriented, value-conscious

---

## 4. Publishing Procedure

### Step 1: Write & Copy
1. Write both EN and ZH `.md` files to `/_posts/`
2. Copy images to `/assets/images/`
3. Verify image paths in markdown match actual filenames

### Step 2: Commit & Push
```bash
cd /Users/syvh/vfxowlsyvh.github.io
git add _posts/YYYY-MM-DD-*.md assets/images/new-image.jpg
git commit -m "Descriptive commit message"
git push origin main
```

If push is rejected:
```bash
git pull origin main --no-rebase
git push origin main
```

### Step 3: Verify
- Posts appear at `https://vfxowlsyvh.github.io/watch/` (or relevant category page)
- Check `/watch/`, `/gem/`, `/art/`, `/proof-of-work/` index pages use `site.categories["category-name"]`

---

## 5. Common Corrections to Remember

- **Red Star** is a Chinese brand associated with Sea-Gull's ecosystem, export-oriented, often unavailable domestically in China.
- **Tongji (统一机)** = China's 1969–1972 standardized movement, communist industrial policy made mechanical.
- **Sea-Gull ST1901** = hand-wound column-wheel chronograph, descendant of Venus 175.
- **Zheng He regulator** = new precision automatic, NOT vintage Tongji. Dual-time, date, power reserve.
- **Blue sunburst Red Star** = hand-winding, solid caseback.
- **Red dial "中国统机 1972"** = the actual vintage Tongji watch, assembled 2022.
- Prices are NOT "petrol station sandwich" cheap. These are German vendor export pieces, higher than AliExpress impulse buys.

---

## 6. Technical Notes

- Jekyll builds from `main` branch automatically via GitHub Pages
- `timezone: UTC` in `_config.yml`
- Posts with future dates may not appear until that date passes
- `exclude:` in `_config.yml` lists files to ignore during build
- Category pages are custom Jekyll templates in `/watch/index.md`, `/gem/index.md`, etc.
