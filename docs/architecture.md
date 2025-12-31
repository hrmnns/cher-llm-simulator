# Architektur – cher-llm-simulator

## Ziel dieses Dokuments

Dieses Dokument beschreibt die **technische und strukturelle Architektur** des Projekts *cher-llm-simulator*.

Es dient als Referenz für:
- die Implementierung der WebApp
- die Weiterentwicklung der Funktionalität
- die Trennung von Logik, Daten und Darstellung
- die langfristige Wartbarkeit des Projekts

Die Architektur ist bewusst **einfach, transparent und frameworkfrei** gehalten.

## Grundlegende Architekturprinzipien

### 1. Single-File-Anwendung (v1)

- Die gesamte Anwendung befindet sich in einer `index.html`.
- Keine Build-Tools, keine externen Abhängigkeiten.
- HTML, CSS und JavaScript sind klar getrennt, aber gemeinsam ausgeliefert.

Vorteile:
- maximale Transparenz
- einfache Verteilung (z. B. GitHub Pages)
- geringe Einstiegshürde

### 2. Trennung von Daten und Logik

Die Anwendung unterscheidet strikt zwischen:

- **Szenario-Daten** (JSON)
- **Simulations- und Steuerlogik** (JavaScript)
- **Darstellung** (HTML/CSS)

Die Didaktik liegt ausschließlich in den Szenarien.

### 3. Datengetriebene Steuerung

Der Ablauf der App wird vollständig durch den aktuellen **App-State** bestimmt.

Keine View enthält implizite Logik über:
- Lernziele
- Erklärtexte
- Tokenisierung

## Zentrale Komponenten

### Szenario-Loader

- Lädt `scenarios/scenarios.json`
- Validiert minimale Struktur
- Stellt Szenarien für die UI bereit

### App-State

Der App-State ist die zentrale Quelle der Wahrheit.

Beispielhafte Struktur:

```js
state = {
  mode: "guided", // guided | sandbox
  scenarioId: "baseline-hund",
  step: "tokenizer",
  scenario: { ... },
  params: {
    temperature: 0.8,
    topP: 0.9
  },
  cache: {
    tokens: [],
    embeddings: [],
    attention: [],
    logits: []
  }
}
```

Der State wird ausschließlich über klar definierte Events verändert.

### Pipeline-Navigation

- Definierte Pipeline-Schritte:
  - input
  - tokenizer
  - embedding
  - attention
  - mlp
  - logits
  - decoding
  - summary

- Navigation:
  - Vor / Zurück
  - Direkter Sprung zu Schritten

Die Pipeline ist **linear**, aber **explorativ nutzbar**.

### Rendering-Engine

- Jeder Pipeline-Schritt besitzt eine eigene Render-Funktion.
- Rendering ist **idempotent**:
  - Kein versteckter Zustand in der View
  - Darstellung ergibt sich vollständig aus dem State

Beispiel:
```js
renderTokenizer(state)
renderAttention(state)
```

## Simulation vs. Replay

### Simulated Mode

- Szenario definiert Input, Tokens und Ausgabe
- Zwischenwerte werden intern berechnet (seeded)
- Ziel: Realismus bei geringem Pflegeaufwand

### Replay Mode

- Szenario enthält explizite Zwischenwerte
- UI spielt diese Werte exakt ab
- Ziel: maximale Reproduzierbarkeit

Die Engine entscheidet automatisch:
- Replay-Daten vorhanden → Replay
- sonst → Simulation

## Responsives Layout

Die Anwendung ist **responsiv** konzipiert.

### Desktop (≥1024px)
- 3-Spalten-Layout:
  - Pipeline
  - Hauptansicht
  - Inspector

### Tablet (≥768px)
- Pipeline als schmale Sidebar oder Top-Bar
- Inspector als einblendbarer Bereich

### Mobile (<768px)
- Pipeline als horizontale Tabs
- Hauptansicht im Fokus
- Inspector / Controls als Bottom Sheet

Alle Funktionen bleiben erreichbar, jedoch gestapelt.

## Visualisierungstechniken

- Token: DOM-Elemente
- Vektoren: Balken / Mini-Charts
- Attention: SVG oder Canvas (Heatmap)
- Wahrscheinlichkeiten: Balkendiagramme

Hover-Effekte sind **optional** und nicht zwingend erforderlich (Touch-Geräte).

## Fehlerbehandlung

- Fehlende oder unvollständige Szenarien werden abgefangen
- UI zeigt erklärende Hinweise statt technischer Fehler
- Ungültige Zustände werden nicht gerendert

## Erweiterbarkeit

Die Architektur erlaubt:
- neue Szenarien ohne Codeänderung
- zusätzliche Pipeline-Schritte
- tiefere technische Ansichten (z. B. KV-Cache)

Dabei bleibt die v1-Struktur stabil.

## Nicht-Ziele der Architektur

Bewusst ausgeschlossen sind:
- Performance-Optimierung
- große Modellgrößen
- externe APIs
- Trainingslogik

Der Fokus liegt auf **Erklärbarkeit**, nicht auf Effizienz.

## Zusammenfassung

Die Architektur des *cher-llm-simulator* ist:

- einfach
- datengetrieben
- transparent
- didaktisch motiviert

Sie unterstützt das zentrale Ziel des Projekts:

> **Verstehen ermöglichen – nicht beeindrucken.**

*Dieses Dokument ist Teil der offiziellen Projektdokumentation.*
