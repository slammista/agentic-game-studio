---
role: system
date: 2026-06-25
description: Checkpointing di sessione. Aggiornato da kb-librarian al termine di ogni sessione produttiva. Il Director legge SOLO questo file all'avvio invece di fare Glob su tutta la KB.
---

# Session Manifest

## Come usarlo

**Fine sessione:** invoca `kb-librarian` con istruzione "aggiorna il session manifest". L'agente popola la sezione "Ultima sessione".

**Inizio sessione:** `dir-game-director` legge questo file per ricostruire il contesto (~300 token) invece di scansionare tutta la KB.

---

## Ultima sessione

**Data:** 2026-08-23
**Durata stimata:** breve — sessione di kickoff creativo
**Agenti attivati:** dir-game-director, kb-librarian

### Asset prodotti
- `production/creative_vision.md` — visione creativa fondativa, **approved**

### Decisioni architetturali
- **Progetto definito:** *Condominio Nove* — roguelike d'azione real-time top-down, registro weird/surreale domestico, lingua master `it`
- **Scope stabilito:** vertical slice (piani 9→6 + Piano Meno Uno intravisto, 1 boss, 4 vicini firmatari, 3 archetipi nemico)
- **Tre pilastri vincolanti:** (1) l'edificio si adatta al giocatore, (2) le Abitudini danno potere in cambio di prevedibilità, (3) il weird nasce solo dalla deformazione del quotidiano
- **Progressione persistente:** solo le firme sul reclamo. Ogni altra persistenza richiede approvazione del Director
- Macroarea `prog-*` confermata **STUB**: nessuna produzione di codice in questo scope

### Asset in pending approval
*(nessuno — la visione creativa è autorità diretta del Director)*

### Conflitti aperti
*(nessuno)*

### Domande aperte
1. Combattimento solo corpo a corpo o anche a distanza?
2. Il boss del vertical slice è battibile alla prima notte o è sconfitta programmata?
3. Le Abitudini hanno UI esplicita o vanno intuite?

### Context per prossima sessione
La visione creativa è approvata ed è la radice della KB: ogni asset successivo deve
esserle coerente. Il progetto entra in **fase di design**. Ordine di dipendenza
consigliato: `design-game-designer` (core loop e combat) → `design-systems-designer`
(Abitudini + Adattamento) → `design-world-designer` (il palazzo e i suoi inquilini)
→ `narr-narrative-designer` (arco della prima notte). Le tre domande aperte vanno
risolte prima o durante il passaggio da game designer a systems designer.

---

## Storico sessioni

| Data | Asset prodotti | Decisioni chiave | Agenti usati |
|---|---|---|---|
| 2026-06-25 | 0 | Init sistema | system |
| 2026-08-23 | 1 | Kickoff *Condominio Nove*: genere, tono, tre pilastri, scope vertical slice | dir-game-director, kb-librarian |
