# Global Explanation Schema (vNext)

Diese Dokumentation beschreibt das **globale Erklärungsschema** für erweiterte
Erklärungen im Projekt **LLM Simulator by cherware.de**.

Das Schema dient dazu, zusätzliche Erklärungstexte
(z. B. Details, Beispiele, Missverständnisse, Verweise)
**datengetrieben, versionierbar und UI-neutral** bereitzustellen.

## Ziel & Einordnung

- Version **v1.0** der App gilt als didaktisch abgeschlossen und eingefroren
- Bestehende Schritt-Erklärungen (Core) bleiben unverändert
- Dieses Schema ist Grundlage für **kommende Versionen (vNext)**

Das Schema:
- ergänzt bestehende Core-Erklärungen
- ersetzt keine Inhalte aus v1.0
- wird von v1.0 **nicht geladen**

## Kompatibilität & Ladeverhalten

- Das globale Erklärungsschema liegt in einer **separaten Datei**
  (z. B. `explanations.vNext.json`)
- Version 1.0 der App ignoriert dieses Schema vollständig
- vNext-Versionen laden das Schema **optional**

Backward Compatibility wird durch **Isolation**, nicht durch Parsing, erreicht.

## Überblick: Schema-Struktur

```json
{
  "meta": { ... },
  "steps": { ... },
  "blocks": { ... },
  "links": { ... }
}
```

## meta

### Zweck
Governance, Versionierung und redaktioneller Kontext.

### Typische Felder
- `schemaVersion` – Version der Struktur (z. B. `"1.0"`)
- `contentVersion` – Version der Inhalte
- `language` – z. B. `"de"`
- `updated` – letztes Änderungsdatum
- `source` – Projekt-/Quellenangabe
- `notes` – optionale redaktionelle Hinweise

> Die App darf **keine Logik** an `meta`-Felder koppeln.

## steps

### Zweck
Zuordnung von Erklärungen zu stabilen Pipeline-Schritt-IDs.

### Struktur pro Step

```json
"tokenization": {
  "coreRef": "v1.steps.tokenization.core",
  "expand": [
    { "blockId": "blk.tokenization.subwords", "priority": 10 }
  ],
  "links": [
    { "linkId": "lnk.wiki.tokenization" }
  ]
}
```

### Felder
- `coreRef` (**verpflichtend**)
  - Referenz auf den v1.0-Core-Text
  - kein Textinhalt
- `expand` (optional)
  - Liste referenzierter Blocks
  - Reihenfolge über `priority`
- `links` (optional)
  - Liste referenzierter Linkouts

> In `steps` werden **keine Texte gepflegt**, nur Referenzen.

## blocks

### Zweck
Wiederverwendbare, aufklappbare Erklärungseinheiten.

### Block-Struktur

```json
{
  "type": "detail",
  "title": "Subwords statt Wörter",
  "body": "Kurze, ergänzende Erklärung."
}
```

### Unterstützte Typen
- `detail` – präzisierende Erklärung
- `misconception` – typische Fehlannahme + Korrektur
- `example` – kurzes, einfaches Beispiel
- `boundary` – Abgrenzung / Gültigkeitsbereich
- `why` – didaktische Begründung

### Regeln
- ergänzend, nicht wiederholend
- kurz (3–5 Sätze)
- wiederverwendbar
- keine Schritt-Logik im Block selbst

## links

### Zweck
Verweise auf weiterführende externe Inhalte (Wiki / Blog).

### Link-Struktur

```json
{
  "label": "Mehr zur Tokenisierung (Wiki)",
  "url": "https://…",
  "target": "external"
}
```

### Regeln
- max. 2 Links pro Step
- keine erklärenden Texte im Link
- vertiefende Inhalte gehören außerhalb der App

## Governance-Regeln (Auszug)

- Max. **3–6 Expand-Blöcke** pro Schritt
- Max. **2 Links** pro Schritt
- Tooltips sind **nicht Teil dieses Schemas**
- Mobile-Nutzung hat Priorität

Die vollständigen UX- und Content-Regeln sind dokumentiert in:

```
/docs/ux/expanded-explanations.md
```

## Abgrenzung

Nicht Bestandteil dieses Schemas:
- scenario-spezifische Hinweise
- UI-/Rendering-Logik
- konkrete Inhaltsbefüllung aller Schritte
- Tooltip-Definitionen

Scenario-spezifische Hinweise können als **optionale Schema-Erweiterung (v1.1)**
ergänzt werden.

## Status

Dieses Dokument beschreibt das **globale Erklärungsschema v1.0**
und dient als verbindliche Referenz für Implementierung und Content-Pflege.
