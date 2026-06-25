# ROLES_INDEX — mappatura ruoli unici da PRE-PRODUZIONE.md

70 righe di task nel documento originale → **49 ruoli univoci**.

## Decisioni di deduplicazione applicate

1. **Ruoli ricorrenti su più fasi** (es. Quest Designer appare in Pre-Produzione, Produzione Narrativa, Post-lancio) → **un solo agente**, responsabilità unite.
2. **Combo "A / B" sulla stessa riga, nessuna delle due in RUOLI DIRETTIVI** → trattate come **etichetta composta unica**, niente split (es. `Video Editor / Marketing Artist`, `Sound Designer / Audio Programmer` → confluito nel solo Sound Designer già esistente).
3. **Eccezione alla regola 2** — quando una delle due metà del combo compare ESPLICITAMENTE nella tabella RUOLI DIRETTIVI (TRASVERSALI) come ruolo distinto, è stata **splittata**:
   - `Producer / Product Manager` (Pre-Prod, riga 2) + `Producer / Project Manager` (Pre-Prod, riga 17) → **Producer** (assorbe analisi di mercato) + **Project Manager** (assorbe pianificazione milestone), perché RUOLI DIRETTIVI separa "Produzione → Producer" da "Gestione progetto → Project Manager".
   - `Lead Programmer / Technical Director` → **Lead Programmer** (esecuzione) + **Technical Director** (direzione tecnica, RUOLI DIRETTIVI).
   - `Lead Programmer / QA` (Post-lancio, patch e bugfix) → confluito in Lead Programmer + QA Tester già esistenti, nessun nuovo ruolo.
   - `QA Tester / Systems Designer` (test bilanciamento) → confluito nei due ruoli già esistenti.
   - `Community Manager / QA Lead` (beta testing pubblico) → confluito nei due ruoli già esistenti.
4. **Art Director** non appare nella tabella task-per-task ma è presente in RUOLI DIRETTIVI → aggiunto come agente direttivo a sé, orchestratore della macroarea Visual/Audio.

## I 49 agenti, per macroarea

### Direzione (7) — orchestratori, riportano a `dir-game-director`
dir-game-director · dir-producer · dir-project-manager · dir-lead-game-designer · dir-narrative-director · dir-art-director · dir-technical-director

### Design (7) — orchestratore: dir-lead-game-designer
design-world-designer · design-game-designer · design-systems-designer · design-quest-designer · design-character-designer · design-level-designer · design-encounter-designer

### Narrativa (7) — orchestratore: dir-narrative-director
narr-narrative-designer · narr-lore-designer · narr-dialogue-writer · narr-character-writer · narr-lore-writer · narr-content-writer · narr-technical-designer

### Visual/Audio (11) — orchestratore: dir-art-director
viz-concept-artist · viz-3d-character-artist · viz-3d-environment-artist · viz-texture-artist · viz-rigger · viz-animator · viz-ui-ux-artist · viz-vfx-artist · viz-technical-artist · viz-sound-designer · viz-composer

### Programmazione (6) — STUB, orchestratore: dir-technical-director
prog-lead-programmer · prog-gameplay-programmer · prog-ui-programmer · prog-ai-programmer · prog-tools-programmer · prog-audio-programmer

### QA (4) — gate trasversale, orchestratore: qa-lead
qa-lead · qa-tester · qa-narrative · qa-ux-researcher

### Business/Lancio (7) — orchestratore: dir-producer
biz-marketing-manager · biz-video-editor-marketing-artist · biz-pr-manager · biz-community-manager · biz-data-analyst · biz-live-ops-producer · biz-customer-support-specialist

**Totale: 7+7+7+11+6+4+7 = 49**
