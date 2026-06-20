## Appendix I — Act-Level Committee Classification

This appendix gives the full specification of the Act-level committee classifier of the Act-Level Committee Classification section: the deterministic ministry-to-committee mapping that drives Tier 1, the closed (committee, topic) dictionary and the prompt that constrain Tier 2, the Tier-2 output schema with a worked example, and the committee distribution Tier 1 produces over the corpus. The implementation is `src/topic_classification/`, with the Tier-1 mapping verified by `scripts/check_tier1_mapping.py`. The committee assignments for several historical or cross-portfolio agencies (§I.2) are working judgments pending a fuller per-keyword audit.

### I.1 Tier-1 ministry-to-committee mapping

The Tier-1 mapping reads the *This Act is administered by [Ministry]* statement recorded on NZL (the *administered in the* variant is treated identically), lower-cases it, and matches it against the substring table below, resolving each statement to one or more of the 12 committee subject areas. Matching is order-sensitive: longer, more specific strings are tested before shorter ones, so that *ministry of social development and the ministry of health* is caught before *ministry of social development*. Table I.1 covers all 173 distinct administering-agency strings observed in the corpus and labels 6,665 Acts (34.6%); the remaining Acts carry no such statement and are left for the LLM tier (Classification Cascade).

**Table I.1 — Tier-1 ministry-to-committee mapping.**

| Administering-agency keyword (lower-cased substring) | Committee(s) |
|---|---|
| `ministry of justice` | Justice |
| `department of justice` | Justice |
| `department for courts` | Justice |
| `new zealand police` | Justice |
| `the police` | Justice |
| `police department` | Justice |
| `department of corrections` | Justice |
| `corrections` | Justice |
| `crown law office` | Justice |
| `crown legal` | Justice |
| `the treasury` | Finance and Expenditure |
| `treasury` | Finance and Expenditure |
| `inland revenue` | Finance and Expenditure |
| `reserve bank` | Finance and Expenditure |
| `state advances corporation` | Finance and Expenditure |
| `rural banking and finance` | Finance and Expenditure |
| `government life insurance` | Finance and Expenditure |
| `earthquake and war damage` | Finance and Expenditure |
| `ministry of business, innovation, and employment` | Economic Development, Science and Innovation / Education and Workforce |
| `ministry of business, innovation and employment` | Economic Development, Science and Innovation / Education and Workforce |
| `ministry of business, employment, and innovation` | Economic Development, Science and Innovation / Education and Workforce |
| `ministry of business,innovation` | Economic Development, Science and Innovation / Education and Workforce |
| `ministry for business, innovation` | Economic Development, Science and Innovation / Education and Workforce |
| `ministry of economic development` | Economic Development, Science and Innovation |
| `ministry of commerce` | Economic Development, Science and Innovation |
| `ministry of consumer affairs` | Economic Development, Science and Innovation |
| `ministry of research, science` | Economic Development, Science and Innovation |
| `department of scientific and industrial research` | Economic Development, Science and Innovation |
| `broadcasting corporation` | Economic Development, Science and Innovation |
| `new zealand broadcasting authority` | Economic Development, Science and Innovation |
| `new zealand broadcasting corporation` | Economic Development, Science and Innovation |
| `broadcasting council` | Economic Development, Science and Innovation |
| `ministry for regulation` | Economic Development, Science and Innovation |
| `tourist hotel corporation` | Economic Development, Science and Innovation |
| `ministry of education` | Education and Workforce |
| `university grants committee` | Education and Workforce |
| `department of labour` | Education and Workforce |
| `labour department` | Education and Workforce |
| `accident compensation corporation` | Education and Workforce |
| `accident rehabilitation and compensation insurance` | Education and Workforce |
| `accident compensation commission` | Education and Workforce |
| `ministry of disabled people` | Social Services and Community |
| `ministry for the environment` | Environment |
| `department of conservation` | Environment |
| `new zealand planning council` | Environment |
| `ministry of civil defence and emergency management` | Governance and Administration |
| `national emergency management agency` | Governance and Administration |
| `canterbury earthquake recovery` | Governance and Administration |
| `ministry of foreign affairs and trade` | Foreign Affairs, Defence and Trade |
| `new zealand customs service` | Foreign Affairs, Defence and Trade |
| `customs department` | Foreign Affairs, Defence and Trade |
| `new zealand defence force` | Foreign Affairs, Defence and Trade |
| `ministry of defence` | Foreign Affairs, Defence and Trade |
| `veterans' affairs` | Foreign Affairs, Defence and Trade |
| `veterans’ affairs` | Foreign Affairs, Defence and Trade |
| `veterans' affairs new zealand` | Foreign Affairs, Defence and Trade |
| `new zealand security intelligence` | Foreign Affairs, Defence and Trade |
| `government communications security` | Foreign Affairs, Defence and Trade |
| `government communications and security` | Foreign Affairs, Defence and Trade |
| `department of internal affairs` | Governance and Administration |
| `parliamentary counsel office` | Governance and Administration |
| `parliamentary service` | Governance and Administration |
| `office of the clerk` | Governance and Administration |
| `department of the prime minister` | Governance and Administration |
| `department of prime minister` | Governance and Administration |
| `state services commission` | Governance and Administration |
| `public service commission` | Governance and Administration |
| `statistics new zealand` | Governance and Administration |
| `te kawa mataaho` | Governance and Administration |
| `valuation department` | Primary Production |
| `national library` | Governance and Administration |
| `ministry of health` | Health |
| `department of health` | Health |
| `ministry of social development and the ministry of health` | Social Services and Community / Health |
| `te puni kōkiri` | Māori Affairs |
| `te puni kokiri` | Māori Affairs |
| `ministry of maori development` | Māori Affairs |
| `ministry of māori development` | Māori Affairs |
| `office for māori crown relations` | Māori Affairs |
| `office for maori crown relations` | Māori Affairs |
| `office of treaty settlements` | Māori Affairs |
| `takutai moana` | Māori Affairs |
| `ministry for primary industries` | Primary Production |
| `ministry of agriculture and forestry` | Primary Production |
| `ministry of fisheries` | Primary Production |
| `department of agriculture` | Primary Production |
| `land information new zealand` | Primary Production |
| `department of land information` | Primary Production |
| `linz` | Primary Production |
| `new zealand government railways` | Transport and Infrastructure |
| `post office` | Transport and Infrastructure |
| `ministry of social development` | Social Services and Community |
| `ministry for social development` | Social Services and Community |
| `oranga tamariki` | Social Services and Community |
| `ministry of housing and urban development` | Social Services and Community |
| `housing corporation` | Social Services and Community |
| `housing new zealand` | Social Services and Community |
| `department of building and housing` | Social Services and Community |
| `sport and recreation new zealand` | Social Services and Community |
| `ministry for culture and heritage` | Social Services and Community |
| `ministry of culture and heritage` | Social Services and Community |
| `public trust` | Social Services and Community |
| `ministry of transport` | Transport and Infrastructure |
| `department of civil aviation` | Transport and Infrastructure |
| `new zealand electricity department` | Transport and Infrastructure |

### I.2 Notable Tier-1 mapping decisions

Most agency names map to their committee by their modern portfolio. The assignments in Table I.2 are judgment calls — historical agencies routed to the committee that inherited their portfolio, or cross-portfolio agencies routed by their dominant remit — and are provisional pending a fuller audit.

**Table I.2 — Notable Tier-1 mapping decisions.**

| Agency keyword | Committee | Rationale |
|---|---|---|
| `tourist hotel corporation` | Economic Development, Science and Innovation | tourism is an Economic subject area |
| civil-defence / emergency-management agencies | Governance and Administration | emergency management is a Governance subject area, not Environment |
| `earthquake and war damage` | Finance and Expenditure | establishes a Treasury-administered insurance fund, not a civil-defence body |
| `land information new zealand`, `valuation department` | Primary Production | "lands, and land information" is a Primary Production subject area |
| `national library` | Governance and Administration | National Library sits under Internal Affairs |
| `post office` | Transport and Infrastructure | historical postal/telegraph infrastructure |
| `department of building and housing` | Social Services and Community | a housing-led department (2004–2012) |
| `ministry for regulation` | Economic Development, Science and Innovation | 2024 ministry with a commerce/business remit |
| MBIE family | Economic + Education (multi-label) | administers both economic-policy and labour/skills/immigration portfolios |

### I.3 Tier-2 (committee, topic) classification dictionary

The Tier-2 prompt constrains the model to the closed set of (committee, topic) pairs in Table I.3; any returned pair outside it is discarded. The dictionary is a snapshot of Zhang's (2026) official taxonomy (`src/topic_classification/taxonomy.py`). It is distinct from the lemma groups of Appendix H: those expand each subject area into morphological variants for the recall and Jaccard metrics, whereas these are the exact labels the LLM must choose among.

**Table I.3 — Tier-2 committee-topic dictionary.**

| Committee | Topics |
|---|---|
| Economic Development, Science and Innovation | business development; tourism; crown minerals; commerce; consumer protection; trading standards; research; science; innovation; intellectual property; broadcasting; communications; information technology |
| Education and Workforce | education; training; employment; immigration; industrial relations; health and safety; accident compensation |
| Environment | conservation; environment; climate change |
| Finance and Expenditure | economic policy; fiscal policy; taxation; revenue; banking and finance; superannuation; insurance; government expenditure; financial performance; public audit |
| Foreign Affairs, Defence and Trade | customs; defence; disarmament; arms control; foreign affairs; trade; veterans’ affairs |
| Governance and Administration | parliamentary services; legislative services; prime minister and cabinet; state services; statistics; internal affairs; civil defence; emergency management; local government |
| Health | health |
| Justice | constitutional matters; electoral matters; human rights; justice; courts; crime; criminal law; police; corrections; crown legal services |
| Māori Affairs | māori affairs; treaty of waitangi negotiations |
| Primary Production | agriculture; biosecurity; racing; fisheries; productive forestry; lands; land information |
| Social Services and Community | social development; social housing; income support; women; children; young people; seniors; pacific peoples; ethnic communities; arts; culture and heritage; sport and recreation; voluntary sector |
| Transport and Infrastructure | transport; transport safety; infrastructure; energy; building and construction |

### I.4 Tier-2 prompt template

The prompt sent to Gemini for each Act (`src/topic_classification/tier2.py`); `{taxonomy}` is the dictionary of §I.3 rendered verbatim and `{act_text}` is the full Act text.

```
You are classifying a New Zealand Act of Parliament by which parliamentary select
committee scrutinises its subject matter.

You will be given the full text of one Act. Read it and assign one or more
(committee, topic, importance) triples that describe what the Act is about.

STRICT CONSTRAINTS
1. Pick committee + topic from the official table below. Use the labels verbatim —
   do not invent, rename, abbreviate, or pluralise.
2. Output JSON only, conforming to this schema:
   {"triples": [{"committee": "<exact committee name>", "topic": "<exact topic
   label>", "importance": <integer 0-100>}, ...]}
3. importance is how central the topic is to this Act (100 = the Act's primary
   purpose; 30-60 = a substantial secondary theme; <30 = incidental). Reserve high
   scores for genuinely central themes.
4. Triples whose (committee, topic) pair is not in the table will be discarded, so
   do not invent.
5. If several topics under one committee apply, emit one triple per topic.
6. Do not output any text outside the JSON object.

OFFICIAL (COMMITTEE, TOPIC) TABLE
{taxonomy}

ACT FULL TEXT
{act_text}
```

### I.5 Tier-2 output schema and worked example

The model is run in JSON mode and returns a single object of the form `{"triples": [{"committee": str, "topic": str, "importance": int 0–100}, ...]}`; triples whose (committee, topic) pair is outside §I.3 are dropped before the Act's committee set is taken. The verbatim response for the Resource Management Act 1991 (eight triples, none dropped) illustrates the cross-portfolio reach a single Act can carry:

```json
{ "triples": [
  { "committee": "Environment Committee",                   "topic": "environment",      "importance": 100 },
  { "committee": "Governance and Administration Committee", "topic": "local government",  "importance":  80 },
  { "committee": "Māori Affairs Committee",                 "topic": "māori affairs",     "importance":  75 },
  { "committee": "Environment Committee",                   "topic": "conservation",      "importance":  70 },
  { "committee": "Transport and Infrastructure Committee",  "topic": "infrastructure",    "importance":  65 },
  { "committee": "Primary Production Committee",             "topic": "lands",             "importance":  60 },
  { "committee": "Justice Committee",                       "topic": "justice",           "importance":  45 },
  { "committee": "Environment Committee",                   "topic": "climate change",    "importance":  40 }
]}
```

### I.6 Tier-1 committee distribution over the corpus

**Table I.4 — Tier-1 committee distribution over the corpus.**

| Committee | Acts |
|---|---:|
| Justice | 1,663 |
| Finance and Expenditure | 1,154 |
| Education and Workforce | 859 |
| Governance and Administration | 790 |
| Economic Development, Science and Innovation | 657 |
| Primary Production | 390 |
| Health | 372 |
| Transport and Infrastructure | 355 |
| Foreign Affairs, Defence and Trade | 292 |
| Social Services and Community | 257 |
| Environment | 192 |
| Māori Affairs | 150 |

Acts assigned to two committees (the MBIE family and the combined social-development-and-health string) are counted in both rows, so the column total (7,131) exceeds the 6,665 labelled Acts.
