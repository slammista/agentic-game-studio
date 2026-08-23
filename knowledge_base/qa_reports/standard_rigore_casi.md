---
role: qa-lead
date: 2026-08-23
author: qa-lead
status: draft
locked_by: null
description: Standard formale di rigore deduttivo per i casi di Pietrafitta. Specifica vincolante per design-quest-designer e griglia di validazione per qa-lead. Nessun caso entra in produzione senza esito PASS su tutti i criteri bloccanti.
depends_on:
  - knowledge_base/production/creative_vision.md
---

# Standard di Rigore — Casi Deduttivi di Pietrafitta

**Ambito.** Si applica a ogni caso della vertical slice (3 casi) e a ogni caso futuro.
**Vincolo di riferimento.** `creative_vision.md` § Vincoli creativi 1–5, Pilastri 1–3, tabella Rischi.
**Regola di esito.** Un solo NO su un criterio bloccante = **REJECT**. Nessuna approvazione condizionata.

---

## 0. Notazione obbligatoria (prerequisito di verificabilità)

Un caso non è verificabile se non è indicizzato. Il quest designer assegna ID stabili a tutto:

| Entità | Formato ID | Esempio |
|---|---|---|
| Casella del verbale | `C1`…`C7` (ordine del modulo) | `C3` = chi |
| Prova raccoglibile | `P-<caso>-<nn>` | `P-01-07` |
| Passo deduttivo | `D-<nn>` | `D-04` |
| Catena deduttiva | `K-A`, `K-B`, `K-C` | `K-B` |
| Depistaggio | `F-<nn>` | `F-02` |
| Confutatore di depistaggio | `X-<nn>` | `X-02a` |
| Luogo | `L-<nn>` | `L-05` |
| Abitante | slug da `world/characters/` | `maresciallo-bardi` |

**Budget-tempo.** `B` = tempo totale disponibile in una giornata (alba → corriera delle 18), espresso nelle unità definite da `design-systems-designer`. Tutte le soglie temporali di questo standard sono frazioni di `B` e restano valide qualunque unità venga scelta.

**Tipi di prova** (tassonomia chiusa, usata dai criteri 3 e 5):
`DOC` documento cartaceo (registro, lettera, ricevuta, orario) · `TES` testimonianza di un abitante · `OSS` osservazione diretta di un luogo o di un oggetto · `ORA` vincolo di orario/percorrenza (corriera, distanze, campane) · `REG` fatto amministrativo noto al segretario a costo zero.

Prove non classificabili in questa tassonomia = **REJECT** finché non riclassificate.

---

## 1. Criterio di unicità della soluzione (bloccante)

> Rischio coperto: *"Un caso risulta ambiguo: due soluzioni entrambe difendibili" — impatto Critico.*

### 1.1 Cosa significa "unica"

La soluzione è unica se e solo se esiste **una sola** assegnazione di valori a `C1…C7` che non viola alcun vincolo derivabile dalle prove del caso. Non basta che la soluzione prevista sia la migliore: ogni altra deve essere **positivamente esclusa** da una prova nominata.

### 1.2 Procedura obbligatoria in tre passaggi

**Passo 1 — Dichiarazione dei domini.**
Per ogni casella, il designer enumera il dominio *visibile al giocatore*: l'insieme finito di valori che il modulo del verbale accetta. Non il dominio "plausibile": quello letterale dell'interfaccia.
Vincoli sui domini:
- `|dominio| ≥ 4` per ogni casella (vedi AP-11).
- Il dominio di `C3` (chi) include tutti i 9 abitanti + `ignoti`, sempre. Ridurre a priori il cast è già un indizio illecito.
- Lo spazio grezzo `|S| = Π |dominio(Ci)|` va calcolato e dichiarato.

**Passo 2 — Eliminazione per vincolo.**
Tabella riga-per-riga: ogni riga elimina uno o più candidati citando la prova che lo fa.
Nessuna riga può contenere motivazioni del tipo *"implausibile"*, *"non avrebbe senso"*, *"nessun movente"*. Solo vincoli fattuali.
Alla fine di questo passo ogni casella ha un **insieme residuo**.

**Passo 3 — Enumerazione del residuo.**
Si calcola `|R| = Π |residuo(Ci)|` e si enumerano **tutte** le `|R|` combinazioni in tabella, ciascuna con l'esito `ESCLUSA da <ID prova>` oppure `SOLUZIONE`.
- Vincolo di praticabilità: `|R| ≤ 48`. Se il residuo supera 48, l'eliminazione del Passo 2 è insufficiente: il caso torna al designer.
- Esattamente **una** riga può portare l'esito `SOLUZIONE`.
- L'enumerazione deve essere completa: righe omesse = REJECT, non "ovvie".

### 1.3 Test del secondo classificato (near-miss)

L'ipotesi più vicina alla verità — quella che differisce dalla soluzione per **una sola casella** — deve essere esclusa da **≥ 2 prove distinte**, di cui **almeno una di tipo `DOC` o `ORA`**.
Motivo: se l'ipotesi rivale cade per una sola testimonianza, il caso è a coltello e un giocatore che non si fida di quel testimone resta legittimamente in dubbio. Una singola esclusione testimoniale non è unicità, è opinione.

### 1.4 Formato di consegna

Il designer allega al caso il file `knowledge_base/quests/<caso-slug>/prova_unicita.md`, con frontmatter standard e **quattro sezioni obbligatorie**, in quest'ordine:

```markdown
## T1 — Domini dichiarati
| Casella | Etichetta | Dominio (enumerato) | |dominio| |

Spazio grezzo |S| = ...

## T2 — Eliminazione per vincolo
| # | Casella/e | Candidati eliminati | Prova (ID) | Tipo | Vincolo applicato (una riga) |

Insiemi residui: C1={...} C2={...} ... — |R| = ...

## T3 — Enumerazione del residuo (completa)
| # | C1 | C2 | C3 | C4 | C5 | C6 | C7 | Esito | Prova che esclude |

## T4 — Near-miss
Ipotesi rivale: <...>  (differisce in <casella>)
Esclusa da: <ID prova 1, tipo> + <ID prova 2, tipo>
```

Assenza di una qualsiasi delle quattro sezioni = il caso non è nemmeno esaminabile: **REJECT procedurale**, senza entrare nel merito.

---

## 2. Criterio di deducibilità (bloccante)

> Nessuna casella si riempie per intuizione, per genere-savviness o per eliminazione emotiva.

### 2.1 Forma canonica del passo deduttivo

Ogni passo `D-nn` è una tripla esplicita:

```
D-04 | premesse: [P-01-03, P-01-11, D-02] | regola: R2 | conclusione: C5 ≠ "roncola"
```

Un passo con premesse non citate per ID, o con conclusione in prosa, non è un passo: è un'asserzione. REJECT.

### 2.2 Catalogo chiuso delle regole di inferenza

Sono ammesse **solo** queste regole. Ogni passo ne dichiara una.

| ID | Regola | Forma |
|---|---|---|
| R1 | Incompatibilità temporale | X era in A all'ora T ⇒ X non ha compiuto Y all'ora T altrove |
| R2 | Incompatibilità spaziale | La distanza A→B richiede ≥ Δt ⇒ X non può essere in entrambi entro Δt |
| R3 | Esclusione per enumerazione chiusa | Solo l'insieme N può fare Y; N−1 elementi esclusi ⇒ resta l'ultimo |
| R4 | Contraddizione arbitrata | Due testimonianze incompatibili + un terzo elemento indipendente che decide quale cade |
| R5 | Vincolo documentale | Un documento datato/firmato/registrato fissa un fatto incompatibile con l'ipotesi |
| R6 | Accesso o capacità | Solo chi possiede chiave/permesso/competenza/forza poteva fare Y |
| R7 | Tracciamento dell'oggetto | Provenienza, possesso o spostamento di un oggetto vincola chi l'ha usato |
| R8 | Vincolo economico o amministrativo | Debito, ricevuta, catasto, atto notarile rendono un'ipotesi materialmente impossibile |

**Il movente non è una regola di inferenza.** Non esiste una regola "R-movente". La casella `C7` (perché) si deduce con R5/R8 — carte, debiti, registri — mai da caratterizzazione psicologica. Vedi AP-07.

Serve una regola nuova? Non si aggiunge in un caso: si chiede a `dir-game-director` (CLAUDE.md § Regole assolute 7) e si aggiorna questo standard.

### 2.3 Grafo di dipendenza (verifica meccanica)

Il designer allega `grafo_deduttivo.md`: un DAG con nodi `P-*` (foglie), `D-*` (interni), `C1…C7` (terminali).
Controlli eseguiti da QA, tutti meccanici:

- **G1 — Nessun orfano.** Ogni `D-*` ha ≥ 1 arco entrante. Ogni `C*` ha ≥ 1 catena che lo raggiunge.
- **G2 — Nessun ciclo.** Un `D` che dipende, direttamente o transitivamente, da se stesso significa che il caso presuppone la propria soluzione. È AP-03 travestito.
- **G3 — Chiusura.** Ogni foglia del grafo è una prova effettivamente raccoglibile nel caso, con luogo e costo-tempo dichiarati. Nessuna foglia "conoscenza generale".
- **G4 — Lessico proibito.** Grep sul testo dei passi: `ovviamente`, `chiaramente`, `è evidente`, `l'unico che poteva`, `non può che essere`, `il tipico`, `sembra`, `probabilmente`, `intuisce`. Ogni occorrenza segnala un passo non dimostrato. Le occorrenze sono ammesse solo nei **dialoghi** dei PNG, mai nel grafo.

### 2.4 Test del passo cieco

Per ogni `D-nn`: si consegnano a un lettore **solo** le premesse citate, senza il resto del caso e senza la soluzione. Se non arriva alla conclusione dichiarata, il passo ha una premessa implicita e va esplicitata.
QA esegue questo test su un campione obbligatorio: **tutti** i passi che alimentano `C3` (chi) e `C6` (mezzo), più il 30% casuale dei restanti.

### 2.5 Test di sostituzione (discriminanza)

Per ogni passo che conclude su un abitante: si sostituisce nel passo il nome del colpevole con quello di ciascuno degli altri 8 abitanti. Il passo deve **cadere** in tutti gli 8 casi. Se regge anche solo per uno, il passo non discrimina e non può essere contato come deduzione verso `C3`.

---

## 3. Criterio di non-banalità (bloccante)

> Un caso che si risolve con una prova schiacciante non merita questo pubblico.

Soglie numeriche, tutte calcolabili da T2/T3 e dal grafo:

| # | Soglia | Valore | Come si verifica |
|---|---|---|---|
| NB-1 | Profondità della catena verso `C3` (chi) | **≥ 4 passi in sequenza**, ognuno che consuma l'output del precedente | Cammino più lungo `P → C3` nel DAG. Passi paralleli non contano come profondità |
| NB-2 | Profondità verso ogni altra casella | **≥ 2 passi** (eccezione: al massimo **1** casella dell'intero caso può essere a profondità 1 — tipicamente la data) | DAG |
| NB-3 | Concorrenza sull'inferenza chiave | `C3` richiede **≥ 3 prove distinte**, di **≥ 2 tipi diversi** della tassonomia § 0 | Insieme delle foglie a monte di `C3` |
| NB-4 | Nessuna prova schiacciante | Nessuna singola prova riduce da sola lo spazio residuo del caso di **> 60%** | Si ricalcola T2 rimuovendo tutte le altre righe: la riduzione ottenuta da quella prova sola |
| NB-5 | Nessuna prova monopolista | Nessuna singola prova è sufficiente a determinare **più di 1** casella | T2, colonna "Casella/e" |
| NB-6 | Volume probatorio | **≥ 14 prove raccoglibili** nel caso | Conteggio `P-*` |
| NB-7 | Scarsità reale (Pilastro 2) | Costo-tempo della raccolta esaustiva **≥ 1,8 × B** | Somma dei costi dichiarati |
| NB-8 | Densità di deduzione | **≥ 8 passi `D-*`** nel caso, ≥ 5 dei quali con più di una premessa | Conteggio sul grafo |
| NB-9 | Anti-tiro sul timbro | Ogni gruppo di tre caselle contigue timbrabile ha `Π |dominio|` **≥ 100** | T1, per ciascuno dei 5 gruppi contigui |

**Nota su NB-9.** È il criterio che protegge il Pilastro 1. Se un gruppo di tre caselle ha 60 combinazioni, un giocatore ostinato lo bruteforza in una giornata reale e il timbro perde significato. La soglia 100 va verificata su *tutti* i gruppi contigui, non sulla media.

---

## 4. Criterio di ridondanza dei percorsi (bloccante)

> *"la scarsità non nasconde la verità, obbliga a sceglierne la strada"* — Pilastro 2.

### 4.1 Quante

- **≥ 3 catene deduttive** che raggiungono `C3` (chi): `K-A`, `K-B`, `K-C`.
- **≥ 2 catene** per ogni altra casella.

### 4.2 Cosa significa "indipendenti"

Non basta che siano scritte separatamente. Test formali:

- **RD-1 — Disgiunzione probatoria.** Per ogni coppia di catene: `|prove(Ki) ∩ prove(Kj)| ≤ 1`. Nessuna prova compare in tutte e tre le catene, con l'unica eccezione del fatto iniziale segnalato la mattina.
- **RD-2 — Disgiunzione delle fonti.** Le tre catene non possono dipendere tutte dallo stesso abitante né tutte dallo stesso luogo. Almeno **2 delle 3** partono da luoghi diversi e da interlocutori diversi.
- **RD-3 — Diversità di regola.** Le tre catene non possono usare tutte la stessa regola di inferenza dominante. Almeno **2 regole distinte** fra R1–R8 sul passo terminale delle tre catene. Tre alibi orari (tre R1) sono una catena sola travestita da tre.
- **RD-4 — Test di rimozione (il più severo, e il più utile).** Si rimuove dal caso, una alla volta:
  - ogni singola prova `P-*` → il caso resta risolvibile al 100%;
  - ogni singolo luogo `L-*` con tutte le sue prove → il caso resta risolvibile;
  - ogni singolo abitante `TES` con tutte le sue testimonianze → il caso resta risolvibile.

  Il designer allega la tabella degli esiti. Anche **un solo** elemento la cui rimozione rende il caso irrisolvibile è un collo di bottiglia: AP-06, REJECT.
- **RD-5 — Percorribilità individuale.** Ogni catena, presa da sola, ha costo-tempo **≤ 0,70 × B**. Una catena che da sola satura la giornata non è un'alternativa reale: è la strada obbligata con due decorazioni accanto.

### 4.3 Formato di consegna

`percorsi.md`, tabella per catena: `ID | prove usate | passi | luoghi toccati | interlocutori | regola terminale | costo-tempo (frazione di B)`, più la matrice di intersezione 3×3 e la tabella del test di rimozione.

---

## 5. Criterio di equità dei depistaggi (bloccante)

> Un falso indizio è legittimo. Un falso indizio non confutabile è un imbroglio.

### 5.1 Quantità

**2 ≤ depistaggi ≤ 4** per caso. Meno di 2: il caso è una linea retta. Più di 4: rumore, non deduzione.

### 5.2 Ogni depistaggio `F-nn` dichiara

| Campo | Obbligo |
|---|---|
| Ipotesi falsa indotta | Formulata come assegnazione di caselle, non come "sospetto" |
| Prova che lo genera | ID |
| Ragione difendibile in-fiction | Vincolo creativo 2: nessuno mente per depistare il giocatore. Movente della bugia esplicito |
| Confutatori `X-nn` | **≥ 2**, distinti, con ID, tipo, luogo e costo-tempo |

### 5.3 I quattro test di equità

- **EQ-1 — Esistenza del confutatore.** Ogni `F` ha ≥ 2 confutatori raccoglibili. Uno solo = un giocatore che quel giorno è andato altrove resta ingannato senza colpa: iniquo.
- **EQ-2 — Indipendenza dal senno di poi.** I prerequisiti di raccolta di ogni `X-nn` **non devono includere** l'aver incontrato `F`, né alcuna prova che compaia esclusivamente nella catena finale. Verifica meccanica: `prerequisiti(X) ∩ ({F} ∪ prove_esclusive_soluzione) = ∅`. Se il confutatore si sblocca solo dopo aver già sospettato il vero colpevole, il depistaggio è ornamentale.
- **EQ-3 — Costo di uscita limitato.** Costo-tempo per raggiungere il confutatore più economico di `F`: **≤ 0,25 × B**. Un depistaggio che costa mezza giornata per essere scartato non è un depistaggio, è una trappola.
- **EQ-4 — Reversibilità.** Imboccare un depistaggio e confutarlo deve lasciare **≥ 1 catena deduttiva completa** ancora percorribile nel tempo residuo. Si verifica sommando: costo del depistaggio + costo del confutatore + costo della catena più economica ≤ `B`.

### 5.4 Crepa obbligatoria per ogni bugia

Vincolo creativo 2 della visione, reso verificabile: ogni personaggio che mente ha una scheda `bugie.md` con `bugia | ragione | crepa (ID prova) | luogo della crepa | costo-tempo`. Una bugia senza crepa nominata con ID = REJECT.

---

## 6. Catalogo degli anti-pattern — rifiuto automatico

Ogni voce presente in un caso è motivo di rigetto. La riga di destra è il motivo per cui un giocatore di Obra Dinn o Golden Idol chiude il gioco.

| ID | Anti-pattern | Perché è fatale |
|---|---|---|
| AP-01 | Colpevole identificabile solo da un dettaglio fisico arbitrario (il mancino, la cicatrice, l'altezza) | Sostituisce la catena logica con una lotteria percettiva: si "vede" o non si vede, non si deduce |
| AP-02 | "Chi mente è colpevole" | Riduce il caso a un test di sincerità e contraddice il vincolo che ogni bugia abbia una ragione propria |
| AP-03 | La prova decisiva compare solo dopo aver già capito | Inverte la causalità del gioco: premia l'indovinare e poi conferma, mai il dedurre |
| AP-04 | Soluzione per convenzione di genere (il maggiordomo, il meno sospetto, il primo a essere scagionato) | Si vince conoscendo i gialli, non il caso: è metagioco, e chi ne legge molti si annoia in dieci minuti |
| AP-05 | Due colpevoli entrambi difendibili | Rompe irreparabilmente la fiducia nel sistema: se una volta il gioco è ambiguo, ogni deduzione successiva diventa scommessa |
| AP-06 | Collo di bottiglia: una prova senza la quale il caso è irrisolvibile | Con tempo scarso equivale a un fallimento casuale deciso a metà mattina |
| AP-07 | Salto di movente: da "aveva un motivo" a "è stato lui" | In un paese di nove persone i moventi si sovrappongono per progetto: il movente conferma, non individua |
| AP-08 | Confessione risolutiva: un PNG che, interrogato bene, dice la risposta | Sostituisce la deduzione con la ricerca del ramo di dialogo giusto |
| AP-09 | Anacronismo probatorio: impronte, balistica, autopsia rapida, telefonata di verifica | Rompe il vincolo 3 e, peggio, insegna al giocatore che le regole del mondo sono negoziabili |
| AP-10 | Richiesta di conoscenza extradiegetica (orari ferroviari reali, dialetto non glossato, nozioni agrarie) | Il giocatore perde per ignoranza di qualcosa che il gioco non gli ha dato: iniquo per definizione |
| AP-11 | Casella con dominio minuscolo (2–3 opzioni) | Il timbro si ottiene tirando a indovinare: distrugge l'anti-bruteforce del Pilastro 1 |
| AP-12 | Il quaderno registra conclusioni ("sembrava nervoso", "forse mentiva") invece di fatti | Il gioco pensa al posto del giocatore: viola il vincolo 4 e svuota l'unica meccanica |
| AP-13 | Coincidenza risolutiva: due eventi indipendenti che si allineano per far quadrare tutto | Il giocatore esperto la riconosce come l'autore che bara, non come il mondo che funziona |
| AP-14 | Depistaggio non confutabile, scartabile solo perché "non era quello" | Trasforma l'errore in arbitrio: il giocatore non impara nulla dall'aver sbagliato |
| AP-15 | Retro-deduzione: le caselle si riempiono solo dopo aver capito tutto il caso | Il timbro a gruppi di tre diventa un muro binario invece che una scala di progresso |
| AP-16 | Testimone onnisciente che ha visto tutto e va solo trovato | Il caso degrada da deduzione a caccia al tesoro, e il tempo diventa l'unico ostacolo |
| AP-17 | Ridondanza finta: tre catene che condividono la prova decisiva | Sembra robusto e ha un unico punto di rottura — è AP-06 nascosto sotto tre nomi |
| AP-18 | Esclusione totale non raccoglibile ("gli altri otto hanno un alibi") oltre il budget-tempo | Chiede una verifica che la giornata non consente: la soluzione è formalmente valida e praticamente irraggiungibile |
| AP-19 | Il numero magico: ore, somme o distanze che tornano solo assumendo una precisione impossibile nel 1954 | Il rigore apparente crolla appena il giocatore chiede "come faccio a saperlo al minuto?" |
| AP-20 | Punizione dell'esplorazione: una prova che confonde senza avere confutazione | Insegna a non guardare, cioè l'opposto di ciò che il gioco chiede |
| AP-21 | La casella verbale che non è un fatto (`perché` risolvibile solo interpretando l'animo di qualcuno) | Rende il verbale un tema di italiano invece di un documento verificabile |
| AP-22 | Dipendenza dall'ordine di raccolta: la stessa prova produce inferenze diverse secondo quando la trovi | Il caso non è un sistema di vincoli ma una sceneggiatura: la deduzione diventa non riproducibile |

---

## 7. Checklist di accettazione operativa

Da compilare per ogni caso. **Un solo NO = REJECT.** Nessun campo lasciato vuoto, nessun "parziale".

**Caso:** ________  **Revisione:** ____  **Data:** ____  **Validatore:** qa-lead

### A. Consegna (procedurale — se fallisce, l'esame si ferma qui)
| # | Controllo | SÌ/NO |
|---|---|---|
| A1 | `prova_unicita.md` presente con T1, T2, T3, T4 complete | |
| A2 | `grafo_deduttivo.md` presente, tutti i passi in forma canonica | |
| A3 | `percorsi.md` presente con matrice di intersezione e test di rimozione | |
| A4 | `bugie.md` presente per ogni personaggio che mente | |
| A5 | Tutti gli ID conformi a § 0; ogni prova classificata nella tassonomia | |
| A6 | Ogni prova ha luogo e costo-tempo dichiarati | |

### B. Unicità
| # | Controllo | SÌ/NO |
|---|---|---|
| B1 | Ogni casella ha `|dominio| ≥ 4`; `C3` include 9 abitanti + `ignoti` | |
| B2 | `|R| ≤ 48` ed enumerazione T3 completa, nessuna riga omessa | |
| B3 | Esattamente una riga di T3 è `SOLUZIONE` | |
| B4 | Ogni esclusione cita una prova; zero motivazioni di plausibilità | |
| B5 | Near-miss escluso da ≥ 2 prove, di cui ≥ 1 `DOC`/`ORA` | |

### C. Deducibilità
| # | Controllo | SÌ/NO |
|---|---|---|
| C1 | Ogni passo dichiara premesse per ID e una regola R1–R8 | |
| C2 | DAG: nessun orfano, nessun ciclo, nessuna foglia extradiegetica (G1–G3) | |
| C3 | Grep lessico proibito sul grafo: zero occorrenze (G4) | |
| C4 | Test del passo cieco superato su tutti i passi verso `C3` e `C6` + 30% campione | |
| C5 | Test di sostituzione: ogni passo su persona cade per tutti gli altri 8 abitanti | |
| C6 | `C7` (perché) dedotta con R5/R8, mai da caratterizzazione | |

### D. Non-banalità
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| D1 | Profondità verso `C3` | ≥ 4 | |
| D2 | Profondità altre caselle (max 1 eccezione a profondità 1) | ≥ 2 | |
| D3 | Prove concorrenti su `C3` / tipi diversi | ≥ 3 / ≥ 2 | |
| D4 | Riduzione massima da una singola prova | ≤ 60% | |
| D5 | Caselle determinate da una singola prova | ≤ 1 | |
| D6 | Prove raccoglibili totali | ≥ 14 | |
| D7 | Costo raccolta esaustiva | ≥ 1,8 × B | |
| D8 | Passi `D-*` totali / con ≥ 2 premesse | ≥ 8 / ≥ 5 | |
| D9 | Combinazioni per ogni gruppo di tre caselle contigue | ≥ 100 | |

### E. Ridondanza
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| E1 | Catene verso `C3` | ≥ 3 | |
| E2 | Catene verso ogni altra casella | ≥ 2 | |
| E3 | Intersezione probatoria per ogni coppia | ≤ 1 prova | |
| E4 | Nessuna prova comune a tutte e tre (salvo fatto iniziale) | — | |
| E5 | ≥ 2 catene con luogo e interlocutore d'ingresso diversi | — | |
| E6 | Regole terminali distinte fra le tre catene | ≥ 2 | |
| E7 | Test di rimozione: prova / luogo / testimone — caso sempre risolvibile | 0 fallimenti | |
| E8 | Costo-tempo di ogni singola catena | ≤ 0,70 × B | |

### F. Equità dei depistaggi
| # | Controllo | Soglia | SÌ/NO |
|---|---|---|---|
| F1 | Numero di depistaggi | 2–4 | |
| F2 | Confutatori per ogni depistaggio | ≥ 2 | |
| F3 | Nessun confutatore presuppone `F` o prove esclusive della soluzione (EQ-2) | — | |
| F4 | Costo del confutatore più economico | ≤ 0,25 × B | |
| F5 | Depistaggio + confutazione + catena più economica | ≤ B | |
| F6 | Ogni bugia ha ragione difendibile e crepa con ID | — | |

### G. Anti-pattern
| # | Controllo | SÌ/NO |
|---|---|---|
| G1 | Passata completa su AP-01…AP-22: nessuno presente | |
| G2 | Se presente, indicare ID e passo/prova coinvolti nel campo Note | |

### Esito
```
VERDETTO: PASS | REJECT
NO rilevati: <elenco ID controllo>
Anti-pattern rilevati: <elenco AP>
Azione richiesta al quest designer: <max 5 righe>
```

---

## 8. Procedura di validazione lato QA

Ordine fisso, si interrompe al primo blocco: **A** (procedurale) → **B** (unicità) → **C** (deducibilità) → **D**/**E**/**F** (soglie, calcolabili in parallelo) → **G** (anti-pattern, sempre eseguita per intero anche se il caso è già REJECT, così il designer riceve una lista completa).

Un caso respinto rientra con **numero di revisione incrementato** e la checklist precedente allegata. QA riesegue l'intera griglia, non solo i punti falliti: una correzione locale può rompere `|R|`, il test di rimozione o NB-9.

## 9. Dipendenze aperte

- Le soglie in frazione di `B` (NB-7, RD-5, EQ-3, EQ-4) diventano numeri assoluti solo quando `design-systems-designer` fissa i costi-tempo. **Fino ad allora nessun caso può ricevere PASS**: al massimo *PASS condizionato ai costi*, stato `review`.
- Il dominio di `C3` include `ignoti` per costruzione: se `dir-game-director` chiude la domanda aperta 2 della visione escludendo quella casella, B1 va aggiornato.
- La regola del timbro a gruppi di tre (NB-9) assume 7 caselle e 5 gruppi contigui. Se il modulo del verbale cambia forma, NB-9 va ricalcolato prima di validare qualunque caso.
