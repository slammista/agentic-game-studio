---
role: qa-lead
date: 2026-08-23
author: qa-lead
status: draft
revision: 2
locked_by: null
description: Standard formale di rigore deduttivo per i casi di Pietrafitta. Specifica vincolante per design-quest-designer e griglia di validazione per qa-lead. Rev.2 — allineato al modulo a 9 caselle / 3 comma disgiunti e alla regola delle 3 stesure. Nessun caso entra in produzione senza esito PASS su tutti i criteri bloccanti.
depends_on:
  - knowledge_base/production/creative_vision.md
  - knowledge_base/systems/core_loop_e_verbale.md
---

# Standard di Rigore — Casi Deduttivi di Pietrafitta

**Ambito.** Ogni caso della vertical slice e ogni caso futuro.
**Riferimenti vincolanti.** `creative_vision.md` § Vincoli 1–5, Pilastri 1–3, Rischi · `systems/core_loop_e_verbale.md` § 2 (modulo), § 3 (timbro e stesure), § 5 (esiti), § 6 (garanzie G1–G8), § 7 (V1–V6).
**Regola di esito.** Un solo NO su un criterio bloccante = **REJECT**. Nessuna approvazione condizionata.

> **Nota di revisione.** La rev.1 era tarata su un modulo a 7 caselle con finestra scorrevole. Il Director ha chiuso la forma su **9 caselle in 3 comma disgiunti, 3 stesure per comma**. La rev.2 rimappa la numerazione, sostituisce la soglia anti-bruteforce (che con gruppi disgiunti misurava la cosa sbagliata) e aggiunge quattro anti-pattern emersi dalla nuova struttura. Due punti richiedono ratifica del Director: § 10.

---

## 0. Notazione obbligatoria (prerequisito di verificabilità)

Un caso non è verificabile se non è indicizzato.

### 0.1 Caselle e comma

| Comma | ID | Casella | Tipo | Origine valori | Tetto strutturale del dominio |
|---|---|---|---|---|---|
| **CM-I** *Del fatto* | `C1` | ORA | ora | quaderno | 24 (mezze) |
| | `C2` | LUOGO | luogo | quaderno | **8** (luoghi del paese) |
| | `C3` | ATTO | qualificazione | **lista chiusa, 6 voci** | **6** |
| **CM-II** *Delle persone* | `C4` | **RESPONSABILE** | persona | quaderno | **9** utili (+`IGNOTI`, mai corretto) |
| | `C5` | PARTE LESA | persona/bene | quaderno | — |
| | `C6` | MEZZO | oggetto | quaderno | — |
| **CM-III** *Delle ragioni* | `C7` | **MOVENTE** | qualificazione | **lista chiusa, 8 voci** | **8** |
| | `C8` | CIRCOSTANZA | opportunità | quaderno | — |
| | `C9` | FONTE | persona/documento | quaderno | — |

`C4` è la casella-chiave del caso (era `C3` in rev.1: **ogni riferimento a "chi" va letto `C4`**).
Le quattro caselle in grassetto hanno un tetto strutturale sotto 12 e attivano la compensazione obbligatoria § 3.2.

### 0.2 Altri ID

| Entità | Formato | Esempio |
|---|---|---|
| Prova raccoglibile | `P-<caso>-<nn>` | `P-01-07` |
| Passo deduttivo | `D-<nn>` | `D-04` |
| Catena deduttiva | `K-<comma>-<lettera>` | `K-II-b` |
| Depistaggio | `F-<nn>` | `F-02` |
| Confutatore | `X-<nn><lettera>` | `X-02a` |
| Luogo | `L-<nn>` | `L-05` |
| Abitante | slug da `world/characters/` | `ottavio-bruni` |
| Valore d'ufficio della Pretura | `U-<casella>` | `U-C4` |

### 0.3 Grandezze

`B` = budget giornaliero = **24 mezze** (`core_loop` § 1.1). Le soglie restano espresse in frazioni di `B`; l'equivalente in mezze è indicativo sulla baseline `core_loop` § 1.2 e va riconfermato da `design-systems-designer`.

`d(Ci)` = **cardinalità di catalogo** della casella: numero di valori distinti di quel tipo che esistono nel caso e sono raccoglibili nel quaderno (per `C3` e `C7`: la lunghezza della lista prestampata). Non è il residuo dopo deduzione: è quanto il modulo accetterebbe da un giocatore che ha raccolto tutto.

`N(CM)` = `Π d(Ci)` sulle tre caselle del comma.

**Tassonomia chiusa dei tipi di prova:** `DOC` documento cartaceo · `TES` testimonianza · `OSS` osservazione diretta di luogo/oggetto · `ORA` vincolo di orario o percorrenza · `REG` fatto amministrativo noto al segretario a costo zero.
Prova non classificabile = REJECT finché non riclassificata.

---

## 1. Criterio di unicità della soluzione (bloccante)

> Rischio coperto: *"due soluzioni entrambe difendibili" — impatto Critico.* Copre `core_loop` V1 e V2.

### 1.1 Definizione

La soluzione è unica se e solo se esiste **una sola** assegnazione a `C1…C9` che non viola alcun vincolo derivabile dalle prove. Ogni altra deve essere **positivamente esclusa** da una prova nominata. Non basta che la soluzione prevista sia la migliore.

Poiché il timbro opera per comma, l'unicità va dimostrata **due volte**: dentro ogni comma (nessuna seconda terna timbrabile — `core_loop` V2) e sull'intero verbale (nessuna combinazione cross-comma alternativa).

### 1.2 Procedura in quattro passaggi

**Passo 1 — Domini dichiarati.** Per ogni casella si enumera `d(Ci)` con i valori effettivi. Vincoli:
- `d(Ci) ≥ 12` per `C1, C5, C6, C8, C9` (nessun tetto strutturale: il designer deve popolarli).
- `C3` = esattamente 6 voci, `C7` = esattamente 8 voci (fissate da `core_loop` § 2.2).
- `C4` include tutti i 9 abitanti + `IGNOTI`; `IGNOTI` non è mai la soluzione (`core_loop` § 2.4) e non conta in `d`.
- Si dichiarano `N(CM-I)`, `N(CM-II)`, `N(CM-III)` e il prodotto totale.

**Passo 2 — Eliminazione per vincolo.** Tabella riga per riga: ogni riga elimina candidati citando la prova. Vietate le motivazioni *"implausibile"*, *"non avrebbe senso"*, *"nessun movente"*. Solo vincoli fattuali. Esito: un insieme residuo per casella.

**Passo 3 — Enumerazione del residuo, per comma.** Tre tabelle separate, una per comma.
- `|R(CM)| ≤ 24` per ciascun comma. Sopra 24 l'eliminazione del Passo 2 è insufficiente: rimandato al designer.
- Enumerazione **completa**: ogni riga con esito `ESCLUSA da <ID prova>` oppure `SOLUZIONE`. Righe omesse = REJECT, non "ovvie".
- Esattamente **una** riga `SOLUZIONE` per comma.

**Passo 4 — Coerenza cross-comma.** Le tre terne-soluzione devono essere mutuamente compatibili, e nessuna combinazione che mescoli una terna corretta con una scartata deve risultare ammissibile. Si dichiarano esplicitamente i vincoli che legano i comma (es. `C4` × `C1`: il responsabile deve poter essere sul luogo a quell'ora).

### 1.3 Test del secondo classificato — per comma

Per **ciascuno dei tre comma**, l'ipotesi che differisce dalla terna corretta per **una sola casella** deve essere esclusa da **≥ 2 prove distinte**, di cui **≥ 1 di tipo `DOC` o `ORA`**.
Motivo: con gruppi disgiunti il timbro conferma una micro-teoria intera. Se la terna rivale cade per una sola testimonianza, il giocatore che non si fida di quel testimone resta legittimamente in dubbio — e brucia una stesura su tre per scoprirlo.

### 1.4 Formato di consegna

`knowledge_base/quests/<caso-slug>/prova_unicita.md`, frontmatter standard, **cinque sezioni** in quest'ordine:

```markdown
## T1 — Domini dichiarati
| Casella | Comma | Etichetta | Valori (enumerati) | d(Ci) |
N(CM-I) = …  N(CM-II) = …  N(CM-III) = …

## T2 — Eliminazione per vincolo
| # | Casella/e | Candidati eliminati | Prova (ID) | Tipo | Vincolo applicato (una riga) |
Residui: C1={…} … |R(CM-I)| = …  |R(CM-II)| = …  |R(CM-III)| = …

## T3 — Enumerazione del residuo (tre tabelle complete)
### T3-I  | # | C1 | C2 | C3 | Esito | Prova che esclude |
### T3-II | # | C4 | C5 | C6 | Esito | Prova che esclude |
### T3-III| # | C7 | C8 | C9 | Esito | Prova che esclude |

## T4 — Coerenza cross-comma
Vincoli inter-comma dichiarati + prova che nessuna combinazione mista è ammissibile.

## T5 — Near-miss (uno per comma)
Comma <n> | terna rivale | casella che differisce | esclusa da <ID, tipo> + <ID, tipo>
```

Sezione mancante = **REJECT procedurale**, senza esame di merito.

---

## 2. Criterio di deducibilità (bloccante)

### 2.1 Forma canonica del passo

```
D-04 | premesse: [P-01-03, P-01-11, D-02] | regola: R2 | conclusione: C6 ≠ "roncola"
```

Premesse non citate per ID o conclusione in prosa: non è un passo, è un'asserzione. REJECT.

### 2.2 Catalogo chiuso delle regole di inferenza

| ID | Regola | Forma |
|---|---|---|
| R1 | Incompatibilità temporale | X era in A all'ora T ⇒ X non ha compiuto Y altrove alla stessa ora |
| R2 | Incompatibilità spaziale | La tratta A→B costa ≥ Δ mezze ⇒ X non può essere in entrambi entro Δ |
| R3 | Esclusione per enumerazione chiusa | Solo l'insieme N può fare Y; N−1 elementi esclusi ⇒ resta l'ultimo |
| R4 | Contraddizione arbitrata | Due testimonianze incompatibili + un terzo elemento indipendente che decide quale cade |
| R5 | Vincolo documentale | Documento datato/firmato/registrato incompatibile con l'ipotesi |
| R6 | Accesso o capacità | Solo chi ha chiave/permesso/competenza/forza poteva compiere Y |
| R7 | Tracciamento dell'oggetto | Provenienza, possesso o spostamento vincolano chi l'ha usato |
| R8 | Vincolo economico o amministrativo | Debito, ricevuta, catasto, atto rendono l'ipotesi materialmente impossibile |

**Il movente non è una regola di inferenza.** Non esiste una "R-movente". Vedi § 2.6 e AP-07.
Regola nuova = si chiede a `dir-game-director` (CLAUDE.md § Regole 7) e si aggiorna questo standard. Mai dentro un caso.

### 2.3 Grafo di dipendenza

Allegato `grafo_deduttivo.md`: DAG con foglie `P-*`, nodi interni `D-*`, terminali `C1…C9`.

- **G-1 Nessun orfano.** Ogni `D-*` ha ≥ 1 arco entrante; ogni `C*` è raggiunto da ≥ 1 catena.
- **G-2 Nessun ciclo.** Un `D` che dipende transitivamente da sé stesso significa che il caso presuppone la propria soluzione: AP-03 travestito.
- **G-3 Chiusura.** Ogni foglia è una prova raccoglibile, con luogo e costo-tempo dichiarati. Nessuna foglia "conoscenza generale".
- **G-4 Lessico proibito.** Grep sui passi: `ovviamente`, `chiaramente`, `è evidente`, `l'unico che poteva`, `non può che essere`, `il tipico`, `sembra`, `probabilmente`, `intuisce`. Zero occorrenze. Ammesse solo nei **dialoghi** dei PNG, mai nel grafo né nelle voci di quaderno.
- **G-5 Conformità al quaderno.** Ogni foglia che alimenta una casella di tipo quaderno deve corrispondere a una **voce di quaderno formulata come fatto** (`core_loop` § 4.1). Una foglia formulata come conclusione viola A4 e il vincolo creativo 4: REJECT.

### 2.4 Test del passo cieco

Si consegnano a un lettore **solo** le premesse citate, senza il resto del caso né la soluzione. Se non raggiunge la conclusione, il passo ha una premessa implicita da esplicitare.
Campione obbligatorio: **tutti** i passi che alimentano `C4`, `C3` e `C7`, più il 30% casuale dei restanti.

### 2.5 Test di sostituzione (discriminanza)

Per ogni passo che conclude su una persona: si sostituisce il nome con quello di ciascuno degli altri 8 abitanti. Il passo deve **cadere** in tutti e 8 i casi. Se regge anche per uno solo, non discrimina e non conta come deduzione verso `C4`.

### 2.6 Requisito rinforzato per le caselle a lista chiusa (`C3` ATTO, `C7` MOVENTE)

Queste due caselle non si trascinano dal quaderno: si scelgono da un elenco prestampato. Non esiste quindi il **vincolo di provenienza** (`core_loop` § 2.2, difesa strutturale n.2) a proteggerle, e i domini sono i più piccoli del modulo. Requisiti aggiuntivi, tutti bloccanti:

- **LC-1 — Esclusione documentata dell'intera lista.** Il dossier nomina, per **ciascuna** delle altre voci della lista, la prova che la esclude: **5 esclusioni** per `C3`, **7 esclusioni** per `C7`. Voce senza esclusione nominata = REJECT.
- **LC-2 — Nessuna autopotatura.** Al massimo **2** voci di `C3` e **3** di `C7` possono essere escluse da prove a costo ≤ 2 mezze. Se la lista si sfoltisce da sola con l'informazione gratuita, resta un testa-o-croce. Vedi AP-25.
- **LC-3 — Premesse dure per `C7`.** Il passo terminale su `C7` usa **R5 o R8** e ha **≥ 3 premesse**, di cui **≥ 2 di tipo `DOC` o `REG`**. Un movente sostenuto solo da `TES` è pettegolezzo, non prova.
- **LC-4 — Premesse dure per `C3`.** Il passo terminale su `C3` ha **≥ 2 premesse**, di cui **≥ 1 di tipo `OSS`** raccolta fuori dal sopralluogo gratuito delle 06:00.
- **LC-5 — Nessuna caratterizzazione.** Nessuna premessa verso `C7` può essere un tratto di personalità, una reputazione o un giudizio morale. Solo carte, cifre, date, atti.

---

## 3. Criterio di non-banalità e anti-bruteforce (bloccante)

### 3.1 Soglie di profondità e volume

| # | Soglia | Valore | Verifica |
|---|---|---|---|
| NB-1 | Profondità verso `C4` (responsabile) | **≥ 4 passi in sequenza** | Cammino più lungo `P → C4`. Passi paralleli non contano come profondità |
| NB-2 | Profondità verso ogni altra casella | **≥ 2 passi**; al massimo **1 casella** dell'intero caso a profondità 1 | DAG |
| NB-3 | Concorrenza su `C4` | **≥ 3 prove distinte**, di **≥ 2 tipi** | Foglie a monte di `C4` |
| NB-4 | Nessuna prova schiacciante | Nessuna prova singola riduce da sola lo spazio residuo del caso di **> 60%** | Si ricalcola T2 con quella sola riga |
| NB-5 | Nessuna prova monopolista | Nessuna prova singola determina **> 1** casella | T2, colonna Casella/e |
| NB-6 | Volume probatorio | **≥ 18 prove raccoglibili** | Conteggio `P-*`. Alzato da 14 (rev.1): 9 caselle, non 7 |
| NB-7 | Scarsità reale (Pilastro 2) | Raccolta esaustiva **≥ 1,8 × B** (≥ 44 mezze) | Somma dei costi dichiarati |
| NB-8 | Densità deduttiva | **≥ 16 passi `D-*`**, di cui **≥ 9** con più di una premessa | Conteggio sul grafo |

### 3.2 Soglie anti-bruteforce — ricalcolate sui comma disgiunti

La rev.1 fissava "≥ 100 combinazioni per gruppo timbrabile". Con gruppi disgiunti e 3 stesure quella soglia è **inerte e mal posta**, per due ragioni:

*(a) È sotto la baseline.* La stima conservativa di `core_loop` § 3.5 è 192 / 210 / 336. Una soglia a 100 non boccerebbe mai nulla di ciò che il game designer già considera prudente: un criterio che non può fallire non è un criterio.

*(b) Misura l'attaccante sbagliato.* `core_loop` § 3.5 modella un attaccante che non sa nulla e tira la terna intera. Quell'attaccante non esiste. L'attaccante reale è il giocatore che ha **dedotto due caselle su tre** e tira la terza: con gruppi disgiunti, 3 stesure e `d(C3) = 6`, la probabilità di timbrare è **3/6 = 50 %**. Il timbro ottenuto per fortuna, per giunta, **retro-conferma le altre due caselle**, restituendo i 7–8 bit che il canale doveva negare. Questo è l'anti-pattern AP-23.

Le soglie sostitutive sono tre, e la vincolante è NB-10.

| # | Soglia | Valore | Verifica |
|---|---|---|---|
| **NB-9** | **Cardinalità di comma** | `N(CM) ≥ 180` per ciascuno dei tre comma | T1 |
| **NB-10** | **Tiro sulla casella residua** | `3 / d(Ci) ≤ 0,25` ⇒ **`d(Ci) ≥ 12`** per `C1, C5, C6, C8, C9` | T1 |
| **NB-11** | **Simmetria del comma** | Vedi § 3.3 — obbligatoria per `C2, C3, C4, C7` (tetto strutturale < 12) | Costi dichiarati |

**Motivazione di NB-9 = 180.** Con 3 stesure la probabilità di timbrare un comma a caso è esattamente `3/N`.

| `N(CM)` | P(comma a caso) | P(≥1 comma su un caso) | P(≥1 comma sui 3 casi) |
|---|---|---|---|
| 100 (soglia rev.1) | 3,00 % | 8,73 % | **24,0 %** |
| **180 (soglia rev.2)** | **1,67 %** | **4,92 %** | **14,0 %** |
| 192 / 210 / 336 (baseline `core_loop`) | 1,56 / 1,43 / 0,89 % | 3,84 % | 11,1 % |
| 528 (se si volesse ≤ 5 % sullo slice) | 0,57 % | 1,70 % | 5,0 % |

A 100, un giocatore su quattro incassa un timbro immeritato nell'arco della slice: inaccettabile per il pubblico di riferimento. A 528 la soglia sarebbe formalmente elegante ma imporrebbe di gonfiare i domini con distrattori inerti — cioè di produrre AP-20 (punizione dell'esplorazione) per difendersi da un attaccante che non esiste. **180 è il valore che rende il criterio mordente restando sotto la baseline del game designer**: un caso costruito più stretto della sua stima prudente viene fermato, un caso conforme passa senza distorsioni. La difesa vera non è qui: è in NB-10 e NB-11.

**Nota di calibrazione.** Confrontando NB-10 con la tabella "spazio pieno" di `core_loop` § 3.5, l'unica casella non conforme è **`C6` MEZZO (10 < 12)**. Il quest designer deve portarla a ≥ 12 oggetti plausibili per caso. Tutte le altre caselle senza tetto sono già conformi (`C1` 24, `C5` 13, `C8` 12, `C9` 14).

### 3.3 NB-11 — Simmetria del comma (il criterio che sostituisce davvero la vecchia NB-9)

Per ogni comma si dichiarano i **costi minimi di determinazione certa** delle tre caselle, ordinati `c₁ ≤ c₂ ≤ c₃` (in mezze). Devono valere tutte e tre le condizioni:

- **NB-11a** — `c₃ ≤ c₁ + c₂`. Se la casella più difficile costa più delle altre due insieme, il giocatore razionale smette di dedurla e la tira con 3 stesure.
- **NB-11b** — al massimo **1 casella per comma** con `c ≤ 2 mezze` (≈ 0,083 × B, "quasi gratuita").
- **NB-11c** — se il comma contiene una casella con `d(Ci) < 12` (cioè `C2`, `C3`, `C4`, `C7`), allora `c₁ + c₂ ≥ 4 mezze` **e** quella casella non può essere quella a costo `c₃`. Le caselle a dominio piccolo non sono mai l'ultima incognita di un comma.

Conseguenza operativa per il **Comma I**: `C3` ATTO (d = 6) non può essere l'ultima casella da chiudere, e `C1`/`C2` non possono essere entrambe quasi gratuite. Questo confligge con la garanzia G2 di `core_loop` § 6 nella sua lettera: vedi § 10.1.

---

## 4. Criterio di ridondanza dei percorsi (bloccante)

> Vision, mitigazione rischio: *"Ogni caso ha almeno tre catene deduttive indipendenti; fallire una non chiude le altre."*

### 4.1 Due assi da non confondere

`core_loop` G3 dice: *tre catene mappate 1:1 sui tre comma, perdere un testimone chiude al massimo un comma*. È **decomposizione**, non ridondanza: se ogni comma ha una sola catena, ogni comma ha un collo di bottiglia, e "chiude al massimo un comma" significa comunque un comma perso senza colpa del giocatore. La vision chiede l'altro asse.

**Si richiedono entrambi.**

| Asse | Requisito |
|---|---|
| **Decomposizione** (G3) | I tre comma sono chiudibili in modo indipendente l'uno dall'altro |
| **Ridondanza** (vision) | Ogni comma è chiudibile per più catene alternative |

### 4.2 Soglie

- **RD-1** — Catene indipendenti per comma: **≥ 2** per CM-I e CM-III, **≥ 3** per **CM-II** (contiene `C4`).
- **RD-2** — Disgiunzione probatoria: per ogni coppia di catene dello stesso comma, `|prove(Ki) ∩ prove(Kj)| ≤ 1`. Nessuna prova compare in tutte le catene di un comma, salvo il fatto iniziale delle 06:00.
- **RD-3** — Disgiunzione delle fonti: le catene di uno stesso comma non dipendono tutte dallo stesso abitante né dallo stesso luogo. Almeno 2 partono da luogo e interlocutore diversi.
- **RD-4** — Diversità di regola: le catene di uno stesso comma usano **≥ 2 regole terminali distinte** fra R1–R8. Tre alibi orari (tre R1) sono una catena sola travestita da tre.
- **RD-5** — **Indipendenza inter-comma.** Nessun comma richiede che un altro comma sia stato *timbrato*. Se CM-III dipende deduttivamente da CM-II, la dipendenza va dichiarata e CM-III deve avere **≥ 1 catena che non passa da CM-II**. Altrimenti un comma esaurito ne trascina un altro e il test RD-6 fallisce a cascata.
- **RD-6** — **Test di rimozione.** Si rimuove dal caso, una alla volta: ogni singola prova `P-*`; ogni singolo luogo `L-*` con tutte le sue prove; ogni singolo abitante con tutte le sue testimonianze. Dopo ogni rimozione **tutti e tre i comma restano chiudibili**. Non "al massimo uno si chiude": **zero**. Un solo fallimento = AP-06, REJECT.
- **RD-7** — Percorribilità individuale: ogni catena, presa da sola, costa **≤ 0,70 × B** (≤ 16 mezze). Una catena che satura la giornata non è un'alternativa, è la strada obbligata con due decorazioni accanto.
- **RD-8** — **Chiusura entro il budget.** Esiste ≥ 1 percorso che chiude tutti e tre i comma in ≤ 24 mezze, e ne esistono **≥ 3 distinti** (`core_loop` V3). I tre percorsi differiscono per ≥ 2 luoghi e ≥ 2 interlocutori.

### 4.3 Consegna

`percorsi.md`: una riga per catena (`ID | comma | prove | passi | luoghi | interlocutori | regola terminale | costo in mezze e in frazione di B`), la matrice di intersezione per comma, la tabella completa del test di rimozione RD-6, e i 3 percorsi integrali di RD-8 con il totale in mezze.

---

## 5. Criterio di equità dei depistaggi (bloccante)

### 5.1 Quantità

**2 ≤ depistaggi ≤ 3 per caso, al massimo 1 per comma.**
Il tetto per comma discende dalle stesure: un giocatore ingannato una volta consuma una stesura e ne conserva 2. Due depistaggi sullo stesso comma gliene lascerebbero 1 — un errore onesto punito come un tiro a caso. Il tetto complessivo scende da 4 (rev.1) a 3 perché i comma sono tre.

### 5.2 Scheda obbligatoria di ogni `F-nn`

| Campo | Obbligo |
|---|---|
| Comma bersaglio | Uno solo |
| Ipotesi falsa indotta | Formulata come **terna** di caselle, non come "sospetto" |
| Prova generatrice | ID |
| Ragione difendibile in-fiction | Vincolo creativo 2: nessuno mente per depistare il giocatore |
| Confutatori `X-nn` | **≥ 2**, distinti, con ID, tipo, luogo, costo |

### 5.3 I test di equità

- **EQ-1 — Esistenza.** Ogni `F` ha ≥ 2 confutatori raccoglibili. Con uno solo, chi quel giorno è andato altrove resta ingannato senza colpa.
- **EQ-2 — Indipendenza dal senno di poi.** `prerequisiti(X) ∩ ({F} ∪ prove_esclusive_soluzione) = ∅`. Un confutatore che si sblocca solo dopo aver già sospettato il colpevole vero è ornamentale.
- **EQ-3 — Costo di uscita.** Il confutatore più economico costa **≤ 0,25 × B** (≤ 6 mezze).
- **EQ-4 — Reversibilità in tempo.** `costo(F) + costo(X più economico) + costo(catena più economica del comma) ≤ B`.
- **EQ-5 — Reversibilità in stesure.** Un giocatore che imbocca e poi confuta ogni depistaggio del caso deve poter chiudere ogni comma con **≥ 1 stesura residua**. Discende da § 5.1 ed è ricontrollato qui a valle dei costi.
- **EQ-6 — Crepa obbligatoria.** Ogni personaggio che mente ha `bugie.md`: `bugia | ragione | crepa (ID prova) | luogo | costo`. Bugia senza crepa nominata = REJECT.

### 5.4 Il completamento d'ufficio è un depistaggio strutturale

`core_loop` § 5.2C: la casella lasciata **in bianco** viene riempita d'ufficio dalla Pretura col valore socialmente più comodo — il forestiero, il pregiudicato, il povero — in modo **deterministico e definito per caso dal quest designer**. È a tutti gli effetti una spinta verso una risposta sbagliata, e va sottoposta ai test di equità.

- **EQ-7 — Il valore d'ufficio non è mai la soluzione.** Per tutte e 9 le caselle: `U-Ci ≠ soluzione(Ci)`. Se coincidesse, non fare nulla pagherebbe. Vedi AP-24. Controllo su nove caselle, nessuna esclusa.
- **EQ-8 — Il valore d'ufficio deve mordere.** `U-Ci` non può essere un valore già escluso dalle prove gratuite delle 06:00: dev'essere un candidato ancora vivo a metà tabella T2. Un default palesemente assurdo rende il bianco indolore e svuota la gerarchia degli esiti di `core_loop` § 5.2.
- **EQ-9 — Il valore d'ufficio è prevedibile.** Il giocatore deve poter sapere **prima delle 18** cosa scriverà la Pretura. Il dossier nomina la fonte in-game da cui lo si deduce (una battuta, un precedente nel Registro degli Atti, una prassi citata). Un default non conoscibile è un costo nascosto e viola A2.
- **EQ-10 — `IGNOTI` non è mai corretto e non è mai punito meccanicamente.** Il costo di dichiarare ignoto è sociale e narrativo (perdita di accesso mirata, `core_loop` § 5.2C). Il dossier nomina **quale porta si chiude** per ogni casella dichiarata ignota. Nessun costo in tempo, stesure o timbri. Vedi AP-26.

---

## 6. Catalogo degli anti-pattern — rifiuto automatico

| ID | Anti-pattern | Perché è fatale |
|---|---|---|
| AP-01 | Colpevole identificabile solo da un dettaglio fisico arbitrario (il mancino, la cicatrice) | Sostituisce la catena logica con una lotteria percettiva: si "vede" o non si vede, non si deduce |
| AP-02 | "Chi mente è colpevole" | Riduce il caso a un test di sincerità e contraddice il vincolo che ogni bugia abbia una ragione propria |
| AP-03 | La prova decisiva compare solo dopo aver già capito | Inverte la causalità: premia l'indovinare e poi conferma, mai il dedurre |
| AP-04 | Soluzione per convenzione di genere (il maggiordomo, il meno sospetto) | Si vince conoscendo i gialli, non il caso: metagioco, e chi ne legge molti si annoia in dieci minuti |
| AP-05 | Due colpevoli entrambi difendibili | Rompe irreparabilmente la fiducia: se una volta il gioco è ambiguo, ogni deduzione dopo è scommessa |
| AP-06 | Collo di bottiglia: una prova senza la quale un comma è inchiudibile | Con 24 mezze equivale a un fallimento casuale deciso a metà mattina |
| AP-07 | Salto di movente: da "aveva un motivo" a "è stato lui" | Con nove abitanti i moventi si sovrappongono per progetto: il movente conferma, non individua |
| AP-08 | Confessione risolutiva: un PNG che, interrogato bene, dice la risposta | Sostituisce la deduzione con la ricerca del ramo di dialogo giusto |
| AP-09 | Anacronismo probatorio: impronte, balistica, autopsia rapida, telefonata di verifica | Rompe il vincolo 3 e insegna che le regole del mondo sono negoziabili |
| AP-10 | Conoscenza extradiegetica richiesta (orari reali, dialetto non glossato, nozioni agrarie) | Il giocatore perde per ignoranza di qualcosa che il gioco non gli ha dato |
| AP-11 | Casella con dominio minuscolo dove non è strutturalmente necessario | Con 3 stesure il timbro si compra tirando: distrugge la difesa n.3 di `core_loop` § 3.4 |
| AP-12 | Il quaderno registra conclusioni ("sembrava nervoso") invece di fatti | Il gioco pensa al posto del giocatore: viola A4 e il vincolo creativo 4 |
| AP-13 | Coincidenza risolutiva: due eventi indipendenti che si allineano per far quadrare tutto | Il giocatore esperto la legge come l'autore che bara, non come il mondo che funziona |
| AP-14 | Depistaggio non confutabile, scartabile solo perché "non era quello" | Trasforma l'errore in arbitrio: dallo sbaglio non si impara nulla |
| AP-15 | Retro-deduzione: le caselle si riempiono solo dopo aver capito tutto il caso | I tre comma diventano tre muri binari invece che tre atti mentali autosufficienti |
| AP-16 | Testimone onnisciente che ha visto tutto e va solo trovato | Il caso degrada da deduzione a caccia al tesoro; il tempo resta l'unico ostacolo |
| AP-17 | Ridondanza finta: più "catene" che condividono la prova decisiva | Sembra robusto e ha un unico punto di rottura — è AP-06 sotto tre nomi |
| AP-18 | Esclusione totale non raccoglibile ("gli altri otto hanno un alibi") oltre le 24 mezze | Soluzione formalmente valida e praticamente irraggiungibile |
| AP-19 | Il numero magico: ore, somme o distanze che tornano solo assumendo una precisione impossibile nel 1954 | Il rigore crolla appena il giocatore chiede "come faccio a saperlo al minuto?" |
| AP-20 | Punizione dell'esplorazione: prova che confonde senza avere confutazione | Insegna a non guardare, cioè l'opposto di ciò che il gioco chiede |
| AP-21 | Casella che non è un fatto (`C7` risolvibile interpretando l'animo di qualcuno) | Rende il verbale un tema di italiano invece di un documento verificabile |
| AP-22 | Dipendenza dall'ordine di raccolta: la stessa prova produce inferenze diverse secondo quando la trovi | Il caso non è un sistema di vincoli ma una sceneggiatura: la deduzione non è riproducibile |
| **AP-23** | **Il comma a due terzi**: due caselle quasi gratuite + una a dominio piccolo | Con 3 stesure la terza si tira a sorte (fino al 50 % su `C3`), e il timbro ottenuto per fortuna **retro-conferma** le altre due: il canale muto del feedback torna a parlare |
| **AP-24** | **Il valore d'ufficio corretto**: la Pretura riempie il bianco con la risposta giusta | Non fare nulla paga più che indagare: distrugge la gerarchia degli esiti e l'intero impianto del Pilastro 3 |
| **AP-25** | **La lista chiusa autopotante**: i distrattori di `C3`/`C7` sono eliminabili gratis | La lista si riduce da sé a due voci e la qualificazione giuridica diventa testa-o-croce |
| **AP-26** | **L'ignoto punito meccanicamente**: dichiarare `NON ACCERTATO` costa tempo, stesure o accesso generico | Il giocatore mente per convenienza invece di essere onesto, e il verbale smette di essere un atto di coscienza |

---

## 7. Checklist di accettazione operativa

**Un solo NO = REJECT.** Nessun campo vuoto, nessun "parziale".

**Caso:** ________ **Revisione:** ____ **Data:** ____ **Validatore:** qa-lead

### A. Consegna (procedurale — se fallisce, l'esame si ferma)
| # | Controllo | SÌ/NO |
|---|---|---|
| A1 | `prova_unicita.md` con T1–T5 complete | |
| A2 | `grafo_deduttivo.md`, tutti i passi in forma canonica | |
| A3 | `percorsi.md` con matrici, test di rimozione RD-6, 3 percorsi RD-8 | |
| A4 | `bugie.md` per ogni personaggio che mente | |
| A5 | Liste chiuse `C3` (6 voci) e `C7` (8 voci) allegate | |
| A6 | Valori d'ufficio `U-C1…U-C9` dichiarati (`core_loop` V5) | |
| A7 | ID conformi § 0; ogni prova classificata; luogo e costo in mezze dichiarati | |

### B. Unicità
| # | Controllo | SÌ/NO |
|---|---|---|
| B1 | `d ≥ 12` per `C1,C5,C6,C8,C9`; `C3`=6, `C7`=8; `C4` = 9 + `IGNOTI` | |
| B2 | `|R(CM)| ≤ 24` per ogni comma; enumerazione T3 completa | |
| B3 | Esattamente una riga `SOLUZIONE` per comma; nessuna seconda terna timbrabile (V2) | |
| B4 | Ogni esclusione cita una prova; zero motivazioni di plausibilità | |
| B5 | T4 coerenza cross-comma: nessuna combinazione mista ammissibile | |
| B6 | T5: tre near-miss, ciascuno escluso da ≥ 2 prove di cui ≥ 1 `DOC`/`ORA` | |

### C. Deducibilità
| # | Controllo | SÌ/NO |
|---|---|---|
| C1 | Ogni passo dichiara premesse per ID e una regola R1–R8 | |
| C2 | DAG: nessun orfano, nessun ciclo, nessuna foglia extradiegetica (G-1/2/3) | |
| C3 | Lessico proibito: zero occorrenze nel grafo e nelle voci di quaderno (G-4) | |
| C4 | Ogni foglia da quaderno è formulata come fatto, mai come conclusione (G-5) | |
| C5 | Passo cieco superato su tutti i passi verso `C4`,`C3`,`C7` + 30% campione | |
| C6 | Sostituzione: ogni passo su persona cade per tutti gli altri 8 abitanti | |
| C7 | LC-1: 5 esclusioni documentate per `C3`, 7 per `C7` | |
| C8 | LC-2: ≤ 2 voci `C3` e ≤ 3 voci `C7` escludibili a costo ≤ 2 mezze | |
| C9 | LC-3/4/5: premesse dure su `C7` e `C3`; nessuna caratterizzazione | |

### D. Non-banalità e anti-bruteforce
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| D1 | Profondità verso `C4` | ≥ 4 | |
| D2 | Profondità altre caselle (max 1 eccezione a profondità 1) | ≥ 2 | |
| D3 | Prove concorrenti su `C4` / tipi diversi | ≥ 3 / ≥ 2 | |
| D4 | Riduzione massima da una singola prova | ≤ 60 % | |
| D5 | Caselle determinate da una singola prova | ≤ 1 | |
| D6 | Prove raccoglibili | ≥ 18 | |
| D7 | Raccolta esaustiva | ≥ 1,8 × B (≥ 44 mezze) | |
| D8 | Passi `D-*` / con ≥ 2 premesse | ≥ 16 / ≥ 9 | |
| D9 | `N(CM)` per ciascuno dei 3 comma | ≥ 180 | |
| D10 | `d(Ci)` per `C1,C5,C6,C8,C9` | ≥ 12 | |
| D11 | NB-11a: `c₃ ≤ c₁ + c₂` in ogni comma | — | |
| D12 | NB-11b: caselle quasi gratuite (`c ≤ 2 mezze`) per comma | ≤ 1 | |
| D13 | NB-11c: `C2,C3,C4,C7` mai la casella `c₃`; `c₁+c₂ ≥ 4` nel loro comma | — | |

### E. Ridondanza
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| E1 | Catene per CM-I / CM-II / CM-III | ≥ 2 / ≥ 3 / ≥ 2 | |
| E2 | Intersezione per coppia di catene dello stesso comma | ≤ 1 prova | |
| E3 | Nessuna prova comune a tutte le catene di un comma (salvo fatto iniziale) | — | |
| E4 | ≥ 2 catene per comma con luogo e interlocutore d'ingresso diversi | — | |
| E5 | Regole terminali distinte per comma | ≥ 2 | |
| E6 | Nessun comma richiede un altro comma timbrato; CM-III ha ≥ 1 catena che salta CM-II | — | |
| E7 | Test di rimozione RD-6: dopo ogni rimozione **tutti e tre** i comma chiudibili | 0 fallimenti | |
| E8 | Costo di ogni singola catena | ≤ 16 mezze | |
| E9 | Percorsi completi entro budget, distinti per ≥ 2 luoghi e ≥ 2 interlocutori | ≥ 3, ≤ 24 mezze | |

### F. Equità
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| F1 | Depistaggi nel caso / per comma | 2–3 / ≤ 1 | |
| F2 | Confutatori per depistaggio | ≥ 2 | |
| F3 | EQ-2: nessun confutatore presuppone `F` o prove esclusive della soluzione | — | |
| F4 | Confutatore più economico | ≤ 6 mezze | |
| F5 | EQ-4: `F` + `X` + catena più economica | ≤ 24 mezze | |
| F6 | EQ-5: chiusura di ogni comma con ≥ 1 stesura residua dopo tutti i depistaggi | — | |
| F7 | EQ-6: ogni bugia ha ragione difendibile e crepa con ID | — | |
| F8 | EQ-7: `U-Ci ≠ soluzione(Ci)` su tutte e 9 le caselle | — | |
| F9 | EQ-8: nessun `U-Ci` già escluso dalle prove gratuite delle 06:00 | — | |
| F10 | EQ-9: fonte in-game da cui il giocatore deduce ogni `U-Ci` | — | |
| F11 | EQ-10: costo dell'ignoto solo sociale; porta chiusa nominata per casella | — | |

### G. Anti-pattern
| # | Controllo | SÌ/NO |
|---|---|---|
| G1 | Passata completa AP-01…AP-26: nessuno presente | |
| G2 | Se presente, indicare ID e passo/prova coinvolti nelle Note | |

### Esito
```
VERDETTO: PASS | REJECT
NO rilevati: <elenco ID controllo>
Anti-pattern rilevati: <elenco AP>
Azione richiesta al quest designer: <max 5 righe>
```

---

## 8. Copertura dei requisiti V1–V6 di `core_loop` § 7

| Requisito game designer | Copertura in questo standard |
|---|---|
| V1 Unicità per casella | § 1.2 Passi 1–3 · B1–B4 |
| V2 Nessuna terna alternativa timbrabile | § 1.2 Passo 3 · B3 · T4 |
| V3 Risolvibilità entro 24 mezze, ≥ 3 percorsi | RD-8 · E9 |
| V4 Nessuna inferenza automatica | G-5 · C4 (verifica sul contenuto; la conformità della UI resta a `qa-ux-researcher`) |
| V5 Copertura d'ufficio | A6 · EQ-7/8/9 · F8–F10 |
| V6 Annuncio del costo | Fuori dal perimetro di questo standard: verifica UI, `qa-ux-researcher` |

---

## 9. Procedura di validazione

Ordine fisso, interruzione al primo blocco: **A** → **B** → **C** → **D**/**E**/**F** (calcolabili in parallelo) → **G** (eseguita per intero anche a caso già respinto, così il designer riceve la lista completa).

Un caso respinto rientra con **revisione incrementata** e la checklist precedente allegata. QA riesegue l'intera griglia: una correzione locale può rompere `|R(CM)|`, NB-9, NB-11 o il test di rimozione.

---

## 10. Conflitti aperti — richiedono ratifica di `dir-game-director`

Non posso modificare `knowledge_base/systems/`. Segnalo due tensioni fra questo standard e `core_loop_e_verbale.md`, entrambe emerse dall'allineamento.

### 10.1 G2 (sopralluogo gratuito) contro NB-11 e AP-23

`core_loop` G2: *«il sopralluogo gratuito delle 06:00 fornisce da solo ≥ 2 delle 3 voci del Comma I»*.
Se `C1` e `C2` sono **determinate** dal sopralluogo, il Comma I si riduce a `C3` con `d = 6` e 3 stesure: **50 % di timbro a testa o croce**, e il timbro retro-conferma ora e luogo. È AP-23 prodotto dalla garanzia stessa.

**Lettura proposta, compatibile con l'intento anti-frustrazione di G2 e adottata da questo standard come NB-12:** il sopralluogo fornisce **voci di quaderno**, non **determinazioni**. Al termine delle 06:00, `C1` e `C2` devono avere **≥ 3 valori candidati mutuamente incompatibili** ciascuna. Il giocatore ha materiale su cui lavorare entro mezzogiorno (intento di G2 preservato), ma la chiusura del comma resta a pagamento e `C3` non è mai l'unica incognita residua.

Se il Director preferisce la lettera di G2, allora va rivista la difesa n.3: 3 stesure su un dominio da 6 non tengono.

### 10.2 G3 (una catena per comma) contro la mitigazione di rischio della vision

`core_loop` G3: *«perdere un testimone chiude al massimo un comma»*. La vision chiede che *«fallire una catena non chiuda le altre»*. Una catena per comma significa un collo di bottiglia per comma: il giocatore che non incrocia quel testimone perde un terzo del verbale senza aver sbagliato nulla.
Questo standard richiede il livello più severo (RD-1, RD-6): **perdere un testimone non chiude alcun comma.** G3 va letta come pavimento minimo, non come specifica.

---

## 11. Dipendenze ancora aperte

- **Costi-tempo.** Le soglie in frazione di `B` usano la baseline `core_loop` § 1.2, dichiarata provvisoria. Finché `design-systems-designer` non la conferma, nessun caso può ricevere PASS pieno: al massimo **`PASS condizionato ai costi`**, stato `review`. Riguarda NB-7, NB-11, RD-7, RD-8, EQ-3, EQ-4.
- **Distanze e orari.** NB-11 e RD-6/RD-8 non sono calcolabili finché `design-world-designer` non consegna la matrice delle distanze in mezze e gli orari dei 9 abitanti per fascia di mezz'ora.
- **Risolto in rev.2:** la casella `IGNOTI` esiste, non è mai timbrabile, la Pretura non la completa d'ufficio. Recepito in B1, EQ-10, AP-26. Il completamento d'ufficio del bianco è recepito in EQ-7/8/9 e AP-24.
