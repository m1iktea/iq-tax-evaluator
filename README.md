# iq-tax-evaluator · 智商税鉴定 Skill

An evidence-first skill for evaluating whether consumer products, supplements, folk remedies, skincare/beauty claims, gadgets, parenting tips, and "common wisdom" are scientifically supported, exaggerated, unsupported, or likely scams.

核心原则：**只认可核验的权威证据；查不到就说不知道；绝不编造研究、数字或结论。**

## What it does

When you ask:

- "X 是智商税吗？"
- "X 有用吗 / 值得买吗 / 靠谱吗？"
- "吃 X 能治 / 预防 / 改善 ... 吗？"
- "Is X a scam / pseudoscience / worth buying?"
- "Does X actually work?"

the skill guides the agent to:

1. Rewrite the question into a concrete, falsifiable claim.
2. Decompose the product into mechanisms, ingredients, or operating principles.
3. Check current authoritative sources before concluding, especially for health, nutrition, safety, or regulatory claims.
4. Grade each mechanism with a five-level verdict: 🟢 evidence-backed, 🟡 partly valid but exaggerated, 🟠 insufficient evidence, 🔴 unsupported/pseudoscience, or ⚪ unknown.
5. Give buying advice by purchase intent instead of a one-size-fits-all answer.

## Install

### Codex

```bash
git clone https://github.com/m1iktea/iq-tax-evaluator.git "${CODEX_HOME:-$HOME/.codex}/skills/iq-tax-evaluator"
```

### Claude Code

```bash
git clone https://github.com/m1iktea/iq-tax-evaluator.git ~/.claude/skills/iq-tax-evaluator
```

To update, `cd` into whichever install path you used and pull:

```bash
cd "${CODEX_HOME:-$HOME/.codex}/skills/iq-tax-evaluator" && git pull
```

## Structure

- `SKILL.md`: concise trigger and workflow instructions.
- `references/source-hierarchy.md`: authoritative source hierarchy and evidence sufficiency rules.
- `references/red-flags.md`: common pseudoscience and marketing red flags.
- `references/examples.md`: regression prompts and common failure modes.
- `agents/openai.yaml`: UI metadata for Codex-style skill listings.

## Use

Ask naturally:

```text
十月结晶的消毒柜值得买吗
益生菌真的能改善免疫力吗
Is collagen supplement a scam?
网红的那个量子能量项链靠谱吗
```

## License

[MIT](./LICENSE) © 2026 m1iktea
