# Game Studio OS

Sistema multi-agente per simulare uno studio di sviluppo videoludico in Claude Code, basato sui ruoli di `PRE-PRODUZIONE.md`.

## Setup

1. `git init` (se non già fatto) → crea un repo su GitHub → `git remote add origin <url>` → push.
2. Apri Claude Code in locale **oppure** avvia una sessione su claude.ai/code (Pro, Max o Team) connettendo questo repo GitHub.
3. Dall'app mobile Claude → sezione **Codice** → trovi la sessione cloud collegata al repo.
4. Claude scopre automaticamente i 49 agenti in `.claude/agents/` e la costituzione in `CLAUDE.md`.

## Come si invoca un agente

Non serve sintassi speciale — basta descrivere il task. Claude (l'orchestratore in sessione) legge le `description` dei file in `.claude/agents/` e dispaccia con il Task tool quello/i pertinenti. Per forzarne uno specifico:

> "Usa l'agente design-quest-designer per progettare la quest del villaggio abbandonato"

Per un task multi-agente (es. "crea mappe coerenti con storia e personaggi"), invoca direttamente l'orchestratore di macroarea competente — qui probabilmente `dir-lead-game-designer` (per il level design) che a sua volta coordina con `dir-narrative-director` per la coerenza con storia/personaggi.

## File di riferimento

- `CLAUDE.md` — costituzione del progetto, sempre in context, regole assolute
- `ROLES_INDEX.md` — mappatura dei 49 ruoli, note sulle deduplicazioni applicate
- `knowledge_base/INDEX.md` — indice di navigazione della KB (aggiornalo man mano)
- `.claude/agents/*.md` — i 49 subagent, organizzati per prefisso: `dir-` direzione, `design-`, `narr-` narrativa, `viz-` visual/audio, `prog-` programmazione (STUB, inattiva), `qa-`, `biz-` business/lancio

## Costi (piano Pro minimo, no Max richiesto)

- Agenti `qa-tester`, `qa-narrative`, `prog-*`, `biz-customer-support-specialist` girano su **Haiku** di default — economici, compiti ripetitivi.
- Gli altri girano su **Sonnet**. Cambia il campo `model` nel frontmatter di un agente per alzare/abbassare il costo.
- Nessun agente carica l'intera Knowledge Base: solo le sottocartelle elencate nel proprio `can_modify`.
