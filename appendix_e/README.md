## Appendix E — Portal JSON Bundle Format (Interactive Graph Portal)

This appendix documents the static JSON bundles used by the interactive graph portal. The bundles are not a second graph-construction method and they are not a live database export. They are browser-ready snapshots generated after the NetworkX graph, centrality scores, community assignments, and chart inputs have already been computed.

### E.1 Related Paths

Table E.1 lists the code paths and data locations used by the static portal bundle.

**Table E.1 — Portal bundle paths.**

| Purpose | Path |
|---|---|
| Bundle build wrapper | `src/web/graph/build_data.sh` |
| Main graph exporter | `src/web/backend/export_graph.py` |
| Precomputed chart exporter | `src/web/backend/export_charts.py` |
| Portal loader and graph hydration | `src/web/graph/public/app.js` |
| Portal chart rendering | `src/web/graph/public/charts.js` |
| Versioned portal bundle directory | `src/web/graph/public/data/<version>/` |
| Current graph bundle | `src/web/graph/public/data/v4/graph.json` |
| Current community bundle | `src/web/graph/public/data/v4/communities.json` |
| Current chart bundle | `src/web/graph/public/data/v4/charts.json` |
| Current audit bundle | `src/web/graph/public/data/v4/stats.json` |
| NetworkX graph input pattern | `data/processed/network_final/pkl/full_network_<version>.pkl` |
| Centrality input pattern | `data/processed/network_final/analysis/centrality_<version>/centrality_scores.csv` |
| Community input pattern | `data/processed/network_final/analysis/communities_<version>/r1.5/` |
| PostgreSQL metadata source | `acts` table in the local `nz_legislation` database |
| Text fallback for word counts | `data/processed/text/` |

The active standalone portal layout loads data from `./data/<version>/`. The older MkDocs layout, retained as a compatibility fallback in the frontend, used `<version>/graph/data/`.

### E.2 Generated Files per Version

Each version directory contains four JSON files (Table E.2).

**Table E.2 — Generated files per portal version.**

| File | Role |
|---|---|
| `graph.json` | Main portal graph. Stores the node list, collapsed directed edge list, Act metadata, relation metadata, centrality scores, community IDs, committee labels, source URLs, and available quote evidence. |
| `communities.json` | Community-label index. Stores the label, keywords, size, top Acts, best committee, and validation scores for each community. |
| `charts.json` | Precomputed chart inputs. Stores layer-evolution, layer-convergence, and per-layer Katz ranking data that would be too expensive to recompute in the browser. |
| `stats.json` | Audit summary. Stores version, generation time, node count, collapsed edge count, original multigraph edge count, bundle size, and metadata-missing counts. |

### E.3 Current Bundle Counts

The current exported portal data reports the bundle counts in Table E.3.

**Table E.3 — Current portal bundle counts.**

| Bundle | Nodes | Collapsed directed edges | Original multigraph edges | `graph.json` size |
|---|---:|---:|---:|---:|
| Current | 19,289 | 119,715 | 148,425 | 59.35 MB |

The distinction between collapsed directed edges and original multigraph edges is important. The NetworkX source graph is a `MultiDiGraph`, so the same source-target pair can carry multiple relation records. For browser rendering, the exporter collapses each source-target pair to one directed edge and stores all relation types for that pair in the edge attributes.

### E.4 `graph.json` Format

`graph.json` is the main file consumed by the portal. Its top-level structure is:

```json
{
  "version": "v4",
  "generatedAt": "2026-06-07T11:07:38.150425Z",
  "measures": ["degree", "in_degree", "out_degree", "katz", "pagerank", "eigenvector", "betweenness", "closeness"],
  "communities": {},
  "committees": [],
  "nodes": [],
  "edges": []
}
```

Each node uses the Graphology-style shape `{ "key": act_id, "attributes": {...} }`. The main node attributes are listed in Table E.4.

**Table E.4 — `graph.json` node attributes.**

| Field | Meaning |
|---|---|
| `title` | Canonical Act title. |
| `year` | Enactment year where available. |
| `date` | Enactment date string where available. |
| `type` | Source category used by the exporter, such as `public`, `local`, `private`, `imperial`, `provincial`, or `nzlii`. |
| `status` | Act status from the metadata table where available. |
| `wordCount` | Word count from PostgreSQL metadata or extracted text fallback. |
| `sourceUrl` | NZL or NZLII URL generated from the Act metadata. |
| `community` | Numeric community ID. |
| `communityLabel` | Human-readable community label where available. |
| `committee` | Best-matching subject select committee label where available. |
| `external` | Whether the node is an external citation-target placeholder. Current default exports exclude external placeholders. |
| `centrality` | Object containing the exported centrality measures listed in `measures`. |

Each edge uses the shape `{ "source": act_id, "target": act_id, "attributes": {...} }`. The main edge attributes are listed in Table E.5.

**Table E.5 — `graph.json` edge attributes.**

| Field | Meaning |
|---|---|
| `relation` | Dominant display relation for the collapsed source-target pair. The exporter chooses the most legally severe relation in the pair, with full repeal and partial repeal ranked above amendment and citation. |
| `relations` | All relation types observed for the source-target pair. This preserves multi-relational information after browser-side edge collapse. |
| `confidence` | Highest confidence value among the collapsed relation records. |
| `quote` | Representative quote evidence for the pair. |
| `evidence` | Optional per-relation evidence array emitted by the current exporter. It records relation-specific confidence and quote values for multi-type pairs. |

Example node from `src/web/graph/public/data/v4/graph.json`:

```json
{
  "key": "public_1993_0105",
  "attributes": {
    "title": "Companies Act 1993",
    "year": 1993,
    "type": "public",
    "status": "In force",
    "wordCount": 180890,
    "sourceUrl": "https://www.legislation.govt.nz/act/public/1993/105/en/latest/",
    "date": "",
    "community": 7,
    "communityLabel": "Companies / Insurance / Trustee",
    "committee": "Finance and Expenditure",
    "external": false,
    "centrality": {
      "degree": 0.0298631273330568,
      "in_degree": 0.0277892990460389,
      "out_degree": 0.0020738282870178,
      "katz": 0.1449512589857315,
      "pagerank": 0.002252679786549,
      "eigenvector": 0.1611785081586263,
      "betweenness": 0.0040670711129753,
      "closeness": 0.2587093744771894
    }
  }
}
```

Example edge from `src/web/graph/public/data/v4/graph.json`:

```json
{
  "source": "public_1993_0105",
  "target": "public_2013_0069",
  "attributes": {
    "relation": "CIT",
    "relations": ["CIT"],
    "confidence": 1.0,
    "quote": "has the same meaning as in section 7 of the Financial Markets Conduct Act 2013",
    "evidence": [
      {
        "relation": "CIT",
        "confidence": 1.0,
        "quote": "has the same meaning as in section 7 of the Financial Markets Conduct Act 2013"
      }
    ]
  }
}
```

### E.5 `communities.json` Format

`communities.json` is keyed by community ID. Each entry stores the community label and supporting interpretation data listed in Table E.6.

**Table E.6 — `communities.json` fields.**

| Field | Meaning |
|---|---|
| `community_id` | Numeric community ID. |
| `label` | Human-readable label assigned to the community. |
| `keywords` | LDA-derived or label-support keywords. |
| `size` | Number of Acts in the community. |
| `top_acts` | Highest-degree or most representative Acts in the community. |
| `best_committee` | Best-matching New Zealand subject select committee. |
| `recall_S` | Recall against the committee keyword set used in the validation step. |
| `lda_jaccard` | Jaccard score between community label evidence and committee evidence. |
| `top3_hits` / `top5_hits` | Whether the best committee appears in the top candidate set. |

Example:

```json
{
  "3": {
    "community_id": 3,
    "label": "Crimes / Proceedings / Summary",
    "keywords": ["crimes", "proceedings", "summary", "courts", "criminal", "children", "district", "registration", "protection", "health", "evidence", "legislation", "police", "drugs", "misuse"],
    "size": 1583,
    "top_acts": [
      {
        "act_id": "public_1961_0043",
        "title": "Crimes Act 1961",
        "degree_in_community": 389
      },
      {
        "act_id": "public_1957_0087",
        "title": "Summary Proceedings Act 1957",
        "degree_in_community": 288
      }
    ],
    "best_committee": "Justice",
    "recall_S": 0.8571,
    "lda_jaccard": 0.1522,
    "top3_hits": 1,
    "top5_hits": 2
  }
}
```

### E.6 `charts.json` Format

`charts.json` stores precomputed chart data (Table E.7). This avoids recomputing expensive seed-expansion and centrality-series operations in JavaScript.

**Table E.7 — `charts.json` fields.**

| Field | Meaning |
|---|---|
| `version` | Bundle version. |
| `generatedAt` | UTC export timestamp. |
| `seeds` | Seed Act IDs used for the default layer-expansion charts. |
| `layer_evolution` | For each layer depth, stores mean and median centrality values over the seed-expanded subgraph. |
| `layer_convergence` | For each centrality measure, stores top-20 trajectory values across layer depths. |
| `layer_top_acts_katz` | Top Acts by Katz at each layer depth and in the full graph, used by the rank-flow visualisation. |

Abbreviated example:

```json
{
  "version": "v4",
  "seeds": [
    "public_2019_0058",
    "public_1989_0044",
    "public_2011_0081",
    "public_2021_0007",
    "public_1993_0105"
  ],
  "layer_evolution": {
    "layers": [1, 2, 3, 4, 5, 6, 7],
    "pagerank": {
      "mean": [0.0001513251, 0.0000669056, 0.0000559075, 0.0000538332, 0.0000535988, 0.0000536044],
      "median": [0.0000266365, 0.0000172473, 0.0000165299, 0.0000164556, 0.0000164193, 0.0000164193]
    }
  },
  "layer_top_acts_katz": {
    "full": [
      {
        "rank": 1,
        "act_id": "public_2019_0058",
        "title": "Legislation Act 2019",
        "year": 2019,
        "score": 0.2855053164868817
      }
    ]
  }
}
```

### E.7 `stats.json` Format

`stats.json` records audit information about the generated bundle:

```json
{
  "version": "v4",
  "generatedAt": "2026-06-07T11:07:38.150425Z",
  "nodes": 19289,
  "edges": 119715,
  "multigraphEdges": 148425,
  "bundleBytes": 62231304,
  "bundleMB": 59.35,
  "nodeStats": {
    "missing_title": 0,
    "missing_source": 0,
    "word_count_from_db": 3789,
    "word_count_from_text": 15500,
    "word_count_missing": 0,
    "external_nodes": 0,
    "external_excluded": 0
  }
}
```

### E.8 Demonstration Queries

The following commands reproduce the examples above from the current bundle:

```bash
jq '.nodes[] | select(.key=="public_1993_0105")' \
  src/web/graph/public/data/v4/graph.json

jq '.edges[] | select(.source=="public_1993_0105" and .target=="public_2013_0069")' \
  src/web/graph/public/data/v4/graph.json

jq '."3"' \
  src/web/graph/public/data/v4/communities.json

jq '{version,nodes,edges,multigraphEdges,bundleMB,nodeStats}' \
  src/web/graph/public/data/v4/stats.json
```

The portal itself performs the same basic operation in browser code: it fetches `graph.json`, optionally fetches `communities.json` and `charts.json`, hydrates a `graphology.DirectedGraph`, and then renders the graph using Sigma or the 3D force-graph view.
