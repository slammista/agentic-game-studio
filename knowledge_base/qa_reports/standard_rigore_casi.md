---
role: qa-lead
date: 2026-08-24
author: qa-lead
status: review
revision: 3
locked_by: null
description: Standard formale di rigore deduttivo per i casi di Pietrafitta. Specifica vincolante per design-quest-designer e griglia di validazione per qa-lead. Rev.3 — baseline dei costi confermata da design-systems-designer (B=24 verificato sulla geografia reale); recepite le prescrizioni di composizione TC-1, TC-2, TC-3, FT-3 e i requisiti FT-2/FT-4; ratificata la definizione di c(Ci) sulle sole azioni; conflitti con core_loop chiusi dalle ratifiche del Director. Lo stato "PASS condizionato ai costi" è abolito: i casi ricevono PASS pieno o REJECT.
depends_on:
  - knowledge_base/production/creative_vision.md
  - knowledge_base/systems/core_loop_e_verbale.md
  - knowledge_base/systems/economia_tempo_e_fiducia.md
---

# Standard di Rigore — Casi Deduttivi di Pietrafitta

**Ambito.** Ogni caso della vertical slice e ogni caso futuro.
**Riferimenti vincolanti.** `creative_vision.md` § Vincoli 1–8, Pilastri 1–3, Rischi, Ratifiche del Director 2026-08-23 · `systems/core_loop_e_verbale.md` § 2 (modulo), § 3 (timbro e stesure), § 5 (esiti), § 7 (V1–V6) · `systems/economia_tempo_e_fiducia.md` § 1.2 (matrice), § 2 (costi d'azione), § 3.2 (griglia di reperibilità), § 4 (verifica di soddisfacibilità), § 5.5 (dorsale d'ufficio), § 6 (completamento d'ufficio).
**Regola di esito.** Un solo NO su un criterio bloccante = **REJECT**. Nessuna approvazione condizionata, in nessuna forma.

> **Nota di revisione — rev.3.**
> Tre cose cambiano rispetto alla rev.2.
> **(a)** I due conflitti con `core_loop_e_verbale.md` segnalati in § 10 sono stati **decisi dal Director a favore del QA** e promossi a vincoli 7 e 8 della vision. § 10 non li elenca più come aperti: li registra come chiusi e ne recepisce la forma definitiva.
> **(b)** `design-systems-designer` ha verificato numericamente tutte le soglie di bilanciamento su `B = 24` e sulla geografia reale di Pietrafitta. Esito: PASS su ogni soglia singola. **La baseline dei costi non è più provvisoria**, e con essa cade lo stato `PASS condizionato ai costi` (§ 9, § 11).
> **(c)** La stessa verifica ha isolato uno scenario reale — un comma costoso più due escursioni fuori dal centro — in cui vincoli tutti individualmente soddisfatti sforano insieme il budget. Le quattro prescrizioni di composizione che lo escludono (**TC-1, TC-2, TC-3, FT-3**) sono recepite qui come criteri bloccanti, dentro le sezioni di competenza. Con esse sono recepiti **FT-2** e **FT-4**, che `economia` § 5.5 e § 5.1 indirizzano esplicitamente a questo documento.
> Aggiunte proprie della rev.3, non derivate da altri agenti e segnalate come tali nel testo: **NB-11d**, **LC-0**, **LC-6**, **EQ-11**, **BD-1**, **AP-27**, **AP-28**.

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

### 0.3 Grandezze, e che cosa conta un costo

`B` = budget giornaliero = **24 mezze**. **Baseline confermata** da `economia_tempo_e_fiducia.md` § 1.2 e § 2: matrice degli spostamenti asimmetrica (salita cara, discesa 1), tabella chiusa dei costi d'azione, sopralluogo delle 06:00 a costo zero in andata e ritorno (SP-1). Le soglie restano espresse in frazioni di `B` e il loro equivalente in mezze è ora **esatto, non indicativo**.

**Nessun caso dichiara costi propri.** Ogni costo in mezze citato in un dossier deve derivare dalle tabelle di `economia` § 1.2 (spostamenti), § 2.1–2.5 (azioni, carte, trasferta) e § 3.2 (reperibilità). Un costo inventato dal caso è REJECT procedurale (A8).

`d(Ci)` = **cardinalità di catalogo** della casella: numero di valori distinti di quel tipo che esistono nel caso e sono raccoglibili nel quaderno (per `C3` e `C7`: la lunghezza della lista prestampata). Non è il residuo dopo deduzione: è quanto il modulo accetterebbe da un giocatore che ha raccolto tutto.

`N(CM)` = `Π d(Ci)` sulle tre caselle del comma.

`c(Ci)` = **costo delle sole azioni** della catena minima che determina con certezza `Ci`, **esclusi gli spostamenti**.

> **Ratifica della definizione di `c(Ci)`** (richiesta come D-4 da `economia` § 4.7 e § 8). **Accolta, senza divergenze.**
> In rev.2 NB-11 diceva «costi minimi di determinazione certa delle tre caselle» senza dichiarare se il cammino vi rientrasse: era un'ambiguità mia, e il systems designer ha ragione a chiedere che sia sciolta prima di usarla. La sciolgo nel suo senso per tre ragioni, in ordine di peso.
> 1. **NB-11 misura la simmetria interna di un comma, non la logistica.** Un comma è squilibrato quando una delle sue tre incognite costa in *lavoro* più delle altre due insieme, al punto che il giocatore razionale smette di dedurla e la tira con una stesura. È una proprietà della struttura probatoria, non del percorso.
> 2. **Con gli spostamenti inclusi il criterio non è ben definito.** Un cammino è condiviso fra più caselle e fra più comma: attribuirlo a ciascuna casella lo conterebbe due o tre volte, e `c₁ ≤ c₂ ≤ c₃` dipenderebbe dall'ordine in cui il giocatore visita i luoghi — cioè da una variabile che il dossier non fissa. Un criterio il cui valore dipende da chi lo calcola non è un criterio.
> 3. **La logistica non resta scoperta.** In rev.2 l'avrei detto con imbarazzo; in rev.3 no, perché la geografia è ora misurata *altrove e meglio*: da **RD-7** e **RD-7b** (costo di catena, spostamenti inclusi), da **RD-8** (percorsi interi), da **RD-10** (`M ≤ 7`) e da **BD-1** (la disuguaglianza di chiusura). L'esclusione dello spostamento da `c(Ci)` non apre un buco: sposta la misura dove è calcolabile.
> Resta una sola scappatoia, che chiudo con **NB-11d** (§ 3.3): rendere difficile un comma spostandone il peso dalle azioni alla salita. NB-11d non tocca alcun numero di `economia` § 4 — è un controllo aggiuntivo su casi futuri, non una ritaratura.

**Che cosa conta ciascuna soglia** — tabella normativa, dirime ogni ambiguità residua:

| Soglia | Azioni | Spostamenti | Nota |
|---|---|---|---|
| NB-7 raccolta esaustiva | ✓ | ✓ (tour minimo su tutti i luoghi con prove) | deve passare **anche** sulle sole azioni |
| NB-11a/b/c, `c(Ci)` | ✓ | ✗ | ratificato qui sopra |
| NB-11d | ✓ | ✓ (solo la salita, solo se isolata) | correttivo, § 3.3 |
| LC-2 «prova a costo ≤ 2 mezze» | ✓ | ✗ | lettura stretta: più prove risultano "gratuite", il criterio morde di più |
| RD-7 · RD-7b | ✓ | ✓ (cammino minimo da `L1`, o dal luogo del sopralluogo se il giocatore vi resta) | |
| RD-8 percorsi completi | ✓ | ✓ | percorso reale, orari di `economia` § 3.2 rispettati |
| RD-10 `M` | — | ✓ | conta i soli spostamenti |
| EQ-3 · EQ-4 | ✓ | ✓ (da `L1`) | |
| BD-1 | ✓ | ✓ | `Σc − S + M` |

**Tassonomia chiusa dei tipi di prova:** `DOC` documento cartaceo · `TES` testimonianza · `OSS` osservazione diretta di luogo/oggetto · `ORA` vincolo di orario o percorrenza · `REG` fatto amministrativo noto al segretario a costo zero (= classe documentale `D0` di `economia` § 2.4).
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
- `C3` = esattamente 6 voci, `C7` = esattamente 8 voci (fissate da `core_loop` § 2.2). Vedi **LC-0** per la stabilità delle due liste.
- `C4` include tutti i 9 abitanti + `IGNOTI`; `IGNOTI` non è mai la soluzione (`core_loop` § 2.4) e non conta in `d`.
- Si dichiarano `N(CM-I)`, `N(CM-II)`, `N(CM-III)` e il prodotto totale.

**Passo 2 — Eliminazione per vincolo.** Tabella riga per riga: ogni riga elimina candidati citando la prova. Vietate le motivazioni *"implausibile"*, *"non avrebbe senso"*, *"nessun movente"*. Solo vincoli fattuali. Esito: un insieme residuo per casella.

**Passo 3 — Enumerazione del residuo, per comma.** Tre tabelle separate, una per comma.
- `|R(CM)| ≤ 24` per ciascun comma. Sopra 24 l'eliminazione del Passo 2 è insufficiente: rimandato al designer.
- Enumerazione **completa**: ogni riga con esito `ESCLUSA da <ID prova>` oppure `SOLUZIONE`. Righe omesse = REJECT, non "ovvie".
- Esattamente **una** riga `SOLUZIONE` per comma.

**Passo 4 — Coerenza cross-comma.** Le tre terne-soluzione devono essere mutuamente compatibili, e nessuna combinazione che mescoli una terna corretta con una scartata deve risultare ammissibile. Si dichiarano esplicitamente i vincoli che legano i comma (es. `C4` × `C1`: il responsabile deve poter essere sul luogo a quell'ora, verificato sulla matrice di `economia` § 1.2).

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

**R2 si calcola sulla matrice asimmetrica** di `economia` § 1.2: la tratta `A→B` e la tratta `B→A` hanno costi diversi, e un passo R2 che usa il costo della discesa per escludere una salita è un errore di merito, non di forma. Con pioggia dichiarata, `L6⇄L7` e `L6⇄L8` non sono percorribili e R2 va ricalcolata sul giro dal paese.

**Il movente non è una regola di inferenza.** Non esiste una "R-movente". Vedi § 2.6 e AP-07.
Regola nuova = si chiede a `dir-game-director` (CLAUDE.md § Regole 7) e si aggiorna questo standard. Mai dentro un caso.

### 2.3 Grafo di dipendenza

Allegato `grafo_deduttivo.md`: DAG con foglie `P-*`, nodi interni `D-*`, terminali `C1…C9`.

- **G-1 Nessun orfano.** Ogni `D-*` ha ≥ 1 arco entrante; ogni `C*` è raggiunto da ≥ 1 catena.
- **G-2 Nessun ciclo.** Un `D` che dipende transitivamente da sé stesso significa che il caso presuppone la propria soluzione: AP-03 travestito.
- **G-3 Chiusura.** Ogni foglia è una prova raccoglibile, con luogo e costo-tempo dichiarati secondo `economia` § 2. Nessuna foglia "conoscenza generale".
- **G-4 Lessico proibito.** Grep sui passi: `ovviamente`, `chiaramente`, `è evidente`, `l'unico che poteva`, `non può che essere`, `il tipico`, `sembra`, `probabilmente`, `intuisce`. Zero occorrenze. Ammesse solo nei **dialoghi** dei PNG, mai nel grafo né nelle voci di quaderno.
- **G-5 Conformità al quaderno.** Ogni foglia che alimenta una casella di tipo quaderno deve corrispondere a una **voce di quaderno formulata come fatto** (`core_loop` § 4.1). Una foglia formulata come conclusione viola A4 e il vincolo creativo 4: REJECT.
- **G-6 Nessuna casella consegnata dalla fiducia** *(recepisce FT-4, `economia` § 5.1, indirizzata a questa sezione)*. Una prova sbloccata da un tier di fiducia entra nel grafo **come foglia** e deve trovarsi ad **almeno 2 passi** da qualunque casella. Un tier che avvicina la risposta è potere, non accesso: viola il "mini-RPG" della vision ed è AP-08. La verifica è meccanica: per ogni foglia marcata `T2`/`T3`, distanza minima verso ogni `C*` ≥ 2.

### 2.4 Test del passo cieco

Si consegnano a un lettore **solo** le premesse citate, senza il resto del caso né la soluzione. Se non raggiunge la conclusione, il passo ha una premessa implicita da esplicitare.
Campione obbligatorio: **tutti** i passi che alimentano `C4`, `C3` e `C7`, più il 30% casuale dei restanti.

### 2.5 Test di sostituzione (discriminanza)

Per ogni passo che conclude su una persona: si sostituisce il nome con quello di ciascuno degli altri 8 abitanti. Il passo deve **cadere** in tutti e 8 i casi. Se regge anche per uno solo, non discrimina e non conta come deduzione verso `C4`.

### 2.6 Requisito rinforzato per le caselle a lista chiusa (`C3` ATTO, `C7` MOVENTE)

Queste due caselle non si trascinano dal quaderno: si scelgono da un elenco prestampato. Non esiste quindi il **vincolo di provenienza** (`core_loop` § 2.2, difesa strutturale n.2) a proteggerle, e i domini sono i più piccoli del modulo. Requisiti aggiuntivi, tutti bloccanti:

- **LC-0 — Stabilità delle liste** *(nuovo in rev.3)*. La lista `C7` MOVENTE è **una sola per l'intera slice**, con ordine di stampa fisso: `economia` § 6.3 definisce `U-C7` come «la prima voce della lista prestampata compatibile con `U-C4` **nell'ordine di stampa**», e un ordine che cambia da un caso all'altro rende `U-C7` non prevedibile, violando EQ-9. Conseguenza operativa: **le 8 voci di `C7` vanno redatte una volta sola, prima del caso 1, e non cambiano.** La lista `C3` ATTO è invece per caso (`core_loop` § 2.2: «6 voci/caso») e va consegnata **con il proprio ordine di gravità dichiarato**, perché `U-C3` è definito come la qualificazione meno grave. Lista senza ordine dichiarato = REJECT procedurale (A5).
- **LC-1 — Esclusione documentata dell'intera lista.** Il dossier nomina, per **ciascuna** delle altre voci della lista, la prova che la esclude: **5 esclusioni** per `C3`, **7 esclusioni** per `C7`. Voce senza esclusione nominata = REJECT.
- **LC-2 — Nessuna autopotatura.** Al massimo **2** voci di `C3` e **3** di `C7` possono essere escluse da prove a costo ≤ 2 mezze (costo di sola azione, § 0.3). Se la lista si sfoltisce da sola con l'informazione gratuita, resta un testa-o-croce. Vedi AP-25.
- **LC-3 — Premesse dure per `C7`.** Il passo terminale su `C7` usa **R5 o R8** e ha **≥ 3 premesse**, di cui **≥ 2 di tipo `DOC` o `REG`**. Un movente sostenuto solo da `TES` è pettegolezzo, non prova.
- **LC-4 — Premesse dure per `C3`.** Il passo terminale su `C3` ha **≥ 2 premesse**, di cui **≥ 1 di tipo `OSS`** raccolta fuori dal sopralluogo gratuito delle 06:00.
- **LC-5 — Nessuna caratterizzazione.** Nessuna premessa verso `C7` può essere un tratto di personalità, una reputazione o un giudizio morale. Solo carte, cifre, date, atti.
- **LC-6 — Il movente non è gratuito** *(nuovo in rev.3)*. Nel passo terminale su `C7` o su `C3` è ammessa **al massimo una** premessa di tipo `REG` (classe `D0`, costo 0). Motivo: `economia` § 2.4 dà costo zero a un'intera classe documentale — orario della corriera, bacheca, confini catastali notori, titolarità delle licenze, matrice delle percorrenze. Senza LC-6, LC-3 sarebbe soddisfacibile con due `REG` a costo 0 più una testimonianza da 1 mezza: un movente formalmente "duro" e materialmente regalato, cioè AP-25 spostato dalla potatura della lista alla determinazione terminale. Con LC-6, `c(C7)` e `c(C3)` non possono collassare sotto la soglia che NB-11b e NB-11c presuppongono.

### 2.7 Requisito rinforzato per la fascia oraria 14:00–15:00

> Recepisce **FT-3** (`economia` § 4.9) senza modifiche di merito. Il conto che la genera è verificato sugli orari reali dei nove abitanti, non su una stima.

`economia` § 4.9 conta, fascia per fascia, le fonti indipendenti disponibili in Pietrafitta: 10, 11, 7, **2**, 5, 10. La fascia **14:00–15:00** è l'unico collo di bottiglia sistemico della mappa — sette abitanti su nove sono in finestra cieca, e **nessun documento del paese data quella fascia**. Delle 2 fonti nominali, 1 è dichiarata debole.

- **FT-3 — Ora critica.** Se `C1` cade nella fascia **14:00–15:00**, il caso deve fornire **≥ 2 fonti non testimoniali** per **ogni casella che dipenda da quell'ora**: almeno una `OSS` materiale (traccia fisica, stato di un oggetto) e almeno una `ORA` derivata da vincolo di percorrenza sulla matrice `economia` § 1.2. Un caso ambientato in quella fascia e sorretto da sole testimonianze viola il vincolo 8 della vision ed è **REJECT**.
  Il divieto riguarda la **casella**, non il **fatto**: un fatto alle 14:30 è legittimo e desiderabile, purché l'ora sia provabile per via materiale.
- **FT-3b — Generalizzazione del criterio** *(estensione di rev.3, stesso merito)*. FT-3 nomina 14:00–15:00 perché è l'unica fascia sotto soglia **sulla mappa attuale**. Se `regions/` o `characters/` cambiano — un abitante in più, un orario spostato, un registro nuovo — QA ricalcola la tabella `economia` § 4.9 e **ogni fascia con ≤ 2 fonti indipendenti eredita automaticamente FT-3**, senza bisogno di una nuova revisione di questo standard. La soglia è il numero di fonti, non l'orologio.

---

## 3. Criterio di non-banalità e anti-bruteforce (bloccante)

### 3.1 Soglie di profondità e volume

| # | Soglia | Valore | Verifica |
|---|---|---|---|
| NB-1 | Profondità verso `C4` (responsabile) | **≥ 4 passi in sequenza** | Cammino più lungo `P → C4`. Passi paralleli non contano come profondità |
| NB-2 | Profondità verso ogni altra casella | **≥ 2 passi**; al massimo **1 casella** dell'intero caso a profondità 1 | DAG |
| NB-3 | Concorrenza su `C4` | **≥ 3 prove distinte**, di **≥ 2 tipi** | Foglie a monte di `C4` |
| NB-4 | Nessuna prova schiacciante | Nessuna prova singola riduce da sola lo spazio residuo del caso di **> 60%** | Si ricalcola T2 con quella sola riga |
| NB-5 | Nessuna prova monopolista | Nessuna prova singola **determina** > 1 casella | T2, colonna Casella/e. *Determinare* ≠ *contribuire*: vedi RD-9 |
| NB-6 | Volume probatorio | **≥ 18 prove raccoglibili** | Conteggio `P-*` |
| NB-7 | Scarsità reale (Pilastro 2) | Raccolta esaustiva **≥ 1,8 × B (≥ 44 mezze)**, contata su azioni + tour minimo; deve superare la soglia **anche sulle sole azioni** | Somma dei costi dichiarati. Il catalogo di riferimento di `economia` § 4.1–4.2 dà 44 azioni + 11 spostamenti = 55 = 2,29 × B |
| NB-8 | Densità deduttiva | **≥ 16 passi `D-*`**, di cui **≥ 9** con più di una premessa | Conteggio sul grafo |

### 3.2 Soglie anti-bruteforce — sui comma disgiunti

La rev.1 fissava "≥ 100 combinazioni per gruppo timbrabile". Con gruppi disgiunti e 3 stesure quella soglia è **inerte e mal posta**, per due ragioni:

*(a) È sotto la baseline.* La stima conservativa di `core_loop` § 3.5 è 1.152 / 1.170 / 1.344 a spazio pieno. Una soglia a 100 non boccerebbe mai nulla di ciò che il game designer già considera prudente: un criterio che non può fallire non è un criterio.

*(b) Misura l'attaccante sbagliato.* `core_loop` § 3.5 modella un attaccante che non sa nulla e tira la terna intera. Quell'attaccante non esiste. L'attaccante reale è il giocatore che ha **dedotto due caselle su tre** e tira la terza: con gruppi disgiunti, 3 stesure e `d(C3) = 6`, la probabilità di timbrare è **3/6 = 50 %**. Il timbro ottenuto per fortuna, per giunta, **retro-conferma le altre due caselle**, restituendo i bit che il canale doveva negare. Questo è l'anti-pattern AP-23.

Le soglie sostitutive sono tre, e la vincolante è NB-10.

| # | Soglia | Valore | Verifica |
|---|---|---|---|
| **NB-9** | **Cardinalità di comma** | `N(CM) ≥ 180` per ciascuno dei tre comma | T1 |
| **NB-10** | **Tiro sulla casella residua** | `3 / d(Ci) ≤ 0,25` ⇒ **`d(Ci) ≥ 12`** per `C1, C5, C6, C8, C9` | T1 |
| **NB-11** | **Simmetria del comma** | Vedi § 3.3 — obbligatoria per `C2, C3, C4, C7` (tetto strutturale < 12) | Costi d'azione dichiarati |

**Motivazione di NB-9 = 180.** Con 3 stesure la probabilità di timbrare un comma a caso è esattamente `3/N`.

| `N(CM)` | P(comma a caso) | P(≥1 comma su un caso) | P(≥1 comma sui 3 casi) |
|---|---|---|---|
| 100 (soglia rev.1) | 3,00 % | 8,73 % | **24,0 %** |
| **180 (soglia rev.2–3)** | **1,67 %** | **4,92 %** | **14,0 %** |
| baseline `core_loop` a spazio pieno | ~0,25 % | 0,77 % | 2,3 % |
| 528 (se si volesse ≤ 5 % sullo slice) | 0,57 % | 1,70 % | 5,0 % |

A 100, un giocatore su quattro incassa un timbro immeritato nell'arco della slice: inaccettabile per il pubblico di riferimento. A 528 la soglia sarebbe formalmente elegante ma imporrebbe di gonfiare i domini con distrattori inerti — cioè di produrre AP-20 (punizione dell'esplorazione) per difendersi da un attaccante che non esiste. **180 è il valore che rende il criterio mordente restando largamente sotto la baseline del game designer**: un caso costruito più stretto della sua stima prudente viene fermato, un caso conforme passa senza distorsioni. La difesa vera non è qui: è in NB-10 e NB-11.

**Nota di calibrazione.** Confrontando NB-10 con la tabella "spazio pieno" di `core_loop` § 3.5, l'unica casella non conforme è **`C6` MEZZO (10 < 12)**. Il quest designer deve portarla a ≥ 12 oggetti plausibili per caso. Tutte le altre caselle senza tetto sono già conformi (`C1` 24, `C5` 13, `C8` 12, `C9` 14).

### 3.3 NB-11 — Simmetria del comma

Per ogni comma si dichiarano i **costi minimi di determinazione certa** delle tre caselle, ordinati `c₁ ≤ c₂ ≤ c₃` (in mezze di **sola azione**, § 0.3). Devono valere tutte le condizioni:

- **NB-11a** — `c₃ ≤ c₁ + c₂`. Se la casella più difficile costa più delle altre due insieme, il giocatore razionale smette di dedurla e la tira con 3 stesure.
- **NB-11b** — al massimo **1 casella per comma** con `c ≤ 2 mezze` (≈ 0,083 × B, "quasi gratuita").
- **NB-11c** — se il comma contiene una casella con `d(Ci) < 12` (cioè `C2`, `C3`, `C4`, `C7`), allora `c₁ + c₂ ≥ 4 mezze` **e** quella casella deve avere costo **strettamente minore** di `c₃`. Le caselle a dominio piccolo non sono mai l'ultima incognita di un comma, e **non lo sono nemmeno a pari merito**: la stretta disuguaglianza (precisazione di rev.3) chiude il caso in cui una casella a dominio piccolo pareggia il massimo del comma e resta di fatto l'ultima da chiudere.
- **NB-11d — Supplemento di isolamento** *(nuovo in rev.3, correttivo della ratifica di `c(Ci)`)*. Se la catena minima di una casella richiede almeno un'azione in un luogo fuori dal centro abitato (`L6`, `L7`, `L8`) e **nessuna** delle altre due caselle dello stesso comma ha una catena minima che passa da quel luogo, il suo costo si ricalcola come `c(Ci) + s`, dove `s` è il costo di **salita** da `L1` a quel luogo secondo `economia` § 1.2 (`L6` → 1 andata / 3 rientro, `L7` → 3, `L8` → 2; con pioggia si usa il giro dal paese). Si riordinano quindi `c₁ ≤ c₂ ≤ c₃` e si riverificano NB-11a/b/c sui valori corretti.
  Motivo: escludere gli spostamenti da `c(Ci)` è corretto perché il cammino è condiviso — ma quando **non** è condiviso da nessun'altra casella del comma, non è logistica: è il costo di quella casella e basta. NB-11d misura solo il caso in cui la condivisione non c'è, e lascia intatti tutti i conti di `economia` § 4 (che non calcolano `c(Ci)` per casella).

**Conseguenza determinata da NB-11c** — è la risposta alla dipendenza D-6 di `economia` § 8, e va letta come specifica, non come suggerimento:

| Comma | Caselle a dominio piccolo | Chi **può** essere la casella `c₃` |
|---|---|---|
| CM-I | `C2` (≤ 8), `C3` (6) | **solo `C1`** ORA |
| CM-II | `C4` (9) | **solo `C5` o `C6`** |
| CM-III | `C7` (8) | **solo `C8` o `C9`** |

Le caselle care di un caso sono dunque sempre fra `C1, C5, C6, C8, C9` — cioè quelle che richiedono un `IN3`, un `D3`, una perlustrazione o una salita. Non è una coincidenza: sono le stesse caselle su cui NB-10 impone `d ≥ 12`. Dominio grande e costo alto vanno insieme; dominio piccolo e costo basso pure. È così che il tiro a caso resta non conveniente in entrambe le direzioni.

Conseguenza per il **Comma I**: `C3` ATTO (d = 6) non può essere l'ultima casella da chiudere, e `C1`/`C2` non possono essere entrambe quasi gratuite. La tensione con la lettera della garanzia G2 di `core_loop` § 6 è **chiusa dal vincolo 7 della vision**: vedi § 10.1.

---

## 4. Criterio di ridondanza dei percorsi e di composizione del caso (bloccante)

> Vision, mitigazione rischio: *"Ogni caso ha almeno tre catene deduttive indipendenti; fallire una non chiude le altre."* · Vincolo 8: *"Perdere un testimone non chiude alcun comma."*

### 4.1 Due assi da non confondere

`core_loop` G3 dice: *tre catene mappate 1:1 sui tre comma, perdere un testimone chiude al massimo un comma*. È **decomposizione**, non ridondanza: se ogni comma ha una sola catena, ogni comma ha un collo di bottiglia, e "chiude al massimo un comma" significa comunque un comma perso senza colpa del giocatore. La vision chiede l'altro asse, e il Director ha ratificato questa lettura (§ 10.2).

**Si richiedono entrambi.**

| Asse | Requisito |
|---|---|
| **Decomposizione** (G3) | I tre comma sono chiudibili in modo indipendente l'uno dall'altro |
| **Ridondanza** (vision, vincolo 8) | Ogni comma è chiudibile per più catene alternative |

### 4.2 Soglie di ridondanza

- **RD-1** — Catene indipendenti per comma: **≥ 2** per CM-I e CM-III, **≥ 3** per **CM-II** (contiene `C4`).
- **RD-2** — Disgiunzione probatoria: per ogni coppia di catene dello stesso comma, `|prove(Ki) ∩ prove(Kj)| ≤ 1`. Nessuna prova compare in tutte le catene di un comma, salvo il fatto iniziale delle 06:00.
- **RD-3** — Disgiunzione delle fonti: le catene di uno stesso comma non dipendono tutte dallo stesso abitante né dallo stesso luogo. Almeno 2 partono da luogo e interlocutore diversi.
- **RD-4** — Diversità di regola: le catene di uno stesso comma usano **≥ 2 regole terminali distinte** fra R1–R8. Tre alibi orari (tre R1) sono una catena sola travestita da tre.
- **RD-5** — **Indipendenza inter-comma.** Nessun comma richiede che un altro comma sia stato *timbrato*. Se CM-III dipende deduttivamente da CM-II, la dipendenza va dichiarata e CM-III deve avere **≥ 1 catena che non passa da CM-II**. Altrimenti un comma esaurito ne trascina un altro e il test RD-6 fallisce a cascata.
- **RD-6** — **Test di rimozione.** Si rimuove dal caso, una alla volta: ogni singola prova `P-*`; ogni singolo luogo `L-*` con tutte le sue prove; ogni singolo abitante con tutte le sue testimonianze. Dopo ogni rimozione **tutti e tre i comma restano chiudibili**. Non "al massimo uno si chiude": **zero**. Un solo fallimento = AP-06, REJECT.
- **RD-7** — Percorribilità individuale: **ogni** catena, presa da sola, costa **≤ 0,70 × B** (≤ 16 mezze), spostamenti inclusi. Una catena che satura la giornata non è un'alternativa, è la strada obbligata con due decorazioni accanto.
- **RD-7b (= TC-3)** — **Esistenza di un ingresso economico.** La catena **più economica di ciascun comma** costa **≤ 12 mezze (0,50 × B)**, spostamenti inclusi.

  > **Perché RD-7b affianca RD-7 invece di sostituirla.** Le due soglie hanno quantificatori diversi e non sono interscambiabili.
  > RD-7 è un **tetto universale**: *nessuna* catena può costare più di 16. Serve a impedire che un'alternativa esista solo sulla carta.
  > RD-7b è un **pavimento di esistenza**: *almeno una* catena per comma deve costare ≤ 12. Serve a garantire che EQ-4 sia soddisfacibile, perché `economia` § 4.5 dimostra che **RD-7 ed EQ-4 non sono simultaneamente saturabili**: con una catena minima da 16, un depistaggio da 5 e il confutatore più economico da 4 si arriva a `25 > B`. Il caso sarebbe formalmente conforme allo standard e materialmente irrisolvibile.
  > Sostituire RD-7 con "12 per tutte le catene" sarebbe l'errore opposto: eliminerebbe le catene alternative legittimamente costose (13–16 mezze) che sono esattamente ciò che il Pilastro 2 chiede — strade diverse con prezzi diversi. Il tetto resta a 16 per le alternative; il pavimento vale sulla minima.
  > Verifica di soddisfacibilità: le otto catene di riferimento di `economia` § 4.3 costano 7–10 mezze. Margine ampio.
- **RD-8** — **Chiusura entro il budget.** Esiste ≥ 1 percorso che chiude tutti e tre i comma in ≤ 24 mezze, e ne esistono **≥ 3 distinti** (`core_loop` V3). I tre percorsi differiscono per ≥ 2 luoghi e ≥ 2 interlocutori, e ciascuno è verificato **contro la griglia di reperibilità** di `economia` § 3.2: un percorso che interroga qualcuno in una mezza in cui non è reperibile non esiste.
- **RD-9 (= TC-1)** — **Condivisione inter-comma.** Nel percorso vincente più economico, almeno **2 azioni da ≥ 2 mezze ciascuna** devono alimentare caselle di **comma diversi**, per un risparmio `S ≥ 4` mezze.

  Non viola NB-5, e la distinzione è vincolante: NB-5 vieta che una prova **determini** più di una casella; RD-9 chiede che una prova **contribuisca come premessa** a passi di comma diversi. Una testimonianza che fissa un'ora (premessa verso `C1`) e menziona un debito (premessa verso `C7`) non determina né l'una né l'altro: entrambe le caselle restano a valle di altri passi.
  Non viola RD-5: condividere un'azione non è richiedere che un comma sia **timbrato**.
- **RD-9b — Le azioni condivise devono essere ridondanti** *(nuovo in rev.3)*. Ciascuna delle azioni condivise di RD-9 è un punto singolo che tocca due comma: è la superficie di rischio che RD-9 introduce. Per ognuna, e per ciascuno dei comma che alimenta, deve esistere una catena alternativa che non la usa, **e il percorso risultante deve ancora chiudere i tre comma in ≤ B**. Il controllo è mirato: si applica alle sole azioni condivise (2–3 per caso), non alle 18+ prove del test RD-6.

  Un RD-6 interamente sensibile al budget — «dopo ogni rimozione esiste ancora un percorso completo ≤ 24» — è stato considerato e **scartato** in rev.3: con il margine misurato di 0–3 mezze nel caso peggiore ammesso (`economia` § 4.7), lo si soddisferebbe solo gonfiando il caso di prove ridondanti, cioè producendo AP-20. RD-6 resta un test di **chiudibilità** topologica; RD-9b è il solo punto in cui diventa anche un test di budget, perché è il solo punto in cui la condivisione lo rende necessario.
- **RD-10 (= TC-2)** — **Escursione unica.** Deve esistere un percorso completo che chiude i tre comma **uscendo dal centro abitato al massimo una volta**, verso `{L6}` **oppure** verso `{L7, L8}`, mai entrambi. Operativamente: **ogni comma deve avere ≥ 1 catena che non richiede la seconda escursione.** Garantisce `M ≤ 7`, e `M = 5` se il fatto è in quota e il giocatore sceglie di restare sul posto (SP-1, `economia` § 3.1).
  Il caso che viola RD-10 è AP-27.
- **RD-11 (= FT-2)** — **Dorsale d'ufficio.** Ogni caso ha, **per ciascun comma**, almeno una catena composta interamente da prove disponibili con **tutti gli abitanti a T0** — cioè carte, osservazioni e vincoli di percorrenza, senza parola di nessuno (`economia` § 5.5).
  È il criterio che rende il vincolo 8 della vision resistente all'**erosione cumulativa**: RD-6 rimuove un abitante alla volta, ma il sistema di fiducia può portarne fino a **4 simultaneamente a T0** (`economia` E-1). La dorsale è ciò che regge in quello stato, e senza di essa RD-6 sarebbe un test a guasto singolo su un sistema a guasti multipli.
  **La dorsale deve a sua volta soddisfare RD-10**: le tre catene T0 devono essere percorribili con al massimo una escursione. Il materiale T0 di Pietrafitta è distribuito su `L1`, `L2`, `L6`, `L7`, `L8`, e tre catene che pescassero una a `L6` e una a `L7` costerebbero `M ≥ 10`, portando la dorsale a ~25 mezze — fuori budget. Vedi § 10.3.

### 4.3 BD-1 — Bilancio di composizione dichiarato *(nuovo in rev.3, bloccante)*

`economia` § 4.7 riduce l'intera questione della soddisfacibilità a una disuguaglianza. Il caso deve dichiararla e dimostrarla, invece di lasciarla implicita:

```
Σc − S + M ≤ B = 24

Σc = Σ (c₁ + c₂ + c₃) sui tre comma       (mezze di sola azione, § 0.3 / § 3.3)
S  = mezze risparmiate dalle azioni condivise fra comma   (RD-9, S ≥ 4)
M  = spostamenti del percorso vincente più economico      (RD-10, M ≤ 7)
```

**`S ≥ 4` è un pavimento, non una garanzia.** Con `Σc = 21` (minimo teorico NB-11) e `M = 5` basta `S ≥ 2`. Ma un caso che rispetti anche solo le soglie minime di rev.3 — CM-II caro per NB-1, `C7` non gratuito per LC-6, disuguaglianza stretta in NB-11c — arriva a `Σc ≈ 26`, e con `M = 7` richiede `S ≥ 9`, cioè **tre** azioni condivise, non due. Per questo il criterio bloccante è la disuguaglianza, non il valore di `S`: `S ≥ 4` resta il minimo formale di RD-9, ma è BD-1 a decidere il PASS. Un caso che non chiude BD-1 è respinto anche se soddisfa RD-9 alla lettera.

### 4.4 Consegna

`percorsi.md`:
- una riga per catena: `ID | comma | prove | passi | luoghi | interlocutori | regola terminale | azioni | spostamenti | totale in mezze | frazione di B`;
- la matrice di intersezione per comma (RD-2);
- la tabella completa del test di rimozione RD-6, più il test mirato RD-9b sulle azioni condivise;
- i 3 percorsi integrali di RD-8 **con orario mezza per mezza**, verificati sulla griglia `economia` § 3.2;
- la dorsale d'ufficio RD-11, tre catene, con il suo `M`;
- **il bilancio BD-1**: `Σc` per comma, `S` con l'elenco delle azioni condivise, `M`, e la disuguaglianza chiusa.

---

## 5. Criterio di equità dei depistaggi (bloccante)

### 5.1 Quantità

**2 ≤ depistaggi ≤ 3 per caso, al massimo 1 per comma.**
Il tetto per comma discende dalle stesure: un giocatore ingannato una volta consuma una stesura e ne conserva 2. Due depistaggi sullo stesso comma gliene lascerebbero 1 — un errore onesto punito come un tiro a caso.

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
- **EQ-3 — Costo di uscita.** Il confutatore più economico costa **≤ 0,25 × B** (≤ 6 mezze), spostamento da `L1` incluso. `economia` § 4.4 dimostra che su **ogni** luogo della mappa esiste un'azione a ≤ 4 mezze: la soglia è strutturalmente raggiungibile ovunque, ma va verificata sul confutatore effettivo, che non è necessariamente l'azione più economica del luogo.
- **EQ-4 — Reversibilità in tempo.** `costo(F) + costo(X più economico) + costo(catena più economica del comma) ≤ B`.
  Peggior caso misurato su Pietrafitta (`economia` § 4.5): `5 + 4 + 7 = 16`. Al limite dello standard, con la catena minima a 16 mezze, si otterrebbe `25 > 24`: è la ragione per cui esiste **RD-7b**, che porta il termine di catena a ≤ 12 e chiude a `≤ 21`.
- **EQ-5 — Reversibilità in stesure.** Un giocatore che imbocca e poi confuta ogni depistaggio del caso deve poter chiudere ogni comma con **≥ 1 stesura residua**.
- **EQ-6 — Crepa obbligatoria.** Ogni personaggio che mente ha `bugie.md`: `bugia | ragione | crepa (ID prova) | luogo | costo`. Bugia senza crepa nominata = REJECT.

### 5.4 Il completamento d'ufficio è un depistaggio strutturale

`core_loop` § 5.2C: la casella lasciata **in bianco** viene riempita d'ufficio dalla Pretura col valore socialmente più comodo, in modo **deterministico**. `economia` § 6.2–6.3 rende la scelta **calcolabile**: indice di comodità sociale `S(v)` per le caselle di tipo persona, regole dichiarate per le altre sette. Il quest designer applica quella funzione, non ne inventa una.

- **EQ-7 — Il valore d'ufficio non è mai la soluzione.** Per tutte e 9 le caselle: `U-Ci ≠ soluzione(Ci)`. Se la funzione `S` restituisce il colpevole, si scala al secondo valore vivo (`economia` § 6.4). Se coincidesse, non fare nulla pagherebbe. Vedi AP-24.
- **EQ-8 — Il valore d'ufficio deve mordere.** `U-Ci` non può essere un valore già escluso dalle prove gratuite delle 06:00: dev'essere un candidato ancora vivo a metà tabella T2.
- **EQ-9 — Il valore d'ufficio è prevedibile.** Il giocatore deve poter sapere **prima delle 18** cosa scriverà la Pretura. Il dossier nomina la fonte in-game da cui lo si deduce. Un default non conoscibile è un costo nascosto e viola A2. La scrittura effettiva di quelle fonti è deliverable di `narr-narrative-designer` (`economia` D-5): ai fini di questo standard il quest designer **dichiara** la fonte prevista, e QA la ricontrolla in sede di validazione narrativa.
- **EQ-10 — `IGNOTI` non è mai corretto e non è mai punito meccanicamente.** Il costo di dichiarare ignoto è sociale e narrativo. Il dossier nomina **quale porta si chiude** per ogni casella dichiarata ignota. Nessun costo in tempo, stesure o timbri. Vedi AP-26.
- **EQ-11 — La prova differita non è mai necessaria** *(nuovo in rev.3)*. La trasferta a Roccalta (`economia` § 2.5, classe `D5`) consegna una prova **nel caso successivo**. Il Director l'ha ratificata con un vincolo assoluto (vision, Ratifiche 2026-08-23): quella prova non può **mai** essere necessaria alla soluzione unica di un caso, solo corroborante. Verifica meccanica, su ogni caso dal secondo in poi:
  1. nessuna prova di classe `D5` compare come foglia di una catena minima (RD-7b);
  2. rimuovendo **tutte** le prove `D5` insieme, i tre comma restano chiudibili e RD-8 continua a esibire 3 percorsi ≤ B;
  3. il dossier del caso è validabile **senza conoscere l'esito del caso precedente**.
  Il punto 2 è più severo di RD-6, che rimuove una prova alla volta: qui la rimozione è in blocco, perché il giocatore che non ha preso la corriera non ne ha nessuna.

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
| AP-23 | **Il comma a due terzi**: due caselle quasi gratuite + una a dominio piccolo | Con 3 stesure la terza si tira a sorte (fino al 50 % su `C3`), e il timbro ottenuto per fortuna **retro-conferma** le altre due: il canale muto del feedback torna a parlare |
| AP-24 | **Il valore d'ufficio corretto**: la Pretura riempie il bianco con la risposta giusta | Non fare nulla paga più che indagare: distrugge la gerarchia degli esiti e l'intero impianto del Pilastro 3 |
| AP-25 | **La lista chiusa autopotante**: i distrattori di `C3`/`C7` sono eliminabili gratis | La lista si riduce da sé a due voci e la qualificazione giuridica diventa testa-o-croce |
| AP-26 | **L'ignoto punito meccanicamente**: dichiarare `NON ACCERTATO` costa tempo, stesure o accesso generico | Il giocatore mente per convenienza invece di essere onesto, e il verbale smette di essere un atto di coscienza |
| **AP-27** | **Il caso a due escursioni**: la chiusura dei tre comma richiede sia `L6` sia `{L7, L8}` | `M ≥ 10` più un comma caro sfonda le 24 mezze: il caso è conforme a ogni soglia singola e materialmente irrisolvibile. È lo scenario isolato da `economia` § 4.7. Viola RD-10 |
| **AP-28** | **Il movente gratuito**: `C7` (o `C3`) determinato da premesse di classe `D0`/`REG` a costo zero | La casella con il dominio più piccolo del modulo diventa anche la più economica: NB-11b e NB-11c saltano insieme e il Comma III si riduce a un tiro su due incognite. Viola LC-6 |

---

## 7. Checklist di accettazione operativa

**Un solo NO = REJECT.** Nessun campo vuoto, nessun "parziale", nessun esito condizionato.

**Caso:** ________ **Revisione:** ____ **Data:** ____ **Validatore:** qa-lead

### A. Consegna (procedurale — se fallisce, l'esame si ferma)
| # | Controllo | SÌ/NO |
|---|---|---|
| A1 | `prova_unicita.md` con T1–T5 complete | |
| A2 | `grafo_deduttivo.md`, tutti i passi in forma canonica | |
| A3 | `percorsi.md` con matrici, RD-6, RD-9b, 3 percorsi RD-8 orari, dorsale RD-11 | |
| A4 | `bugie.md` per ogni personaggio che mente | |
| A5 | Liste chiuse `C3` (6 voci, **con ordine di gravità dichiarato**) e `C7` (8 voci, ordine di stampa della slice) allegate — LC-0 | |
| A6 | Valori d'ufficio `U-C1…U-C9` dichiarati e derivati da `economia` § 6.2–6.3 | |
| A7 | ID conformi § 0; ogni prova classificata; luogo e costo in mezze dichiarati | |
| **A8** | **Ogni costo citato deriva dalle tabelle di `economia` § 1.2 / § 2 / § 3.2; nessun costo inventato dal caso** | |
| **A9** | **Bilancio BD-1 dichiarato in `percorsi.md` con `Σc`, `S`, `M` e disuguaglianza chiusa** | |
| **A10** | **Meteo del caso dichiarato** (la mulattiera del Fosso è impraticabile con pioggia: cambia R2, `M` e RD-10) | |

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
| **C10** | **LC-6: ≤ 1 premessa `REG`/`D0` nel passo terminale su `C3` e su `C7`** | |
| **C11** | **G-6 (FT-4): ogni foglia sbloccata da un tier è a ≥ 2 passi da qualunque casella** | |
| **C12** | **FT-3: se `C1` è in 14:00–15:00, ≥ 2 fonti non testimoniali (1 `OSS` + 1 `ORA`) per ogni casella dipendente da quell'ora** | |
| **C13** | **R2 calcolata sulla matrice asimmetrica, direzione corretta, meteo applicato** | |

### D. Non-banalità e anti-bruteforce
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| D1 | Profondità verso `C4` | ≥ 4 | |
| D2 | Profondità altre caselle (max 1 eccezione a profondità 1) | ≥ 2 | |
| D3 | Prove concorrenti su `C4` / tipi diversi | ≥ 3 / ≥ 2 | |
| D4 | Riduzione massima da una singola prova | ≤ 60 % | |
| D5 | Caselle **determinate** da una singola prova | ≤ 1 | |
| D6 | Prove raccoglibili | ≥ 18 | |
| D7 | Raccolta esaustiva (azioni + tour minimo, **e** sole azioni) | ≥ 1,8 × B (≥ 44) | |
| D8 | Passi `D-*` / con ≥ 2 premesse | ≥ 16 / ≥ 9 | |
| D9 | `N(CM)` per ciascuno dei 3 comma | ≥ 180 | |
| D10 | `d(Ci)` per `C1,C5,C6,C8,C9` | ≥ 12 | |
| D11 | NB-11a: `c₃ ≤ c₁ + c₂` in ogni comma | — | |
| D12 | NB-11b: caselle quasi gratuite (`c ≤ 2 mezze` di azione) per comma | ≤ 1 | |
| D13 | NB-11c: `C2,C3,C4,C7` con costo **strettamente minore** di `c₃`; `c₁+c₂ ≥ 4` nel loro comma | — | |
| **D14** | **NB-11d: supplemento di isolamento applicato e NB-11a/b/c riverificate sui valori corretti** | — | |

### E. Ridondanza e composizione
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| E1 | Catene per CM-I / CM-II / CM-III | ≥ 2 / ≥ 3 / ≥ 2 | |
| E2 | Intersezione per coppia di catene dello stesso comma | ≤ 1 prova | |
| E3 | Nessuna prova comune a tutte le catene di un comma (salvo fatto iniziale) | — | |
| E4 | ≥ 2 catene per comma con luogo e interlocutore d'ingresso diversi | — | |
| E5 | Regole terminali distinte per comma | ≥ 2 | |
| E6 | Nessun comma richiede un altro comma timbrato; CM-III ha ≥ 1 catena che salta CM-II | — | |
| E7 | Test di rimozione RD-6: dopo ogni rimozione **tutti e tre** i comma chiudibili | 0 fallimenti | |
| E8 | RD-7: costo di **ogni** catena | ≤ 16 mezze | |
| E9 | RD-8: percorsi completi entro budget, distinti, **verificati sulla griglia oraria** | ≥ 3, ≤ 24 mezze | |
| **E10** | **RD-7b (TC-3): catena più economica di ciascun comma** | ≤ 12 mezze | |
| **E11** | **RD-9 (TC-1): azioni da ≥ 2 mezze condivise fra comma / risparmio `S`** | ≥ 2 azioni / `S ≥ 4` | |
| **E12** | **RD-9b: ogni azione condivisa ha alternativa per entrambi i comma, e il percorso alternativo chiude ≤ B** | — | |
| **E13** | **RD-10 (TC-2): esiste un percorso completo con ≤ 1 escursione; ogni comma ha ≥ 1 catena senza la seconda** | `M ≤ 7` | |
| **E14** | **RD-11 (FT-2): dorsale d'ufficio T0 per ciascun comma, essa stessa conforme a RD-10 e ≤ B** | — | |
| **E15** | **BD-1: `Σc − S + M ≤ 24` dimostrata sui valori del caso** | — | |

### F. Equità
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| F1 | Depistaggi nel caso / per comma | 2–3 / ≤ 1 | |
| F2 | Confutatori per depistaggio | ≥ 2 | |
| F3 | EQ-2: nessun confutatore presuppone `F` o prove esclusive della soluzione | — | |
| F4 | Confutatore più economico (spostamento incluso) | ≤ 6 mezze | |
| F5 | EQ-4: `F` + `X` + catena più economica del comma | ≤ 24 mezze | |
| F6 | EQ-5: chiusura di ogni comma con ≥ 1 stesura residua dopo tutti i depistaggi | — | |
| F7 | EQ-6: ogni bugia ha ragione difendibile e crepa con ID | — | |
| F8 | EQ-7: `U-Ci ≠ soluzione(Ci)` su tutte e 9 le caselle | — | |
| F9 | EQ-8: nessun `U-Ci` già escluso dalle prove gratuite delle 06:00 | — | |
| F10 | EQ-9: fonte in-game dichiarata per ogni `U-Ci` | — | |
| F11 | EQ-10: costo dell'ignoto solo sociale; porta chiusa nominata per casella | — | |
| **F12** | **EQ-11: nessuna prova `D5` in catena minima; rimosse in blocco, i tre comma restano chiudibili e RD-8 regge** | — | |

### G. Anti-pattern
| # | Controllo | SÌ/NO |
|---|---|---|
| G1 | Passata completa AP-01…AP-28: nessuno presente | |
| G2 | Se presente, indicare ID e passo/prova coinvolti nelle Note | |

### Esito
```
VERDETTO: PASS | REJECT
NO rilevati: <elenco ID controllo>
Anti-pattern rilevati: <elenco AP>
Azione richiesta al quest designer: <max 5 righe>
```

---

## 8. Copertura dei requisiti esterni

### 8.1 `core_loop` § 7 — V1–V6

| Requisito game designer | Copertura in questo standard |
|---|---|
| V1 Unicità per casella | § 1.2 Passi 1–3 · B1–B4 |
| V2 Nessuna terna alternativa timbrabile | § 1.2 Passo 3 · B3 · T4 |
| V3 Risolvibilità entro 24 mezze, ≥ 3 percorsi | RD-8 · RD-10 · BD-1 · E9, E13, E15 |
| V4 Nessuna inferenza automatica | G-5 · G-6 · C4, C11 (la conformità della UI resta a `qa-ux-researcher`) |
| V5 Copertura d'ufficio | A6 · EQ-7/8/9 · F8–F10 |
| V6 Annuncio del costo | Fuori dal perimetro di questo standard: verifica UI, `qa-ux-researcher`, su `economia` § 7 |

### 8.2 `creative_vision` — vincoli 1–8

| Vincolo | Copertura |
|---|---|
| 1 Nessun soprannaturale / coincidenza risolutiva | AP-13 · G1 |
| 2 Ogni bugia ha ragione e crepa | EQ-6 · F7 · AP-02 |
| 3 1954 è un vincolo | AP-09 · AP-19 · G-3 |
| 4 Il quaderno registra fatti | G-5 · AP-12 · C4 |
| 5 Risolvibile al 100 % in una giornata | RD-8 · BD-1 · EQ-11 · E9, E15, F12 |
| 6 Uno slot, nessun reload | Fuori perimetro (tecnico); il suo effetto è presupposto da § 3.2 |
| 7 Il sopralluogo dà candidati, mai determinazioni | § 10.1 · NB-12 · AP-23 · verificato su Pietrafitta in `economia` § 4.8 |
| 8 Perdere un testimone non chiude alcun comma | RD-6 · RD-11 · FT-3 · E7, E14, C12 |

### 8.3 `economia_tempo_e_fiducia` — prescrizioni indirizzate al QA

| Origine | Recepita come | Sezione |
|---|---|---|
| TC-1 | RD-9 (+ RD-9b) | § 4.2 |
| TC-2 | RD-10 (+ AP-27) | § 4.2 |
| TC-3 | RD-7b | § 4.2 |
| FT-3 | FT-3 (+ FT-3b) | § 2.7 |
| FT-2 | RD-11 | § 4.2 |
| FT-4 | G-6 | § 2.3 |
| D-4 (definizione di `c(Ci)`) | ratificata | § 0.3 |
| D-6 (caselle care) | tabella determinata | § 3.3 |
| § 6.2–6.3 (funzione `S`, regole `U-Ci`) | EQ-7/8/9 · A6 | § 5.4 |

---

## 9. Procedura di validazione

Ordine fisso, interruzione al primo blocco: **A** → **B** → **C** → **D**/**E**/**F** (calcolabili in parallelo) → **G** (eseguita per intero anche a caso già respinto, così il designer riceve la lista completa).

**Esiti ammessi: `PASS` o `REJECT`. Nessun altro.** Lo stato `PASS condizionato ai costi` della rev.2 è **abolito**: esisteva perché la baseline `core_loop` § 1.2 era dichiarata provvisoria, e `economia_tempo_e_fiducia.md` § 1.2 / § 2 / § 4 l'ha confermata e verificata su `B = 24`. Un caso che soddisfa la griglia riceve **PASS pieno** e passa a `qa-cross-domain` e al batch approval del Director senza riserve economiche.

**Passaggio aritmetico obbligatorio, prima di dichiarare PASS.** I gruppi D ed E non sono verificabili "a occhio": QA ricalcola, sui numeri del dossier e non su quelli dichiarati dal designer,
1. `Σc` per comma e l'ordinamento `c₁ ≤ c₂ ≤ c₃`, con il supplemento NB-11d dove applicabile (D11–D14);
2. il costo di ogni catena, azioni + spostamenti sulla matrice `economia` § 1.2 nella direzione corretta (E8, E10);
3. i tre percorsi RD-8 mezza per mezza contro la griglia di reperibilità `economia` § 3.2 (E9);
4. la disuguaglianza BD-1 (E15).
Discordanza fra numeri dichiarati e ricalcolati = REJECT su A8, senza esame di merito: un dossier che sbaglia i propri conti non è verificabile.

Un caso respinto rientra con **revisione incrementata** e la checklist precedente allegata. QA riesegue l'intera griglia: una correzione locale può rompere `|R(CM)|`, NB-9, NB-11 o il test di rimozione.

**Rivalidazione forzata.** Un caso già PASS torna in coda di validazione se cambia una delle basi su cui è stato calcolato: la matrice `economia` § 1.2, la tabella dei costi § 2, la scala di reticenza § 2.2, la griglia di reperibilità § 3.2, `B`, o le liste chiuse LC-0. È la ragione per cui il PASS pieno è ora possibile senza essere fragile: non è condizionato, è **datato** rispetto a una baseline che, se cambia, si dichiara.

---

## 10. Conflitti — stato

### 10.A Chiusi

#### 10.1 G2 (sopralluogo gratuito) contro NB-11 e AP-23 — **CHIUSO, ratificato a favore del QA**

`core_loop` G2 garantiva che il sopralluogo delle 06:00 desse «≥ 2 delle 3 voci del Comma I». Se `C1` e `C2` sono **determinate**, il Comma I si riduce a `C3` con `d = 6` e 3 stesure: 50 % di timbro a testa o croce, e il timbro retro-conferma ora e luogo.

**Decisione del Director (2026-08-23):** vince la lettura del QA, promossa a **vincolo 7 della vision**. Il sopralluogo fornisce **voci di quaderno**, non determinazioni; al termine delle 06:00 `C1` e `C2` hanno ciascuna **≥ 3 valori candidati mutuamente incompatibili**. Recepito qui come **NB-12**, criterio bloccante:

> **NB-12 — Il sopralluogo dà materiale, non risposte.** Nessuna voce di sopralluogo e nessuna **coppia** di voci può ridurre `C1` o `C2` sotto i 3 candidati incompatibili. Il sopralluogo produce **5–8 voci** (SP-2, `economia` § 4.8), nessuna dirimente. Violazione = AP-23, REJECT.

`economia` § 4.8 lo dimostra costruttivamente sulla geografia reale: 4 ancoraggi orari indipendenti e discordi (cenere, roggia, brina, bestie governate) e 3 candidati-luogo per ciascuno dei tre possibili luoghi di ritrovamento, generati dal fatto che i luoghi alti condividono substrato, vegetazione e confini. L'intento anti-frustrazione di G2 sopravvive: il Comma I resta il più economico dei tre e chiudibile entro mezzogiorno.

#### 10.2 G3 (una catena per comma) contro il vincolo 8 — **CHIUSO, ratificato a favore del QA**

`core_loop` G3: «perdere un testimone chiude al massimo un comma». Un collo di bottiglia per comma significa un terzo di verbale perso senza colpa del giocatore.

**Decisione del Director (2026-08-23):** vince la lettura del QA, promossa a **vincolo 8 della vision** — *nessuna singola fonte può essere l'unico accesso a una casella*. **G3 vale come pavimento minimo, non come specifica.** Restano vincolanti RD-1 e RD-6 nella loro forma severa, ora affiancati da RD-11 per l'erosione cumulativa della fiducia.

#### 10.3 D5 / trasferta a Roccalta — **CHIUSO in sede di vision, nessuna azione del Director richiesta**

`economia` D-7 chiede al Director il via libera sulla regola D5 (prova che arriva nel caso successivo). **Il via libera esiste già**: vision, Ratifiche del Director 2026-08-23, con il vincolo assoluto che quella prova non sia mai necessaria alla soluzione unica di un caso. Recepito come **EQ-11** (§ 5.3). Segnalo a `dir-lead-game-designer` che **D-7 può essere chiusa senza nuova istruttoria**.

### 10.B Aperti — emersi dal confronto con `economia_tempo_e_fiducia.md`

#### 10.4 FT-2 (dorsale d'ufficio) contro TC-2 (escursione unica)

**Le due prescrizioni sono entrambe di `economia`, e non sono state verificate l'una contro l'altra.**

`economia` § 5.5 richiede, per ciascun comma, una catena interamente percorribile con tutti gli abitanti a T0, e stima il costo della dorsale completa in «~15 mezze di azione + 4–6 di spostamento = 19–21 ≤ 24 ✓». La stima presuppone `M = 4–6`. Ma la tabella del materiale T0 nella stessa sezione lo distribuisce su `L1`, `L2`, `L6`, `L7`, `L8`: se le tre catene T0 pescano una a `L6` e una a `{L7, L8}`, la dorsale richiede **due escursioni**, `M ≥ 10`, e il totale sale a **~25 mezze — fuori budget**, oltre a violare TC-2/RD-10.

Non è un difetto di taratura: è un vincolo di composizione mancante. Lo standard lo chiude imponendo che **la dorsale RD-11 soddisfi essa stessa RD-10** (§ 4.2, checklist E14).

- **Decisione richiesta a:** `design-systems-designer` via `dir-lead-game-designer` — conferma che la lettura è corretta e che la stima 19–21 va intesa sotto vincolo di escursione unica.
- **Ricade sul Director** solo in caso di dissenso, o se il systems designer ritiene che il materiale T0 di Pietrafitta non basti a costruire tre catene dentro una sola escursione: in quel caso il conflitto è fra il vincolo 8 della vision e il budget, e la decisione non è mia.
- **Nel frattempo** lo standard applica la lettura restrittiva. Nessun caso è bloccato: E14 è verificabile così com'è.

#### 10.5 TC-1 (`S ≥ 4`) è un pavimento, non una garanzia di chiusura

`economia` § 4.7 dimensiona `S ≥ 4` sullo scenario «CM-II caro, una escursione, `Σc = 24`». Ma lo standard rev.3 stringe la composizione in tre punti che alzano `Σc`: NB-11c a disuguaglianza stretta, LC-6 (il movente non è gratuito), NB-11d (supplemento di isolamento). Con `Σc ≈ 26` e `M = 7` servono **3 azioni condivise, non 2** (`S ≥ 9`).

Non chiedo di alzare TC-1 — sarebbe una costante inventata al posto di un conto. Lo standard rende invece **bloccante la disuguaglianza stessa** (BD-1, § 4.3): il caso dichiara `Σc`, `S`, `M` e dimostra la chiusura. `S ≥ 4` resta il minimo formale di RD-9; è BD-1 a decidere il PASS.

- **Decisione richiesta a:** nessuno, salvo dissenso di `design-systems-designer`. La segnalo perché **cambia il modo in cui TC-1 va letta** dal quest designer: soddisfare TC-1 non significa aver chiuso il budget.
- **Effetto su `economia`:** nessuna cifra di quel documento è invalidata. I tre percorsi di § 4.6 chiudono a 24/24/24 e restano la dimostrazione costruttiva.

---

## 11. Dipendenze

### 11.1 Chiuse in rev.3

| Dipendenza (rev.2) | Stato | Chiusa da |
|---|---|---|
| **Costi-tempo.** Baseline provvisoria; nessun PASS pieno possibile | **CHIUSA** | `economia` § 1.2, § 2, § 4. NB-7, NB-11, RD-7, RD-8, EQ-3, EQ-4 sono ora calcolabili su cifre confermate. Stato `PASS condizionato ai costi` **abolito** (§ 9) |
| **Distanze e orari.** NB-11 e RD-6/RD-8 non calcolabili senza matrice e orari | **CHIUSA** | `economia` § 1.2 (matrice asimmetrica 8×8) e § 3.2 (griglia di reperibilità dei nove in mezze, regola FIN-1) |
| **Definizione di `c(Ci)`** (ambiguità mia in rev.2) | **CHIUSA** | Ratificata in § 0.3 nella lettura del systems designer: sole azioni, spostamenti esclusi. Correttivo NB-11d |
| **Composizione del caso.** Scenario a budget negativo isolato da `economia` § 4.7 | **CHIUSA** | TC-1/2/3 e FT-3 recepiti come RD-9, RD-10, RD-7b, FT-3; più BD-1 e AP-27/AP-28 |

### 11.2 Aperte — e che cosa bloccano davvero

| # | Verso | Cosa manca | Blocca l'avvio di `design-quest-designer`? |
|---|---|---|---|
| **Q-1** | `design-world-designer` (D-1 di `economia`) | Ratifica della scala di reticenza R1/R2/R3 e della quantizzazione FIN-1 delle presenze | **No.** Se il world designer dissente su un'attribuzione R, cambiano i costi `AS`/`IN2`/`IN3` e con essi `c(Ci)`, RD-7/7b, BD-1. I casi già validati rientrano per **rivalidazione forzata** (§ 9), che è il meccanismo previsto. Non serve attendere |
| **Q-2** | `narr-narrative-designer` (D-5 di `economia`) | Esposizione diegetica della prassi della Pretura, richiesta da EQ-9 | **No.** F10 si soddisfa con la **dichiarazione** della fonte prevista da parte del quest designer; la scrittura è deliverable narrativo e QA la ricontrolla in validazione narrativa |
| **Q-3** | `design-quest-designer` stesso | La lista `C7` MOVENTE (8 voci, ordine di stampa fisso per l'intera slice — LC-0) va redatta **prima del caso 1**, non dentro di esso | **Sì, ma è suo.** È il primo deliverable della sua stessa macroarea, non un'attesa su altri. `U-C7` non è prevedibile senza un ordine di stampa stabile |
| **Q-4** | `design-systems-designer` | Conferma su § 10.4 (dorsale d'ufficio sotto vincolo di escursione unica) | **No.** Lo standard applica la lettura restrittiva; E14 è verificabile subito. La conferma serve a evitare che il quest designer riceva due letture diverse |
| **Q-5** | `viz-ui-ux-artist` / `qa-ux-researcher` | V6 (annuncio del costo) e V4 (nessuna inferenza automatica nella UI) | **No.** Fuori dal perimetro di questo standard, dichiarato in § 8.1 |

### 11.3 Giudizio di prontezza

**Nessuna dipendenza bloccante residua verso altri agenti.** `design-quest-designer` può partire sul caso 1 con questo standard come specifica, a due condizioni interne al suo lavoro: redigere per prima la lista `C7` (Q-3), e dichiarare il meteo del caso (A10), perché con pioggia cambiano R2, `M` e RD-10.

Riserva metodologica, non bloccante: le soglie di rev.3 non sono mai state esercitate su un caso reale. Il primo caso è anche il collaudo della griglia; se un criterio si rivela inapplicabile o vuoto sul primo dossier, la correzione appartiene a questo file — non al caso.
