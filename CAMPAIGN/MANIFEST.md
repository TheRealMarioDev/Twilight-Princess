# Twilight Princess AI Campaign — Manifest

This is the authoritative map of the campaign infrastructure on the `campaign-infrastructure` branch.

## How a new campaign chat should use this file

The player should not have to provide file paths manually.

After loading `CAMPAIGN/BOOTSTRAP.md`, inspect this manifest and retrieve the listed files directly from the repository. If the current scene requires a file not listed here, inspect the repository for additional relevant campaign files and load them as needed.

Do not ask the player for a path merely because a file is needed. Discover it from this manifest or the repository yourself.

If a listed file genuinely cannot be accessed or does not exist, report that specific problem rather than asking the player to enumerate repository paths.

## Repository

`TheRealMarioDev/Twilight-Princess`

Branch: `campaign-infrastructure`

## Authoritative campaign files

### Campaign runtime

- `CAMPAIGN/BOOTSTRAP.md` — Entry point for new chats; loading behavior, startup rules, player agency, and campaign premise.
- `CAMPAIGN/MANIFEST.md` — This file; authoritative map of campaign infrastructure.
- `CAMPAIGN/GM_PROTOCOL.md` — Runtime procedure for scene preparation, narration, continuity, state updates, dialogue memory, canon handling, and romance handling.

### Canon rules and progression

- `CANON/canon_rules.md` — Final canon-enforcement hierarchy, mandatory checkpoints, player-agency rules, and divergence policy.
- `CANON/chapter_guides.md` — Chronological Twilight Princess campaign chapter structure and progression gates.
- `CANON/knowledge_gates.md` — Character-specific information boundaries and spoiler/knowledge-leak prevention.
- `CANON/characters_major_minor.md` — Major and minor character reference information.
- `CANON/items_and_progression.md` — Item, equipment, progression, and dependency reference.
- `CANON/optional_content.md` — Optional content integration rules; includes the mandatory Ending Blow exception.

### Persistent state

- `STATE/schema.md` — Definition of the persistent state model and required memory fields.
- `STATE/canon_status.json` — Current campaign/world state. This is the live state and must be treated as mutable campaign data, not as immutable canon.
- `STATE/initial_relationships.json` — Starting relationship baselines, including Link and Ilia.

## Authority order

When information conflicts, use this hierarchy:

1. Current live state in `STATE/` for what has actually happened in this campaign.
2. `CANON/canon_rules.md` for canon enforcement and player-agency rules.
3. Relevant `CANON/` chapter/character/item/knowledge documents for the underlying Twilight Princess canon and campaign design.
4. `CAMPAIGN/GM_PROTOCOL.md` for runtime behavior.
5. `CAMPAIGN/BOOTSTRAP.md` for startup and loading behavior.

If live state records a genuine player-created divergence, do not overwrite it simply to restore the original canon outcome.

## Current known directory structure

```text
CAMPAIGN/
├── BOOTSTRAP.md
├── MANIFEST.md
└── GM_PROTOCOL.md

CANON/
├── canon_rules.md
├── chapter_guides.md
├── knowledge_gates.md
├── characters_major_minor.md
├── items_and_progression.md
└── optional_content.md

STATE/
├── schema.md
├── canon_status.json
└── initial_relationships.json
```

This is the list of campaign-infrastructure files currently known to the campaign system. It is not a claim that unrelated files cannot exist elsewhere in the repository.

## Runtime retrieval guidance

Do not load every file repeatedly if it is irrelevant to the current scene. Always load the runtime/bootstrap and current state as required by `GM_PROTOCOL.md`, then retrieve relevant canon and relationship material for the current scene.

Examples:

### Ordon / Ilia scene
Prioritize:
- `CAMPAIGN/GM_PROTOCOL.md`
- `CANON/canon_rules.md`
- `CANON/chapter_guides.md`
- `CANON/knowledge_gates.md`
- `CANON/characters_major_minor.md`
- `STATE/canon_status.json`
- `STATE/initial_relationships.json`
- `STATE/schema.md`

### Dungeon progression
Prioritize the above plus:
- `CANON/items_and_progression.md`
- relevant chapter section in `CANON/chapter_guides.md`

### Ilia memory restoration
Prioritize the above plus:
- relevant character information
- `CANON/items_and_progression.md`
- relevant chapter progression
- current relationship/state/memory records

### Any new file discovered later
If additional campaign files are added to the repository, update this manifest so future chats can discover them automatically.
