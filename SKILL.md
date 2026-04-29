---
name: iq-tax-evaluator
description: Use when user asks whether a product, supplement, health claim, folk remedy, skincare/beauty product, parenting tip, gadget, or piece of "common wisdom" is scientifically valid, worth buying, exaggerated, or a scam. Triggers on Chinese queries like "X是智商税吗", "X有用吗", "X值得买吗", "X靠谱吗", "X真的能...吗", "吃X能治/预防/改善吗", and English equivalents such as "is X a scam/pseudoscience/worth buying" or "does X actually work". Use authoritative, current evidence with citations; for health, nutrition, safety, regulatory, or current product claims, verify with live authoritative sources before concluding and say "证据不足/不知道" if evidence cannot be verified.
---

# 智商税鉴定 Skill (IQ Tax Evaluator)

## Core Rule

鉴定生活中的产品、保健品、偏方、"常识" 是否有科学依据。**只认可核验的权威证据；查不到就说不知道；绝不编造研究、数字或结论。**

> 如果没有权威来源支持，必须明确说 "不知道 / 证据不足"。
> If no authoritative source supports a claim, say "I don't know / insufficient evidence".

## Non-Negotiables

- Treat the user request as an evidence assessment, not a vibe check or purchase persuasion.
- For health, nutrition, supplements, skincare, medical devices, product safety, regulation, or claims that may have changed, search current authoritative sources before giving a verdict. If live search or source access is unavailable, say the evaluation is incomplete and do not make a firm claim.
- Cite only sources you can actually access and link. "I remember a study" is not evidence.
- Do not cite marketing pages, seller copy, KOL posts, personal anecdotes, or unverifiable "某某医生说" as evidence.
- Separate "no evidence found", "evidence is mixed/insufficient", and "evidence shows it does not work".
- Do not directly extrapolate animal, cell, or mechanism-only evidence to real-world human effectiveness.
- For disease treatment, pregnancy, children, chronic disease, medication interactions, or serious symptoms, give evidence context but do not replace medical care; tell the user to consult a qualified clinician.

## Reference Files

Load only the reference needed for the task:

- [references/source-hierarchy.md](references/source-hierarchy.md): authoritative source hierarchy, search targets, and evidence sufficiency rules.
- [references/red-flags.md](references/red-flags.md): common pseudoscience and marketing red flags.
- [references/examples.md](references/examples.md): regression prompts, expected behavior, and common traps.

## Workflow

### Step 0: Define the Claim

Rewrite the user's question into a concrete, falsifiable claim before evaluating.

Examples:

- "值得买吗" -> "For which buying intent is this better than cheaper alternatives?"
- "能增强免疫吗" -> "Does it reduce clinically meaningful infections or improve validated immune outcomes?"
- "能治疗/预防 X 吗" -> "Does it improve or prevent X in humans at the proposed dose and population?"

If intent is unclear but common intents are obvious, enumerate likely intents in the answer instead of asking a follow-up. Ask only when the missing context would materially change safety or the verdict.

### Step 1: Decompose Mechanisms

Break the product or claim into underlying mechanisms, active ingredients, or operating principles.

- Complex products must usually have at least 2 mechanisms, unless the product is genuinely a single active ingredient or single physical mechanism.
- For brand/model claims, separate mechanism evidence from execution evidence: the mechanism may work while a specific product's quality, dose, concentration, wavelength, certification, or testing remains unverified.
- If a mechanism uses vague terms such as "量子", "能量", "频率", "激活细胞", "排毒", or "酸碱体质", first translate it into a standard scientific concept. If no standard concept exists, mark that mechanism 🔴.

### Step 2: Search Evidence Per Mechanism

For each mechanism, try at least three search angles before using 🟠 or ⚪:

1. English academic or technical terms, preferably systematic reviews, guidelines, or authoritative reviews.
2. Official institution, guideline, regulator, or independent testing source.
3. Chinese authoritative or professional source when the product, market, or user context is Chinese.

Record each useful source as: URL, organization/journal, year, and one-sentence conclusion. Use [references/source-hierarchy.md](references/source-hierarchy.md) to select sources and decide whether evidence is sufficient.

### Step 3: Grade Each Mechanism

Use one verdict per mechanism:

| Verdict | Meaning | Use When |
|---|---|---|
| 🟢 有科学依据 | Evidence supports the claim under relevant conditions | For medical/treatment claims: consistent systematic reviews, RCTs, or guidelines. For ordinary physical/consumer mechanisms: multiple authoritative sources, accepted science, or credible independent tests agree. Never use 🟢 from mechanism plausibility alone. |
| 🟡 部分有效但被夸大 | Some evidence exists, but marketing overstates effect, population, dose, or certainty | Benefit is limited to specific conditions, strains, doses, devices, populations, or outcomes. |
| 🟠 证据不足 | Evidence is weak, indirect, conflicting, or not enough for a firm conclusion | Mostly animal/cell studies, small studies, mechanism speculation, low-quality studies, or real disagreement among authoritative sources. |
| 🔴 无科学依据 / 智商税 | Evidence or basic science contradicts the claim | Authoritative sources reject it, high-quality evidence shows no meaningful benefit, or the claimed mechanism has no valid scientific referent. |
| ⚪ 我不知道 | Authoritative evidence cannot be found or accessed | Use only after the three search angles fail or source access prevents verification. Say exactly what could not be verified. |

### Step 4: Synthesize and Advise by Intent

Combine mechanism verdicts into one overall verdict, then answer "should I buy it" by purchase intent.

- A key mechanism 🔴 usually makes the overall verdict 🔴.
- All mechanisms 🟢 but necessity, cost, or product execution is questionable -> usually 🟡.
- Mechanisms are plausible but human/product evidence is weak -> 🟠.
- Mechanisms cannot be verified -> ⚪.
- Buying advice must not be one-size-fits-all. Map each common intent to the relevant mechanism verdict.

Example:

| Purchase Intent | Mechanism Verdict | Advice |
|---|---|---|
| 预防抗生素相关腹泻 | 🟢 | 可以考虑，认准有临床证据的菌株。 |
| 改善 IBS / 便秘 | 🟡 | 可以试，但效果依菌株和人群而异。 |
| 健康人日常增强免疫 | 🟠/🔴 | 通常没必要，优先睡眠、运动、饮食。 |

## Output Format

Start with the conclusion. Do not put a separate "Claim" section.

```markdown
## 结论
<overall emoji> **一句话判断** —— 买 / 不买 / 看情况 + 主因一句话。

## 该不该买（按购买意图）

- 🟢 **如果你是为了 <intent A>（对应机制）** -> 值得/可以考虑，认准 <条件>。
- 🟡 **如果你是为了 <intent B>（对应机制）** -> 可以试，但 <限制>。
- 🟠 **如果你是为了 <intent C>（对应机制）** -> 证据不足，没必要优先买；<替代方案>。
- 🔴 **如果你是为了 <intent D>（对应机制）** -> 不建议花钱。

通用替代方案：...
真正要注意的风险：...

## 机制拆解与逐项证据

### <emoji> 机制 1：<名称>
一句话说明机制和产品声称。
- [来源 机构/年份](url)：关键结论。
- [来源 机构/年份](url)：关键结论。

### <emoji> 机制 2：<名称>
一句话说明机制和产品声称。
- [来源 机构/年份](url)：关键结论。

## 为什么综合判为 <emoji>
2-3 句话说明各机制档位如何合成综合档。硬上限 3 句。

## 我不确定的
只在存在 ⚪ 或重要执行信息缺失时写：没查到什么、还需要什么信息才能进一步判断。
```

## Output Checklist

- 结论段是第一段，1-2 句，不前置铺垫。
- 已把问题改写成可验证主张，但没有单独开 "Claim" 段。
- 复杂产品拆成至少 2 个机制；单一成分/单一机制产品可以例外。
- 每个机制标题都有独立 emoji verdict。
- 每条关键事实都有可点击来源链接。
- 购买建议按意图分条，每条映射回具体机制。
- "为什么综合判为 X" 不超过 3 句。
- 没有把营销、个人经验或品牌赞助内容当作证据。
- 没有把 "证据不足" 写成 "肯定无效"，也没有把 "机制合理" 写成 "已经有效"。
- 医疗高风险场景包含必要的就医/专业咨询边界。

## Bottom Line

这个 skill 的价值不在于多快判定 "智商税"，而在于**该说不知道时明确说不知道**。
