## Appendix D — Empty-Target Acts by Category (Post-processing and Title Resolution)

This appendix supports Table 4.4 by listing concrete Acts behind each of the empty-target categories named in the Post-processing and Title Resolution section. The complete population is 1,025 Acts; the lists below show every Imperial Act and every foreign-agreement Act in the empty population, plus a representative sample of local and private Acts spanning the timeline.

### D.1 Imperial Acts (5 / 5 in the empty population)

These pre-NZ statutes were carried into NZ law and contain no New-Zealand-Act references. Table D.1 lists the entire imperial empty-target population.

**Table D.1 — Imperial empty-target Acts.**

| Act ID | Title |
|---|---|
| `imperial_1275_0001` | Statutes of Westminster; The First 1275 |
| `imperial_1297_0029` | Magna Carta 1297 |
| `imperial_1354_0003` | Civil and Criminal Justice Statute 1354 |
| `imperial_1368_0003` | Observance of Due Process of Law Statute 1368 |
| `imperial_1751_0023` | Calendar (New Style) Act 1751 |

Two further Imperial Acts in the corpus (`imperial_1861_0101` *Statute Law Revision Act 1861*, `imperial_1887_0054` *British Settlements Act 1887*) also extract empty under the current pipeline; they are included in the 1,025 figure.

### D.2 Acts approving foreign agreements (5 / 5 in the empty population)

A title-pattern probe ("Agreement", "Convention", "Treaty", "Compact", "United Nations", "Charter", "Protocol") against the 1,025 empty Acts returned exactly five matches (Table D.2). These Acts ratify or empower a foreign agreement and contain no other-NZ-Act citations by construction.

**Table D.2 — Foreign-agreement empty-target Acts.**

| Act ID | Title |
|---|---|
| `public_1851_0013` | Bank Charters Act 1851 |
| `public_1873_0036` | Telegraph Cables Subsidy Agreement Ratification Act 1873 |
| `local_1882_0012`  | Rangipo-Murimotu Agreement Validation Act 1882 |
| `public_1944_0021` | United Nations Relief and Rehabilitation Administration Act 1944 |
| `public_1951_0058` | Treaty of Peace (Japan) Act 1951 |

This is the entire foreign-agreement empty-target population — about 0.5% of the 1,025 empties. The "foreign-agreement" category is therefore a tiny tail rather than a co-equal third of the empty population, as an earlier draft of the Post-processing and Title Resolution section implied.

### D.3 Local and private Acts — representative sample

Local and private legislation (empowering, validation, vesting, sale, exchange, and reserve Acts) is the dominant empty category. Table D.3 gives up to three Acts per decade from the 1840s onward and spans the entire timeline up to 1987 (the corpus contains essentially no empty post-1990 entries). Each Act legislates about a named council, trust, asset, or land parcel and cites no other NZ statute.

**Table D.3 — Local and private empty-target sample.**

| Act ID | Title |
|---|---|
| `local_1841_0001` | New Zealand Banking Company Act 1841 |
| `local_1844_0001` | Union Bank of Australia Act 1844 |
| `local_1845_0001` | Naturalization Act 1845 |
| `local_1860_0002` | Purchas and Ninnis Flax Patent Act 1860 |
| `local_1860_0003` | Nelson Roman Catholic Endowments Sale Act 1860 |
| `local_1860_0004` | Nelson Wesleyan Schoolmaster's Land Sale Act 1860 |
| `local_1874_0001` | Colonial Bank of New Zealand Act 1874 |
| `local_1875_0004` | Napier Swamp Nuisance Act 1875 |
| `local_1877_0010` | Waiwera School Glebe Sale Act 1877 |
| `local_1880_0001` | Taonui-Ahuaturanga Land Act 1880 |
| `local_1880_0009` | Invercargill Drill-shed Site Act 1880 |
| `local_1881_0011` | Timaru Water-Race Reserve Act 1881 |
| `local_1890_0002` | Omaka Recreation Reserve Sale Act 1890 |
| `local_1890_0010` | Auckland Harbour Board Empowering Act 1890 |
| `local_1890_0016` | Stratford County Act 1890 |
| `local_1901_0009` | Egmont County Act 1901 |
| `local_1901_0022` | Kiwitea County Council Offices Act 1901 |
| `local_1902_0001` | University of Otago Empowering Act 1902 |
| `local_1910_0013` | Waikouaiti County Council Reserve Vesting Act 1910 |
| `local_1910_0025` | Thames Harbour Board Empowering Act 1910 |
| `local_1911_0005` | Greytown Town Lands and Hospital Lands Exchange Act 1911 |
| `local_1921_0010` | Grey Collection Exchange Act 1921 |
| `local_1922_0004` | Wairau River District Loans Act 1922 |
| `local_1922_0021` | Whangarei Borough Leasing Empowering Act 1922 |
| `local_1930_0010` | Hawke's Bay County Empowering Act 1930 |
| `local_1931_0005` | Cameron and Soldiers' Memorial Park (Masterton) Trustees Empowering Act 1931 |
| `local_1933_0006` | Bluff Harbour Board Empowering Act 1933 |
| `local_1940_0002` | Waitara Borough Empowering Act 1940 |
| `local_1946_0003` | Nelson City Empowering Act 1946 |
| `local_1964_0005` | Napier City (Kennedy Park) Motel Empowering Act 1964 |
| `local_1965_0018` | East Coast Bays Borough Empowering Act 1965 |
| `local_1968_0007` | Christchurch Town Hall Empowering Act 1968 |
| `local_1973_0003` | Manukau City Empowering (Wiri Hotel Site) Act 1973 |
| `local_1976_0001` | Porirua City (Financial Unification) Act 1976 |
| `local_1977_0003` | Upper Hutt City (Representation and Financial Unification) Act 1977 |
| `local_1986_0008` | Invercargill City Council (Differential Rating Validation) Act 1986 |
| `local_1987_0003` | Whakatane District Council Empowering Act 1987 |

The sampling rule is "up to three Acts per decade in lexicographic act-ID order from the empty-target set, restricted to `local_*` IDs". The full empty-target population is regenerable from `data/processed/relations_final/` with `python3 -m src.audits.empty_relations_distribution`.
