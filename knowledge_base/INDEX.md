# Knowledge Base INDEX

Aggiorna questo file ogni volta che crei una nuova entità. Ogni agente legge SOLO le cartelle elencate nel proprio `can_modify` (vedi `.claude/agents/<slug>.md`) — non l'intera KB.

| Cartella | Contenuto | Agenti che scrivono |
|---|---|---|
| world/ | continenti, geografia | design-world-designer |
| regions/ | regioni, città | design-world-designer, design-level-designer |
| factions/ | fazioni | design-world-designer |
| characters/ | design + narrativa personaggi | design-character-designer, narr-character-writer |
| timeline/ | cronologia eventi | narr-narrative-designer, narr-lore-designer |
| narrative/ | trama, archi, finali | narr-narrative-designer |
| dialogue/ | dialoghi + implementazione | narr-dialogue-writer, narr-technical-designer |
| lore/ | struttura, prosa, documenti in-world | narr-lore-designer, narr-lore-writer, narr-content-writer |
| quests/ | missioni | design-quest-designer |
| systems/ | meccaniche, economia, bilanciamento | design-game-designer, design-systems-designer |
| levels/ | layout, blockout, encounter | design-level-designer, design-encounter-designer |
| art_direction/ | stile visivo | dir-art-director |
| assets_visual/ | concept, 3D, texture, rigging, animazione, UI, VFX, integrazione | viz-* |
| assets_audio/ | SFX, musica | viz-sound-designer, viz-composer |
| production/ | GDD, roadmap, market analysis, decisioni | dir-* |
| marketing/ | strategia, store, press kit, community | biz-* |
| live_ops/ | metriche, eventi, feedback, supporto | biz-* |
| qa_reports/ | piano test, bug, report narrativi/UX | qa-* |

## Voci attuali

_(vuoto — popola man mano che crei contenuto. Formato riga: `- [nome entità](percorso/file.md) — breve descrizione — stato)`)_
