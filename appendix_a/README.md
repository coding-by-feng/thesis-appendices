## Appendix A — Title-Collision Acts (Stage 1, Step 4c)

Stage 1 of the deduplication pipeline detects thirteen pairs of Acts whose members share an identical strictly-normalised title but represent genuinely different Acts. Step 4c splits every such pair so that both Acts retain their own canonical entry. At resolver-build time, however, only one entry per shared title can occupy the `title_map` keyspace (Title Uniqueness for Graph Construction), and the entry inserted earlier in canonical-Act order is shadowed by the later one. The thirteen pairs and their resolver winners are listed in Table A.1; all twenty-six Acts are public, and no collisions occur in the local, private, provincial, or imperial categories.

**Table A.1 — NZL-internal title collisions and resolver winners.**

| # | Loser act_id | Loser year | Loser title | Winner act_id | Winner year | Winner title |
|---|---|---|---|---|---|---|
| 1 | `public_1882_0041` | 1882 | Crown and Native Lands Rating Act 1882 | `public_1883_0042` | 1883 | Crown and Native Lands Rating Act 1882 |
| 2 | `public_1912_0028` | 1912 | Public Revenues Amendment Act 1912 | `public_1912_0032` | 1912 | Public Revenues Amendment Act 1912 |
| 3 | `public_1920_0001` | 1920 | Imprest Supply | `public_1984_0001` | 1984 | Imprest Supply |
| 4 | `public_1920_0023` | 1920 | Immigration Restriction Amendment | `public_1951_0014` | 1951 | Immigration Restriction Amendment |
| 5 | `public_1920_0034` | 1920 | Companies Amendment | `public_1952_0066` | 1952 | Companies Amendment |
| 6 | `public_1920_0065` | 1920 | Marriage Amendment | `public_1991_0129` | 1991 | Marriage Amendment |
| 7 | `public_1952_0058` | 1952 | Public Works Amendment | `public_1987_0062` | 1987 | Public Works Amendment |
| 8 | `public_1961_0048` | 1961 | University of Otago Amendment Act 1961 | `public_2000_0006` | 2000 | University of Otago Amendment Act 1961 |
| 9 | `public_1963_0022` | 1963 | Indecent Publications Act 1963 | `public_1972_0136` | 1972 | Indecent Publications Act 1963 |
| 10 | `public_1979_0016` | 1979 | Imprest Supply Act (No 2) | `public_1991_0112` | 1991 | Imprest Supply Act (No 2) |
| 11 | `public_1987_0059` | 1987 | Volunteers Employment Protection Amendment | `public_1990_0114` | 1990 | Volunteers Employment Protection Amendment |
| 12 | `public_1990_0117` | 1990 | Customs Amendment Act (No. 2) | `public_1991_0084` | 1991 | Customs Amendment Act (No. 2) |
| 13 | `public_2004_0076` | 2004 | Fisheries Amendment Act (No 3) 2004 | `public_2004_0104` | 2004 | Fisheries Amendment Act (No 3) 2004 |

**Cause categories.** *Bare-title amendment* — the registered short title omits the enactment year, so amendments made in different decades collide on identical titles and can only be distinguished by act number (rows 3, 4, 5, 6, 7, 11; six pairs). *Year-bearing title across years* — the short title includes a fixed year as part of the official name, but the Act was re-enacted or substantially re-issued in a later year (rows 1, 8, 9; three pairs). *Numbered variant across years* — *(No 2)* / *(No. 2)* style numbered Acts appearing in different years with otherwise identical short titles (rows 10, 12; two pairs). *Within-year duplicate short title* — two Acts in the same calendar year share an identical short title, distinguished only by act number (rows 2, 13; two pairs).

Bare-title amendments dominate because the database short title for nineteenth- and early twentieth-century amendment Acts often did not include the year of enactment. The within-year duplicates, while few, are the most important to preserve because they represent two genuinely separate enactments that would otherwise be indistinguishable in the graph.
