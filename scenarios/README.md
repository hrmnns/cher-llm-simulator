# Szenarien – Guided Simulation (v1)

Dieses Verzeichnis enthält die **didaktischen Szenarien** für den *LLM Simulator by cherware.de*.

Die Szenarien sind das **Herzstück der Anwendung**:
Sie definieren, *was* gezeigt wird, *wie* es erklärt wird und *worauf* der Nutzer achten soll.

Der Anwendungscode visualisiert ausschließlich die Pipeline –
**alle didaktischen Lernpfade und inhaltlichen Akzente stecken in den Szenarien**.

## Einordnung (v1)

In Version v1 unterscheidet der Simulator klar zwischen:

- **Guided Simulation** (szenariobasiert, didaktisch geführt)
- **Mechanik-Sandbox** (freie Eingabe, ohne didaktische Garantie)

Dieses Verzeichnis bezieht sich **ausschließlich auf den Guided Mode**.
Szenarien sind nicht für die Sandbox gedacht und setzen **keine freie Texteingabe** voraus.

## Referenzszenarien (v1)

Ein Teil der Szenarien ist als **Referenzszenarien** gekennzeichnet.

Referenzszenarien sind:

- didaktisch eingefroren
- strukturelle und inhaltliche Vorlagen
- Vergleichsbasis für spätere Versionen

Sie definieren den **kanonischen v1-Zustand** der Szenariostruktur.

Aktuell enthaltene Referenzszenarien:

- **Baseline – Einfache Begriffsabfrage**  
  Einführung in tokenbasierte Verarbeitung und probabilistische Textgenerierung.

- **Komposita – Subword-Zerlegung am Beispiel „Hundeleine“**  
  Vertiefung der Tokenisierung anhand zusammengesetzter Begriffe.

Referenzszenarien liegen unter:

```
scenarios/v1/*.reference.json
```

Sie werden innerhalb von v1 **nicht verändert**.

## Überblick

- Alle Szenarien werden als JSON-Dateien definiert.
- Jedes Szenario beschreibt **genau einen Lernfall**.
- Neue Szenarien können ergänzt werden, **ohne den Anwendungscode zu ändern**.

## Didaktisches Prinzip

Jedes Szenario soll:

1. **genau einen Hauptlernfokus** haben  
2. auf **kontrollierten Eingaben** basieren  
3. **keine falschen Erwartungen** an reale Modellintelligenz erzeugen  

Szenarien sind keine Tests und keine Benchmarks,
sondern **didaktische Konstrukte**.

Beispiele für typische Lernfoki:

- Tokenisierung & Subwords (z. B. Komposita)
- Mehrdeutigkeit ohne Kontext
- Einfluss von Instruktionen auf die Ausgabeform
- Iterative Token-Generierung
- Wahrscheinlichkeiten und Sampling (konzeptionell)

## Aufbau eines Szenarios (Kurzfassung)

Ein Szenario besteht aus folgenden Pflichtbestandteilen:

- Metadaten (ID, Titel, Lernziele)
- Prompt-Stack (System / Instruktion / User)
- Tokenisierung (Tokens + IDs)
- Erwartete Ausgabe
- Erklärtexte (Highlights)

Optional können zusätzliche Fokus- oder Replay-Informationen ergänzt werden,
um Abläufe präziser zu steuern.

## Beispiel (vereinfacht)

```json
{
  "id": "komposita-hundeleine",
  "title": "Komposita – Subword-Zerlegung am Beispiel „Hundeleine“",
  "learningGoals": [
    "Subword-Repräsentation",
    "Umgang mit zusammengesetzten Begriffen"
  ],
  "mode": "simulated",
  "promptStack": {
    "system": "Du bist ein sachlicher Assistent.",
    "instruction": "Antworte kurz und präzise.",
    "user": "Was ist eine Hundeleine?"
  },
  "tokenization": {
    "tokens": [
      { "text": "Hund", "id": 204 },
      { "text": "e", "id": 205 },
      { "text": "leine", "id": 206 }
    ]
  },
  "generation": {
    "outputText": "Eine Hundeleine ist eine Leine, mit der ein Hund geführt wird."
  },
  "highlights": {
    "focusByStep": {
      "tokenizer": "Subword-Zerlegung"
    },
    "explain": [
      {
        "at": "tokenizer",
        "text": "Zusammengesetzte Wörter werden oft in mehrere Subwords zerlegt."
      }
    ]
  }
}
```

## Guided Simulation vs. Mechanik-Sandbox

Szenarien werden **ausschließlich im Guided Mode** verwendet.

- Im **Guided Mode** sind Prompt, Tokenisierung und Ausgabe kontrolliert
  und auf ein Lernziel abgestimmt.
- In der **Mechanik-Sandbox** läuft dieselbe Pipeline,
  jedoch ohne Szenarien und ohne didaktische Leitplanken.

Szenarien sollen daher:

- keine freie Texteingabe voraussetzen
- nicht versuchen, Sandbox-Verhalten zu erklären
- bewusst auf Klarheit statt Vollständigkeit setzen

## Simulated- vs. Replay-Szenarien

### Simulated

- Prompt, Tokens und Ausgabe sind vorgegeben
- Zwischenwerte werden intern simuliert
- geringerer Pflegeaufwand
- Standardfall für v1

### Replay

- Zwischenschritte (z. B. Attention-Gewichte) sind explizit definiert
- maximale Reproduzierbarkeit
- geeignet für Vorträge, Schulungen und Erklärvideos

Beide Varianten können kombiniert werden,
sollten jedoch didaktisch klar getrennt bleiben.

## Gute Szenarien erkennen

Ein gutes Szenario:

- ist kurz und fokussiert  
- erklärt *warum* etwas passiert, nicht nur *dass*  
- vermeidet unnötige Komplexität  
- lässt sich in wenigen Minuten erfassen  

Wenn ein Szenario mehrere Effekte gleichzeitig erklären soll,
ist es meist besser, es aufzuteilen.

## Weiterführende Dokumentation

- `docs/json-schema.md` – vollständige Feldbeschreibung
- `docs/concept.md` – didaktisches Gesamtkonzept
- `docs/guided-vs-sandbox.md` – Modus-Erklärung

*Die Szenarien sind bewusst kuratiert – Qualität geht vor Quantität.*
