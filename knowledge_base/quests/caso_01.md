---
role: quests
date: 2026-08-24
author: dir-game-director
status: draft
locked_by: null
description: Caso 1 della vertical slice — "I tre vaglia". Sottrazione di valori postali in danno di Assunta Marucci. Caso di apertura, interamente risolvibile nel centro abitato, zero escursioni obbligatorie. Include soluzione delle 9 caselle, dimostrazione di unicità, tre catene indipendenti, tre depistaggi confutabili.
depends_on:
  - knowledge_base/production/creative_vision.md
  - knowledge_base/systems/core_loop_e_verbale.md
  - knowledge_base/systems/economia_tempo_e_fiducia.md
  - knowledge_base/regions/pietrafitta.md
  - knowledge_base/characters/abitanti_pietrafitta.md
  - knowledge_base/qa_reports/standard_rigore_casi.md
---

# Caso 1 — I tre vaglia

**Posizione nella slice:** primo, ordine fisso.
**Escursioni fuori dal centro richieste: ZERO.** Verifica RD-10 in §7.

## 1. Il fatto (verità oggettiva, non modificabile dal giocatore)

Pietro Marucci, emigrato in Belgio, ha spedito alla madre Assunta tre vaglia — gennaio, febbraio, marzo 1954 — per complessive 21.000 lire. Nessuno dei tre è arrivato.

**Renzo Bianconi**, titolare della ricevitoria postale, li ha incassati imitando la firma di Assunta sulle quietanze. Il denaro è andato al sanatorio di Passo Corvo, dove è ricoverata sua moglie Ada: quattromila lire al mese, più dell'utile dell'emporio.

L'ultimo, il 6 marzo, l'ha incassato alle 17:30, nei venti minuti in cui chiude da solo il sacco postale in partenza.

**Assunta non sa di essere stata derubata.** Crede che il figlio l'abbia dimenticata, e ne parla come di una vergogna familiare. È questa la ragione per cui il fatto emerge solo oggi: una lettera di Pietro, arrivata ieri, dice «i soldi ve li ho mandati tutti e tre».

Assunta non l'ha letta. **Assunta non sa leggere.**

## 2. La soluzione unica del verbale

| # | Casella | Valore corretto |
|---|---|---|
| 1 | ORA | 6 marzo 1954, ore 17:30–17:50 |
| 2 | LUOGO | Retro della ricevitoria, Emporio Bianconi (L3) |
| 3 | ATTO | Sottrazione di valori postali |
| 4 | RESPONSABILE | Renzo Bianconi |
| 5 | PARTE LESA | Assunta Marucci |
| 6 | MEZZO | Quietanza con firma imitata |
| 7 | MOVENTE | Stato di necessità |
| 8 | CIRCOSTANZA | La chiusura solitaria del sacco postale |
| 9 | FONTE | Bollettario dei vaglia, cucito, tre matrici strappate |

### Liste chiuse prestampate

**ATTO (6 voci, questo caso):** sottrazione di valori postali · falsità in scrittura privata · smarrimento colposo di corrispondenza · truffa in danno di privato · appropriazione di cosa smarrita · insolvenza fraudolenta.

**MOVENTE (8 voci, unica per l'intera slice — LC-0):** lucro · stato di necessità · occultamento di altro illecito · rancore per fatti di guerra · causa d'onore · contesa di confine · timore di pubblica rivelazione · negligenza senza fine di profitto.

## 3. Dimostrazione di unicità

### T1 — Domini dichiarati

| Casella | Dominio dei candidati raccoglibili |
|---|---|
| ORA | 6 gen · 4 feb · 6 mar mattina · 6 mar 12:30–15:00 · **6 mar 17:30–17:50** · 7 mar |
| LUOGO | Emporio banco · **retro ricevitoria** · piazza (L2) · municipio (L1) · osteria (L4) |
| ATTO | le 6 voci prestampate |
| RESPONSABILE | Renzo · Bruno · Assunta · Bardi · Nerina · **IGNOTI** |
| PARTE LESA | Assunta · Pietro Marucci · l'Amministrazione postale |
| MEZZO | quietanza con firma imitata · bollettario · sacco postale · registro raccomandate |
| MOVENTE | le 8 voci prestampate |
| CIRCOSTANZA | chiusura solitaria del sacco · assenza di controlli · analfabetismo della parte lesa · lontananza di Pietro |
| FONTE | bollettario vaglia · lettera di Pietro · Nerina Vaccari · Assunta · contabili di Roccalta |

### T2 — Eliminazione per vincolo

**Comma I.** Le tre date di emissione sono note dalla lettera di Pietro; ma solo il vaglia di marzo ha una matrice strappata **con lo strappo ancora fresco e la cucitura non riassestata**, e il bollettario è cucito, quindi l'ordine è inalterabile: la matrice mancante sta fra il n. 3341 (ore 17:10, cliente Pieri) e il n. 3343 (ore 17:55, sacco già chiuso). L'intervallo è forzato: **17:30–17:50**. Il luogo segue: le quietanze si firmano al retro, non al banco, e alle 17:30 il banco è visibile dalla piazza. L'atto è determinato dal fatto che il valore è *postale* e non privato — chi sceglie «falsità in scrittura privata» qualifica il mezzo al posto dell'atto.

**Comma II.** Renzo è l'unico che possa accedere al bollettario cucito: è l'unico licenziatario. Bruno cade su due date (6 gennaio e 4 febbraio sono un mercoledì e un giovedì: Bruno scende solo martedì e venerdì). Assunta cade sul mezzo: **firma con croce e non sa tracciare la propria firma in lettere** — la quietanza porta una firma in corsivo, che lei è materialmente incapace di produrre. Il suo segreto è la prova della sua innocenza. La parte lesa è Assunta e non Pietro: il vaglia è pagabile al destinatario, e il danno patrimoniale è di chi non ha ricevuto.

**Comma III.** Il movente è vincolato dalla cifra e dalla destinazione: 21.000 lire in tre mesi contro una retta di 4.000 al mese. Non c'è arricchimento — il quaderno del credito dell'emporio mostra che Renzo ha *aumentato* il credito concesso ai clienti nello stesso trimestre. «Lucro» è falsificato dai numeri. La circostanza è l'unica finestra materialmente disponibile. La fonte è il solo documento che regga in Pretura: la testimonianza di Assunta è invalidata dalla sua stessa dichiarazione precedente («mio figlio non manda più nulla»).

### T3 — Residuo

Una sola combinazione sopravvive a tutti i vincoli, per ciascun comma. Nessun comma ammette una seconda assegnazione compatibile.

### T4 — Coerenza cross-comma

Il MEZZO (firma imitata) esige un RESPONSABILE alfabetizzato con accesso al bollettario: elimina simultaneamente Assunta e chiunque non sia il licenziatario. La CIRCOSTANZA (chiusura solitaria) esige l'ORA del Comma I. I tre commi non sono indipendenti nella verità, solo nel percorso.

### T5 — Near-miss (uno per comma)

| Comma | Near-miss | Perché cade |
|---|---|---|
| I | ATTO = falsità in scrittura privata | Qualifica il mezzo, non il fatto. Il valore sottratto è postale |
| II | PARTE LESA = Pietro Marucci | Pietro è il mittente; il vaglia è pagabile ad Assunta |
| III | MOVENTE = lucro | Il quaderno del credito mostra credito in aumento, non accumulo |

## 4. Le tre catene deduttive indipendenti

**Catena A — Comma I (documentale, tutta in L3).** Bollettario cucito → tre salti di numerazione → strappi visibili → il n. 3342 manca fra due orari registrati. *Non richiede alcun testimone.*

**Catena B — Comma II (testimoniale + materiale).** Assunta all'emporio fra le 6:40 e le 7:20, o alla messa prima alle 6:00 → dichiara che Pietro non manda più nulla → la lettera di Pietro dice il contrario → una delle due affermazioni è falsa e il punto di contatto è il banco. La firma sulle quietanze si confronta con i fogli di famiglia al municipio (L1): croce contro corsivo. *Non richiede il bollettario.*

**Catena C — Comma III (sociale).** Ada Bianconi ricoverata → la retta è nota a Bardi (osteria, 13:00–14:30) e a Nerina, che è la sorella → il quaderno del credito e le bolle merce mostrano un'attività in perdita. *Non richiede né il bollettario né Assunta.*

**Verifica del vincolo 8:** nessuna casella dipende da una fonte sola. Assunta è sostituibile con i fogli di famiglia; Nerina con Bardi; il bollettario con le quietanze. Perdere un testimone non chiude alcun comma.

## 5. I depistaggi e le loro confutazioni

| # | Depistaggio | Perché è plausibile | Confutazione raggiungibile |
|---|---|---|---|
| D1 | **Bruno Marucci** — deve 8.400 lire all'emporio e ha sette ore cieche al giorno | È il sospetto ovvio del paese | Due delle tre riscossioni cadono in giorni in cui non è sceso in paese (scende solo martedì e venerdì). Bollettario + memoria di Nerina sulle presenze |
| D2 | **Assunta stessa** — ha incassato e dimenticato, o si è fatta ingannare da un terzo | Confonde le date, dice di aver «controllato» carte che non ha letto | Firma con croce sui fogli di famiglia (L1). Non può aver prodotto una firma in corsivo |
| D3 | **Dott. Bardi** — 340.000 lire di debiti di gioco | Movente finanziario schiacciante | Alle 17:30 è all'osteria a carte con Rovina e il geometra, ogni giorno, con molti testimoni |

**Equità (EQ-3):** ciascuna confutazione è raggiungibile con una sola azione da un luogo del centro. Nessun depistaggio si elimina «col senno di poi».

## 6. Conseguenze sull'accesso nel Caso 2

| Esito del verbale | Effetto |
|---|---|
| **Corretto** (Renzo responsabile) | Renzo perde licenza e libertà. **Nerina si chiude**: perde il fratello per mano del segretario. Cade come fonte sulle partenze della corriera e sulle bolle della farina. Assunta passa a fiducia alta: il segretario le ha restituito il figlio |
| **Sbagliato su Bruno** | **Assunta si chiude** — è sua madre. Il paese perde l'unica testimone della strada alta. Renzo resta al banco e continuerà a mentire sugli orari altrui |
| **Sbagliato su Assunta** | Il paese giudica l'atto crudele. Assunta e Nerina si chiudono entrambe. È l'esito peggiore possibile |
| **IGNOTI sul responsabile** | Nessuno è colpito. Renzo resta libero e **sa di essere stato sfiorato**: nel Caso 3 sarà più cauto e più utile, perché ha bisogno di dimostrarsi collaborativo |
| **In bianco** | La Pretura completa d'ufficio con il valore socialmente più comodo: **Lidia Sacchetti**, forestiera. Una donna innocente e sola viene segnata per un reato che non poteva commettere. Conseguenze gravissime nel Caso 2 |

## 7. Verifica dei vincoli di composizione

| Vincolo | Esito |
|---|---|
| **RD-10 / TC-2** (max una escursione) | **Zero escursioni.** Tutte le prove stanno in L1–L4. Assunta è raggiungibile in centro fra le 5:35 e le 7:20 senza salire alla Cerreta |
| **FT-2** (dorsale a fiducia T0) | Le catene A e B sono interamente documentali: bollettario, fogli di famiglia, lettera. Nessuna richiede fiducia guadagnata |
| **RD-9 / TC-1** (azioni condivise) | Tre: la visita al municipio serve al Comma II (firma) e al Comma III (fascicoli); Nerina serve al Comma II e al III; il bollettario al I e al II |
| **Vincolo 7** (sopralluogo) | Il sopralluogo delle 06:00 alla ricevitoria dà 4 candidati ORA incompatibili (i tre mesi + il giorno di ieri) e 3 candidati LUOGO (banco, retro, sacco già in piazza). Nessuna coppia determina |

## 8. Gancio narrativo

Il caso insegna tre cose senza dirle: che i documenti battono i testimoni, che il segreto di una persona può essere la prova della sua innocenza, e che chiudere bene un verbale può costare al segretario una fonte per sempre.

Lascia in campo, non risolto: **perché Pietro scriveva e nessuno leggeva.** Assunta ha in casa tre anni di lettere che non ha mai letto. Ci sono dentro cose che riguardano il Caso 3.

Consegna a `narr-narrative-designer`: la lettera del 6 marzo è il primo oggetto del gioco. Va scritta.
