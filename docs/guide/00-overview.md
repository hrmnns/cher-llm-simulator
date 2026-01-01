# LLM Simulator – Dokumentationsübersicht

## Zweck dieser Dokumentation

Diese Dokumentation beschreibt den **LLM Simulator by cherware.de** in seinem **Referenzstand v1.3.40**.  
Ziel ist es, den technischen Verarbeitungsweg eines Large Language Models **schrittweise, erklärbar und reproduzierbar** darzustellen – ohne Anspruch auf Modelltreue oder semantische Korrektheit.

Die Dokumentation richtet sich an **IT-affine Nutzer**, die verstehen möchten,

- wie ein Prompt technisch verarbeitet wird,
- welche Zwischenschritte dabei existieren,
- und welche Effekte sich durch das Verändern von Parametern beobachten lassen.

## Was der LLM Simulator ist

Der LLM Simulator ist eine **didaktische Simulation** zentraler LLM-Grundprinzipien.  
Er visualisiert den Weg eines Texteingangs durch eine vereinfachte Pipeline:

**Eingabe → Tokenisierung → Embeddings → Attention → MLP → Logits → Decoding → Zusammenfassung**

Dabei liegt der Fokus auf:

- Transparenz statt Ergebnisqualität  
- Mechanik statt Bedeutung  
- Beobachtbarkeit statt Optimierung  

Alle Berechnungen sind **seeded**, **deterministisch** oder **szenariobasiert**, um Effekte reproduzierbar erklären zu können.

## Was der LLM Simulator nicht ist

Der Simulator ist **kein echtes Sprachmodell**. Insbesondere:

- keine echte Inferenz  
- keine realen Modellgewichte  
- keine Aussage über Qualität, Wahrheit oder Sinnhaftigkeit von Antworten  
- keine vollständige oder exakte Transformer-Implementierung  

Die erzeugten Ausgaben sind entweder:
- **vorgegeben** (Guided-Modus) oder
- **bewusst inhaltsleer / technisch** (Sandbox-Modus)

## Guided vs. Sandbox – Grundprinzip

### Guided Mode
- Kuratierte Referenzszenarien  
- Vorgegebene Tokenisierung und Ausgabe  
- Fokus auf **Erklärung, Vergleichbarkeit und Reproduzierbarkeit**  
- Empfohlener Modus für das Verständnis der Pipeline  

### Sandbox Mode
- Freie Texteingabe  
- Klare Warnung: **keine semantische Garantie**  
- Dient primär als UI- und Denkgerüst  
- In v1 bewusst unvollständig (Platzhalter für v2)

## Aufbau der Dokumentation

Die Dokumentation ist entlang der **Pipeline** und der **beobachtbaren Parameterwirkungen** strukturiert.

### Überblick über die Dokumente

- **00-overview.md**  
  Einordnung, Abgrenzung, Navigationshilfe  

- **01-pipeline.md**  
  Beschreibung aller Pipeline-Schritte:
  - was passiert technisch  
  - was ist in der App sichtbar  
  - was kann beobachtet werden  

- **02-parameters-embeddings.md**  
  Wirkung früher Parameter (z. B. `d_model`, Positional Encoding)

- **03-parameters-attention-mlp.md**  
  Kontextbildung, Attention-Gewichtung, MLP-Vergleich, Delta-Effekte

- **04-parameters-logits-decoding.md**  
  Logits, Wahrscheinlichkeiten, Sampling, Temperature, Top-K, Top-P, Seed

## Dokumentationsprinzipien

Diese Dokumentation folgt bewusst festen Leitplanken:

- **App-nah**: Es wird nur beschrieben, was in der App tatsächlich existiert.  
- **Beobachtungsorientiert**: Fokus auf „Was sehe ich?“ statt „Was sollte sein?“  
- **Didaktisch reduziert**: Vereinfachung ist explizit, nicht implizit.  
- **Versionsgebunden**: Aussagen beziehen sich immer auf einen konkreten App-Stand.  
- **Ohne Marketing-Sprache**: Keine Versprechen, keine Bewertungen, keine Überhöhung.

## Referenzstand

Diese Dokumentation bezieht sich auf:

- **LLM Simulator by cherware.de**  
- **Version:** v1.3.40  
- **Codebasis:** Single-File `index.html`  
- **Szenarien:** `scenarios/scenarios.json` (Guided Mode)

Abweichungen in späteren Versionen werden explizit dokumentiert.

## Wie diese Dokumentation zu lesen ist

Die Dokumente sind **nicht als Tutorial** gedacht.  
Sie sollen ermöglichen:

- gezieltes Nachschlagen  
- bewusstes Experimentieren  
- saubere mentale Modelle über LLM-Abläufe  

Empfohlenes Vorgehen:
1. Overview lesen  
2. Pipeline einmal vollständig durchgehen  
3. Danach gezielt Parameterwirkungen untersuchen  
