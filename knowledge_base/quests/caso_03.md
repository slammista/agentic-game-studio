---
role: quests
date: 2026-08-24
author: dir-game-director
status: draft
locked_by: null
description: Caso 3 della vertical slice — "Protocollo 217". Morte del Cav. Amilcare Rovina. Caso terminale: il verbale deve qualificare una morte che tre persone hanno interesse a far passare per naturale, e la circostanza abilitante è un atto del protagonista stesso.
depends_on:
  - knowledge_base/production/creative_vision.md
  - knowledge_base/systems/core_loop_e_verbale.md
  - knowledge_base/systems/economia_tempo_e_fiducia.md
  - knowledge_base/regions/pietrafitta.md
  - knowledge_base/characters/abitanti_pietrafitta.md
  - knowledge_base/qa_reports/standard_rigore_casi.md
  - knowledge_base/quests/caso_01.md
  - knowledge_base/quests/caso_02.md
---

# Caso 3 — Protocollo 217

**Posizione nella slice:** terzo e ultimo, ordine fisso.
**Escursioni fuori dal centro richieste: UNA** (facoltativa su una delle tre catene). Verifica RD-10 in §7.

## 1. Il fatto (verità oggettiva)

Il Cavalier Amilcare Rovina è trovato morto nel suo studio alle 17:20, dalla governante. Il dott. Bardi constata alle 17:50 un **collasso cardiaco** e firma. Il paese si prepara a un funerale imponente.

La constatazione è falsa e Bardi lo sa. Rovina si è ucciso con il veronal che Bardi stesso gli prescriveva da due anni, fra le 13:30 e le 15:30, nella sua finestra di riposo. Il bicchiere è stato lavato dalla governante prima che arrivasse chiunque, per decoro, senza malizia — è una figura d'ambiente e non prova nulla, ma il suo gesto spiega perché non c'è residuo.

**Perché quel giorno.** Tre giorni fa Aldo Fenaroli è salito in canonica e ha chiesto a don Alceste, per la seconda volta in vita sua, di chi fosse figlio. Il parroco ha taciuto di nuovo. Ma ha commesso l'unico errore della sua vita da prete: **ha avvisato Rovina**, per pietà, perché si preparasse.

E c'è la seconda metà, quella che riguarda il giocatore. Nel registro delle richieste d'archivio del municipio — che il segretario compila di propria mano ogni volta che estrae un fascicolo — c'è una riga con la data di ieri e il numero **217**.

Rovina passava ogni mattina dalla piazza. Il municipio è a un minuto. Il registro delle richieste è pubblico.

**Ha capito che il segretario stava per arrivarci.**

Il vero oggetto del verbale non è dunque la morte, che nessuno ha causato per mano altrui, ma la **falsa constatazione** di Bardi — l'unico reato commesso da un vivo in questa giornata.

## 2. La soluzione unica del verbale

| # | Casella | Valore corretto |
|---|---|---|
| 1 | ORA | Ore 17:50 (constatazione), fatto principale fra le 13:30 e le 15:30 |
| 2 | LUOGO | Studio di casa Rovina |
| 3 | ATTO | Falsa constatazione di decesso |
| 4 | RESPONSABILE | Elio Bardi |
| 5 | PARTE LESA | La fede pubblica |
| 6 | MEZZO | Certificato di morte per causa naturale |
| 7 | MOVENTE | Timore di pubblica rivelazione |
| 8 | CIRCOSTANZA | Le cambiali del responsabile nelle mani del defunto |
| 9 | FONTE | Ricettario a madre e figlia, veronal, ultime tre spedizioni |

**ATTO (6 voci, questo caso):** omicidio · istigazione al suicidio · **falsa constatazione di decesso** · omissione di referto · morte per causa naturale · somministrazione colposa di medicinali.

Il MOVENTE resta la lista unica di slice (LC-0).

## 3. Dimostrazione di unicità

### T1 — Domini dichiarati

| Casella | Candidati |
|---|---|
| ORA | 13:30–15:30 · 15:30–17:00 · **17:50** · 17:20 (ritrovamento) |
| LUOGO | **studio Rovina** · camera · loggia · osteria |
| ATTO | le 6 voci |
| RESPONSABILE | **Bardi** · Aldo · Don Alceste · Nerina · il defunto stesso · IGNOTI |
| PARTE LESA | **la fede pubblica** · Aldo Fenaroli · gli eredi · Amilcare Rovina |
| MEZZO | **certificato di morte naturale** · veronal · cambiali · il registro d'archivio |
| MOVENTE | le 8 voci |
| CIRCOSTANZA | **le cambiali in mano al defunto** · la richiesta del protocollo 217 · la visita di Aldo in canonica · l'assenza di residui nel bicchiere |
| FONTE | **ricettario a madre e figlia** · registro condotta · matrici certificati · don Alceste · registro richieste d'archivio |

### T2 — Eliminazione per vincolo

**Comma I.** Il fatto giuridicamente perseguibile non è la morte ma l'atto che la certifica. Il collasso cardiaco è escluso dal **ricettario a madre e figlia**, obbligatorio per gli ipnotici: le ultime tre spedizioni di veronal a Rovina sono ravvicinate e crescenti, e l'ultima è di ieri. Un medico che ha spedito quella quantità e constata un collasso senza disporre l'ispezione **sa** ciò che scrive. Chi qualifica «morte per causa naturale» sta trascrivendo il certificato invece di verificarlo; chi qualifica «omicidio» non trova né mezzo né esecutore in alcun dominio.

**Comma II.** Bardi è l'unico che possa commettere questo atto: è l'unico medico condotto. La parte lesa non è Rovina né gli eredi — nessuno ha subito danno patrimoniale — ma la fede pubblica, perché il reato è la falsità in atto. Il mezzo è il certificato, non il veronal: il veronal è il mezzo della morte, che non è il fatto contestato.

**Comma III.** Il movente non è il denaro né la protezione del defunto. Bardi firma perché **le proprie cambiali sono nello studio del morto**: alla morte di Rovina quelle carte passano agli eredi, e un'ispezione sul cadavere significa magistrato in casa, inventario dello studio, cambiali alla luce. La circostanza è esattamente quella. La fonte è il documento che regge da solo: il ricettario, che è a madre e figlia e quindi non falsificabile a posteriori.

### T3 — Residuo
Una sola assegnazione sopravvive per comma. «Istigazione al suicidio» cade perché richiede un istigatore: don Alceste ha avvisato Rovina per pietà, e l'avviso di una verità che sta per emergere non è istigazione in nessuna lettura del dominio raccoglibile.

### T4 — Coerenza cross-comma
Il MOVENTE (timore di rivelazione) e la CIRCOSTANZA (cambiali nello studio) esigono un RESPONSABILE che abbia carte in quello studio: solo Bardi e Nerina, e Nerina non firma certificati. Il MEZZO (certificato) esige l'ORA delle 17:50.

### T5 — Near-miss

| Comma | Near-miss | Perché cade |
|---|---|---|
| I | ATTO = morte per causa naturale | È la tesi del certificato. Il ricettario la falsifica |
| II | PARTE LESA = Aldo Fenaroli | Aldo perde un padre che non sapeva di avere, ma non è leso dall'atto falso |
| III | MOVENTE = stato di necessità | Il movente di Bardi è la paura, non il bisogno: le cambiali non si estinguono con la firma |

## 4. Le tre catene deduttive indipendenti

**Catena A — Comma I (documentale sanitaria).** Ricettario a madre e figlia → tre spedizioni di veronal, crescenti, l'ultima di ieri → incompatibilità con la causa certificata. *Interamente al municipio (registro della condotta e ricettario sono depositati là).*

**Catena B — Comma II (documentale amministrativa).** Matrici dei certificati di Bardi contro registro della condotta: undici certificati senza visita corrispondente. Stabilisce che quella firma è già stata venduta prima d'ora. *Municipio.*

**Catena C — Comma III (sociale e d'archivio).** Le cambiali: se lo studio è accessibile, direttamente; altrimenti dal libro dei debiti dell'osteria (Bardi deve 3.200 a Nerina) e dalla memoria di Nerina sulle carte che Rovina teneva. In alternativa: **protocollo 217**, che spiega perché Rovina fosse arrivato al punto, e che stabilisce la circostanza per via indipendente. *Municipio o osteria: nessuna salita.*

**Verifica del vincolo 8:** il Comma III ha tre vie di cui due documentali. Se Nerina è chiusa per l'esito del Caso 1 e lo studio è chiuso per l'esito del Caso 2, resta il protocollo 217, che è **accessibile al solo protagonista per diritto d'ufficio** e non dipende da nessuna fiducia. La catena di riserva del caso terminale è deliberatamente inchiudibile: nessun esito precedente può murare il giocatore.

## 5. I depistaggi e le loro confutazioni

| # | Depistaggio | Perché è plausibile | Confutazione |
|---|---|---|---|
| D1 | **Aldo Fenaroli** ha ucciso il padre naturale scoperto | Movente enorme, nessun alibi, ed è salito in paese quel giorno | Il libretto della roggia e i clienti collocano la macina; ma soprattutto **Aldo non sa ancora del 1944**. Il movente attribuitogli richiede una conoscenza che non ha, e il registro delle richieste d'archivio prova che il 217 non è mai stato estratto da altri che dal segretario |
| D2 | **Don Alceste** — ha avvisato Rovina, dunque ha voluto la sua morte | L'avviso è reale e il parroco lo ammetterà, con dolore | L'istigazione esige la volontà dell'evento. La sua finestra 13:00–15:00 è cieca ma il palazzo Rovina è sulla piazza, e alle 15:00 è al confessionale visto da tutti. Nessuna via d'accesso allo studio |
| D3 | **Nerina Vaccari** — la cambiale in bianco muore con lui | Movente economico netto e finestra del giovedì | La cambiale in bianco **non si estingue** con la morte: passa agli eredi ed è più pericolosa. La sua morte la danneggia. Verificabile sul libro dei debiti e sulla natura del titolo |

## 6. Esito e chiusura della slice

| Esito | Effetto |
|---|---|
| **Corretto** (Bardi, falsa constatazione) | Il medico è radiato e il paese resta senza condotta. Ma il verbale, per reggere, **nomina il veronal e la mano che l'ha preso**: Pietrafitta scopre che il Cavaliere si è ucciso, e comincia a chiedersi perché. Il 217 esce dall'archivio da solo |
| **ATTO = omicidio su Aldo** | Un innocente che non sapeva di essere figlio viene processato per parricidio. È l'esito più crudele possibile della slice, ed è pienamente raggiungibile: tutte le apparenze lo sostengono |
| **ATTO = morte per causa naturale** | Il verbale conferma il certificato. Bardi resta, le cambiali spariscono nell'inventario, il 217 torna a dormire. Il paese non saprà mai niente, e il segretario ha fatto esattamente il lavoro che ci si aspettava da lui. **Non è un fallimento meccanico: è la fine più amara** |
| **IGNOTI sul responsabile** | La Pretura archivia. Il segretario ha dichiarato di non sapere, ed è vero. Onestà senza giustizia |
| **In bianco** | Completamento d'ufficio: la Pretura scrive **Aldo Fenaroli**, marginale, senza protettori, presente sul luogo. Il verbale che il segretario non ha scritto condanna il figlio del morto |

## 7. Verifica dei vincoli di composizione

| Vincolo | Esito |
|---|---|
| **RD-10 / TC-2** | **Una escursione al massimo, e facoltativa.** Tutte e tre le catene si chiudono fra L1 municipio, L4 osteria e casa Rovina (piazza). La salita al mulino serve solo a confutare D1, e D1 è confutabile anche dal registro delle richieste d'archivio, in centro |
| **FT-2** (dorsale T0) | Catene A e B interamente documentali al municipio, accessibili per diritto d'ufficio. Il protagonista non ha bisogno di alcuna fiducia guadagnata per chiudere due commi su tre |
| **RD-9 / TC-1** | Quattro azioni condivise: il registro della condotta serve al I e al II; il ricettario al I e al III; il libro dei debiti al II e al III; il 217 al III e alla confutazione di D1 |
| **FT-3** | Il fatto principale cade nella fascia cieca 13:30–15:30, ma **nessuna casella dipende da testimonianza in quella fascia**: il Comma I si chiude sul ricettario, il II sulle matrici, il III sulle cambiali o sul 217 |
| **Vincolo 7** | Il sopralluogo delle 06:00 nello studio dà 4 candidati ORA (13:30–15:30 / 15:30–17:00 / 17:20 / 17:50) e 3 LUOGO (studio / camera / loggia). Il ritrovamento non è il fatto, e il bicchiere lavato impedisce che una coppia si determini |
| **Vincolo D5** (trasferta Roccalta) | Le ricevute della pompa di benzina **corroborano** Bardi ma non sono mai necessarie: la catena B le sostituisce integralmente. Conforme alla ratifica del Director |

## 8. Il filo dei tre casi

Caso 1: un uomo ruba per pagare un sanatorio, e la vittima non sa di essere vittima.
Caso 2: un uomo brucia per nascondere, e il paese legge odio dove c'era paura.
Caso 3: un uomo firma il falso per proteggere sé stesso, e un altro è morto perché **il segretario ha chiesto un fascicolo**.

La progressione non è di gravità, è di **implicazione**. Nel primo il protagonista osserva. Nel secondo interpreta. Nel terzo scopre che la propria diligenza è una delle circostanze del fatto — e deve decidere se scriverlo nel verbale, sapendo che la casella CIRCOSTANZA accetta il valore «richiesta d'archivio del 217, registrata a nome del segretario».

**Quella riga è compilabile.** È la scelta finale della slice, e nessun sistema la giudica: il timbro scatta comunque, perché è vera.

Consegna a `narr-narrative-designer`: l'ultima schermata non è la Pretura. È la corriera delle 18 che parte, e il segretario che resta sulla piazza.
