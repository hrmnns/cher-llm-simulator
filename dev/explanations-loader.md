# Explanations Loader – Pseudologik & Fallback-Strategie

Diese Dokumentation beschreibt die **Loader-Logik** für globale,
optionale Erklärungen im Projekt **LLM Simulator by cherware.de**.

Sie dient als **technische Referenz** für die Implementierung
und ist bewusst **UI-neutral** formuliert.

## Ziel

- Optionale, nicht-blockierende Ladung erweiterter Erklärungen
- Volle Funktionsfähigkeit der App ohne Zusatzdaten
- Robuste Fallbacks bei fehlenden oder unvollständigen Daten
- Saubere Trennung zwischen Datenzugriff, Auflösung und Rendering

## Einordnung

- Version **v1.0** der App lädt ausschließlich `scenarios.json`
- Erweiterte Erklärungen werden über eine **separate Datei**
  (z. B. `explanations.vNext.json`) bereitgestellt
- v1.0 ignoriert diese Datei vollständig
- vNext lädt sie optional

## Datenfluss (Übersicht)

1. Load `scenarios.json` (verpflichtend)
2. Bestimme aktiven Pipeline-Schritt (App-State)
3. Try load `explanations.vNext.json` (optional)
4. Baue ein **Explanation View Model** für den aktiven Schritt

## Module & Verantwortlichkeiten

### A) DataLoader

**Zweck:** I/O, Parsing, minimale Validierung  
**Kein UI-Wissen**

#### Verantwortlich für:
- Laden von `scenarios.json`
- Optionales Laden von `explanations.vNext.json`
- Graceful Degradation bei Fehlern

#### Pseudologik:
- `loadScenarioData()`
  - fetch `scenarios.json`
  - parse JSON
  - minimale Validierung (`meta`, `scenarios`)
- `loadExplanationDataOptional()`
  - try fetch `explanations.vNext.json`
  - bei Fehler → `null`
  - parse JSON
  - minimale Validierung (`steps` vorhanden)

### B) ExplanationResolver

**Zweck:** Auflösen & Zusammenstellen der erklärungsrelevanten Daten  
**Kein Rendering**

#### Input:
- `activeStepId`
- `coreTextProvider(stepId)`
- optional `ExplanationData`

#### Output:
```text
ExplanationVM {
  coreText,
  expandBlocks[],
  links[]
}
```

#### Pseudologik:
1. `coreText = coreTextProvider(activeStepId)`
2. Initialisiere `expandBlocks = []`, `links = []`
3. Wenn `ExplanationData == null` → return Core-only VM
4. Hole `stepNode = ExplanationData.steps[activeStepId]`
   - fehlt → return Core-only VM
5. Resolve Expand:
   - iteriere `stepNode.expand`
   - resolve `blockId` → `blocks`
   - fehlende Blocks überspringen
   - sortiere nach `priority` (Default 100)
   - max. 6 Blocks
6. Resolve Links:
   - iteriere `stepNode.links`
   - resolve `linkId` → `links`
   - fehlende Links überspringen
   - max. 2 Links
7. return `ExplanationVM`

### C) Normalizer

**Zweck:** Defensive Verarbeitung und Zukunftssicherheit

#### Regeln:
- Blocks benötigen: `type`, `title`, `body`
- Unbekannte `type`-Werte → Block überspringen
- Links benötigen: `label`, `url`
- Default `target = external`

## App-Integration

### App-Start
- Lade `scenarios.json`
- Lade `explanations.vNext.json` **asynchron & optional**
- Speichere ExplanationData nullable im App-State

### Step-Wechsel
- Baue ExplanationVM für aktiven Step
- Übergib VM an Erklärungskomponente
- Core-Text wird immer gerendert
- Expand-/Link-Bereiche nur bei vorhandenen Daten

## Fallback-Strategie (verbindlich)

| Situation | Verhalten |
|--------|----------|
| Datei fehlt | Nur Core anzeigen |
| JSON ungültig | Nur Core anzeigen |
| Step nicht vorhanden | Nur Core anzeigen |
| Block fehlt | Überspringen |
| Link fehlt | Überspringen |

Es darf **keine sichtbaren Fehler** für Endnutzer geben.

## Logging & Debugging

- Logging nur im **Debug-/Dev-Modus**
- Produktionsmodus bleibt still
- Warnungen für:
  - Parse-Fehler
  - fehlende Block-/Link-Referenzen

## Abgrenzung

Nicht Bestandteil dieser Logik:
- UI-/Rendering-Details
- Accordion-/Expand-Design
- scenario-spezifische Hinweise
- Content-Erstellung

## Status

Dieses Dokument ist die **technische Referenz**
für die Implementierung des Erklärungs-Loaders in vNext.
