---
role: production
date: 2026-08-23
author: dir-game-director
status: approved
locked_by: null
supersedes: "Visione creativa precedente (Condominio Nove, roguelike d'azione) — abbandonata su decisione del committente prima di qualsiasi asset dipendente."
description: Visione creativa fondativa del progetto. Documento radice — ogni altro asset della KB deve essere coerente con questo file.
---

# Visione Creativa — PIETRAFITTA

## Identità del progetto

| Campo | Valore |
|---|---|
| Titolo di lavorazione | **Pietrafitta** |
| Genere | Mini-RPG investigativo / gioco di logica a casi episodici |
| Tono | Giallo di provincia italiana, 1954. Realistico, umano, senza soprannaturale |
| Prospettiva | 2D, vista laterale o isometrica leggera; esplorazione a luoghi discreti |
| Sessione tipo | **Un caso = una giornata di gioco = 25–40 minuti** |
| Scope corrente | **Vertical slice**: 3 casi collegati (vedi sezione dedicata) |
| Lingua master | Italiano |

## Logline

Sei il segretario comunale di Pietrafitta, ottocento anime sull'Appennino.
Non sei un poliziotto: sei l'uomo che deve scrivere cosa è successo. Hai una
giornata per capirlo, e alle diciotto la corriera porta il tuo verbale in
Pretura. Quello che scrivi diventa la verità ufficiale — anche quando è
sbagliata.

## I tre pilastri

### Pilastro 1 — Il verbale è la meccanica

Il gioco non ti chiede di cliccare sul colpevole. Ti chiede di **compilare un
documento**: un modulo prestampato con caselle vuote da riempire con nomi,
oggetti, ore, moventi. `Il giorno __, alle ore __, __ ha __ ai danni di __,
servendosi di __, perché __.`

Il verbale si verifica da solo: è diviso in **tre commi disgiunti di tre caselle
ciascuno**, e un comma si fissa col timbro solo quando tutte e tre le sue caselle
sono corrette. Il giocatore riceve conferma del progresso senza mai sapere *quale*
singola casella fosse giusta. Questo rende impossibile la forza bruta e premia il
ragionamento a gruppi — deduci un nesso intero, non una variabile isolata.

> **Correzione di design (2026-08-23, `design-game-designer`, accolta dal Director).**
> La prima stesura di questo pilastro prevedeva una finestra *scorrevole* di tre
> caselle contigue. È stata scartata: con `1-2-3` già timbrato, testare `2-3-4`
> isolerebbe il valore della casella 4, e il timbro degraderebbe in un oracolo
> casella-per-casella. I commi **disgiunti** garantiscono che ogni conferma resti
> un predicato congiuntivo su tre incognite.

Il legame tra finzione e sistema è totale: la deduzione non è una metafora del
lavoro del protagonista, **è** il lavoro del protagonista.

### Pilastro 2 — Il tempo è l'unica risorsa

Una giornata, dall'alba alla corriera delle diciotto. Ogni azione la consuma:
salire al podere costa più che attraversare la piazza, far parlare un
reticente costa più che ascoltare un chiacchierone, rileggere i registri
comunali costa un'ora piena.

Non puoi interrogare tutti. Non puoi visitare tutto. Ogni caso ha più prove di
quante tu possa raccogliere, e la soluzione è raggiungibile da percorsi
diversi: **la scarsità non nasconde la verità, obbliga a sceglierne la strada.**

Conseguenza per il design: nessun caso deve avere un'unica catena deduttiva
obbligata. Vincolo vincolante per `design-quest-designer`.

### Pilastro 3 — Il paese ricorda quello che hai scritto

La verità di un caso non cambia mai. Il **verbale** sì. Se depositi il nome
sbagliato, il caso si chiude comunque: la Pretura non torna indietro, e
Pietrafitta va avanti con un innocente segnato e un colpevole libero.

Le conseguenze sono di accesso, non di punteggio. La sorella di un uomo
ingiustamente accusato non ti aprirà più la porta — e nel caso successivo era
lei l'unica testimone della strada alta. Un colpevole lasciato libero compare
di nuovo, più cauto.

Non esiste schermata di game over. Esiste un paese che si chiude, o che si
fida.

## Cosa significa "mini-RPG" qui

**C'è:** un personaggio con un nome e una posizione sociale, una mappa piccola
da percorrere, dialoghi con scelta di approccio, un inventario di documenti,
una gestione di risorse (tempo, fiducia), e conseguenze persistenti tra i casi.

**Non c'è, per decisione vincolante:** combattimento, punti esperienza, livelli,
e soprattutto **nessuna statistica che risolva un enigma al posto del
giocatore.** Nessun tiro di "Intuito" rivela mai un indizio. Se una prova è
ottenibile, lo è perché il giocatore è andato nel posto giusto e ha chiesto la
cosa giusta a chi poteva rispondere.

La progressione tra i casi è **accesso**: nuove chiavi, nuovi registri
consultabili, persone che ora ti parlano. Mai potere.

## Core loop

```
Mattina — un fatto viene segnalato. Ricevi il modulo di verbale vuoto.
  ↓
Giri il paese: luoghi, persone, documenti. Ogni azione consuma tempo.
  ↓
Il quaderno registra automaticamente ciò che hai visto e sentito — fatti, non conclusioni.
  ↓
Compili le caselle del verbale combinando le voci del quaderno.
  ↓
Tre caselle contigue corrette → timbro, si fissano.
  ↓
Ore 18: la corriera parte. Depositi il verbale, completo o no.
  ↓
Il paese reagisce a ciò che hai scritto. Il caso successivo parte da lì.
```

## Cosa rende il gioco diverso

| Convenzione del genere | Cosa facciamo noi |
|---|---|
| L'investigatore è un professionista con autorità | È un impiegato senza potere, che deve chiedere permesso |
| Raccogli tutti gli indizi, poi risolvi | Non puoi raccoglierli tutti: il tempo finisce prima |
| Sbagliare = riprovare il caso | Sbagliare = il caso è chiuso male, e il gioco continua così |
| L'accusa è un clic sul ritratto del colpevole | L'accusa è un documento articolato che deve reggere in ogni sua parte |
| Gli indizi sono fisici (impronte, sangue) | Gli indizi sono sociali: orari, debiti, parentele, chi era dove e perché mentiva |

## Pubblico di riferimento

Giocatori di deduzione pura (Return of the Obra Dinn, The Case of the Golden
Idol, Her Story) che cercano casi più brevi e un contesto umano invece che
astratto. Sovrapposizione con lettori di giallo mediterraneo — Camilleri,
Sciascia — e con chi gioca RPG narrativi brevi per le conseguenze, non per il
combattimento.

Non è un gioco per chi vuole azione, né per chi vuole essere rassicurato di
aver ragione.

## Vincoli creativi (vincolanti per ogni macroarea)

1. **Nessun soprannaturale, nessuna coincidenza risolutiva.** Ogni caso deve
   essere spiegabile con moventi ordinari: soldi, terra, vergogna, gelosia,
   paura.
2. **Ogni bugia di un personaggio ha una ragione difendibile**, e almeno una
   crepa verificabile altrove. Un testimone non mente mai solo per depistare
   il giocatore.
3. **1954 è un vincolo, non una decorazione.** Niente telefoni, niente analisi
   scientifiche, niente archivi rapidi. Si deduce da registri di carta,
   orari della corriera, memoria delle persone.
4. **Il quaderno registra solo fatti osservati, mai conclusioni.** Il gioco non
   pensa per il giocatore.
5. **Ogni caso deve essere risolvibile al 100% con le informazioni disponibili
   in una singola giornata**, pur non essendo possibile raccoglierle tutte.
   Verificato da `qa-lead` su ogni caso, senza eccezioni.
6. **Uno slot di salvataggio automatico. Nessun salvataggio manuale, nessun
   reload del caso.** Vincolo tecnico con valore creativo: senza di esso ogni
   difesa contro il tentativo casuale è aggirabile ricaricando, e la giornata
   smette di essere una decisione. Sollevato da `design-game-designer`, accolto
   dal Director.

## Scope — Vertical Slice

**Obiettivo:** tre casi collegati, completi e rifiniti. Tre perché è il minimo
per far sentire il Pilastro 3: il primo stabilisce, il secondo mostra la
conseguenza, il terzo la fa pesare.

### Dentro lo scope

| Area | Deliverable |
|---|---|
| Mondo | Pietrafitta: 8 luoghi percorribili + la mappa del paese |
| Sistemi | Sistema del verbale (caselle, timbro a gruppi di tre), sistema tempo, sistema fiducia/accesso |
| Casi | **3 casi** con soluzione unica e percorsi deduttivi multipli |
| Personaggi | 9 abitanti: ciascuno con orario della giornata, un segreto, una ragione per mentire |
| Narrativa | Arco dei tre casi + il filo che li collega |
| Dialoghi | Alberi per 9 abitanti × 3 casi, con varianti secondo la fiducia |
| Documenti | Registri comunali, lettere, orari della corriera — indizi leggibili in-game |
| Art direction | Palette e riferimenti: provincia appenninica anni '50 |
| Audio | Direzione sonora + palette SFX ambientali |
| UI/UX | **Il modulo del verbale e il quaderno** — sono l'interfaccia principale, priorità massima |
| QA | Piano di test: risolvibilità di ogni caso, assenza di soluzioni ambigue |

### Fuori scope (esplicitamente rimandato)

- Casi dal quarto in poi e la stagione completa
- Sistema di reputazione con enti esterni (Pretura, Curia, Carabinieri)
- Localizzazione (resta `it` master, vedi `production/config.md`)
- Qualsiasi produzione di codice: la macroarea `prog-*` resta **STUB** finché
  non esiste una codebase reale (vedi `CLAUDE.md`)

## Rischi identificati

| Rischio | Impatto | Mitigazione |
|---|---|---|
| Un caso risulta ambiguo: due soluzioni entrambe difendibili | **Critico** — distrugge la fiducia nel gioco | Ogni caso passa una verifica di unicità formale in `qa_reports/`. Nessun caso entra in produzione senza. |
| Il giocatore si blocca e la giornata finisce senza progresso | Alto | Ogni caso ha almeno tre catene deduttive indipendenti; fallire una non chiude le altre. |
| Il verbale a caselle risulta un esercizio di compilazione noioso | Alto | La UI del verbale è priorità massima per `viz-ui-ux-artist`. Il timbro deve essere una piccola ricompensa fisica e soddisfacente. |
| Il vincolo temporale genera frustrazione anziché tensione | Medio | Il tempo consumato è sempre annunciato prima dell'azione. Mai costi nascosti. |
| Il "mini-RPG" fa aspettare progressione da RPG e delude | Medio | Comunicare fin dalla prima schermata che si cresce in accesso, non in potenza. Verificato da `qa-ux-researcher`. |

## Domande aperte per la prossima sessione

1. **Se il verbale è incompleto alle 18, cosa succede?** Si deposita parziale
   (e la Pretura decide male da sola), oppure il giocatore è obbligato a
   riempire ogni casella anche tirando a indovinare?
2. **Il giocatore può rifiutarsi di accusare?** Esiste una casella "ignoti" —
   onesta ma con un suo costo sociale?
3. **I tre casi sono in ordine fisso o scegliibile?** L'ordine fisso rende il
   Pilastro 3 controllabile; la scelta lo rende più personale.

---

**Prossimi passi consigliati** (in ordine di dipendenza):
`design-game-designer` (loop della giornata e meccanica del verbale) →
`design-systems-designer` (costi in tempo, fiducia, regola del timbro) →
`design-world-designer` (Pietrafitta e i suoi nove abitanti) →
`design-quest-designer` (i tre casi) → `narr-narrative-designer` (il filo che
li lega).

Nota di sequenza: **i nove abitanti vanno definiti prima dei casi**, non dopo.
I casi nascono dalle relazioni tra le persone, non il contrario.
