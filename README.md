# English Vocabulary Data for Learners

Open, learner-focused, machine-readable **English vocabulary data**. The first module is a
**synonym thesaurus** — one meaning per row, with plain-English definitions, three difficulty
levels, and verified synonym sets. More modules (antonyms, CEFR wordlists, confusables, …) are
planned.

**2138 entries · all `verified:true` · MIT licensed · JSON (source of truth) + CSV (human view)**

> Built as an AI-assisted draft, then passed through automated checks and a per-entry semantic
> audit. Every entry carries a `verified` flag so downstream users know exactly what passed review.

---

## Why this data

- **Made for language learners & vocabulary tools.** Synonyms are grouped by *sense* (one meaning
  per row), so an app, flashcard deck, or study tool can pick the exact meaning it needs instead of
  a jumbled word list.
- **3 difficulty tiers** map naturally to beginner / intermediate / advanced decks.
- **No example sentences in the core fields** — compact and cheap to ship and reuse.
- **Plain-English definitions**, written for learners, not lexicographers.

---

## Schema

JSON (source of truth) — each object is one meaning (`sense`) of a word:

```json
{
  "word": "feasible",
  "sense": "possible to do",
  "pos": "adj",
  "definition": "possible to do or achieve",
  "level": 3,
  "synonyms": ["practicable", "workable", "viable"],
  "verified": true,
  "note": ""
}
```

CSV columns (pipe-joined synonyms, `QUOTE_ALL`):

| column       | meaning                                   |
|--------------|-------------------------------------------|
| `word`       | headword                                  |
| `sense`      | short meaning label (one row per sense)   |
| `pos`        | part of speech: `n` `v` `adj` `adv` …     |
| `definition` | plain-English definition                  |
| `level`      | difficulty: `1` beginner / `2` intermediate / `3` advanced |
| `synonyms`   | near-synonyms for this sense, `|`-separated |
| `verified`   | `True` if it passed automated + semantic audit |
| `note`       | editorial note (empty unless audited)     |
| `related`    | related terms (only for words with no strict synonyms, e.g. `infrastructure`) |

---

## Stats (current module: synonyms)

| metric         | value |
|----------------|-------|
| total entries  | 2138  |
| level 1        | 307   |
| level 2        | 892   |
| level 3        | 939   |
| verified:true  | 2138  |

Part of speech: noun 453 · adjective 842 · verb 823 · adverb 17 · preposition 1 · conjunction 2.

Most entries carry 3–4 near-synonyms (3: 1997 rows, 4: 126 rows).

Sample headwords — Level 1: `happy sad big small fast slow good bad hot cold …`;
Level 2: `important improve strange angry beautiful clever dangerous quiet brave …`;
Level 3: `feasible controversial elaborate substantial infrastructure influential prominent abundant ambiguous …`

---

## Files

```
english-vocabulary/
├── README.md
├── LICENSE                 (MIT)
├── stats.json              (computed, machine-readable)
└── data/
    ├── en-synonym-thesaurus.json   ← source of truth (nested)
    └── en-synonym-thesaurus.csv    ← flat, human view
```

---

## How it's maintained

1. AI-assisted drafting of word → sense → definition → synonyms in batches.
2. **Automated checks** on every batch: self-references (a word listed as its own synonym),
   empty synonym lists, duplicate `(word, sense)` keys.
3. **Per-entry semantic audit** of near-synonym validity, definition/sense alignment, and
   difficulty labeling; fixes are applied to the JSON, then re-synced.
4. `verified:true` marks entries that passed all of the above.

> Honest caveat: automated checks + AI-assisted audit reduce but do not **eliminate** errors.
> Independent review before production use is recommended.

---

## License

MIT — see [LICENSE](LICENSE). You can use this data for commercial products, apps, and research;
attribution is appreciated but not required.

---

## Roadmap

- Expand the synonym dataset further.
- Add modules: antonyms, CEFR wordlists, confusables, collocations.
- Add example sentences as an optional separate field.
