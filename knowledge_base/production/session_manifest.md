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
**Durata stimata:** breve — kickoff creativo + pivot di progetto
**Agenti attivati:** dir-game-director, kb-librarian

### Asset prodotti
- `production/creative_vision.md` — visione creativa fondativa, **approved**

### Decisioni architetturali
- **Pivot eseguito:** la prima direzione (*Condominio Nove*, roguelike d'azione weird) è stata abbandonata su decisione del committente prima che esistesse qualsiasi asset dipendente. Nessuna invalidazione a cascata. Storia consultabile in git.
- **Progetto definito:** *Pietrafitta* — mini-RPG investigativo a casi episodici, logica deduttiva, giallo di provincia italiana 1954, lingua master `it`
- **Scope stabilito:** vertical slice a **3 casi collegati**, 8 luoghi, 9 abitanti
- **Tre pilastri vincolanti:** (1) il verbale a caselle è la meccanica di deduzione, con timbro di conferma a gruppi di tre; (2) il tempo di una giornata è l'unica risorsa e non basta mai per raccogliere tutto; (3) il verbale sbagliato resta agli atti e chiude accessi nei casi successivi
- **Decisione di design vincolante:** nessuna statistica RPG può risolvere un enigma. La progressione è **accesso** (chiavi, registri, fiducia), mai potere. Nessun combattimento, nessun livello, nessun punto esperienza.
- **Vincolo di sequenza:** i 9 abitanti vanno definiti **prima** dei 3 casi — i casi nascono dalle relazioni
- **Vincolo di qualità non negoziabile:** ogni caso deve avere soluzione unica e formalmente verificata da `qa-lead`, e almeno tre catene deduttive indipendenti
- Macroarea `prog-*` confermata **STUB**: nessuna produzione di codice in questo scope

### Asset in pending approval
*(nessuno — la visione creativa è autorità diretta del Director)*

### Conflitti aperti
*(nessuno)*

### Domande aperte
1. Verbale incompleto alle ore 18: deposito parziale o compilazione obbligatoria?
2. Esiste una casella "ignoti" — accusa rifiutata onestamente, con un costo sociale?
3. I tre casi sono in ordine fisso o scegliibile dal giocatore?

### Context per prossima sessione
La visione creativa è approvata ed è la radice della KB: ogni asset successivo deve
esserle coerente. Il progetto entra in **fase di design**. Ordine di dipendenza
consigliato: `design-game-designer` (loop della giornata e meccanica del verbale) →
`design-systems-designer` (costi in tempo, fiducia, regola del timbro) →
`design-world-designer` (Pietrafitta e i nove abitanti) → `design-quest-designer`
(i tre casi) → `narr-narrative-designer` (il filo conduttore).
Le tre domande aperte vanno risolte con `design-game-designer`, perché
determinano la forma del loop.

---

## Storico sessioni

| Data | Asset prodotti | Decisioni chiave | Agenti usati |
|---|---|---|---|
| 2026-06-25 | 0 | Init sistema | system |
| 2026-08-23 | 1 | Kickoff, poi pivot a *Pietrafitta*: mini-RPG investigativo, tre pilastri, scope 3 casi | dir-game-director, kb-librarian |
