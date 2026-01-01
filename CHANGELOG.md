# Changelog – cher-llm-simulator

## v1.0 – Didaktische Referenzversion

### Zielsetzung
v1 dient der erklärbaren Visualisierung zentraler Konzepte moderner
Large Language Models (LLMs).  
Der Fokus liegt auf Nachvollziehbarkeit, Reproduzierbarkeit und didaktischer
Klarheit – nicht auf realistischer Modellinferenz.

### Enthaltene Funktionen

#### Pipeline & Visualisierung
- Klar strukturierte Pipeline:
  Input → Tokenisierung → Embeddings → Attention → MLP → Logits → Decoding → Summary
- Schrittweise Navigation mit erklärenden Texten pro Pipeline-Stufe
- Kontextsensitiver Fokus je Schritt (didaktische Perspektive)

#### Szenarien (Guided Mode)
- Kuratierte Szenarien mit:
  - vorgegebenem Prompt-Stack
  - expliziter Tokenisierung
  - deterministischer Ausgabe
- Lernziele und Fokus je Szenario
- Override-Mechanismus für schrittweise Fokustexte

#### Sandbox (v1)
- Freie Texteingabe
- Sichtbarer technischer Ablauf
- **Keine semantische oder inhaltliche Garantie**
- Bewusst als UI-Gerüst für spätere Versionen ausgelegt

#### Erklärungen & Summary
- Konsistente, IT-affine Erklärtexte
- Klar abgegrenzte Hinweise zu Vereinfachungen
- Zusammenfassung mit:
  - Prompt-Stack
  - Ausgabe
  - Verarbeitungsweg
  - zentralen Erkenntnissen
  - Run-Snapshot

### Bewusste Vereinfachungen in v1

- Keine echte LLM-Inference
- Keine echten Modellgewichte
- Keine echte Tokenizer-Implementierung (BPE o. ä.)
- Deterministische, seeded Simulation
- Stark reduzierte Dimensionen (d_model, Heads, Layer)
- Sandbox ohne inhaltlich sinnvolle Antworten

Diese Vereinfachungen sind **Absicht** und Teil des didaktischen Konzepts.

### Nicht Teil von v1 (Ausblick)

- Stochastisches Sampling mit reproduzierbarer Historie
- Szenario-übergreifende Vergleichsläufe
- Erweiterte Sandbox mit konfigurierbarer Simulation
- Persistente Runs / Exporte
- Mehrsprachige Szenarien

### Status
v1 gilt als stabil und inhaltlich abgeschlossen.
