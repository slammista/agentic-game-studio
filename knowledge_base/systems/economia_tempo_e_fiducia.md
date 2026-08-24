---
role: design-systems-designer
date: 2026-08-23
author: design-systems-designer
status: draft
locked_by: null
description: Bilanciamento operativo di Pietrafitta — conversione minuti/mezze con dislivello asimmetrico, tabella completa dei costi d'azione, verifica numerica di soddisfacibilità delle soglie di rigore su B=24, tier di fiducia e accesso, parametrizzazione del completamento d'ufficio della Pretura, costo della trasferta a Roccalta.
depends_on:
  - knowledge_base/production/creative_vision.md
  - knowledge_base/systems/core_loop_e_verbale.md
  - knowledge_base/regions/pietrafitta.md
  - knowledge_base/characters/abitanti_pietrafitta.md
  - knowledge_base/qa_reports/standard_rigore_casi.md
---

# Economia del tempo, della fiducia e dell'accesso — Pietrafitta

Autorità gerarchica applicata in questo documento: `creative_vision.md` vincoli 7-8 **superano** G2 e G3 di `core_loop_e_verbale.md` § 6. Dove i due divergono ho tarato sulla vision.

---

## 1. Conversione minuti → mezze

### 1.1 Regola di conversione (CV)

```
mezze(A→B) = ceil( (minuti(A→B) − 2) / 30 ) + gradini_saliti(A→B)
```

| Termine | Definizione | Giustificazione diegetica |
|---|---|---|
| `ceil(·/30)` | quantizzazione al rintocco successivo del campanile | il segretario annota gli orari a mezze: non esiste altro orologio pubblico (`regions` § Le campane) |
| `− 2 minuti` | tolleranza di rintocco | 30, 31, 32 minuti sono "mezz'ora". Elimina i salti di soglia su differenze di un minuto (L1→L8 = 30′ e L3→L8 = 31′ costano uguale) |
| `gradini_saliti` | +1 per ogni gradino altimetrico superato **in salita**, 0 in discesa | «la salita si paga»: si arriva col fiato corto, ci si ferma alla fontana. È il termine che preserva l'asimmetria del world designer |

**Gradini altimetrici** (da `regions` § Altimetria):

| Gradino | Quota | Luoghi |
|---|---|---|
| G0 — fondovalle | q. 520 | L6 Mulino |
| G1 — crinale/paese | q. 780 | L1 Municipio · L2 Piazza · L3 Emporio · L4 Osteria · L5 Chiesa |
| G2 — versante alto | q. 900–940 | L7 Cerreta · L8 Cava |

G0→G2 (mulattiera del Fosso) sale due gradini: +2.

### 1.2 Matrice dei costi di spostamento (mezze)

Righe = partenza, colonne = arrivo. **La matrice non è simmetrica.**

| da ↓ / a → | L1 | L2 | L3 | L4 | L5 | L6 | L7 | L8 |
|---|---|---|---|---|---|---|---|---|
| **L1** Municipio | — | 1 | 1 | 1 | 1 | **1** | **3** | **2** |
| **L2** Piazza | 1 | — | 1 | 1 | 1 | **1** | **3** | **2** |
| **L3** Emporio | 1 | 1 | — | 1 | 1 | **1** | **3** | **2** |
| **L4** Osteria | 1 | 1 | 1 | — | 1 | **1** | **3** | **3** |
| **L5** Chiesa | 1 | 1 | 1 | 1 | — | **2** | **2** | **2** |
| **L6** Mulino | **3** | **3** | **3** | **3** | **3** | — | **4** | **4** |
| **L7** Cerreta | 1 | 1 | 1 | 1 | 1 | **2** | — | 1 |
| **L8** Cava | 1 | 1 | 1 | 1 | 1 | **1** | 1 | — |

**Asimmetrie prodotte** (verifica del vincolo del world designer):

| Coppia | Salita | Discesa | Δ |
|---|---|---|---|
| L1 ⇄ L7 | 3 | 1 | **3×** |
| L1 ⇄ L6 | 3 | 1 | **3×** |
| L1 ⇄ L8 | 2 | 1 | 2× |
| L5 ⇄ L7 | 2 | 1 | 2× |
| L6 ⇄ L8 (mulattiera) | 4 | 1 | **4×** |
| L6 ⇄ L7 (mulattiera) | 4 | 2 | 2× |
| L7 ⇄ L8 | 1 | 1 | 1× (stesso gradino, 15′) |

**Conseguenza di design:** partire dall'alto è economico, salire è caro. È la leva che rende reale la prima scelta della giornata (§ 3.1) e conferma le "tre conseguenze geografiche vincolanti" di `regions`.

**Condizione meteo (da `regions` L8).** Con pioggia la mulattiera del Fosso è impraticabile: `L6⇄L7` e `L6⇄L8` **non percorribili**. Il giro deve passare dal paese (L6→L1→L7 = 3+3 = 6 mezze). Il quest designer dichiara il meteo del caso; il costo è annunciato come sempre.

**Scostamento dalla baseline di `core_loop` § 1.2** — dichiarato, non implicito:

| Baseline game designer | Mia taratura | Motivo |
|---|---|---|
| centro–centro 1 | 1 | confermata |
| borgo⇄periferia 2 | 2–3 salita, 1 discesa | la baseline non conosceva il dislivello |
| periferia⇄periferia 3 | L7⇄L8 = **1**; L6⇄L7 = 4/2 | L7 e L8 distano 15′ sullo stesso gradino: 3 mezze sarebbero una tassa senza terreno sotto. Il costo del triangolo alto non è la distanza interna, è la salita e l'assenza di carte e di gente |

---

## 2. Tabella dei costi d'azione

Ogni riga è annunciata in preview con costo e **ora di conclusione** prima della conferma (A2, vincolo di visione). Nessun costo condizionale, nessun costo nascosto, nessun costo variabile a runtime.

### 2.1 Movimento e presenza

| Cod. | Azione | Costo | Nota |
|---|---|---|---|
| `MV` | Spostarsi | matrice § 1.2 | |
| `AT` | Attendere / presidiare un luogo | **1 per mezza** | si sceglie l'ora di fine; il costo è mostrato come totale |
| `CR` | Cercare una persona fuori postazione fissa | **2** | Bruno nei campi, don Alceste in visite, Bardi nelle frazioni. Produce comunque un fatto (A3): «alle 10:00 non era all'aia» |

### 2.2 Parola — il costo dipende dalla reticenza

**Scala di reticenza R** derivata da `characters` (segreto protetto + esistenza di un canale di rifiuto legittimo). **Derivata, non inventata: da ratificare da `design-world-designer`** (§ 8, dipendenza D-1).

| R | Definizione | Costo base | Abitanti |
|---|---|---|---|
| **R1** | Parla volentieri. Il rischio è la falsità, non il silenzio | **1** | Renzo Bianconi · Nerina Vaccari |
| **R2** | Dice il vero salvo su una materia circoscritta | **2** | Lidia Sacchetti · Elio Bardi · Assunta Marucci |
| **R3** | Protegge qualcosa di più grande di sé, con un rifiuto difendibile | **3** | Don Alceste · Cav. Rovina · Bruno Marucci · Aldo Fenaroli |

| Cod. | Azione | Costo | Condizione |
|---|---|---|---|
| `AS` | Chiedere a un R1 | 1 | tema aperto al tier corrente |
| `IN2` | Interrogare un R2 | 2 | idem |
| `IN3` | Interrogare un R3 | 3 | idem |
| `+OC` | Supplemento «interlocutore occupato» | **+1** | Lidia in lezione · Renzo con clientela al banco 09:00–12:30 · Aldo alla macina · Nerina in servizio pranzo 11:00–14:30 |
| `LV` | Insistere con una leva | **base +1** | richiede a quaderno una voce di tipo `DOC`/`ORA`/`OSS` pertinente. **Costa −1 tier di fiducia**, annunciato prima. Max 1 per abitante per caso |
| `NB` | Chiedere un'informazione neutra (dov'è X, che ora è, chi è passato) | **1** a chiunque | non dipende da R: non è materia protetta |

**Tre tipi distinti di chiusura di un tema** — la distinzione è vincolante per il quest designer:

| Chiusura | Si apre con | Esempio |
|---|---|---|
| **di reticenza** | `LV` insistere con leva documentale | Bruno sui campi; Renzo sugli orari altrui |
| **di fiducia** | tier (§ 5), mai con la leva | il libro dei debiti di Nerina; i libri degli affitti di Rovina |
| **assoluta** | mai per via di parola | sigillo confessionale di don Alceste; Rovina sul protocollo n. 217. La prova esiste solo su carta o per terzi |

La chiusura assoluta è ciò che rende il vincolo 8 strutturale invece che negoziabile: dove un uomo non parlerà mai, il caso **deve** avere una carta.

### 2.3 Osservazione

| Cod. | Azione | Costo | Ambito |
|---|---|---|---|
| `ES` | Esaminare un ambiente definito | **1** | sacrestia, stalla, retro dell'emporio, un palmento, la loggia |
| `PE` | Perlustrare un'area aperta | **2** | L8 cava e mulattiera, i campi della Cerreta, il castagneto, l'aia, la riva della Fitta |

### 2.4 Carte — sei classi documentali

| Classe | Definizione | Costo | Documenti di Pietrafitta |
|---|---|---|---|
| **D0** | Fatto amministrativo che il segretario già conosce (tipo `REG` del QA) | **0** | orario della corriera · avvisi in bacheca · confini catastali notori · chi è titolare di quale licenza · la matrice delle percorrenze stessa |
| **D1** | Registro corrente, nel luogo dove sei, a indice diretto | **1** | registro di classe · registro della pesa · registro delle macinate · libretto della roggia · libretto colonico · quaderno del credito · quaderno delle giornate di bracciantato |
| **D2** | Registro d'archivio con ricerca per anno o per nome | **2** | protocollo comunale per annata · fogli di famiglia · ruoli d'imposta · registro della condotta medica · registro delle offerte parrocchiali · licenze e nulla osta · fascicoli personali |
| **D3** | Registro con ricerca cieca: numero o data non noti | **3** | registri parrocchiali 1817–1930 · stato delle anime · protocollo 1944 **prima** di conoscere il n. 217 · atti di donazione per repertorio |
| **D4** | Documento privato: il detentore può rifiutare | **2 + tier** | libro dei debiti (Nerina, T2) · libri degli affitti e cambiali (Rovina, T2) · bollettario dei biglietti (Renzo, T2) · matrici dei vaglia (Renzo, **mai**) |
| **D5** | Fuori comune | **§ 2.5** | contabili postali di Roccalta · ricevute della pompa di benzina · foglio di corsa · registri di Pretura, ospedale, carabinieri |

**Nota su D3.** Il protocollo 1944 n. 217 costa **3** finché il giocatore non ha il numero, **2** quando l'ha. Il numero è a sua volta una prova. È il modo corretto di rendere caro un documento senza renderlo irraggiungibile.

### 2.5 D5 — la trasferta a Roccalta (vincolo richiesto dal world designer)

| Cod. | Azione | Costo | Esito |
|---|---|---|---|
| `TR` | Salire sulla corriera delle **07:25** per Roccalta | **tutte le mezze residue** (23 su 24 se si parte dalla prima corriera utile) | rientro alle 17:35, con **sola compilazione e timbro** residui |
| — | Il documento richiesto | — | **arriva nel caso successivo**, non in questo |

Fondamento diegetico, non regola arbitraria: l'ufficio postale di Roccalta rilascia le contabili **su richiesta scritta**, e il foglio di corsa «resta a Roccalta, consultabile solo il giorno dopo» (`regions` § Orario della corriera). La trasferta **deposita una richiesta**; la carta torna col sacco postale del giorno dopo.

Conseguenze quantificate:
- Durante un caso, contabili postali e ricevute della pompa di benzina sono **irraggiungibili**: costo 23/24 = **0,96 B** e resa nulla in giornata. Le prove definitive contro Bianconi e Bardi restano fuori portata, come richiesto.
- Fra i casi sono **progressione di accesso** (Pilastro 3): un caso sacrificato compra una prova per il successivo. È un baratto legittimo, pesantissimo, e annunciato.
- Nel **terzo caso** (ultimo della slice) il gioco lo dichiara in preview: «le contabili arriverebbero a ruolo chiuso». A2 rispettato: nessun costo occulto.

### 2.6 Costo zero — elenco chiuso, invariato

`core_loop` § 1.3, che confermo integralmente e a cui aggiungo: consultare la **matrice dei costi** e la **griglia di reperibilità** (§ 3.2) è gratuito. Il giocatore deve poter pianificare senza pagare per sapere quanto costa.

---

## 3. La giornata

### 3.1 Il sopralluogo delle 06:00 — regola SP-1

| Voce | Valore |
|---|---|
| Costo | **0 mezze** |
| Trasferimento di andata al luogo del fatto | **0** — il messo comunale accompagna il segretario all'alba |
| Al termine | il giocatore sceglie: **rientrare a L1** (0 mezze) oppure **restare sul posto** (0 mezze) |
| In entrambi i casi | 24 mezze intatte alle 06:00 |

Motivo del trasferimento gratuito in entrambe le direzioni: senza di esso il budget effettivo dipenderebbe dal luogo del fatto (un fatto alla Cerreta costerebbe 1 mezza di rientro, uno al mulino 3), e i casi non sarebbero comparabili. Con SP-1 la posizione di partenza diventa **la prima decisione della giornata**, gratuita e informata: restare in quota costa vicinanza alle carte, rientrare costa la salita.

### 3.2 Quantizzazione delle presenze — regola FIN-1

Gli orari di `characters` sono in minuti reali; le azioni sono in mezze. Regola: **ogni fascia di presenza si arrotonda alla mezza che ne contiene almeno metà.** Un'azione richiede che l'interlocutore sia presente per **tutta** la sua durata.

Conseguenza già dirimente: Assunta è in paese 06:40–07:20 (40 minuti reali) → quantizzata a **06:30–07:30 = 2 mezze**, il che la rende interrogabile in paese con `IN2` **esattamente e solo** in quella finestra. Senza FIN-1 sarebbe interrogabile solo alla Cerreta, e la strada alta diventerebbe un collo di bottiglia geografico.

**Griglia di reperibilità in mezze** (giorno feriale tipo; `L·` = luogo dove è interrogabile, `—` = non reperibile, `≈` = reperibile con `CR` 2 mezze):

| Fascia | Alceste | Rovina | Assunta | Bruno | Renzo | Nerina | Lidia | Bardi | Aldo |
|---|---|---|---|---|---|---|---|---|---|
| 06:00–06:30 | L5 | — | L5 | — | — | L4 | — | — | L6 |
| 06:30–07:30 | L5 canon. | — | **L2/L3** | — | L3 (da 07:00) | L4 | L3 | — | L6 |
| 07:30–09:00 | **L5 sacr.** | L2 casa | — | ≈L7 | L3 `+OC` | L4/L3 | L1 `+OC` | L1 (lun/gio) | L6 |
| 09:00–10:30 | — visite | **L2 loggia** | L7 | ≈L7 | L3 `+OC` | L4 | L1 `+OC` | L1 (lun/gio) o — | L6 |
| 10:30–12:00 | — visite | L7 (lun/mer/ven) o — | L7 | ≈L7 | L3 `+OC` | L4 `+OC` | L1 `+OC` | — | L6 |
| 11:00–12:00 | L5 oratorio | ↑ | ↑ | ↑ | ↑ | ↑ | ↑ | ↑ | ↑ |
| 12:00–13:00 | L5 canon. | — | **L7** | **L7** | — | L4 `+OC` | L4 | L4 | L6 |
| 13:00–14:30 | — | — | L7 | ≈L7 | — | L4 `+OC` | L1 | **L4** | L6 |
| 14:30–15:00 | — | — | L7 | ≈L7 | — | — | L1 | — | L6 |
| 15:00–16:00 | **L5 conf.** | L2 studio | L7 | ≈L7 | L3 | — | L1 (lun/gio) | — | L6 |
| 16:00–17:00 | — | L2 studio | L7 | L7 stalla | L3 | L4 | — | — | L6 |
| 17:00–17:30 | — | **L2/L4** | L7 | L7 | L3 | L4 | — | L4 | L6 |
| 17:30–18:00 | L5 funz. | L2/L4 | L7 | L3/L4 (mar/ven) | L3 (retro) | L4 | — | L4 | L4 (lun/mer/sab) |

Derivata da `characters` § giornate tipo. Non modifica quel file: lo quantizza. Ratifica richiesta (§ 8, D-1).

### 3.3 Capienza informativa della giornata

| Profilo di percorso | Spostamenti `M` | Azioni `A` | Prove raccolte | + voci di sopralluogo |
|---|---|---|---|---|
| Centro puro | 5 | 19 | 11 | 5–8 |
| Una escursione in quota, partendo dall'alto | 5 | 19 | 10 | 5–8 |
| Una escursione al mulino | 7 | 16 | 10 | 5–8 |

**Da 15 a 19 elementi di quaderno per giornata**, contro un catalogo di caso da 18–22 prove: il giocatore ne vede il **45–70 %**. Pilastro 2 rispettato per costruzione.

---

## 4. Verifica di soddisfacibilità — il conto

`B = 24 mezze`. Tutte le soglie di `qa_reports/standard_rigore_casi.md` rev.2 pertinenti al bilanciamento.

### 4.1 Caso-modello di riferimento

Non è un caso: è un **catalogo probatorio di riferimento** ancorato ai luoghi e alle persone reali, usato per rendere calcolabili le soglie. Il quest designer non è tenuto a usarlo, è tenuto a produrre un caso i cui numeri stiano dentro gli stessi limiti.

| ID | Luogo | Prova | Tipo | Costo azione |
|---|---|---|---|---|
| P01 | L1 | protocollo 1953: assenza di nulla osta forestale | DOC D2 | 2 |
| P02 | L1 | fogli di famiglia: firma a croce | DOC D2 | 2 |
| P03 | L1 | registro della condotta medica: lacune | DOC D2 | 2 |
| P04 | L1 | registro di classe: quattro supplenze | DOC D1 | 1 |
| P05 | L1 | fascicolo personale Sacchetti | DOC D2 | 2 |
| P06 | L1 | Lidia in aula | TES `IN2`+`OC` | 3 |
| P07 | L2 | registro della pesa pubblica | DOC D1 | 1 |
| P08 | L2 | Rovina in loggia | TES `IN3` | 3 |
| P09 | L2 | libri degli affitti (T2) | DOC D4 | 2 |
| P10 | L3 | Renzo al banco | TES `AS` | 1 |
| P11 | L3 | bollettario dei biglietti (T2) | DOC D4 | 2 |
| P12 | L3 | matrici dei vaglia — accesso mai concesso | DOC D4 | — |
| P13 | L4 | Nerina | TES `AS` | 1 |
| P14 | L4 | libro dei debiti (T2) | DOC D4 | 2 |
| P15 | L4 | Bardi a pranzo | TES `IN2` | 2 |
| P16 | L5 | don Alceste in sacrestia | TES `IN3` | 3 |
| P17 | L5 | registro battesimi 1920 ff. 34–35 | DOC D3 | 3 |
| P18 | L5 | registro delle offerte | DOC D2 | 2 |
| P19 | L5 | stato delle anime 1921 | DOC D3 | 3 |
| P20 | L6 | Aldo al mulino | TES `IN3` | 3 |
| P21 | L6 | registro delle macinate | DOC D1 | 1 |
| P22 | L6 | libretto della roggia | DOC D1 | 1 |
| P23 | L7 | Assunta al casale | TES `IN2` | 2 |
| P24 | L7 | Bruno nei campi (`CR` 2 + `IN3` 3) | TES | 5 |
| P25 | L7 | libretto colonico | DOC D1 | 1 |
| P26 | L8 | perlustrazione della cava | OSS `PE` | 2 |

**26 prove ≥ 18** (NB-6 ✓). Somma dei costi d'azione (escluso P12, inaccessibile): **44 mezze**.

### 4.2 NB-7 — Raccolta esaustiva ≥ 1,8 × B

Soglia: ≥ 43,2 → **≥ 44 mezze**.

| Componente | Mezze |
|---|---|
| Somma dei costi d'azione delle 25 prove accessibili | **44** |
| Tour hamiltoniano minimo L1→L2→L3→L4→L5→L7→L8→L6→L1 (1+1+1+1+2+1+1+3) | **11** |
| **Totale raccolta esaustiva** | **55 = 2,29 × B** |

**PASS.** Passa anche nella lettura più restrittiva (sole azioni: 44 = 1,83 × B ✓). Margine sul minimo: +11 mezze / +25 %.

### 4.3 RD-7 — Ogni catena ≤ 0,70 × B (≤ 16 mezze)

Otto catene di riferimento, costo = azioni + cammino minimo da L1.

| Catena | Comma | Itinerario | Prove | Azioni | Sposta­menti | **Totale** | × B |
|---|---|---|---|---|---|---|---|
| K-I-a | I | L1→L2→L4 | P07 P08 P13 | 5 | 2 | **7** | 0,29 |
| K-I-b | I | L1→L5→L7 | P16 P23 | 5 | 3 | **8** | 0,33 |
| K-I-c | I | L1→L8→L7 | P26 P24 | 7 | 3 | **10** | 0,42 |
| K-II-a | II | L1→L3 | P01 P03 P10 P11 | 7 | 1 | **8** | 0,33 |
| K-II-b | II | L1→L4→L3 | P15 P14 P10 | 5 | 2 | **7** | 0,29 |
| K-II-c | II | L1→L5→L7 | P17 P18 P23 | 7 | 3 | **10** | 0,42 |
| K-III-a | III | L1→L2 | P02 P04 P06 P08 | 9 | 1 | **10** | 0,42 |
| K-III-b | III | L1→L6→L1 | P20 P21 P22 | 5 | 4 | **9** | 0,38 |

**PASS.** Massimo 10 mezze = 0,42 × B, contro un tetto di 0,70 × B. Margine 40 %.
Copertura RD-1: 3 catene per CM-I, 3 per CM-II, 2 per CM-III ✓ (CM-II richiede ≥ 3).

### 4.4 EQ-3 — Confutatore più economico ≤ 0,25 × B (≤ 6 mezze)

Costo minimo di accesso a **una** prova, per ogni luogo della mappa, partendo da L1:

| Luogo | Spostamento da L1 | Azione più economica disponibile | Totale | ≤ 6 ? |
|---|---|---|---|---|
| L1 | 0 | D1 registro di classe | **1** | ✓ |
| L2 | 1 | D1 registro della pesa | **2** | ✓ |
| L3 | 1 | `AS` Renzo | **2** | ✓ |
| L4 | 1 | `AS` Nerina | **2** | ✓ |
| L5 | 1 | `ES` sacrestia | **2** | ✓ |
| L6 | 1 | D1 macinate | **2** | ✓ |
| L7 | 3 | D1 libretto colonico | **4** | ✓ |
| L8 | 2 | `PE` perlustrare | **4** | ✓ |

**PASS su tutta la mappa.** Peggior caso 4 mezze = 0,17 × B. Nessuna posizione di Pietrafitta rende un confutatore irraggiungibile. Il risultato dipende dal fatto che **tutte le discese costano 1**: è la conseguenza voluta dell'asimmetria.

### 4.5 EQ-4 — `costo(F) + costo(X min) + costo(catena più economica) ≤ B`

| Termine | Peggior caso misurato | Fonte |
|---|---|---|
| `costo(F)` — raccogliere il depistaggio | 5 (azione `IN3` 3 + salita 2) | § 2 |
| `costo(X min)` — confutatore più economico | 4 | § 4.4 |
| `costo(K min)` — catena più economica del comma | 7 | § 4.3 |
| **Somma** | **16 = 0,67 × B** | |

**PASS**, margine 8 mezze.

**Ma il caso peggiore ammissibile dallo standard non passa.** Se il quest designer sfrutta il tetto RD-7 fino in fondo (catena da 16), si ottiene `5 + 4 + 16 = 25 > 24`: **FAIL**. La soglia RD-7 e la soglia EQ-4 non sono simultaneamente saturabili.

> **Prescrizione TC-3 (derivata, vincolante per `design-quest-designer`).**
> La **catena più economica di ciascun comma** deve costare **≤ 12 mezze (0,50 × B)**. Con `costo(F) + costo(X) ≤ 9` — soffitto verificato in § 4.4 e § 2 — si ottiene `≤ 21 ≤ B` con 3 mezze di margine. Il tetto RD-7 di 16 mezze resta valido per le catene **alternative**, non per la più economica.
> Soddisfacibile: le otto catene di riferimento costano 7–10 mezze.

### 4.6 RD-8 / V3 — Tre percorsi distinti che chiudono i tre comma in ≤ 24

Verificati **contro gli orari reali** della griglia § 3.2, giorno feriale, tempo asciutto.

#### Percorso α — di paese (martedì)

| Ora | Azione | Costo | Residuo |
|---|---|---|---|
| 06:00 | sopralluogo, rientro a L1 (SP-1) | 0 | 24 |
| 06:00–07:00 | L1 · P01 protocollo D2 | 2 | 22 |
| 07:00–08:00 | L1 · P03 registro condotta D2 | 2 | 20 |
| 08:00–08:30 | L1→L2 | 1 | 19 |
| 08:30–09:00 | L2 · P07 registro della pesa D1 | 1 | 18 |
| 09:00–10:30 | L2 · P08 Rovina in loggia `IN3` | 3 | 15 |
| 10:30–11:00 | L2→L3 | 1 | 14 |
| 11:00–11:30 | L3 · P10 Renzo `AS` (`+OC` non dovuto: 11:00 sotto le 12:30 con banco pieno → applicato) | 1 | 13 |
| 11:30–12:30 | L3 · P11 bollettario D4 (T2) | 2 | 11 |
| 12:30–13:00 | L3→L4 | 1 | 10 |
| 13:00–14:00 | L4 · P15 Bardi `IN2` | 2 | 8 |
| 14:00–14:30 | L4 · P13 Nerina `AS` | 1 | 7 |
| 14:30–15:00 | L4→L1 | 1 | 6 |
| 15:00–16:00 | L1 · P02 fogli di famiglia D2 | 2 | 4 |
| 16:00–16:30 | L1 · P04 registro di classe D1 | 1 | 3 |
| 16:30–17:30 | L1 · P05 fascicolo personale D2 | 2 | 1 |
| 17:30–18:00 | L1→L2 fermata, ultima stesura | 1 | **0** |

`M = 5 · A = 19 · 24/24 · 11 prove.` Finestre rispettate: Rovina in loggia 09:00–10:30 (3 mezze esatte), emporio chiuso alle 12:30, Bardi all'osteria 13:00–14:30, osteria chiusa alle 14:30.

#### Percorso β — versante alto (fatto in quota, il giocatore **resta sul posto**)

| Ora | Azione | Costo | Residuo |
|---|---|---|---|
| 06:00 | sopralluogo a L8, resta sul posto (SP-1) | 0 | 24 |
| 06:00–07:00 | L8 · P26 perlustrare la cava `PE` | 2 | 22 |
| 07:00–07:30 | L8→L7 | 1 | 21 |
| 07:30–09:00 | L7 · P24 Bruno al casale `IN3` (07:30–08:00 colazione + campi vicini) | 3 | 18 |
| 09:00–10:00 | L7 · P23 Assunta `IN2` | 2 | 16 |
| 10:00–10:30 | L7 · P25 libretto colonico D1 | 1 | 15 |
| 10:30–12:00 | L7 · P08′ Rovina in visita ai fondi `IN3` (lun/mer/ven) | 3 | 12 |
| 12:00–12:30 | L7→L5 | 1 | 11 |
| 12:30–13:30 | L5 · P18 registro delle offerte D2 | 2 | 9 |
| 13:30–14:00 | L5→L1 | 1 | 8 |
| 14:00–15:00 | L1 · P03 registro condotta D2 | 2 | 6 |
| 15:00–16:00 | L1 · P01 protocollo D2 | 2 | 4 |
| 16:00–16:30 | L1 · P04 registro di classe D1 | 1 | 3 |
| 16:30–17:00 | L1→L3 | 1 | 2 |
| 17:00–17:30 | L3 · P10 Renzo `AS` | 1 | 1 |
| 17:30–18:00 | L3→L2 fermata | 1 | **0** |

`M = 5 · A = 19 · 24/24 · 10 prove.` Il percorso dimostra il valore di SP-1: partendo dall'alto, ogni discesa costa 1 e gli spostamenti restano 5 nonostante due luoghi in quota.

#### Percorso γ — mulino (mercoledì)

| Ora | Azione | Costo | Residuo |
|---|---|---|---|
| 06:00 | sopralluogo, rientro a L1 | 0 | 24 |
| 06:00–06:30 | L1→L6 (discesa) | 1 | 23 |
| 06:30–08:00 | L6 · P20 Aldo `IN3` | 3 | 20 |
| 08:00–08:30 | L6 · P21 registro macinate D1 | 1 | 19 |
| 08:30–09:00 | L6 · P22 libretto della roggia D1 | 1 | 18 |
| 09:00–10:30 | L6→L1 (salita, +1 gradino) | 3 | 15 |
| 10:30–11:30 | L1 · P03 registro condotta D2 | 2 | 13 |
| 11:30–12:00 | L1 · P04 registro di classe D1 | 1 | 12 |
| 12:00–12:30 | L1→L4 | 1 | 11 |
| 12:30–13:30 | L4 · P14 libro dei debiti D4 (T2) | 2 | 9 |
| 13:30–14:30 | L4 · P15 Bardi `IN2` | 2 | 7 |
| 14:30–15:00 | L4→L3 (arrivo alla riapertura) | 1 | 6 |
| 15:00–15:30 | L3 · P10 Renzo `AS` | 1 | 5 |
| 15:30–16:30 | L3 · P11 bollettario D4 | 2 | 3 |
| 16:30–17:00 | L3→L2 | 1 | 2 |
| 17:00–17:30 | L2 · P07 registro della pesa D1 | 1 | 1 |
| 17:30–18:00 | ultima stesura alla fermata (1 mezza di riserva) | 1 | **0** |

`M = 7 · A = 16 · 24/24 · 10 prove.`

**Distinzione RD-8** (≥ 2 luoghi e ≥ 2 interlocutori di differenza):

| | Luoghi | Interlocutori |
|---|---|---|
| α | L1 L2 L3 L4 | Rovina · Renzo · Bardi · Nerina |
| β | L8 L7 L5 L1 L3 | Bruno · Assunta · Rovina · Renzo |
| γ | L6 L1 L4 L3 L2 | Aldo · Bardi · Renzo |

α vs β: 4 luoghi e 3 interlocutori di differenza ✓ · α vs γ: 3 e 3 ✓ · β vs γ: 4 e 3 ✓. **PASS.**

### 4.7 Il conto critico — dove il sistema è al limite

Sommo i requisiti minimi imposti da NB-11 e verifico contro `B`.

**Definizione operativa di `c(Ci)` che adotto** (chiarimento richiesto: § 8, D-4): `c(Ci)` = costo delle sole **azioni** della catena minima che determina `Ci`, **esclusi gli spostamenti**. Motivo: NB-11 misura la simmetria interna di un comma, non la logistica; gli spostamenti sono già misurati da RD-7 e RD-8. Con la lettura opposta il criterio conterebbe più volte lo stesso cammino e diventerebbe incalcolabile.

**Minimo teorico di un comma imposto da NB-11:**

| Vincolo | Effetto sui costi ordinati `c₁ ≤ c₂ ≤ c₃` |
|---|---|
| NB-11b — max 1 casella con `c ≤ 2` | `c₂ ≥ 3` e `c₃ ≥ 3` |
| NB-11c — `c₁ + c₂ ≥ 4` (vale per **tutti e tre** i comma: CM-I contiene C2 e C3, CM-II contiene C4, CM-III contiene C7) | `c₁ ≥ 1` |
| NB-11a — `c₃ ≤ c₁ + c₂` | `c₃ ≤ 4` |
| **Minimo per comma** | `1 + 3 + 3 =` **7 mezze di azione** |

**Il conto:**

```
Σ c_comma (minimo teorico)         =  7 + 7 + 7  = 21 mezze di azione
Σ c_comma (realistico, CM-II caro   =  7 + 10 + 7 = 24 mezze di azione
per NB-1 profondità ≥ 4 su C4)
M (spostamenti minimi)             =  5   percorso di centro
                                   =  5   una escursione partendo dall'alto
                                   =  7   una escursione dal paese
                                   = 10   due escursioni (quota + mulino)
```

Disuguaglianza da soddisfare:  `Σ c_comma − S + M ≤ 24`
dove `S` = mezze risparmiate perché un'azione alimenta caselle di **comma diversi**.

| Scenario | Σ c | M | S necessario | Esito |
|---|---|---|---|---|
| Minimo NB-11, centro | 21 | 5 | **≥ 2** | soddisfacibile facilmente |
| Minimo NB-11, una escursione dal paese | 21 | 7 | **≥ 4** | soddisfacibile |
| CM-II caro, una escursione dal paese | 24 | 7 | **≥ 7** | soddisfacibile solo con 3 azioni condivise |
| CM-II caro, **due escursioni** (quota + mulino) | 24 | 10 | **≥ 10** | **NON soddisfacibile** |

**Esito onesto: i vincoli sono simultaneamente soddisfacibili su B = 24 e sulla geografia reale, ma non per ogni caso conforme allo standard QA.** Il margine nel caso peggiore ammesso dallo standard è **negativo di 4–10 mezze**. Servono due prescrizioni che lo standard rev.2 non contiene. Non è una modifica a `B` né ai costi: è un vincolo di composizione del caso.

> **TC-1 — Condivisione inter-comma.** Nel percorso vincente più economico, almeno **2 azioni da ≥ 2 mezze** devono alimentare caselle di **comma diversi** (`S ≥ 4`). Non viola NB-5: NB-5 vieta che una prova *determini* più di una casella, non che *contribuisca* come premessa a passi di comma diversi. Il caso-modello lo soddisfa naturalmente: `P08` Rovina alimenta C1 (ora) e C7 (movente); `P23` Assunta alimenta C2 (luogo) e C8 (circostanza).
>
> **TC-2 — Escursione unica.** Deve esistere un percorso completo che chiude i tre comma **uscendo dal centro al massimo una volta**, verso `{L6}` **oppure** verso `{L7, L8}`, mai entrambi. Operativamente: ogni comma deve avere ≥ 1 catena che non richiede la seconda escursione. Garantisce `M ≤ 7`, e `M = 5` se il fatto è in quota e il giocatore resta sul posto (SP-1).
>
> **TC-3** — vedi § 4.5: catena più economica di ogni comma ≤ 12 mezze.

Con TC-1 + TC-2 + TC-3 la disuguaglianza chiude: `24 − 7 + 7 = 24 ≤ B` ✓, e i tre percorsi di § 4.6 sono la dimostrazione costruttiva che il limite è raggiungibile.

### 4.8 Vincolo 7 della vision — il sopralluogo dà candidati, mai determinazioni

Da dimostrare: alle 06:00, **a costo zero e nel tempo di una sola azione**, `C1` ORA e `C2` LUOGO devono avere ciascuna **≥ 3 valori candidati mutuamente incompatibili**.

**Capienza dell'azione.** Un sopralluogo è un'osservazione simultanea di una scena, non una sequenza. Occupa in finzione la fascia 05:30–06:00 (prima campana → messa prima). 8 voci di quaderno in 30 minuti reali = ~4 minuti a voce: realistico per un uomo che gira attorno a un fatto con un taccuino. **Specifica SP-2: il sopralluogo produce da 5 a 8 voci, nessuna delle quali dirimente.**

**≥ 3 candidati per `C1` ORA — meccanismo su Pietrafitta.** Il paese ha **un solo orologio pubblico**, il campanile, e *non si sente al Mulino né alla Cava* (`regions` § Le campane). Ne discende che ogni ancoraggio orario in quota o a valle è **indiretto**, e gli ancoraggi indiretti disponibili sono più d'uno e discordi:

| Voce di sopralluogo | Ora suggerita | Fonte del vincolo |
|---|---|---|
| «la cenere del focolare era ancora tiepida» | 04:00–06:00 | fisica del focolare |
| «il livello della roggia era già calato» | dopo l'apertura delle paratoie, 05:00 | `regions` L6: al Mulino l'ora si desume dalla roggia |
| «la brina sul sentiero alto era intatta a monte del cippo» | prima delle 05:30 sul tratto alto | esposizione del versante |
| «le bestie erano già governate» | dopo le 05:30 | `characters` Bruno 04:45–05:30 |

Quattro voci → almeno tre valori di ORA mutuamente incompatibili (l'ora del fatto è una sola). Nessuna coppia determina: la cenere e la roggia riguardano luoghi diversi; la brina e le bestie riguardano versanti diversi. **✓**

**≥ 3 candidati per `C2` LUOGO — meccanismo geografico.** Il principio è: **il luogo del ritrovamento ≠ il luogo del fatto**, e la geografia di Pietrafitta fornisce catene di trasporto naturali già stabilite dal world designer.

| Se il ritrovamento è a… | Candidati incompatibili generati | Vettore |
|---|---|---|
| L6 Mulino | **L6, L8, L7** | il torrente Fitta scende dal versante alto; la mulattiera del Fosso collega L8 a L6 in 28′ di discesa |
| L8 Cava | **L8, L7, L5** | il Campo del Fosso (beneficio parrocchiale) è a 20′ da L8, 12′ da L7, 18′ da L5 |
| L2 Piazza | **L2, L4, L3** | la fermata, l'osteria di fronte e l'emporio condividono trenta metri di dislivello e tutti i passanti delle 07:00–07:25 |

Voci di sopralluogo che li sostengono senza determinarne uno: «fango di quota sulle scarpe» (compatibile con L7 e L8 e col Campo del Fosso), «polvere di arenaria» (la cava **e** il monolite in piazza sono la stessa arenaria — `regions` § Toponimo), «una foglia di castagno» (il castagneto confina con L7 e L8). **Nessuna coppia determina, perché i tre luoghi alti condividono substrato, vegetazione e confini.** ✓

**Vincolo negativo, verificabile da QA:** nessuna voce di sopralluogo e nessuna coppia di voci può ridurre `C1` o `C2` a meno di 3 candidati. Se ciò accade, il caso ricade in AP-23 (`standard` § 6) ed è REJECT.

**Compatibilità con l'intento anti-frustrazione di G2:** il Comma I resta il più economico dei tre (§ 4.3: K-I-a costa 7 mezze, la catena più economica del caso-modello) e chiudibile entro mezzogiorno. G2 sopravvive nel suo scopo, non nella sua lettera. ✓

### 4.9 Vincolo 8 della vision — ≥ 2 fonti indipendenti per ogni casella critica

Da dimostrare **contro gli orari reali dei nove**, non in astratto. Conto, per ogni fascia, le fonti indipendenti disponibili: persone reperibili con testimonianza utilizzabile (`TES`), documenti che datano quella fascia (`DOC`), vincoli di percorrenza derivabili dalla matrice § 1.2 (`ORA`), tracce osservabili (`OSS`).

Le sei figure d'ambiente (Gemma Sordi, Vittoria Sanna, Rosa Fenaroli, Ada Bianconi, Egisto Pieri, Egidio Nardi) **non sono contate**: `characters` § Note 4 le dichiara non-prova.

| Fascia | `TES` reperibili e utilizzabili | `DOC` che datano | `ORA` | Fonti totali | ≥ 2 ? |
|---|---|---|---|---|---|
| 06:00–08:00 | Alceste, Assunta, Nerina, Renzo (dalle 07:00), Lidia, Aldo — **6** | bollettario biglietti (07:00–07:20) · elenco raccomandate · registro macinate (paratoie 05:00) | matrice: L6→L1 = 40′ | **10** | ✓ |
| 08:00–12:00 | Renzo (banco, alibi solidissimo), Lidia (25 bambini), Rovina (loggia, tutta la piazza), Nerina, Aldo, Assunta — **6** | registro di classe firmato · registro della pesa · registro condotta (lun/gio) · macinate | matrice: L6/L7 ↔ centro | **11** | ✓ |
| 12:00–14:00 | Nerina (sala piena), Bardi, Lidia, Assunta↔Bruno (reciproci) — **5** | libro dei debiti (consumazioni datate) | matrice | **7** | ✓ |
| **14:00–15:00** | Lidia (aula, presenza *probabile* non certa), Aldo (clienti radi), Assunta (sola) — **1 utilizzabile con certezza** | **nessuno** | matrice | **2, di cui 1 debole** | **⚠ critico** |
| 15:00–16:00 | Alceste (confessioni), Renzo (banco), Lidia (lun/gio) — **3** | quaderno del credito | matrice | **5** | ✓ |
| 16:00–18:00 | Renzo, Nerina, Rovina, Bardi (17:00+), Alceste (17:30+), Assunta, Bruno (stalla 16–17) — **7** | bollettario · sacco postale 17:30 | matrice | **10** | ✓ |

**Risultato.** Il vincolo 8 è soddisfatto su cinque fasce su sei con ampio margine. **La fascia 14:00–15:00 è l'unico collo di bottiglia sistemico della mappa**: `characters` § Mappa delle finestre cieche la dichiara cieca o quasi per sette dei nove, e nessun documento di Pietrafitta la data.

> **Prescrizione FT-3 (vincolante per `design-quest-designer`).**
> Se `C1` cade nella fascia **14:00–15:00**, il caso deve fornire **≥ 2 fonti non testimoniali** per ogni casella che dipenda da quell'ora: almeno una `OSS` materiale (traccia fisica, stato di un oggetto) e almeno una `ORA` da vincolo di percorrenza sulla matrice § 1.2. Un caso ambientato in quella fascia e sorretto da sole testimonianze viola il vincolo 8 della vision ed è **REJECT**.
> Il divieto non riguarda il *fatto*, riguarda la *casella*: un fatto alle 14:30 è legittimo e anzi desiderabile (`characters`: «un caso ambientato alle 14:30 apre tutto») purché l'ora sia provabile per via materiale.

**Verifica specifica del collo di bottiglia noto — la strada alta all'alba.** `regions` L7 dichiara Assunta «testimone unico di un intero versante» fra le 05:00 e le 07:00. Verifica delle fonti alternative per la classe di caselle «presenza sul versante alto 05:30–07:30»:

| # | Fonte | Tipo | Indipendente da Assunta? |
|---|---|---|---|
| 1 | Assunta Marucci | `TES` | — |
| 2 | Tracce alla Cava e sulla mulattiera (`PE`, 2 mezze): cenere, impronte nel fango, oggetti dimenticati | `OSS` | ✓ `regions` L8 le dichiara esplicitamente |
| 3 | Matrice di percorrenza: chi è al Mulino alle 07:00 non può essere a L7 prima delle 09:00 (L6→L7 = 4 mezze) | `ORA` | ✓ derivata dalla mappa, costo 0 (D0) |
| 4 | Registro delle macinate + registro della pesa: chi ha portato grano o pesato, e quando | `DOC` | ✓ |
| 5 | Registro parrocchiale delle presenze alla messa prima (le quattro anziane sono figure di sfondo, ma la **presenza di Assunta stessa** è confermata da don Alceste) | `TES`/`DOC` | ✓ verifica *su* Assunta, non *tramite* Assunta |

**4 fonti indipendenti da Assunta. ✓** Perdere Assunta (accusandola ingiustamente, o accusando Bruno) non chiude alcun comma, come richiesto dal vincolo 8. **PASS.**

### 4.10 Prospetto riassuntivo della verifica

| Soglia | Richiesto | Ottenuto | Esito |
|---|---|---|---|
| NB-6 volume probatorio | ≥ 18 prove | 26 | **PASS** |
| NB-7 raccolta esaustiva | ≥ 1,80 × B (43,2) | **55 = 2,29 × B** | **PASS** +25 % |
| RD-1 catene per comma | 2 / 3 / 2 | 3 / 3 / 2 | **PASS** |
| RD-7 catena singola | ≤ 0,70 × B (16,8) | max **10 = 0,42 × B** | **PASS** +40 % |
| RD-8 / V3 percorsi completi | ≥ 3 distinti, ≤ 24 | **24 / 24 / 24** | **PASS** con TC-1, TC-2 |
| EQ-3 confutatore più economico | ≤ 0,25 × B (6) | max **4 = 0,17 × B** su ogni luogo | **PASS** |
| EQ-4 F + X + catena minima | ≤ B (24) | **16** nel modello; **25** al limite RD-7 | **PASS** con TC-3 |
| Vision § 7 sopralluogo | ≥ 3 candidati incompatibili C1 e C2, costo 0 | 4 candidati ORA · 3 candidati LUOGO, dimostrati sulla geografia | **PASS** |
| Vision § 8 ≥ 2 fonti indipendenti | ogni casella critica | 5–11 per fascia; **4 alternative ad Assunta** sulla strada alta | **PASS** salvo fascia 14:00–15:00 → **TC/FT-3** |
| Bilancio complessivo | — | soddisfacibile, **margine 0–3 mezze nel caso peggiore ammesso** | **PASS condizionato** a TC-1, TC-2, TC-3, FT-3 |

**Non propongo di modificare `B`, né i costi, né le distanze.** Il sistema chiude a 24 mezze. Ciò che manca allo standard rev.2 sono quattro vincoli di **composizione del caso**, non di economia: TC-1, TC-2, TC-3, FT-3. Senza di essi esistono casi formalmente conformi allo standard e materialmente irrisolvibili su questa mappa — e il pubblico se ne accorgerebbe.

---

## 5. Fiducia e accesso

### 5.1 Principio operativo — il divieto assoluto

> **Nessun parametro di questo capitolo rende più facile *dedurre*. Rende raggiungibile una prova, e nient'altro.**

Regole che lo garantiscono, e che sono verificabili meccanicamente:

| # | Regola | Verifica |
|---|---|---|
| FT-0a | Il tier **non modifica mai** un costo in mezze | grep sulla tabella § 2: nessun costo dipende da T |
| FT-0b | Il tier **non modifica mai** il testo di una voce di quaderno | una voce sbloccata a T2 è formulata come fatto, identica a come sarebbe a T1 |
| FT-0c | Il tier **non produce mai** una conclusione, un suggerimento, un collegamento | A4, vincolo creativo 4 |
| **FT-4** | **Nessun tier consegna una casella.** Una prova sbloccata da un tier entra nel grafo come **foglia**, e deve trovarsi ad almeno **2 passi** da qualunque casella | grafo deduttivo, § 2.3 dello standard QA |

FT-4 è la difesa contro AP-08 (confessione risolutiva): se un tier alto facesse dire a qualcuno la risposta, la fiducia sarebbe potere.

### 5.2 I quattro tier

| Tier | Nome | Significato | Cosa apre |
|---|---|---|---|
| **T0** | Porta chiusa | risponde solo a domande neutre (`NB`) | nulla. Ogni tema è chiuso; l'azione produce comunque un fatto (A3) |
| **T1** | Conoscenza d'ufficio | *default* | i temi pubblici: cosa ha visto, dove era, chi è passato |
| **T2** | Fiducia | ti considera persona, non carica | i **documenti privati** (D4) e **la presenza fuori orario** |
| **T3** | Confidenza | rarissimo | un tema che il personaggio non affronterebbe con nessuno |

**La presenza fuori orario è la forma più pura di accesso**: a T2 la persona ti riceve in una mezza in cui la griglia § 3.2 la dà non reperibile. Non ti dice di più: ti dice *quando ti pare*. Estensioni consentite, per abitante, dichiarate:

| Abitante | Estensione concessa a T2 |
|---|---|
| Don Alceste | canonica 13:00–15:00 (riposo) |
| Rovina | studio 15:30–17:00 senza appuntamento; **mai** 13:30–15:30 né il giovedì 14:30–16:00 |
| Assunta | casale in qualunque mezza fra 08:00 e 19:00 |
| Bruno | ti dice **dove sarà**, annullando il costo `CR` (2 mezze) |
| Renzo | retro dell'emporio 12:30–15:00; **mai** 17:30–17:50 |
| Nerina | osteria chiusa 14:30–16:00; **mai** il giovedì |
| Lidia | aula 13:30–15:00; **mai** 16:00–18:00 |
| Bardi | casa 07:30–08:20 e 18:00–20:00 |
| Aldo | mulino in qualunque mezza; **mai** il giovedì prima delle 08:00 |

Le esclusioni non sono capricci: sono esattamente le finestre cieche in cui `characters` colloca i segreti. **Il tier non compra il segreto.**

### 5.3 Tabella dei tier per abitante

| Abitante | R | T iniziale (caso 1) | T1 apre | T2 apre | Tetto |
|---|---|---|---|---|---|
| Don Alceste | R3 | T1 | offerte, stato delle anime | registri parrocchiali 1817–1930 (D3); ciò che sa **fuori** dal confessionale | **T2** — il sigillo è chiusura assoluta |
| Cav. Rovina | R3 | T1 | libri degli affitti su richiesta formale | studio, cambiali del portafoglio | **T2** — mai il 1944 |
| Assunta | R2 | T1 | libretto colonico, conferimenti | il casale, la vicenda dei vaglia di Pietro | **T3** — l'analfabetismo detto da lei, e solo da lei |
| Bruno | R3 | **T0** | — | i suoi spostamenti reali nei campi | **T2** — mai la cava |
| Renzo | R1 | **T2** | quaderno del credito | bollettario dei biglietti | **T2** — le matrici dei vaglia sono chiusura assoluta |
| Nerina | R1 | T1 | bolle del vino e della farina | libro dei debiti | **T2** — mai il giovedì |
| Lidia | R2 | T1 | registro di classe | fascicolo personale, biglietti intestati | **T2** — mai le 16:00–18:00 |
| Bardi | R2 | T1 | (il registro della condotta è al Municipio: **accesso di diritto a T0**) | le lacune del registro spiegate una per una | **T2** — mai le cambiali |
| Aldo | R3 | T1 | macinate, libretto della roggia | le bolle che non tornano | **T2** — mai il mercoledì notte |

Sette abitanti su nove hanno **tetto T2**. È voluto: il segreto è la materia dei casi, e consegnarlo per fiducia sarebbe AP-08. T3 esiste per una sola persona perché una sola cosa in questo paese si dice per fiducia e non si prova con una carta.

**Stato iniziale:** Bruno parte a T0 («parla poco perché parlare non gli è mai servito»), Renzo a T2 («il personaggio più affabile del paese» — ed è la trappola: il più accessibile è il più inaffidabile), gli altri sette a T1.

### 5.4 Guadagno e perdita — quantificati

Scala numerica `T0 = 0 … T3 = 3`. Ogni Δ è **annunciato prima** quando è conseguenza di un'azione in-caso, e **mostrato nell'epilogo del mattino dopo** quando è conseguenza del verbale.

| Evento | Δ | Su chi | Quando |
|---|---|---|---|
| Verbale con **3 comma timbrati** | **+1** | parte lesa e congiunti | epilogo |
| Verbale con 3 comma timbrati | **−2** | congiunti del responsabile vero | epilogo |
| `C4` **errata su persona reale** | **→ T0, bloccato per il resto della slice** | l'accusato | epilogo |
| `C4` errata su persona reale | **−2** | congiunti dell'accusato | epilogo |
| `C4` errata su persona reale | **−1** | l'intero schieramento dell'accusato (`regions` § Schieramenti) | epilogo |
| `C4` = `IGNOTI` con parte lesa identificata | **−1** | parte lesa e congiunti | epilogo |
| Casella **in bianco** riempita d'ufficio contro Y (§ 6) | **−1** | Y e congiunti | epilogo |
| **Prova umiliante usata in pubblico** (scriptata dal quest designer) | **−2** | l'interessato | in-caso, immediato, annunciato |
| Prova umiliante usata in pubblico | **−1** | schieramento dell'interessato | in-caso |
| `LV` insistere con leva su tema chiuso | **−1** | l'interlocutore, max 1 volta per caso | in-caso, annunciato nella preview |
| Riservatezza mantenuta su richiesta esplicita (scriptata) | **+1** | l'interessato | epilogo |
| Atto di riparazione (scriptato, max 1 per caso) | **T0 → T1** | il riparato | epilogo |

**Propagazione ai congiunti** — la rete è quella di `characters` § Parentela, con una regola che la governa:

> **La propagazione richiede che il congiunto sappia di esserlo.**

| Legame | Propaga? |
|---|---|
| Renzo ⇄ Nerina (fratelli) | ✓ piena |
| Assunta ⇄ Bruno (madre-figlio) | ✓ piena |
| Rovina → Aldo (padre naturale) | **✗ — Aldo non sa.** Sospetta, e il sospetto non è parentela |
| Lidia | **✗ — nessun parente in paese.** «L'unica veramente sola, e questo la rende sacrificabile» |

Che accusare ingiustamente Lidia non costi nulla in propagazione è la cosa più crudele del sistema, ed è esatta: nel 1954 la forestiera sola è quella che si può bruciare senza che nessuno protesti. La conseguenza c'è, ma è solo sua.

### 5.5 Quanto costa davvero un verbale sbagliato — il conto

Somma iniziale dei tier = `7×T1 + T0(Bruno) + T2(Renzo)` = **9 punti su 27**.

| Esito del caso 1 | Δ totale | Somma dopo | Abitanti a T0 |
|---|---|---|---|
| 3 comma timbrati, responsabile vero senza congiunti | +1 | 10 | 1 |
| 3 comma timbrati, responsabile con un congiunto | +1 −2 | 8 | 1–2 |
| `C4` errata su Bruno | Bruno→T0 (già), Assunta −2 → T0, schieramento «terra che lavora» −1 | 6 | **2** — e **Assunta è persa**: il testimone della strada alta |
| `C4` errata su Renzo | Renzo→T0, Nerina −2 → T0 | 5 | **2** — e si perdono **entrambe** le fonti sulle partenze della corriera |
| `C4` = `IGNOTI` | −1 sulla parte lesa | 8 | 0–1 |
| Tre caselle in bianco su tre persone diverse | −3 | 6 | 0–3 |

Il caso peggiore documentato è l'accusa errata a Renzo: chiude in un colpo il bollettario dei biglietti **e** la memoria di Nerina sulle partenze — le due fonti che `characters` § Note 5 indica come «agganci al Pilastro 3 già predisposti».

> **E-1 — Tetto di erosione.** In nessun momento della slice più di **4 abitanti** possono trovarsi a T0. Se un esito porterebbe il quinto a T0, l'effetto si converte automaticamente in **−1 tier** (T1 → T0 diventa T2 → T1 dove applicabile, altrimenti l'abitante resta a T1). Il gioco non lo spiega; l'epilogo lo rende visibile come reticenza attenuata.
>
> Motivo: senza tetto, tre casi consecutivi mal chiusi renderebbero il terzo caso irrisolvibile, e la punizione smetterebbe di essere «accesso» per diventare «game over differito» — vietato dalla vision (G7).

> **FT-2 — Dorsale d'ufficio.** Ogni caso deve avere, **per ciascun comma**, almeno una catena interamente composta da prove disponibili con **tutti gli abitanti a T0**.
>
> Materiale sempre disponibile a T0, verificato su Pietrafitta:
>
> | Fonte | Luogo | Costo | Tipo |
> |---|---|---|---|
> | Protocollo comunale, fogli di famiglia, ruoli, licenze, nulla osta | L1 | 2 (D2) | `DOC` |
> | Registro della condotta medica, registro di classe, fascicoli | L1 | 1–2 | `DOC` |
> | Registro della pesa pubblica, bacheca | L2 | 0–1 | `DOC`/`REG` |
> | Registro delle macinate, libretto della roggia | L6 | 1 (D1) | `DOC` |
> | Libretto colonico | L7 | 1 (D1) | `DOC` |
> | Perlustrazione della cava e dei campi | L7, L8 | 2 (`PE`) | `OSS` |
> | Matrice delle percorrenze | ovunque | **0** (D0) | `ORA` |
>
> Costo di una dorsale completa per tre comma: ~15 mezze di azione + 4–6 di spostamento = **19–21 ≤ 24** ✓. La dorsale è percorribile, austera e sufficiente. È ciò che garantisce meccanicamente il vincolo 8 anche sotto erosione massima.

Il giocatore che ha bruciato mezzo paese ha ancora un lavoro da fare: leggere carte da solo, in un archivio, senza che nessuno gli parli. È esattamente il mestiere che il gioco descrive.

---

## 6. Completamento d'ufficio della Pretura — parametrizzazione

`core_loop` § 5.2C fissa la regola; qui la rendo **calcolabile**, così che il quest designer la applichi invece di inventarla caso per caso.

### 6.1 I due stati, distinti e non confondibili

| Stato della casella | La Pretura | Costo | Effetto sulla fiducia |
|---|---|---|---|
| **In bianco** | **completa d'ufficio** con `U-Ci`, deterministico | **nessun costo meccanico**; il danno è che il valore d'ufficio colpisce qualcuno | −1 al colpito e ai suoi congiunti (§ 5.4) |
| **`IGNOTI` / `NON ACCERTATO`** | **non completa.** Il fatto resta a carico di ignoti | **nessun costo in tempo, stesure o accesso generico** (EQ-10, AP-26) | −1 alla sola parte lesa e ai suoi congiunti, **porta nominata dal quest designer** |

L'ignoto non è mai punito meccanicamente. È l'unica onestà che il modulo consente, e costa solo agli occhi di chi si aspettava giustizia.

### 6.2 Indice di comodità sociale `S(v)` — la funzione che sceglie `U-Ci` sulle persone

`U-C4` (e ogni altra casella di tipo persona) = **il valore con `S` massimo fra quelli ancora vivi a metà tabella T2**, escluso il valore-soluzione.

| Modificatore | `S` |
|---|---|
| Forestiero (residente da < 5 anni, nato fuori comune) | **+3** |
| Già segnato in un verbale precedente della slice | **+3** |
| Senza congiunti in paese | **+2** |
| Povero o senza titolo giuridico su ciò che lavora | **+2** |
| Donna sola che esercita un'attività | **+1** |
| Titolare di contratto o di licenza | **−1** |
| Notabile o licenziatario di pubblico servizio | **−2** |
| Protetto dallo schieramento «la proprietà» (`regions` § Schieramenti) | **−3** |

**Calcolo per i nove** (caso 1, nessun precedente):

| Abitante | Composizione | `S` |
|---|---|---|
| **Lidia Sacchetti** | +3 forestiera, +2 senza congiunti | **5** |
| **Elio Bardi** | +3 forestiero, +2 senza congiunti in paese, −2 notabile | **3** |
| Bruno Marucci | +2 senza titolo | **2** |
| Assunta Marucci | +2 povera, −1 titolare del contratto | **1** |
| Aldo Fenaroli | +2 marginale, −1 licenza del molino | **1** |
| Nerina Vaccari | +1 donna sola con esercizio, −1 licenza | **0** |
| Renzo Bianconi | −2 licenziatario di pubblico servizio | **−2** |
| Don Alceste | −3 proprietà | **−3** |
| Cav. Rovina | −3 proprietà, −2 notabile | **−5** |

Ordine d'ufficio: **Sacchetti > Bardi > Bruno Marucci > Assunta Marucci = Fenaroli > Vaccari > Bianconi > Guidotti > Rovina.**
Pareggio (Assunta/Aldo): tie-break **alfabetico per cognome, poi per nome**. Deterministico, mai casuale.

Il termine `+3 già segnato` è l'aggancio al Pilastro 3: **un innocente accusato nel caso 1 diventa il default della Pretura nel caso 2.** Non serve altro per far pesare l'errore.

### 6.3 Regole d'ufficio per le caselle non-persona

| Casella | Regola d'ufficio `U-Ci` | Deterministica perché |
|---|---|---|
| `C1` ORA | la **prima mezza** della fascia in cui il maggior numero di abitanti dello schieramento «proprietà» e «commercio» ha alibi verificabile, fra i candidati ancora vivi | si conta sulla griglia § 3.2. In Pietrafitta è quasi sempre la fascia 09:00–12:00 |
| `C2` LUOGO | il luogo **senza carta e senza presenze regolari**: **L8 Cava vecchia** | `regions` L8: «l'unico luogo senza carta, il buco nero della verificabilità». La Pretura scrive sempre che è successo dove nessuno può smentire |
| `C3` ATTO | la voce della lista prestampata con la **qualificazione meno grave**, secondo l'ordine di gravità che il quest designer dichiara con la lista | la lista è chiusa e ordinata |
| `C5` PARTE LESA | il **titolare formale del bene o del fondo**, non chi lo lavora o lo detiene | catasto e contratti. Alla Cerreta la parte lesa d'ufficio è **Rovina**, mai i Marucci. Se coincide con la soluzione (EQ-7), si scende al secondo titolare formale |
| `C6` MEZZO | l'**attrezzo di uso comune del ceto più basso** fra i candidati vivi | inventario del caso, ordinato |
| `C7` MOVENTE | la **prima voce della lista prestampata compatibile con `U-C4`** nell'ordine di stampa, fra quelle che ne aggravano la posizione | ordine di stampa fisso |
| `C8` CIRCOSTANZA | la circostanza **che non richiede prova**: l'incustodito, l'aperto, il non sorvegliato | ordinamento dichiarato |
| `C9` FONTE | **«la pubblica voce»** | è l'unica fonte che non è né persona né documento e che non si può verificare. Sempre disponibile, mai corretta |

### 6.4 Vincoli sul completamento d'ufficio (già in `standard` § 5.4, qui resi calcolabili)

| # | Vincolo | Come si verifica con questa parametrizzazione |
|---|---|---|
| EQ-7 | `U-Ci ≠ soluzione(Ci)` su tutte e 9 | se la funzione `S` restituisce il colpevole, si scala al secondo `S` |
| EQ-8 | `U-Ci` deve essere ancora vivo a metà T2 | la funzione si applica **solo ai candidati vivi**: garantito per costruzione |
| EQ-9 | il giocatore deve poterlo prevedere prima delle 18 | la funzione è **diegeticamente esposta**: il segretario conosce la prassi della Pretura. `U-C2 = L8` è deducibile da una battuta d'ambiente; `U-C9 = «la pubblica voce»` compare in ogni verbale precedente del Registro degli Atti; l'ordine `S` è il senso comune del paese, dichiarato da un PNG nel caso 1. **Dipendenza verso `narr-narrative-designer`** (§ 8, D-5) |
| AP-24 | il valore d'ufficio non è mai la risposta giusta | EQ-7 |

---

## 7. Costi da annunciare — specifica per la UI

Preview obbligatoria prima di ogni conferma (A2, V6). Formato minimo:

```
CONSULTARE il registro delle macinate        1 mezza    →  08:30
INTERROGARE Aldo Fenaroli (riluttante)       3 mezze    →  09:30
SALIRE alla Cerreta                          3 mezze    →  11:00   ▲ in salita
SCENDERE al paese                            1 mezza    →  11:30   ▼ in discesa
INSISTERE con Nerina, leva: bolle della farina
                                             2 mezze    →  13:00
                                             ⚠ questo le costerà la fiducia
PRENDERE la corriera per Roccalta       tutta la giornata → 17:35
                                             ⚠ le carte arriveranno domani
```

Requisiti vincolanti per `viz-ui-ux-artist`:
1. Il costo e **l'ora di conclusione** sono sempre entrambi mostrati.
2. Salita e discesa hanno **marcatura visiva distinta** (▲/▼): l'asimmetria dev'essere leggibile senza aprire la tabella.
3. La matrice dei costi e la griglia di reperibilità sono consultabili **a costo zero, in qualunque momento**.
4. La preview di `LV` dichiara la perdita di fiducia **prima** della conferma.
5. La preview non dice mai cosa si otterrà: dice cosa si spende. Il costo è noto, la resa no.

---

## 8. Dipendenze da rimandare

| # | Verso | Cosa | Blocca |
|---|---|---|---|
| **D-1** | `design-world-designer` | **Ratifica** della scala di reticenza R1/R2/R3 (§ 2.2) e della quantizzazione delle presenze in mezze (§ 3.2). Entrambe derivate da `characters`, nessuna modifica a quel file. Se il world designer dissente su un'attribuzione R, cambiano i costi di § 2.2 e vanno rifatti i conti di § 4.6 | § 2.2, § 3.2, § 4.6 |
| **D-2** | `qa-lead` via `dir-lead-game-designer` | **Recepire nello standard rev.3** le quattro prescrizioni derivate in § 4: **TC-1** (condivisione inter-comma ≥ 2 azioni), **TC-2** (escursione unica, `M ≤ 7`), **TC-3** (catena più economica di ogni comma ≤ 12 mezze), **FT-3** (fascia 14:00–15:00 richiede ≥ 2 fonti non testimoniali). Senza di esse esistono casi conformi allo standard e materialmente irrisolvibili in 24 mezze: il conto è in § 4.7 | tutti i casi |
| **D-3** | `qa-lead` | § 11 dello standard dichiara che nessun caso può avere PASS pieno finché i costi non sono confermati. **Questo documento li conferma.** Le soglie NB-7, NB-11, RD-7, RD-8, EQ-3, EQ-4 sono ora calcolabili. Richiedo la rimozione dello stato `PASS condizionato ai costi` | passaggio dei casi in produzione |
| **D-4** | `qa-lead` | **Chiarimento formale di `c(Ci)` in NB-11**: adotto «costo delle sole azioni della catena minima, esclusi gli spostamenti» (§ 4.7). Con la lettura opposta NB-11 conta più volte lo stesso cammino e diventa incalcolabile. Serve ratifica | NB-11, D11–D13 della checklist |
| **D-5** | `narr-narrative-designer` | **Esposizione diegetica di EQ-9**: la prassi della Pretura (§ 6.2–6.3) deve essere conoscibile in-game prima delle 18. Servono: una battuta d'ambiente sul «si scrive sempre che è successo alla cava», la formula «la pubblica voce» nei verbali del Registro degli Atti, e un PNG che nel caso 1 enunci l'ordine di comodità sociale | EQ-9, F10 |
| **D-6** | `design-quest-designer` | Vincolo tecnico che discende da NB-11c: le caselle a dominio piccolo (`C2`, `C3`, `C4`, `C7`) non possono essere la casella più costosa del loro comma. Con la tabella § 2, ciò significa che **`C1`, `C5`, `C6`, `C8`, `C9` devono essere le caselle care** — cioè quelle che richiedono `IN3`, `D3` o una salita | NB-11c, D13 |
| **D-7** | `dir-game-director` | La regola D5 § 2.5 (esito differito al caso successivo) introduce una **progressione di accesso tra i casi non prevista dalla vision**: un caso sacrificato compra una prova per il successivo. È coerente col Pilastro 3 ma è una regola nuova (CLAUDE.md § Regole 7). Chiedo il via libera | § 2.5 |
