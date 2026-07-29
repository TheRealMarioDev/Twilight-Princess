# Twilight Princess AI Campaign — Manifest

This is the authoritative map of the campaign infrastructure on the `campaign-infrastructure` branch.

## How a new campaign chat should use this file

The player should not have to provide file paths manually.

After loading `CAMPAIGN/BOOTSTRAP.md`, inspect this manifest and retrieve the listed files directly from the repository. If the current scene requires a file not listed here, inspect the repository for additional relevant campaign files and load them as needed.

Do not ask the player for a path merely because a file is needed. Discover it from this manifest or the repository yourself.

If a listed file genuinely cannot be accessed or does not exist, report that specific problem rather than asking the player to enumerate repository paths.

Whenever a new campaign-support file is created, add it to this manifest immediately.

## Repository

`TheRealMarioDev/Twilight-Princess`

Branch: `campaign-infrastructure`

## Authoritative campaign files

### Campaign runtime

- `CAMPAIGN/BOOTSTRAP.md` — Entry point for new chats; discovery rules, startup rules, player agency, and campaign premise.
- `CAMPAIGN/MANIFEST.md` — This file; authoritative map of campaign infrastructure.
- `CAMPAIGN/GM_PROTOCOL.md` — Runtime procedure for scene preparation, narration, continuity, state updates, dialogue memory, canon handling, and romance handling.

### Canon rules and progression

- `CANON/canon_rules.md` — Final canon-enforcement hierarchy, mandatory checkpoints, player-agency rules, and divergence policy.
- `CANON/chapter_guides.md` — Chronological Twilight Princess campaign chapter structure and progression gates.
- `CANON/knowledge_gates.md` — Character-specific information boundaries and spoiler/knowledge-leak prevention.
- `CANON/characters_major_minor.md` — Major and minor character reference information.
- `CANON/items_and_progression.md` — Item, equipment, progression, and dependency reference.
- `CANON/optional_content.md` — Optional content integration rules; includes the mandatory Ending Blow exception.

### Persistent state — read/write stores

These files are campaign memory, not static canon. The AI should read the relevant stores before a scene and write/update them after significant events. The player should never need to manually provide these paths.

- `STATE/schema.md` — Definition of the persistent state model and required memory fields.
- `STATE/current.json` — Unified live snapshot of the current campaign state; primary quick-load state.
- `STATE/canon_status.json` — Detailed canon/event progression state retained for compatibility and granular tracking.
- `STATE/initial_relationships.json` — Immutable starting relationship baselines.
- `STATE/relationships.json` — Live relationship state, including affection, trust, closeness, memories, promises, conflicts, secrets, and relationship changes.
- `STATE/characters.json` — Live character state: locations, condition, goals, knowledge, relationships, memories, dialogue, actions, and canon status.
- `STATE/inventory.json` — Live inventory, equipment, currency, collectibles, keys, quest items, progression items, skills, and upgrades.
- `STATE/quest_state.json` — Live main-quest and side-quest state, dependencies, availability, completion, and failure.
- `STATE/memories.json` — Persistent important memories, major dialogue, promises, secrets, revelations, trauma, and recurring personal details.
- `STATE/events.json` — Append-only significant-event history. Use this to preserve what happened and why state changed.
- `STATE/divergences.json` — Persistent tracker for genuine player-created deviations from canon.
- `STATE/saves.json` — Snapshot index for major campaign milestones.

## What each state store is for

### `STATE/current.json`
Use for fast orientation at the beginning of a scene. It should reflect the latest known state. It is a summary, not a replacement for detailed history.

### `STATE/canon_status.json`
Use for detailed progression through the predefined canon event sequence, including mandatory checkpoints such as Ending Blow.

### `STATE/relationships.json`
Use whenever a relationship is changed, referenced, tested, or emotionally relevant. Preserve meaningful history rather than reducing a relationship to a single number.

### `STATE/characters.json`
Use for persistent NPC state. Characters retain their own knowledge, goals, locations, memories, relationships, and consequences.

### `STATE/inventory.json`
Use whenever Link obtains, loses, equips, consumes, upgrades, or learns something represented as an item/skill/progression resource.

### `STATE/quest_state.json`
Use whenever a main quest or side quest becomes available, changes stage, is completed, fails, or has a dependency altered.

### `STATE/memories.json`
Use for important dialogue and memories that may matter later. Exact wording should be retained when the exact words could become important; otherwise use faithful summaries.

### `STATE/events.json`
Append a significant event after it occurs. Events should record time, location, participants, what happened, meaningful dialogue, relationship effects, state changes, canon impact, and divergence impact.

### `STATE/divergences.json`
Use only when the player's actual actions change, prevent, reorder, or substantially alter an established canon outcome. Do not use it merely because Link explored or spoke differently within an event that still occurred normally.

### `STATE/saves.json`
Record milestone snapshots without deleting historical snapshots.

## Authority order

When information conflicts, use this hierarchy:

1. Current live state in `STATE/` for what has actually happened in this campaign.
2. `CANON/canon_rules.md` for canon enforcement and player-agency rules.
3. Relevant `CANON/` chapter/character/item/knowledge documents for underlying Twilight Princess canon and campaign design.
4. `CAMPAIGN/GM_PROTOCOL.md` for runtime behavior.
5. `CAMPAIGN/BOOTSTRAP.md` for startup and loading behavior.

If live state records a genuine player-created divergence, do not overwrite it simply to restore the original canon outcome.

`STATE/initial_relationships.json` is the starting baseline; once the campaign is active, `STATE/relationships.json` is authoritative for the current relationship state.

## Current known campaign infrastructure

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
├── current.json
├── canon_status.json
├── initial_relationships.json
├── relationships.json
├── characters.json
├── inventory.json
├── quest_state.json
├── memories.json
├── events.json
├── divergences.json
└── saves.json
```

This is the complete list of campaign-infrastructure files currently known to the campaign system. It is not a claim that unrelated source/project files cannot exist elsewhere in the repository.

## Runtime retrieval protocol

At campaign startup:
1. Load `CAMPAIGN/BOOTSTRAP.md`.
2. Load this manifest.
3. Load `CAMPAIGN/GM_PROTOCOL.md`.
4. Load the canon rules and the current chapter material.
5. Load `STATE/current.json`, `STATE/canon_status.json`, `STATE/relationships.json`, `STATE/characters.json`, `STATE/inventory.json`, `STATE/quest_state.json`, `STATE/memories.json`, `STATE/events.json`, and `STATE/divergences.json`.
6. Use `STATE/initial_relationships.json` only to verify/initialize starting baselines.
7. Use `STATE/saves.json` when resuming from a milestone snapshot.

Before a scene:
- Read the current state stores relevant to the scene.
- Read the relevant canon chapter, character, knowledge, item, and optional-content material.
- Check for contradictions between current state and canon.
- Check NPC knowledge boundaries.
- Check relationship and memory continuity.

After a significant scene:
- Update `STATE/current.json`.
- Update any affected specialized state stores.
- Append the significant event to `STATE/events.json`.
- Record any genuine canon divergence in `STATE/divergences.json`.
- Record important dialogue/memories in `STATE/memories.json` and/or `STATE/relationships.json`.
- Update quest, character, inventory, and canon progression stores as appropriate.
- Update `STATE/saves.json` at major milestones when practical.

## Retrieval examples

### Ordon / Ilia scene
Read:
- runtime protocol
- canon rules
- current chapter
- knowledge gates
- character reference
- current state
- relationships
- character state
- memories/events as relevant

Write after significant changes:
- current state
- relationships
- characters
- memories
- events
- quest state if applicable

### Dungeon progression
Additionally read:
- items/progression
- relevant chapter progression
- current inventory
- quest state
- canon status

Write after significant changes:
- inventory
- current state
- quest state
- canon status
- events
- memories/relationships when relevant

### Ilia memory restoration
Additionally read:
- relevant Ilia character material
- item/progression rules for the Horse Call
- relevant chapter progression
- relationship state
- memories/events
- current inventory

Write after the restoration event:
- relationship state
- character state
- memories
- inventory
- current state
- canon status
- events
- divergence state if the player altered the expected outcome

## Adding future files

If additional campaign files are created later — such as dedicated character records, relationship records, chapter supplements, event archives, or save snapshots — they must be added to this manifest immediately. Future chats should inspect this manifest rather than relying on a hard-coded list in a prompt.
