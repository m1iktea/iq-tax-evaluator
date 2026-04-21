# iq-tax-evaluator · 智商税鉴定 Skill

A [Claude Code](https://docs.claude.com/claude-code) skill for fact-checking consumer products, supplements, folk remedies, and "common wisdom" against authoritative scientific evidence — and, crucially, **admitting uncertainty instead of making things up** when evidence is lacking.

一个用于鉴定生活中产品、保健品、偏方、"常识" 是否是智商税的 Claude Code skill。**核心原则：只认权威证据，查不到就说不知道，绝不编造。**

---

## What it does

When you ask things like:

- "X 是智商税吗？"
- "X 有用吗 / 值得买吗 / 靠谱吗？"
- "Is X a scam / pseudoscience / worth buying?"
- "吃 X 能治 / 预防 / 改善 ... 吗？"

the skill makes Claude:

1. **Translate** your question into a concrete, falsifiable claim.
2. **Search authoritative sources** in a strict hierarchy (Cochrane, PubMed, WHO, FDA, CDC, NHS, NEJM/Lancet/JAMA/BMJ, Consumer Reports, 国家卫健委, 丁香医生, etc.).
3. **Refuse to cite** marketing pages, KOL content, 小红书 / 抖音 personal anecdotes, or brand-sponsored "research".
4. **Assign a five-level verdict** — 🟢 evidence-backed / 🟡 exaggerated / 🟠 insufficient evidence / 🔴 pseudoscience / ⚪ **I don't know**.
5. **Force itself to say "I don't know"** when authoritative sources aren't available, instead of fabricating plausible-sounding answers.

## The Iron Rule

> If no authoritative source supports a claim, the skill MUST say *"insufficient evidence / I don't know"* — never fabricate studies, numbers, or conclusions.
>
> 如果没有权威来源支持，必须明确说 "不知道 / 证据不足"，绝不编造研究、数据或结论。

## Install

### Claude Code (personal skill)

```bash
git clone https://github.com/m1iktea/iq-tax-evaluator.git ~/.claude/skills/iq-tax-evaluator
```

That's it. Claude Code auto-discovers skills in `~/.claude/skills/`. Next time you ask "X 是智商税吗" the skill will activate.

To update:

```bash
cd ~/.claude/skills/iq-tax-evaluator && git pull
```

### Project-scoped skill

If you prefer to scope the skill to a single project:

```bash
mkdir -p .claude/skills
git clone https://github.com/m1iktea/iq-tax-evaluator.git .claude/skills/iq-tax-evaluator
```

## How to use it

Just ask naturally:

```
> 十月结晶的消毒柜值得买吗
> 益生菌真的能改善免疫力吗
> Is collagen supplement a scam?
> 网红的那个量子能量项链靠谱吗
```

Claude will pick up the skill automatically and walk through:

1. 主张 (Claim)
2. 证据摘要 (Evidence with linkable sources)
3. 判定 (one of the five levels)
4. 为什么是这个判定 (Reasoning)
5. 实用建议 (Practical advice — price, who actually needs it, safer/cheaper alternatives, real risks)
6. 不确定性 / 局限 (Explicit uncertainty)

## Source Hierarchy

**Tier 1 — International authorities**
Cochrane · PubMed/NIH · WHO · FDA/EMA/MHRA · CDC/ECDC · NEJM/Lancet/JAMA/BMJ · UpToDate/DynaMed · USDA/EFSA · Consumer Reports/Which?

**Tier 2 — Chinese authorities**
国家卫健委 · 国家药监局 (NMPA) · 市场监管总局 · 中国营养学会 · 中华医学会各分会诊疗指南 · 丁香医生 / 丁香园 · 果壳网 / 科学松鼠会

**Tier 3 — Use cautiously**
Wikipedia (only as a jump-off to the actual cited source) · single studies not yet included in systematic reviews

**❌ Not evidence**
Marketing pages · KOL / 小红书 / 抖音 / 公众号 anecdotes · brand-sponsored "research" · "thousand-year-old wisdom" · "some doctor said" without a findable source

## Red Flags the skill watches for

- "量子 / 纳米 / 负离子 / 远红外 / 能量 / 频率" used as hand-waving
- "排毒 / 酸碱体质 / 增强免疫力 / 激活细胞"
- "祖传 / 宫廷 / 千年古方" applied to modern conditions
- "纯天然所以无副作用"
- NASA / Nobel / overseas endorsements with no verifiable link
- Before-after testimonials without clinical data
- Cures-everything claims
- High prices on cheap, commodity ingredients
- Urgency tactics ("limited stock", "last chance")
- Claimed mechanisms that violate basic physics / chemistry / biology

## Contributing

This skill is personally maintained. Issues and PRs welcome — particularly:

- New authoritative sources to add to the hierarchy (especially non-English ones)
- Additional red-flag patterns
- Cases where the skill made Claude fabricate something anyway (so we can plug the hole)

## License

[MIT](./LICENSE) © 2026 m1iktea

## Acknowledgements

Inspired by evidence-based medicine principles, the Cochrane Collaboration approach to systematic review, and the general ethos that "I don't know" is a valid and often correct answer.
