# Persistent Campaign State Schema

This document defines the information the AI must preserve between scenes/turns. It is a schema, not the live campaign state.

## Core state
- `campaign_status`: design | ready | active | paused | complete
- `current_chapter`
- `current_event_id`
- `calendar.day`
- `calendar.time_of_day`
- `calendar.exact_time` when useful
- `calendar.location`
- `calendar.weather` when relevant
- `canon_deviation_status`

## Link
- current form: human | wolf
- physical condition / injuries
- stamina / fatigue
- inventory
- equipped items
- ammunition/resources
- hearts / health upgrades
- learned skills
- known information
- secrets Link has not discovered
- current goals
- immediate concerns
- important memories
- recent dialogue/actions that may matter later

## Relationships
Every important relationship uses a persistent record:
- `character_id`
- relationship type
- current trust/affection/respect/tension where meaningful
- relationship stage
- known shared memories
- unresolved conflicts
- promises/debts
- secrets between them
- last meaningful interaction
- NPC's independent feelings toward Link

### Ilia-specific relationship state
Track separately:
- romantic stage
- mutual awareness of attraction
- meaningful romantic memories
- affection/trust
- unresolved emotional wounds
- Ilia's current memory state
- memories lost because of the amnesia
- memories recovered
- campaign-created memories that are compatible with canon
- Horse Call status
- reunion status
- last interaction
- current physical location

Do not reduce the Ilia relationship to one numeric affection value.

## Character state
For every major/minor recurring character when relevant:
- current location
- current activity
- alive/dead/unknown
- current knowledge
- beliefs/misconceptions
- relationship to Link
- relationship to other important characters
- current goal
- schedule/availability
- unresolved story threads
- last interaction with Link

## World state
Track:
- Twilight coverage by region
- restored Light Spirits
- Fused Shadows acquired
- Mirror Shards acquired
- Mirror of Twilight condition
- dungeon completion
- bosses defeated
- important NPC relocations
- opened/closed routes
- major settlements' current condition
- important objects moved/destroyed/repaired
- side quest states

## Canon progression
For each canon event:
- pending
- active
- completed
- altered
- skipped only if explicitly approved as a divergence

When altered:
- original event
- exact player cause
- immediate result
- long-term consequences
- whether later canon can still occur

## Inventory ledger
Each major item should store:
- acquired boolean
- acquisition event
- current holder
- current location if not held by Link
- upgrades
- condition if relevant
- known by whom

## Dialogue/memory ledger
Store only meaningful dialogue rather than every line ever spoken:
- speaker
- listener(s)
- approximate time/location
- subject
- exact wording only when the line is intentionally important
- summarized content otherwise
- promises/threats/confessions/revelations
- emotional significance
- who remembers it

This is the campaign's long-term memory. It should be queried before generating a scene involving the same subject or relationship.

## Quest ledger
Each quest stores:
- quest ID
- canon/optional/campaign-created
- status
- giver/source
- objective
- prerequisites
- current clues
- known participants
- deadline/urgency if any
- rewards
- consequences

## Scene checkpoint
After each significant scene, update at minimum:
1. time/location
2. Link condition
3. inventory changes
4. relationship changes
5. character location changes
6. new information learned
7. important dialogue/memories
8. quest changes
9. canon event progress
10. new divergence or consequence

## Anti-amnesia rule
Never overwrite a previous important memory merely because the current scene does not mention it. New state is additive unless something explicitly changes.

## Anti-retcon rule
Never silently rewrite established campaign history. If a contradiction appears, flag it as a continuity issue and resolve it using the existing state, canon, or an explicit divergence.
