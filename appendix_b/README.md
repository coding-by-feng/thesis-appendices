## Appendix B — Cross-Source Title Collisions (Resolver, Title Uniqueness for Graph Construction)

After Stage 3 cross-source resolution, 1,864 NZLII Acts survive as NZLII-only canonical entries (Cross-Source Resolution). When the title resolver in the Title Uniqueness for Graph Construction section builds its `{normalised_title → act_id}` index over all 19,289 canonical Acts, seventy-four of these surviving NZLII titles collide with an NZL title on the resolver's normalised key. Every collision has the same cause: the NZLII title carries a trailing `(YYYY No N)` parenthetical that the NZL title does not, and the resolver's parenthetical strip removes it, leaving identical keys. The index is built in canonical-Act order with the NZL corpus loaded first, so the NZL Act is the resolver winner in every case and the NZLII Act is shadowed as an inbound target.

In every row of Table B.1, the *loser* is the NZLII Act and the *winner* is the NZL Act, because the resolver loads the NZL corpus first and the matching NZLII title therefore arrives second under an already-occupied key. The *Loser year* column reports the year recorded in the NZLII canonical CSV (the parent-Act filing year for amendment Acts), and the *Winner year* reports the NZL Act's enactment year — the two differ for amendment Acts that NZLII files under the parent year.

**Table B.1 — Cross-source title collisions and resolver winners.**

| # | Loser act_id | Loser year | Loser title | Winner act_id | Winner year | Winner title |
|---|---|---|---|---|---|---|
| 1 | `nzlii_tbaghsaa19601960n21415` | 1960 | Thames Boys' and Girls' High School Amendment Act 1960 (1960 No 21) | `public_1960_0021` | 1960 | Thames Boys' and Girls' High School Amendment Act 1960 |
| 2 | `nzlii_obaghsaa19611961n92426` | 1961 | Otago Boys' and Girls' High Schools Amendment Act 1961 (1961 No 92) | `public_1961_0092` | 1961 | Otago Boys' and Girls' High Schools Amendment Act 1961 |
| 3 | `nzlii_tbaghsaa19631963n20415` | 1963 | Thames Boys' and Girls' High School Amendment Act 1963 (1963 No 20) | `public_1963_0020` | 1963 | Thames Boys' and Girls' High School Amendment Act 1963 |
| 4 | `nzlii_obaghsaa19681968n98426` | 1968 | Otago Boys' and Girls' High Schools Amendment Act 1968 (1968 No 98) | `public_1968_0098` | 1968 | Otago Boys' and Girls' High Schools Amendment Act 1968 |
| 5 | `nzlii_mca19691969n41234` | 1969 | Minors' Contracts Act 1969 (1969 No 41) | `public_1969_0041` | 1969 | Minors' Contracts Act 1969 |
| 6 | `nzlii_qetsaconzaa19801980n135586` | 1980 | Queen Elizabeth The Second Arts Council of New Zealand Amendment Act 1980 (1980 No 135) | `public_1981_0135` | 1981 | Queen Elizabeth The Second Arts Council of New Zealand Amendment Act 1980 |
| 7 | `nzlii_rraa19801980n136255` | 1980 | Race Relations Amendment Act 1980 (1980 No 136) | `public_1981_0136` | 1981 | Race Relations Amendment Act 1980 |
| 8 | `nzlii_raa19801980n137191` | 1980 | Rating Amendment Act 1980 (1980 No 137) | `public_1981_0137` | 1981 | Rating Amendment Act 1980 |
| 9 | `nzlii_rbonzaa19801980n138351` | 1980 | Reserve Bank of New Zealand Amendment Act 1980 (1980 No 138) | `public_1981_0138` | 1981 | Reserve Bank of New Zealand Amendment Act 1980 |
| 10 | `nzlii_rbaa19801980n140248` | 1980 | River Boards Amendment Act 1980 (1980 No 140) | `public_1981_0140` | 1981 | River Boards Amendment Act 1980 |
| 11 | `nzlii_scarcaa19801980n141513` | 1980 | Soil Conservation and Rivers Control Amendment Act 1980 (1980 No 141) | `public_1981_0141` | 1981 | Soil Conservation and Rivers Control Amendment Act 1980 |
| 12 | `nzlii_sscoeaa19801980n142539` | 1980 | State Services Conditions of Employment Amendment Act 1980 (1980 No 142) | `public_1981_0142` | 1981 | State Services Conditions of Employment Amendment Act 1980 |
| 13 | `nzlii_slcraa19801980n143502` | 1980 | Statutory Land Charges Registration Amendment Act 1980 (1980 No 143) | `public_1981_0143` | 1981 | Statutory Land Charges Registration Amendment Act 1980 |
| 14 | `nzlii_sfaa19801980n144245` | 1980 | Stock Foods Amendment Act 1980 (1980 No 144) | `public_1981_0144` | 1981 | Stock Foods Amendment Act 1980 |
| 15 | `nzlii_tstbaa19801980n145458` | 1980 | Taranaki Scholarships Trust Board Amendment Act 1980 (1980 No 145) | `public_1981_0145` | 1981 | Taranaki Scholarships Trust Board Amendment Act 1980 |
| 16 | `nzlii_tsaeezaa19801980n146536` | 1980 | Territorial Sea and Exclusive Economic Zone Amendment Act 1980 (1980 No 146) | `public_1981_0146` | 1981 | Territorial Sea and Exclusive Economic Zone Amendment Act 1980 |
| 17 | `nzlii_taa19801980n147206` | 1980 | Tokelau Amendment Act 1980 (1980 No 147) | `public_1981_0147` | 1981 | Tokelau Amendment Act 1980 |
| 18 | `nzlii_utaa19801980n148267` | 1980 | Unit Titles Amendment Act 1980 (1980 No 148) | `public_1981_0148` | 1981 | Unit Titles Amendment Act 1980 |
| 19 | `nzlii_uaa19801980n149286` | 1980 | Universities Amendment Act 1980 (1980 No 149) | `public_1981_0149` | 1981 | Universities Amendment Act 1980 |
| 20 | `nzlii_vaa19801980n150219` | 1980 | Valuers Amendment Act 1980 (1980 No 150) | `public_1981_0150` | 1981 | Valuers Amendment Act 1980 |
| 21 | `nzlii_vlaa19801980n151276` | 1980 | Vegetables Levy Amendment Act 1980 (1980 No 151) | `public_1981_0151` | 1981 | Vegetables Levy Amendment Act 1980 |
| 22 | `nzlii_wascaa19801980n153400` | 1980 | Water and Soil Conservation Amendment Act 1980 (1980 No 153) | `public_1981_0153` | 1981 | Water and Soil Conservation Amendment Act 1980 |
| 23 | `nzlii_wamaa19801980n154321` | 1980 | Weights and Measures Amendment Act 1980 (1980 No 154) | `public_1981_0154` | 1981 | Weights and Measures Amendment Act 1980 |
| 24 | `nzlii_wcaa19801980n155362` | 1980 | Workers' Compensation Amendment Act 1980 (1980 No 155) | `public_1981_0155` | 1981 | Workers' Compensation Amendment Act 1980 |
| 25 | `nzlii_uta19801980n156231` | 1980 | Urban Transport Act 1980 (1980 No 156) | `public_1981_0156` | 1981 | Urban Transport Act 1980 |
| 26 | `nzlii_ssaa19801980n157293` | 1980 | Social Security Amendment Act 1980 (1980 No 157) | `public_1981_0157` | 1981 | Social Security Amendment Act 1980 |
| 27 | `nzlii_mlaepa19801980n162473` | 1980 | Maternity Leave and Employment Protection Act 1980 (1980 No 162) | `public_1981_0162` | 1981 | Maternity Leave and Employment Protection Act 1980 |
| 28 | `nzlii_solaa19801980n168266` | 1980 | Sale of Liquor Amendment Act 1980 (1980 No 168) | `public_1981_0168` | 1981 | Sale of Liquor Amendment Act 1980 |
| 29 | `nzlii_nz1990ca19881988n168262` | 1990 | New Zealand 1990 Commission Act 1988 (1988 No 168) | `public_1988_0168` | 1988 | New Zealand 1990 Commission Act 1988 |
| 30 | `nzlii_ca1955aa19941994n4235` | 1955 | Companies Act 1955 Amendment Act 1994 (1994 No 4) | `public_1994_0004` | 1994 | Companies Act 1955 Amendment Act 1994 |
| 31 | `nzlii_ca1993aa19941994n6235` | 1993 | Companies Act 1993 Amendment Act 1994 (1994 No 6) | `public_1994_0006` | 1994 | Companies Act 1993 Amendment Act 1994 |
| 32 | `nzlii_ca1955aa219941994n7262` | 1955 | Companies Act 1955 Amendment Act (No 2) 1994 (1994 No 7) | `public_1994_0007` | 1994 | Companies Act 1955 Amendment Act (No 2) 1994 |
| 33 | `nzlii_ca1955aa319941994n81262` | 1955 | Companies Act 1955 Amendment Act (No 3) 1994 (1994 No 81) | `public_1994_0081` | 1994 | Companies Act 1955 Amendment Act (No 3) 1994 |
| 34 | `nzlii_ca1993aa219941994n82262` | 1993 | Companies Act 1993 Amendment Act (No 2) 1994 (1994 No 82) | `public_1994_0082` | 1994 | Companies Act 1993 Amendment Act (No 2) 1994 |
| 35 | `nzlii_ita1976aa19951995n17244` | 1976 | Income Tax Act 1976 Amendment Act 1995 (1995 No 17) | `public_1995_0017` | 1995 | Income Tax Act 1976 Amendment Act 1995 |
| 36 | `nzlii_ita1994aa19951995n18244` | 1994 | Income Tax Act 1994 Amendment Act 1995 (1995 No 18) | `public_1995_0018` | 1995 | Income Tax Act 1994 Amendment Act 1995 |
| 37 | `nzlii_a199495sea19951995n29477` | 1994 | Appropriation (1994/95 Supplementary Estimates) Act 1995 (1995 No 29) | `public_1995_0029` | 1995 | Appropriation (1994/95 Supplementary Estimates) Act 1995 |
| 38 | `nzlii_ita1994aa319951995n71271` | 1994 | Income Tax Act 1994 Amendment Act (No 3) 1995 (1995 No 71) | `public_1995_0071` | 1995 | Income Tax Act 1994 Amendment Act (No 3) 1995 |
| 39 | `nzlii_ita1994aa419951995n73271` | 1994 | Income Tax Act 1994 Amendment Act (No 4) 1995 (1995 No 73) | `public_1995_0073` | 1995 | Income Tax Act 1994 Amendment Act (No 4) 1995 |
| 40 | `nzlii_ita1976aa319951995n74271` | 1976 | Income Tax Act 1976 Amendment Act (No 3) 1995 (1995 No 74) | `public_1995_0074` | 1995 | Income Tax Act 1976 Amendment Act (No 3) 1995 |
| 41 | `nzlii_ita1994aa519951995n79271` | 1994 | Income Tax Act 1994 Amendment Act (No 5) 1995 (1995 No 79) | `public_1995_0079` | 1995 | Income Tax Act 1994 Amendment Act (No 5) 1995 |
| 42 | `nzlii_ita1994aa619951995n82271` | 1994 | Income Tax Act 1994 Amendment Act (No 6) 1995 (1995 No 82) | `public_1995_0082` | 1995 | Income Tax Act 1994 Amendment Act (No 6) 1995 |
| 43 | `nzlii_a199495fra19961996n10339` | 1994 | Appropriation (1994/95 Financial Review) Act 1996 (1996 No 10) | `public_1996_0010` | 1996 | Appropriation (1994/95 Financial Review) Act 1996 |
| 44 | `nzlii_ita1994aa19961996n17244` | 1994 | Income Tax Act 1994 Amendment Act 1996 (1996 No 17) | `public_1996_0017` | 1996 | Income Tax Act 1994 Amendment Act 1996 |
| 45 | `nzlii_ita1976aa19961996n18244` | 1976 | Income Tax Act 1976 Amendment Act 1996 (1996 No 18) | `public_1996_0018` | 1996 | Income Tax Act 1976 Amendment Act 1996 |
| 46 | `nzlii_ita1994aa319961996n58271` | 1994 | Income Tax Act 1994 Amendment Act (No 3) 1996 (1996 No 58) | `public_1996_0058` | 1996 | Income Tax Act 1994 Amendment Act (No 3) 1996 |
| 47 | `nzlii_ca1955aa19961996n114235` | 1955 | Companies Act 1955 Amendment Act 1996 (1996 No 114) | `public_1996_0114` | 1996 | Companies Act 1955 Amendment Act 1996 |
| 48 | `nzlii_ca1993aa19961996n115235` | 1993 | Companies Act 1993 Amendment Act 1996 (1996 No 115) | `public_1996_0115` | 1996 | Companies Act 1993 Amendment Act 1996 |
| 49 | `nzlii_ita1994aa19971997n25244` | 1994 | Income Tax Act 1994 Amendment Act 1997 (1997 No 25) | `public_1997_0025` | 1997 | Income Tax Act 1994 Amendment Act 1997 |
| 50 | `nzlii_ca1955aa19971997n26235` | 1955 | Companies Act 1955 Amendment Act 1997 (1997 No 26) | `public_1997_0026` | 1997 | Companies Act 1955 Amendment Act 1997 |
| 51 | `nzlii_ca1993aa19971997n27235` | 1993 | Companies Act 1993 Amendment Act 1997 (1997 No 27) | `public_1997_0027` | 1997 | Companies Act 1993 Amendment Act 1997 |
| 52 | `nzlii_fa21990aa19971997n73221` | 1990 | Finance Act (No 2) 1990 Amendment Act 1997 (1997 No 73) | `public_1997_0073` | 1997 | Finance Act (No 2) 1990 Amendment Act 1997 |
| 53 | `nzlii_y2000ida19991999n25331` | 2000 | Year 2000 Information Disclosure Act 1999 (1999 No 25) | `public_1999_0025` | 1999 | Year 2000 Information Disclosure Act 1999 |
| 54 | `nzlii_sraa19991999n67319` | 1999 | Ship Registration Amendment Act 1999 (1999 No 67) | `public_1999_0046` | 1999 | Ship Registration Amendment Act 1999 |
| 55 | `nzlii_vaa19991999n76197` | 1999 | Veterans' Affairs Act 1999 (1999 No 76) | `public_1999_0076` | 1999 | Veterans' Affairs Act 1999 |
| 56 | `nzlii_fa1996aa19991999n101238` | 1996 | Fisheries Act 1996 Amendment Act 1999 (1999 No 101) | `public_1999_0101` | 1999 | Fisheries Act 1996 Amendment Act 1999 |
| 57 | `nzlii_fa1983aa19991999n102238` | 1983 | Fisheries Act 1983 Amendment Act 1999 (1999 No 102) | `public_1999_0102` | 1999 | Fisheries Act 1983 Amendment Act 1999 |
| 58 | `nzlii_fa1983aa219991999n105265` | 1983 | Fisheries Act 1983 Amendment Act (No 2) 1999 (1999 No 105) | `public_1999_0105` | 1999 | Fisheries Act 1983 Amendment Act (No 2) 1999 |
| 59 | `nzlii_mpa1991aa20012001n12321` | 1991 | Maori Purposes Act 1991 Amendment Act 2001 (2001 No 12) | `public_2001_0012` | 2001 | Maori Purposes Act 1991 Amendment Act 2001 |
| 60 | `nzlii_mpa1993aa20012001n15321` | 1993 | Maori Purposes Act 1993 Amendment Act 2001 (2001 No 15) | `public_2001_0015` | 2001 | Maori Purposes Act 1993 Amendment Act 2001 |
| 61 | `nzlii_ca1955aa20012001n17235` | 1955 | Companies Act 1955 Amendment Act 2001 (2001 No 17) | `public_2001_0017` | 2001 | Companies Act 1955 Amendment Act 2001 |
| 62 | `nzlii_ca1993aa20012001n18235` | 1993 | Companies Act 1993 Amendment Act 2001 (2001 No 18) | `public_2001_0018` | 2001 | Companies Act 1993 Amendment Act 2001 |
| 63 | `nzlii_a200001fra20022002n3339` | 2000 | Appropriation (2000/01 Financial Review) Act 2002 (2002 No 3) | `public_2002_0003` | 2002 | Appropriation (2000/01 Financial Review) Act 2002 |
| 64 | `nzlii_vra20022002n39211` | 2002 | Victims' Rights Act 2002 (2002 No 39) | `public_2002_0039` | 2002 | Victims' Rights Act 2002 |
| 65 | `nzlii_troit200203a20032003n6373` | 2002 | Taxation (Annual Rates of Income Tax 2002-03) Act 2003 (2003 No 6) | `public_2003_0006` | 2003 | Taxation (Annual Rates of Income Tax 2002–03) Act 2003 |
| 66 | `nzlii_lga2002aa20042004n63310` | 2002 | Local Government Act 2002 Amendment Act 2004 (2004 No 63) | `public_2004_0063` | 2004 | Local Government Act 2002 Amendment Act 2004 |
| 67 | `nzlii_lga1974aa20042004n64310` | 1974 | Local Government Act 1974 Amendment Act 2004 (2004 No 64) | `public_2004_0064` | 2004 | Local Government Act 1974 Amendment Act 2004 |
| 68 | `nzlii_pavca20052005n74327` | 2005 | Prisoners' and Victims' Claims Act 2005 (2005 No 74) | `public_2005_0074` | 2005 | Prisoners' and Victims' Claims Act 2005 |
| 69 | `nzlii_lga2002aa20062006n26310` | 2002 | Local Government Act 2002 Amendment Act 2006 (2006 No 26) | `public_2006_0026` | 2006 | Local Government Act 2002 Amendment Act 2006 |
| 70 | `nzlii_lga1974aa20062006n27310` | 1974 | Local Government Act 1974 Amendment Act 2006 (2006 No 27) | `public_2006_0027` | 2006 | Local Government Act 1974 Amendment Act 2006 |
| 71 | `nzlii_ca1988aa20072007n5248` | 1988 | Coroners Act 1988 Amendment Act 2007 (2007 No 5) | `public_2007_0005` | 2007 | Coroners Act 1988 Amendment Act 2007 |
| 72 | `nzlii_ca2006aa20072007n6248` | 2006 | Coroners Act 2006 Amendment Act 2007 (2007 No 6) | `public_2007_0006` | 2007 | Coroners Act 2006 Amendment Act 2007 |
| 73 | `nzlii_pavcaa20072007n29407` | 2007 | Prisoners' and Victims' Claims Amendment Act 2007 (2007 No 29) | `public_2007_0029` | 2007 | Prisoners' and Victims' Claims Amendment Act 2007 |
| 74 | `nzlii_lga2002aa20072007n69310` | 2002 | Local Government Act 2002 Amendment Act 2007 (2007 No 69) | `public_2007_0069` | 2007 | Local Government Act 2002 Amendment Act 2007 |

**Cause.** A single class — *NZLII metadata-suffix collision*. NZLII titles carry an editorial trailing `(YYYY No N)` parenthetical (the Imperial-style year-and-number citation) that NZL does not include in its short title. The resolver's parenthetical strip is necessary to bridge the two sources for the 14,108 Acts that *do* match across sources (Cross-Source Resolution), but for the 74 Acts in this table the strip removes the only token that distinguished them from a same-titled NZL Act. The shadowing has no effect on Stage 3 cross-source matching, which uses fuzzy `token_set_ratio ≥ 90` over candidate pairs that retain the parenthetical and so does not collapse these titles. The collisions are therefore strictly a property of the resolver's read-side, parenthetical-stripping normalisation. A year-context disambiguation step that consulted both candidate `act_id`s before returning a winner would eliminate the shadowing without weakening Stage 3 cross-source coverage; this is recorded as future work in the conclusion.
