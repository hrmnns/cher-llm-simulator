# JSON-Schema – Szenarien (cher-llm-simulator)

## Ziel dieses Dokuments

Dieses Dokument beschreibt das **formale JSON-Schema** für Szenarien im Projekt *cher-llm-simulator*.

Es dient dazu:

- neue Szenarien konsistent zu erstellen
- strukturelle Fehler frühzeitig zu erkennen
- didaktischen Drift zu vermeiden
- Szenarien maschinell zu validieren

Das Schema ist bewusst **pragmatisch** gehalten und orientiert sich an den didaktischen Zielen des Projekts.

## Überblick

Szenarien werden in einer JSON-Datei definiert, typischerweise:

```
scenarios/scenarios.json
```

Die Datei besteht aus:
- Metadaten (`meta`)
- einer Liste von Szenarien (`scenarios`)

## Top-Level-Struktur

```json
{
  "meta": { ... },
  "scenarios": [ ... ]
}
```

### meta (Pflicht)

```json
{
  "version": "1.0",
  "project": "cher-llm-simulator",
  "description": "Guided scenarios for explaining LLM core mechanics",
  "defaultScenarioId": "baseline-hund"
}
```

**Bedeutung:**
- `version`: Version des Szenario-Formats
- `project`: Projektkennung
- `description`: Kurzbeschreibung
- `defaultScenarioId`: ID des beim Start geladenen Szenarios

## Szenario-Objekt

Jedes Szenario ist ein eigenständiges Objekt mit klarer didaktischer Funktion.

### Pflichtfelder

```json
{
  "id": "string",
  "title": "string",
  "learningGoals": ["string"],
  "mode": "simulated | replay",
  "promptStack": { ... },
  "tokenization": { ... },
  "generation": { ... },
  "highlights": { ... }
}
```

## Felddetails

### id (string, Pflicht)

Eindeutige Kennung des Szenarios.

Beispiel:
```json
"id": "kompositum-hundeleine"
```

### title (string, Pflicht)

Kurzbeschreibung des Szenarios für die UI.

### learningGoals (array, Pflicht)

Liste der Lernziele dieses Szenarios.

Regel:
- mindestens ein Eintrag
- jedes Szenario fokussiert sich auf **einen Hauptaspekt**

### mode (string, Pflicht)

Legt fest, wie das Szenario ausgeführt wird.

Zulässige Werte:
- `simulated` – Zwischenwerte werden berechnet
- `replay` – Zwischenwerte sind explizit vorgegeben

### promptStack (object, Pflicht)

Definiert den vollständigen Prompt.

```json
{
  "system": "string",
  "instruction": "string",
  "user": "string"
}
```

Alle Teile sind Text und werden gleich behandelt.

### tokenization (object, Pflicht)

Definiert die Tokenisierung des Prompts.

```json
{
  "tokens": [
    { "text": "Hund", "id": 104 }
  ]
}
```

- `text`: Token-Text (inkl. Leerzeichen, falls relevant)
- `id`: numerische Token-ID (didaktisch)

### generation (object, Pflicht)

Definiert die erwartete Ausgabe.

```json
{
  "outputText": "string",
  "steps": [ ... ]
}
```

- `outputText`: vollständige Zielausgabe
- `steps`: optional, detaillierte Generationsschritte

#### steps (optional)

```json
{
  "step": 1,
  "topK": [
    { "token": "Ein", "p": 0.42 }
  ],
  "chosenToken": "Ein"
}
```

### highlights (object, Pflicht)

Didaktische Hervorhebungen und Erklärtexte.

```json
{
  "tokenFocus": ["Hund"],
  "explain": [
    {
      "at": "tokenizer",
      "text": "string"
    }
  ]
}
```

- `tokenFocus`: optionale Liste hervorzuhebender Tokens
- `explain`: kontextbezogene Erklärungen

#### at (string)

Legt fest, **bei welchem Pipeline-Schritt** der Text angezeigt wird.

Zulässige Werte:

```
input
tokenizer
embedding
attention
mlp
logits
decoding
summary
```

## Replay-Daten (optional)

Für Replay-Szenarien können Zwischenwerte explizit definiert werden.

Beispiel:

```json
"replay": {
  "layers": [
    {
      "layer": 1,
      "heads": [
        {
          "head": 1,
          "attention": [
            [0.2, 0.8],
            [0.5, 0.5]
          ]
        }
      ]
    }
  ]
}
```

Diese Daten werden **direkt visualisiert**, ohne Berechnung.

## Validierungsregeln (informell)

- Alle Pflichtfelder müssen vorhanden sein
- `id` muss eindeutig sein
- `learningGoals` darf nicht leer sein
- `tokens` darf nicht leer sein
- `outputText` darf nicht leer sein

Weitere Regeln können später formalisiert werden.

## Erweiterbarkeit

Das Schema ist bewusst offen für:
- zusätzliche Felder
- neue Visualisierungsebenen
- weitere Pipeline-Schritte

Breaking Changes sollten über eine neue `version` erfolgen.

## Zusammenfassung

Das Szenario-JSON ist:

- die didaktische Wahrheit der Anwendung
- die Grundlage für Erweiterungen
- bewusst einfach, aber strukturiert

> **Wenn sich etwas nicht sauber im JSON ausdrücken lässt,  
> ist es meist auch didaktisch nicht sauber genug.**

*Dieses Dokument ist Teil der offiziellen Projektdokumentation.*
