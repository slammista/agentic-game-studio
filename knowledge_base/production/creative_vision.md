---
role: production
date: 2026-08-23
author: dir-game-director
status: approved
locked_by: null
description: Visione creativa fondativa del progetto. Documento radice — ogni altro asset della KB deve essere coerente con questo file.
---

# Visione Creativa — CONDOMINIO NOVE

## Identità del progetto

| Campo | Valore |
|---|---|
| Titolo di lavorazione | **Condominio Nove** |
| Genere | Roguelike d'azione, real-time, top-down |
| Tono | Weird / surreale — burocrazia domestica che diventa organismo |
| Prospettiva | Dall'alto, camera fissa per stanza |
| Sessione tipo | 20–35 minuti per run |
| Scope corrente | **Vertical slice** (vedi sezione dedicata) |
| Lingua master | Italiano |

## Logline

Ogni notte il tuo palazzo si riorganizza. Scendi al Piano Meno Uno per consegnare
un reclamo all'Amministrazione — l'unico documento che può sciogliere il contratto
che lega gli inquilini all'edificio. Non ci sei mai arrivato. L'edificio ti ha
visto provare, e ha imparato.

## I tre pilastri

### Pilastro 1 — L'edificio è un avversario che ricorda

La progressione meta non è nelle mani del giocatore: è nell'edificio. Ogni run
lascia una traccia. Il palazzo mura le scale che usi troppo, sposta l'ascensore
lontano dalla tua rotta abituale, mette guardie dove hai vinto facile. Non è
difficoltà crescente: è **difficoltà personalizzata**. Due giocatori diversi
affrontano due palazzi diversi dopo dieci run.

Conseguenza di design: nessuna build ottimale esiste a lungo. La soluzione che
funziona smette di funzionare perché l'hai usata.

### Pilastro 2 — Le Abitudini: potere che ti rende prevedibile

Ripetere un comportamento (stessa arma, stessa rotta, stesso stile di combat)
accumula una **Abitudine**. Le Abitudini sono potenti — danno bonus concreti e
crescenti. Ma ogni Abitudine è anche il canale attraverso cui l'edificio ti
legge: più è forte, più precisa è la contromossa.

Il giocatore è costantemente davanti alla stessa domanda: *rafforzo ciò che
funziona, o rompo lo schema prima che l'edificio lo chiuda?* È la tensione
centrale del gioco, e va sentita in ogni singola run.

### Pilastro 3 — Il perturbante sta nel quotidiano, non nel mostruoso

Niente demoni, niente tentacoli gratuiti. L'orrore surreale nasce da oggetti
domestici presi sul serio: un avviso di condominio che continua ad aggiornarsi
mentre lo leggi, un vicino che ti ringrazia per una cortesia che non gli hai
mai fatto, il contatore del gas che conta all'indietro qualcosa che non è gas.

Regola vincolante per tutti i reparti: **ogni elemento weird deve avere una
controparte mondana riconoscibile.** Se un asset non è riconducibile alla vita
di un palazzo reale, non entra nel gioco.

## Core loop

```
Ti svegli nel tuo appartamento (Piano 9) con un reclamo in mano
  ↓
Scendi di piano in piano — stanze procedurali, combattimento real-time
  ↓
Raccogli Attrezzi (armi) e Cortesie (potenziamenti dai vicini)
  ↓
Accumuli Abitudini → più forte, più leggibile
  ↓
L'edificio reagisce in tempo reale (chiude rotte, schiera contromisure)
  ↓
Muori / vieni "sfrattato" → torni al Piano 9
  ↓
L'edificio si riorganizza sulla base di ciò che hai fatto
  ↓
Il reclamo, però, resta. È l'unica cosa che nessun reset cancella.
```

Il reclamo è la spina dorsale narrativa: **si riempie di firme**. Ogni vicino
che convinci firma. Le firme persistono tra le run. Le firme sono la vera
progressione del giocatore — e sono narrative, non statistiche.

## Cosa rende il gioco diverso

| Convenzione del genere | Cosa facciamo noi |
|---|---|
| Meta-progressione = il giocatore diventa più forte | Meta-progressione = l'edificio diventa più mirato; il giocatore accumula alleati |
| Build ottimale da scoprire e ripetere | Ogni build si autodistrugge se ripetuta |
| Morte = fallimento da riavvolgere | Morte = notte finita; la mattina è canonica, non un reset |
| Ambientazione fantasy/sci-fi | Palazzo italiano anni '70, portineria, avvisi, tapparelle |

## Pubblico di riferimento

Giocatori di roguelike d'azione (Hades, Dead Cells, Returnal) che hanno esaurito
la novità del genere e cercano un sistema che reagisca a loro. Sovrapposizione
con l'audience di weird fiction giocabile (Inscryption, Anatomy, Kentucky Route
Zero). Non un gioco per chi cerca power fantasy pulita.

## Vincoli creativi (vincolanti per ogni macroarea)

1. Nessun elemento visivo, sonoro o narrativo può uscire dal registro
   "palazzo abitato". Il weird entra per deformazione del familiare.
2. L'edificio non parla mai in prima persona. Si esprime solo tramite
   architettura, avvisi affissi e comportamento degli inquilini.
3. Nessun tutorial testuale esplicito. Le regole si imparano dai cartelli
   condominiali, che sono diegetici e inaffidabili.
4. Il giocatore non ha nome, volto, né voce. È "l'inquilino del Nove".
5. Le firme sui reclami sono l'unica risorsa persistente narrativamente
   giustificata. Ogni altra persistenza va approvata dal Director.

## Scope — Vertical Slice

**Obiettivo:** una fetta verticale completa e rifinita, non un gioco intero
abbozzato. Deve essere sufficiente a far provare i tre pilastri in una sessione
di 30 minuti.

### Dentro lo scope

| Area | Deliverable |
|---|---|
| Mondo | Il palazzo: 1 edificio, piani 9 → 6 + Piano Meno Uno intravisto |
| Sistemi | Core combat, sistema Abitudini, sistema Adattamento dell'edificio, economia delle Cortesie |
| Livelli | 4 piani con layout procedurale + 1 arena di boss |
| Encounter | 3 archetipi di avversario + 1 boss (l'Amministratore Pro Tempore) |
| Personaggi | 4 vicini firmatari, ciascuno con condizione per firmare |
| Narrativa | Arco della prima notte + 3 avvisi condominiali evolutivi |
| Dialoghi | 4 alberi di dialogo (uno per vicino) |
| Art direction | Palette, riferimenti, regole di deformazione del familiare |
| Audio | Direzione sonora + palette SFX domestici |
| QA | Piano di test dei tre pilastri |

### Fuori scope (esplicitamente rimandato)

- Piani 5 → 1 e il finale vero
- Sistema di crafting degli Attrezzi
- Modalità di difficoltà aggiuntive
- Localizzazione (resta `it` master, vedi `production/config.md`)
- Qualsiasi produzione di codice: la macroarea `prog-*` resta **STUB** finché
  non esiste una codebase reale (vedi `CLAUDE.md`)

## Rischi identificati

| Rischio | Impatto | Mitigazione |
|---|---|---|
| L'Adattamento dell'edificio risulta punitivo anziché stimolante | Alto — uccide il pilastro 1 | Il contro-adattamento chiude rotte ma ne apre sempre almeno una nuova. Mai sottrazione netta. |
| Le Abitudini sono troppo lente da accumulare per farsi sentire in una run | Alto | Devono maturare entro 2 piani, non entro 2 run. Vincolo per systems designer. |
| Il registro weird scivola nell'horror generico | Medio | Vincolo creativo 1, verificato da `qa-cross-domain` su ogni asset. |
| Il palazzo italiano risulta illeggibile a un pubblico internazionale | Medio | Lo specifico culturale è un punto di forza, non un ostacolo: si comunica per immagini, non per riferimenti testuali. |

## Domande aperte per la prossima sessione

1. Il combattimento è ad armi bianche corpo a corpo o include distanza?
2. Il boss del vertical slice è battibile alla prima notte, o è per design una
   sconfitta narrativa programmata?
3. Le Abitudini sono visibili al giocatore come UI esplicita, o vanno intuite?

---

**Prossimi passi consigliati** (in ordine di dipendenza):
`design-game-designer` (core loop e combat) → `design-systems-designer`
(Abitudini + Adattamento) → `design-world-designer` (il palazzo e i suoi
inquilini) → `narr-narrative-designer` (arco della prima notte).
