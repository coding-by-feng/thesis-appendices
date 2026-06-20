## Appendix H — Subject-Area Validation Lemma Groups (Subject-Area Validation Method and Results)

This appendix supports the Subject-Area Validation Method section by listing in full the twelve committee subject areas used to compute the content-similarity recall S(c, j) and lemma-group Jaccard J(c, j). Each subject area is a list of lemma groups, where a lemma group is a frozenset of morphological variants (plurals, adjective forms, conjugations) that all count as a single matching unit under Sakhaee's (2020, §3.2.2) content-similarity definition. Ten committees use parliament.nz's verbatim subject-area bullets with only morphological variants added; two committees — Environment and Māori Affairs — additionally receive a New Zealand-specific synonym layer because their parliament.nz bullets are too narrow to surface the actual corpus vocabulary (Marine Reserves Act, Wildlife Act, Treaty settlement Acts, etc.). Definitions live in `src/network_analysis/community.py:82-389` (`PORTFOLIOS_PARLIAMENT` and `PORTFOLIOS_PARLIAMENT_EXPANDED`; the code retains the legacy name *portfolio* for what this thesis calls a committee subject area).

### H.1 Morphological-variant groups (verbatim parliament.nz bullets)

Ten of the twelve committees carry no domain synonyms beyond the parliament.nz subject bullets. The lemma groups below list only morphological variants of the verbatim bullet words.

**Economic Development, Science and Innovation** — 19 groups
```
{business, businesses} · {development, developments, develop} · {tourism, tourist, tourists}
{crown, crowns} · {mineral, minerals} · {commerce, commercial} · {consumer, consumers}
{protection, protections, protective, protect} · {trading, trade, trades, trader}
{standard, standards} · {research, researches, researcher} · {science, sciences, scientific}
{innovation, innovations, innovative, innovate} · {intellectual} · {property, properties}
{broadcasting, broadcast, broadcaster} · {communication, communications}
{information} · {technology, technologies, technological}
```

**Education and Workforce** — 10 groups
```
{education, educational} · {training, train, trains, trained}
{employment, employ, employed, employer, employers}
{immigration, immigrant, immigrants, immigrate} · {industrial, industry, industries}
{relations, relation} · {health, healthy} · {safety, safe, safer}
{accident, accidents} · {compensation, compensations, compensate, compensated}
```

**Finance and Expenditure** — 14 groups
```
{economic, economy, economies, economical} · {fiscal} · {policy, policies}
{taxation, tax, taxes, taxing} · {revenue, revenues} · {banking, bank, banks}
{finance, finances, financial} · {superannuation, super}
{insurance, insurances, insurer, insure} · {government, governments, governmental}
{expenditure, expenditures, expense, expenses} · {performance, performances, perform}
{public, publics} · {audit, audits, auditor, auditors, auditing}
```

**Foreign Affairs, Defence and Trade** — 9 groups
```
{customs, custom} · {defence, defences, defend, defender}
{disarmament, disarm, disarming} · {arms, arm} · {control, controls, controlled, controlling}
{foreign} · {affairs, affair} · {trade, trades, trading, trader} · {veterans, veteran}
```

**Governance and Administration** — 16 groups
```
{parliamentary, parliament, parliaments} · {legislative, legislation, legislate}
{services, service} · {prime} · {minister, ministers, ministerial, ministry, ministries}
{cabinet, cabinets} · {state, states} · {statistics, statistic, statistical}
{internal} · {affairs, affair} · {civil} · {defence, defences}
{emergency, emergencies} · {management, manage, manager, managers, manages}
{local, locals, locally} · {government, governments, governmental}
```

**Health** — 1 group
```
{health, healthy}
```

**Justice** — 14 groups
```
{constitutional, constitution, constitutions} · {electoral, election, elections, elector, electors}
{matters, matter} · {human, humans, humanity} · {rights, right}
{justice, justices} · {courts, court} · {crime, crimes, criminal, criminals}
{law, laws} · {police} · {corrections, correction, correctional, correct}
{crown, crowns} · {legal} · {services, service}
```

**Primary Production** — 8 groups
```
{agriculture, agricultural} · {biosecurity} · {racing, race, races}
{fisheries, fishery, fishing, fish}
{productive, production, produce, products, product}
{forestry, forest, forests, forester} · {lands, land} · {information}
```

**Social Services and Community** — 20 groups
```
{social, socially} · {development, developments, develop} · {housing, house, houses}
{income, incomes} · {support, supports, supported, supporting}
{women, woman, womens} · {children, child, childrens}
{young, youngest, youth, youths} · {people, person, persons, peoples}
{seniors, senior} · {pacific} · {ethnic, ethnicity, ethnicities}
{communities, community} · {arts, art, artist, artistic}
{culture, cultures, cultural} · {heritage, heritages}
{sport, sports, sporting} · {recreation, recreational}
{voluntary, volunteer, volunteers} · {sector, sectors}
```

**Transport and Infrastructure** — 6 groups
```
{transport, transports, transportation} · {safety, safe, safer}
{infrastructure, infrastructures} · {energy, energies}
{building, build, builds, buildings, builder}
{construction, constructions, construct, constructed}
```

### H.2 NZ-specific synonym extensions

The Environment and Māori Affairs subject areas carry an additional synonym layer in `PORTFOLIOS_PARLIAMENT_EXPANDED` (`community.py:346-389`) on top of their verbatim parliament.nz bullets. The verbatim groups are repeated here for completeness.

**Environment** — 4 verbatim + 10 NZ-statute synonym groups

Verbatim:
```
{conservation, conserve, conservancy} · {environment, environmental, environments}
{climate, climates, climatic} · {change, changes, changed, changing}
```

NZ-specific synonyms (Marine Reserves Act, Wildlife Act, Pollution Control Acts, Heritage New Zealand Pouhere Taonga Act, etc.):
```
{parks, park} · {reserves, reserve} · {marine} · {wildlife}
{pollution, pollute, polluting} · {biodiversity} · {coastal, coast, coasts}
{water, waters} · {waste, wastes} · {heritage, heritages}
```

Deliberately excluded synonyms: *fisheries*, *forests*, *native* — they overlap with Primary Production and Treaty-settlement vocabulary and would double-count.

**Māori Affairs** — 5 verbatim + 12 Treaty-settlement synonym groups

Verbatim:
```
{maori, māori} · {affairs, affair} · {treaty, treaties} · {waitangi}
{negotiations, negotiation, negotiate, negotiated, negotiating}
```

NZ-specific synonyms (modern Treaty settlement Acts rarely use *māori*/*treaty*/*waitangi* in their LDA top-5 — they are dominated by iwi names and *claims*/*settlement*):
```
{iwi} · {hapu, hapū} · {ngati, ngāti}
{claim, claims, claimant, claimants} · {settlement, settlements}
{taiao} · {whenua} · {mana} · {kaitiaki, kaitiakitanga}
{tikanga} · {rangatira, rangatiratanga} · {redress}
```

### H.3 Why the asymmetry

The other ten committees' parliament.nz subject bullets cover the corpus vocabulary adequately on their own. Adding NZ-specific synonyms only to Environment and Māori Affairs was driven by an empirical gap: under the verbatim-only dictionary, Māori Affairs scored 0 against every community at r=1.5, and Environment missed every Marine Reserves / Wildlife / Pollution statute. The expansion was the minimum intervention required to recover non-zero subject-area counts for these two committees while leaving the ten unaffected committees unchanged.
