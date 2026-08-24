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
| qa_reports/ | piano test, bug, report narrativi/UX, cross-domain | qa-*, qa-cross-domain |
| staging/ | output DRY-RUN non ancora approvati | tutti (solo in modalità DRY-RUN) |
| i18n/ | traduzioni per lingue attive + glossari multi-lingua | biz-localization-manager |
| production/config.md | modalità operativa (PROD/DRY-RUN) e impostazioni globali | dir-game-director |
| production/pending_approval.md | coda batch approval per dir-game-director | orchestratori dir-* |
| production/session_manifest.md | checkpointing sessione, context per avvio | kb-librarian |

## Voci attuali

| Nome | Percorso | Agente | Data | Stato |
|---|---|---|---|---|
| Visione Creativa — Pietrafitta | [production/creative_vision.md](production/creative_vision.md) | dir-game-director | 2026-08-23 | approved |
| Core loop e meccanica del verbale | [systems/core_loop_e_verbale.md](systems/core_loop_e_verbale.md) | design-game-designer | 2026-08-23 | draft |
| Pietrafitta — paese e 8 luoghi | [regions/pietrafitta.md](regions/pietrafitta.md) | design-world-designer | 2026-08-23 | draft |
| I nove abitanti e la rete di relazioni | [characters/abitanti_pietrafitta.md](characters/abitanti_pietrafitta.md) | design-world-designer | 2026-08-23 | draft |
| Standard di rigore dei casi (rev.2) | [qa_reports/standard_rigore_casi.md](qa_reports/standard_rigore_casi.md) | qa-lead | 2026-08-23 | draft |
| Economia del tempo e della fiducia | [systems/economia_tempo_e_fiducia.md](systems/economia_tempo_e_fiducia.md) | design-systems-designer | 2026-08-23 | draft |
