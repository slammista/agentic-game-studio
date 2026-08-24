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

### Seconda parte di sessione — pipeline agenti (2026-08-23 sera)

**Completati:** `design-game-designer` (loop + verbale), `design-world-designer`
(paese + nove abitanti), `qa-lead` (standard di rigore rev.2).

**Interrotto dal limite di sessione, da rilanciare:**
`design-systems-designer` → `systems/economia_tempo_e_fiducia.md`. **Nessun file
prodotto**, va rifatto da zero col mandato originale.

**Non ancora lanciato:** `design-quest-designer` (i tre casi).

### Stato di blocco — leggere prima di riprendere

`design-quest-designer` **non è lanciabile** finché non esiste la baseline dei
costi-tempo. Lo standard QA esprime le soglie in frazioni del budget giornaliero
`B`; senza la tabella dei costi confermata da `design-systems-designer`, nessun
caso può ricevere PASS pieno — al massimo `PASS condizionato ai costi`.

Ordine obbligato alla ripresa:
1. `design-systems-designer` → `systems/economia_tempo_e_fiducia.md`
   (conversione minuti→mezze, costi, fiducia/accesso, verifica di
   soddisfacibilità delle soglie QA su `B = 24`)
2. `design-quest-designer` → i tre casi, con lo standard QA come specifica
3. `qa-lead` → validazione dei tre casi sulla checklist §7
4. `kb-librarian` → chiusura di sessione

### Decisioni del Director in questa parte di sessione
- Ratificata la scrittura di `design-world-designer` in `characters/`
- Ratificati **entrambi** i conflitti QA vs game designer **a favore del QA**
  (vincoli 7 e 8 della visione creativa)
- Promosso a vincolo di progetto: uno slot di autosalvataggio, nessun reload

### Context per prossima sessione
La visione creativa è approvata ed è la radice della KB. Design del loop, del
mondo e dello standard di qualità sono in `draft` e coerenti fra loro dopo le
ratifiche. Manca l'anello economico, e da esso dipendono i casi.

---

## Storico sessioni

| Data | Asset prodotti | Decisioni chiave | Agenti usati |
|---|---|---|---|
| 2026-06-25 | 0 | Init sistema | system |
| 2026-08-23 | 1 | Kickoff, poi pivot a *Pietrafitta*: mini-RPG investigativo, tre pilastri, scope 3 casi | dir-game-director, kb-librarian |
