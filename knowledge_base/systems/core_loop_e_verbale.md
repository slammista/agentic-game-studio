---
role: design-game-designer
date: 2026-08-23
author: design-game-designer
status: draft
locked_by: null
depends_on:
  - knowledge_base/production/creative_vision.md
description: Specifica implementabile del loop della giornata, dell'anatomia del verbale a tre comma, della regola del timbro e del quaderno. Documento fondativo dei sistemi di Pietrafitta — vincolante per systems, world e quest designer.
---

# Core Loop e Meccanica del Verbale — Pietrafitta

## 0. Assiomi di sistema

| # | Assioma | Conseguenza operativa |
|---|---|---|
| A1 | **Il pensiero è gratis. Il movimento e la parola costano.** | Leggere, riordinare, compilare, cancellare, ipotizzare: 0 tempo. Spostarsi, chiedere, esaminare, consultare: tempo. |
| A2 | **Nessun costo è nascosto.** | Ogni azione mostra il costo e l'ora d'arrivo prima della conferma. |
| A3 | **Nessuna azione a vuoto.** | Ogni azione che consuma tempo produce ≥ 1 voce di quaderno. Anche il rifiuto di rispondere è un fatto. |
| A4 | **Il sistema non inferisce.** | Il quaderno ordina e filtra. Non conclude, non segnala contraddizioni, non valuta rilevanza. |
| A5 | **Il feedback è a gruppi, mai a casella.** | Nessuna meccanica può isolare la correttezza di una singola casella. Vedi §3.3. |

---

## 1. Struttura della giornata

### 1.1 Unità di tempo

| Elemento | Valore |
|---|---|
| Unità base | **la mezza** — mezz'ora, scandita dal campanile |
| Giornata | 06:00 → 18:00 |
| Budget totale | **24 mezze** |
| Azione tipo | 1 mezza (parlare con chi è disponibile, nel luogo dove ti trovi) |
| Mosse significative attese | 12–16 per giornata (azione + spostamento) |
| Durata reale sessione | 25–40 min |

Il tempo avanza **solo per azione del giocatore**. Non esiste timer reale. Un giocatore può restare due ore vere davanti al quaderno senza perdere una mezza.

### 1.2 Tabella dei costi (baseline — taratura fine a `design-systems-designer`)

| Verbo | Costo | Nota |
|---|---|---|
| **Spostarsi** — entro il borgo | 1 mezza | Luoghi contigui del centro |
| **Spostarsi** — borgo ⇄ periferia | 2 mezze | Poderi, strada alta, mulino |
| **Spostarsi** — periferia ⇄ periferia | 3 mezze | Non passa dal centro |
| **Ascoltare** — persona disponibile | 1 mezza | Chiacchierone, parte lesa, curioso |
| **Interrogare** — persona reticente | 2 mezze | Esito legato al tier di fiducia |
| **Insistere** — secondo passaggio con una leva | 2 mezze | Richiede una voce di quaderno come leva |
| **Esaminare** — luogo o oggetto | 1 mezza | Sopralluogo puntuale |
| **Consultare** — registro comunale, di consorzio, parrocchiale | 2 mezze | Un'ora piena di carte |
| **Attendere** — presidiare un luogo | 1 mezza per mezza | Per intercettare qualcuno al suo orario |

### 1.3 Azioni a costo zero (elenco chiuso)

Aprire e leggere il quaderno · filtrare e ordinare il quaderno · rileggere un documento già acquisito · compilare, cambiare o cancellare una casella del verbale · consultare la mappa e la tabella dei costi · scrivere postille personali · apporre il timbro (il timbro non consuma tempo, vedi §3).

### 1.4 Aperture e chiusure fisse

| Ora | Evento | Costo |
|---|---|---|
| 06:00 | **Segnalazione del fatto.** Consegna del modulo di verbale vuoto. | 0 |
| 06:00 | **Primo sopralluogo**, obbligatorio e gratuito. Fornisce ≥ 2 voci utili al Comma I. | 0 |
| 12:00 | **Rintocco di mezzogiorno.** Il modulo viene riletto ad alta voce: elenco delle caselle ancora in bianco. Non è un indizio, è una checklist. | 0 |
| 17:30 | **Ultima stesura.** Spostamenti e interrogatori si chiudono. Restano solo compilazione e timbro. | — |
| 18:00 | **La corriera.** Consegna. Vedi §5. | — |

### 1.5 Orari degli abitanti

Ogni abitante ha una collocazione per fascia di mezz'ora. Il tempo non è solo budget: è **scheduling**. Chi è al mulino alle 9 non c'è alle 15. Presidiare un luogo (§1.2, *Attendere*) è la contromossa esplicita. — Definizione a `design-world-designer`.

---

## 2. Anatomia del verbale

### 2.1 Il modulo

**9 caselle in 3 comma da 3.** I comma sono **fissi e non sovrapposti**. Non esiste finestra scorrevole (motivazione formale in §3.3).

```
COMMA I  — DEL FATTO
  Il giorno 〔1 ORA〕 in 〔2 LUOGO〕 si è verificato 〔3 ATTO〕

COMMA II — DELLE PERSONE
  ad opera di 〔4 RESPONSABILE〕 ai danni di 〔5 PARTE LESA〕
  servendosi di 〔6 MEZZO〕

COMMA III — DELLE RAGIONI
  per 〔7 MOVENTE〕 essendo che 〔8 CIRCOSTANZA〕
  come risulta da 〔9 FONTE〕
```

### 2.2 Tipizzazione e origine dei valori

| # | Casella | Tipo | Origine dei valori | "Ignoto" ammesso |
|---|---|---|---|---|
| 1 | ORA | ora | Quaderno | NON ACCERTATA |
| 2 | LUOGO | luogo | Quaderno | NON ACCERTATO |
| 3 | ATTO | qualificazione | **Lista chiusa prestampata sul modulo** (6 voci/caso) | — (obbligatoria) |
| 4 | RESPONSABILE | persona | Quaderno | **IGNOTI** |
| 5 | PARTE LESA | persona o bene | Quaderno | NON ACCERTATA |
| 6 | MEZZO | oggetto | Quaderno | NON ACCERTATO |
| 7 | MOVENTE | qualificazione | **Lista chiusa prestampata sul modulo** (8 voci) | NON ACCERTATO |
| 8 | CIRCOSTANZA | fatto abilitante | Quaderno (voci di tipo *opportunità*) | NON ACCERTATA |
| 9 | FONTE | persona o documento | Quaderno | NON ACCERTATA |

**Vincolo di provenienza (difesa strutturale n.2):** 7 caselle su 9 accettano **solo valori già presenti nel quaderno**. Non esistono menu onniscienti. Un nome mai raccolto non è scrivibile: il segretario non mette in un atto pubblico ciò che non ha sentito. Lo spazio delle mosse è nullo all'alba e cresce insieme alla capacità di dedurre.

ATTO e MOVENTE fanno eccezione perché sono **qualificazioni giuridiche del Ministero**, prestampate sul modulo. È anche il modo in cui il gioco rispetta A4: il quaderno non registra mai un movente (sarebbe una conclusione), registra il debito, la lite, la lettera.

### 2.3 Perché questo raggruppamento

1. **Ogni comma è un atto mentale autosufficiente.** I = ricostruire la scena. II = attribuire. III = dimostrare. Tre domande separate, non tre fette arbitrarie della stessa frase.
2. **Mappa 1:1 sulle tre catene deduttive indipendenti** richieste dalla vision (mitigazione del rischio "il giocatore si blocca"). Perdere un testimone chiude al massimo **un** comma, mai il verbale.
3. **Dentro il comma le tre caselle si vincolano a vicenda.** Ora + Luogo restringono gli Atti possibili; Responsabile + Mezzo restringono la Parte lesa; Movente + Circostanza determinano quale Fonte regga. Il timbro quindi conferma **una micro-teoria**, non tre fatti scollegati: è informazione utile, non un semplice check.
4. **Difficoltà crescente e ordinata.** Il Comma I è quasi sempre chiudibile con osservazione diretta; il II richiede l'incrocio degli orari; il III richiede il segreto, cioè la parte sociale del caso. Chi ha capito poco chiude comunque il primo: anti-frustrazione strutturale, non concessa dal sistema ma prodotta dalla forma del modulo.
5. **Nessuna casella è isolabile.** Con gruppi disgiunti, l'esito del timbro non è mai attribuibile a una casella singola. Con finestre scorrevoli lo sarebbe: vedi §3.3.

### 2.4 Lo stato "ignoto"

Tre stati distinti per casella, con esiti distinti alle 18:

| Stato | Significato | Timbrabile |
|---|---|---|
| **Compilata** | Il segretario afferma un valore | Sì |
| **Ignota** (`IGNOTI` / `NON ACCERTATO`) | Il segretario dichiara formalmente di non sapere | **Mai** |
| **In bianco** | Il segretario non si è espresso | No |

Regola vincolante: **una casella dichiarata ignota non è mai corretta, quindi il suo comma non si timbra mai.** Serve a chiudere l'exploit "riempi tutto di ignoti e guarda cosa si timbra". Non è una penalità: è la definizione stessa dello stato. Il costo di dichiarare ignoto è **sociale e narrativo** (§5.C), mai meccanico.

`IGNOTI` e `in bianco` non sono la stessa cosa e il gioco lo esplicita: l'ignoto è un atto di onestà, il bianco è un'omissione che la Pretura riempie al posto tuo, e la riempie male.

---

## 3. La regola del timbro

### 3.1 Quando scatta

Nel momento in cui la **terza casella di un comma riceve un valore** — cioè quando il comma è completo — il comma si autovaluta, istantaneamente e senza costo di tempo.

- **Tutte e tre esatte** → il timbro tondo del Comune si appone. Il comma si blocca in sola lettura per il resto della giornata.
- **Almeno una errata / ignota / (il comma non può essere completo con un bianco)** → nessun timbro. La riga viene **barrata a inchiostro** e si passa alla riga successiva.

Prima del completamento, il giocatore può riempire, svuotare e riordinare le caselle **all'infinito e gratis**. Il sistema interviene solo alla terza.

### 3.2 Cosa comunica esattamente

| Segnale | Significato letterale | Cosa NON dice |
|---|---|---|
| Timbro | Le tre voci di questo comma sono tutte esatte | — |
| Riga barrata | Almeno una delle tre è errata o ignota | Quante ne sbagli. Quali. Se ne hai una giusta. |

Nessun feedback graduato, nessun caldo/freddo, nessun conteggio parziale, nessuna animazione differenziata per "quasi". **Un solo bit per stesura.**

### 3.3 Perché i gruppi sono fissi e non scorrevoli

Ipotesi scartata: timbro su qualsiasi terna consecutiva 1..9 (7 finestre).

Controesempio che la uccide: con `1-2-3` timbrato, il giocatore cambia solo la casella 4 e testa la finestra `2-3-4`. Poiché 2 e 3 sono note corrette, l'esito di `2-3-4` rivela **la correttezza isolata della casella 4**. La finestra scorrevole degenera in un oracolo per casella singola e consente il brute force lineare (9 × valori invece di 3 × combinazioni). Viola A5 e il Pilastro 1 della vision.

**Gruppi disgiunti: l'esito è sempre e solo un predicato congiuntivo su tre incognite.** Nessuna sequenza di mosse produce informazione su una casella isolata.

### 3.4 Difesa n.3 — le tre stesure

Il modulo è un foglio di carta con la copia carbone. Si scrive a inchiostro.

> **Ogni comma ammette 3 stesure.** Una stesura si consuma solo quando il comma viene *completato* (terza casella riempita) e non si timbra.

- Stesura 1 fallita → riga barrata, si riscrive sotto. **Restano 2.**
- Stesura 2 fallita → seconda barratura. **Resta 1.**
- Stesura 3 fallita → **comma esaurito**: il modulo è deturpato, il comma va in Pretura come scritto nell'ultima stesura, non più modificabile.

Il contatore delle stesure residue è sempre visibile. Al riempimento della terza casella compare **conferma esplicita**: *«Chiudere il comma? Resta 1 stesura su 3.»* — nessun consumo accidentale (A2).

Esaurire un comma **non è game over**: gli altri due restano lavorabili fino alle 18.

Perché è la regola giusta e non una punizione: **compilare resta gratis e illimitato, solo l'affermazione è contata.** Il giocatore che ha ristretto la terza casella a due candidati ha 3 stesure e 2 candidati: il tentativo informato riesce sempre. Il sistema punisce il tiro a caso e perdona il dubbio ristretto.

**Un solo slot di salvataggio, automatico e continuo. Nessun salvataggio manuale, nessun ricaricamento del caso dal menu.** Senza questo, ogni difesa qui sopra è aggirabile.

### 3.5 Dimostrazione anti-forza-bruta

**Spazio teorico pieno** (tutti i valori del caso disponibili — scenario più favorevole all'attaccante):

| Comma | Cardinalità | Combinazioni |
|---|---|---|
| I | ORA 24 × LUOGO 8 × ATTO 6 | **1.152** |
| II | RESP 9 × LESA 13 × MEZZO 10 | **1.170** |
| III | MOVENTE 8 × CIRC 12 × FONTE 14 | **1.344** |
| **Verbale intero** | prodotto | **1.811.496.960** (≈ 1,81 miliardi) |
| **Costo brute force sequenziale** | somma (i comma sono indipendenti) | **3.666 tentativi**, ~1.833 attesi |

3.666 tentativi da 6 secondi l'uno = **~6,1 ore di clic** per una giornata di gioco che ne dura 0,5. Ma il numero non è la difesa principale: il punto è che **non c'è gradiente**. Ogni fallimento elimina 1 combinazione su 1.152, cioè lo 0,087% dello spazio. Discesa nulla.

**Spazio realistico** (quaderno di fine giornata, ipotesi conservativa — il giocatore ha già ristretto molto):

| Comma | Cardinalità ristretta | Combinazioni |
|---|---|---|
| I | 8 ore × 4 luoghi × 6 atti | **192** |
| II | 6 persone × 7 parti lese × 5 mezzi | **210** |
| III | 8 moventi × 6 circostanze × 7 fonti | **336** |

Con il tetto di 3 stesure per comma:

| Evento | Probabilità |
|---|---|
| Azzeccare il Comma I a caso | 3 / 192 = **1,56 %** |
| Azzeccare il Comma II a caso | 3 / 210 = **1,43 %** |
| Azzeccare il Comma III a caso | 3 / 336 = **0,89 %** |
| **Verbale intero corretto a caso** | 1,99 × 10⁻⁶ = **1 su ~502.000** |
| Almeno un comma azzeccato a caso | **3,84 %** — innocuo: un comma non rivela nulla degli altri |

**Bilancio informativo.** Identificare il Comma II richiede log₂(210) = **7,71 bit**. Una stesura fallita ne restituisce log₂(210/209) = **0,0069 bit**. Tre stesure = 0,0206 bit = **0,27 % dell'informazione necessaria.** Il canale di feedback è progettato per essere quasi muto: l'informazione deve venire dal paese, non dal modulo.

**Tre difese sovrapposte, ciascuna sufficiente a rendere non conveniente la forza bruta:**
1. Gruppi disgiunti → nessun feedback per casella singola (§3.3).
2. Vincolo di provenienza → lo spazio delle mosse è limitato a ciò che hai raccolto (§2.2).
3. Tre stesure per comma → il numero di affermazioni è finito e piccolo (§3.4).

---

## 4. Il quaderno

### 4.1 Cosa registra

Automaticamente, a costo zero, ogni volta che un'azione produce un'osservazione. **Solo fatti osservati, mai conclusioni** (vincolo 4 della vision).

Formato di una voce:

```
[TIPO]  Contenuto testuale del fatto
        — fonte · luogo · ora di raccolta
```

Esempi ammessi / vietati:

| Ammesso (fatto) | Vietato (conclusione) |
|---|---|
| «Bruni deve 40.000 lire al consorzio dal marzo scorso.» | «Bruni aveva un movente economico.» |
| «Marchetti dice di essere stato al mulino dalle 9 alle 12.» | «L'alibi di Marchetti non regge.» |
| «Alle 11 Marchetti non ha voluto rispondere.» | «Marchetti nasconde qualcosa.» |
| «La chiave del granaio era appesa in cucina.» | «Chiunque entrasse in cucina poteva aprire il granaio.» |

Il quaderno registra ciò che è **stato detto**, con la fonte. Non ciò che è vero. Due voci in contraddizione restano entrambe a quaderno, nessuna marcata come falsa.

### 4.2 Tipi delle voci

`PERSONA` · `ORA` · `LUOGO` · `OGGETTO` · `OPPORTUNITÀ` · `FONTE`

Coincidono con i tipi delle caselle del verbale: è ciò che rende il trascinamento tipizzato e inequivocabile. Non esistono voci di tipo `MOVENTE` né `ATTO` — sono qualificazioni del modulo, non osservazioni (§2.2).

### 4.3 Lettura e filtro (costo 0)

- **Per persona** — tutto ciò che riguarda un abitante.
- **Per ora** — la griglia della giornata: chi ha detto di essere dove, a che ora, secondo chi.
- **Per luogo** — tutto ciò che è stato osservato o riferito su un posto.

**Confine invalicabile (A4):** il quaderno **ordina**, non **inferisce**. Due dichiarazioni incompatibili sulla stessa fascia oraria appaiono affiancate perché l'ordinamento cronologico è un'operazione che il segretario può fisicamente fare con dei foglietti — ma **nessun colore, nessuna icona, nessun testo le etichetta come contraddizione**. Il giudizio è del giocatore.

Nessuna voce è mai marcata come rilevante o irrilevante. Il quaderno raccoglie anche il pettegolezzo inutile e non lo distingue.

### 4.4 Postille

Il giocatore può annotare testo libero su qualunque voce e in margine al quaderno. Le postille non sono mai leggibili dal sistema, mai trascinabili in una casella, mai valutate. Costo 0. Servono al giocatore esperto per tracciare ipotesi che il gioco si rifiuta di tracciare per lui.

### 4.5 Dal quaderno al verbale

1. Il giocatore apre il verbale e seleziona una casella.
2. La colonna del quaderno si filtra **automaticamente sul solo tipo di quella casella**. Nessun altro filtro, nessun ordinamento per probabilità.
3. Trascina la voce nella casella.
4. La casella mostra la **forma verbalizzata** (voce «Bruni Ottavio, mezzadro al podere Sant'Elena» → casella `OTTAVIO BRUNI`).
5. Sotto la casella resta un **rimando alla voce sorgente**, cliccabile: il giocatore può sempre risalire a *perché* ha scritto quel nome.

Trascinare non consuma tempo né stesure. La stesura si consuma solo al completamento del comma (§3.4).

---

## 5. Le ore diciotto

### 5.1 Sequenza

| Ora | Cosa accade |
|---|---|
| 17:30 | Rintocco d'avviso. **Ultima stesura**: spostamenti e interrogatori si chiudono. Restano compilazione e timbro. Il segretario scrive in piedi al banco della fermata. |
| 18:00 | La corriera. Il verbale è congelato. |
| Prima della consegna | **Il conto della busta**: il gioco dichiara quante caselle sono `timbrate` / `scritte non timbrate` / `dichiarate ignote` / `in bianco`. Nessuna informazione nuova (il timbro mancante era già visibile), ma il giocatore sa esattamente cosa sta consegnando (A2). |
| Consegna | Il verbale non è più modificabile. Nessuna schermata di esito, nessun punteggio, nessuna percentuale. |

### 5.2 I tre esiti

#### A — Completo e corretto (3 comma timbrati)

- La Pretura non richiede chiarimenti. Il fatto entra nei registri come lo hai scritto.
- La persona indicata è perseguita; la parte lesa è riconosciuta.
- **Accesso:** fiducia in aumento con la parte lesa e i suoi congiunti; in calo con i congiunti del responsabile. Nel caso successivo, almeno un testimone che avrebbe taciuto parla.
- Il gioco non dice «hai vinto». Il riscontro è l'epilogo del mattino dopo.

#### B — Completo e sbagliato (9 caselle piene, ≥ 1 comma non timbrato)

Il verbale è comunque atto pubblico. La Pretura procede su quanto scritto.

| Errore | Conseguenza |
|---|---|
| Casella 4 `RESPONSABILE` errata su persona reale | **Errore giudiziario.** L'accusato è segnato, la sua famiglia chiude la porta. Il colpevole reale resta libero e nel caso seguente è più cauto (Pilastro 3). |
| Casella 4 corretta, errori altrove | Il fatto è attribuito bene ma raccontato male: attenuanti immeritate, oppure un `MOVENTE` sbagliato che diffama qualcuno. Conseguenza minore ma reale. |
| Comma I errato, II corretto | L'atto è contestato nella ricostruzione: il procedimento si trascina, il colpevole ha tempo. |

Nessun testo dice mai «sbagliato». Il giocatore lo scopre dalle conseguenze.

**Verifica differita:** esiste il **Registro degli Atti**. A fine slice (dopo il terzo caso) il giocatore può rileggere i tre verbali depositati con annotato ciò che è emerso dopo. Un giocatore di deduzione deve poter verificare il proprio ragionamento — ma **mai durante**, sempre dopo.

#### C — Parziale o con ignoti

| Stato della casella | Trattamento in Pretura |
|---|---|
| **In bianco** | La Pretura la completa **d'ufficio**, con il valore socialmente più comodo: il forestiero, il pregiudicato, il povero. **Deterministico, mai casuale** — il valore d'ufficio di ogni casella è definito per caso da `design-quest-designer`. Questa è la vera punizione del bianco. |
| **`IGNOTI` / `NON ACCERTATO`** | La Pretura **non** completa d'ufficio. Il fatto resta a carico di ignoti. **Nessun innocente colpito.** |

Costo dell'ignoto — sociale, mai meccanico:
- Il caso resta aperto: il colpevole torna, più cauto.
- Chi si aspettava giustizia (parte lesa, congiunti) perde fiducia nel segretario. **Perdita di accesso mirata**, non generica: chiude una porta specifica, individuata dal quest designer.

Comma parzialmente compilato: si applica casella per casella. Il comma non è mai timbrabile con bianchi o ignoti.

**Gerarchia degli esiti**, dal migliore al peggiore: `timbrato` > `scritto e corretto ma non timbrabile per un ignoto nello stesso comma` > `dichiarato ignoto` > `scritto e sbagliato` > `in bianco`.
Il bianco è peggio dell'errore perché delega la scelta a chi sceglierà sempre il più debole.

---

## 6. Anti-frustrazione — garanzie vincolanti

| # | Garanzia | Vincolo per chi |
|---|---|---|
| G1 | **Nessuna azione a vuoto.** Ogni azione che costa tempo produce ≥ 1 voce di quaderno, anche solo «X ha rifiutato di rispondere alle 11». | quest designer |
| G2 | **Il Comma I è quasi garantito.** Il sopralluogo gratuito delle 06:00 fornisce da solo ≥ 2 delle 3 voci del Comma I. Nessun caso può avere il Comma I irrisolvibile prima delle 12:00. | quest designer |
| G3 | **Tre catene indipendenti**, mappate 1:1 sui tre comma. Perdere un testimone chiude al massimo un comma. | quest designer |
| G4 | **Rintocco delle 12** come checklist, non come indizio: rilegge le caselle in bianco, non suggerisce cosa metterci. | narrative designer |
| G5 | **Nessun timer reale.** Il tempo avanza solo per azione. | — |
| G6 | **Nessuna perdita accidentale.** Conferma esplicita prima di consumare una stesura. | UI/UX |
| G7 | **Nessun game over.** Il caso successivo parte comunque, dalla situazione che hai creato. | — |
| G8 | **Nessuna statistica risolve nulla.** Non esiste tiro, abilità o percentuale in tutto il documento. | tutti |

---

## 7. Requisiti di verifica per `qa-lead`

| # | Requisito | Criterio di fallimento |
|---|---|---|
| V1 | **Unicità per casella.** Per ogni casella esiste esattamente un valore corretto; ogni altro valore presente nel quaderno è **falsificabile** con almeno una prova raggiungibile nella giornata. | Esiste un valore alternativo difendibile e non falsificabile → il caso non entra in produzione. |
| V2 | **Nessuna terna alternativa timbrabile.** Nessun comma ammette due terne corrette. | Doppio timbro possibile. |
| V3 | **Risolvibilità entro 24 mezze.** Esiste almeno un percorso da ≤ 24 mezze che chiude tutti e tre i comma, e ne esistono ≥ 3 distinti (uno per catena). | Percorso unico o costo > 24. |
| V4 | **Nessuna inferenza automatica.** Nessun filtro o ordinamento del quaderno produce un giudizio (contraddizione, rilevanza, sospetto). | Presenza di marcatura valutativa. |
| V5 | **Copertura d'ufficio.** Ogni casella di ogni caso ha un valore d'ufficio della Pretura definito. | Casella senza valore d'ufficio. |
| V6 | **Annuncio del costo.** Nessuna azione consuma tempo senza averlo dichiarato prima. | Costo non mostrato in preview. |

---

## 8. Dipendenze in uscita

| Destinatario | Cosa serve | Blocca |
|---|---|---|
| `design-systems-designer` | Taratura definitiva della tabella §1.2; tier di fiducia e regole di accesso; parametrizzazione del completamento d'ufficio | Bilanciamento del budget 24 |
| `design-world-designer` | 8 luoghi con matrice delle distanze in mezze; 9 abitanti con orario per fascia di mezz'ora e tier di reticenza | §1.2, §1.5, V3 |
| `design-quest-designer` | Per ogni caso: mappatura delle 9 soluzioni sulle 3 catene; liste chiuse `ATTO` (6) e `MOVENTE` (8); valori d'ufficio; garanzie G1–G3 | V1, V2, V3, V5 |
| `narr-narrative-designer` | Giustificazione diegetica del timbro; testo delle barrature; epiloghi dei tre esiti; testo del rintocco delle 12 | §3.1, §5.2, G4 |
| `viz-ui-ux-artist` | Modulo a 3 comma × 3 righe di stesura; contatore stesure residue; quaderno tipizzato con drag e rimando alla voce sorgente; il conto della busta | Priorità massima da vision |
