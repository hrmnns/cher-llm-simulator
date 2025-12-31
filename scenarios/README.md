# Szenarien – Guided Simulation

Dieses Verzeichnis enthält die **didaktischen Szenarien** für den *cher-llm-simulator*.

Die Szenarien sind das **Herzstück der Anwendung**:  
Sie definieren, *was* gezeigt wird, *wie* es erklärt wird und *worauf* der Nutzer achten soll.

Der Anwendungscode visualisiert lediglich die Pipeline –  
**alle inhaltlichen Lernpfade stecken in den Szenarien**.

## Überblick

- Alle Szenarien werden in einer oder mehreren JSON-Dateien definiert.
- Jedes Szenario beschreibt einen **konkreten Lernfall** (z. B. Tokenisierung, Komposita, Mehrdeutigkeit).
- Neue Szenarien können ergänzt werden, **ohne den Code zu ändern**.

Standarddatei:

```
scenarios.json
```

## Didaktisches Prinzip

Jedes Szenario soll:

1. **genau einen Hauptlernfokus** haben  
2. auf **kontrollierten Eingaben** basieren  
3. **keine falschen Erwartungen** an „echte“ Modellintelligenz erzeugen  

Beispiele für Lernfoki:
- Tokenisierung & Subwords (z. B. „Hundeleine“)
- Mehrdeutigkeit ohne Kontext (z. B. „Bank“)
- Einfluss von Instruktionen auf die Ausgabeform
- Iterative Token-Generierung
- Sampling & Wahrscheinlichkeiten

## Aufbau eines Szenarios (Kurzfassung)

Ein Szenario besteht aus folgenden Pflichtbestandteilen:

- Metadaten (ID, Titel, Lernziele)
- Prompt-Stack (System / Instruktion / User)
- Tokenisierung (Tokens + IDs)
- Erwartete Ausgabe
- Erklärtexte (Highlights)

Optional können Replay-Daten ergänzt werden, um Abläufe exakt vorzugeben.

## Beispiel (vereinfacht)

```json
{
  "id": "kompositum-hundeleine",
  "title": "Komposita: Hundeleine",
  "learningGoals": [
    "Subword-Tokenisierung verstehen"
  ],
  "mode": "simulated",
  "promptStack": {
    "system": "Du bist ein sachlicher Assistent.",
    "instruction": "Antworte kurz.",
    "user": "Was ist eine Hundeleine?"
  },
  "tokenization": {
    "tokens": [
      { "text": "Hund", "id": 104 },
      { "text": "eleine", "id": 207 }
    ]
  },
  "generation": {
    "outputText": "Eine Hundeleine ist eine Leine zum Führen eines Hundes."
  },
  "highlights": {
    "explain": [
      {
        "at": "tokenizer",
        "text": "Komposita werden in bekannte Teilstücke zerlegt."
      }
    ]
  }
}
```

## Guided Simulation vs. Mechanik-Sandbox

Szenarien werden primär für den **Guided Mode** verwendet.

- Im *Guided Mode* sind Prompt, Tokens und Ausgabe kontrolliert.
- Im *Mechanik-Sandbox*-Modus kann dieselbe Pipeline mit freier Eingabe verwendet werden, jedoch ohne didaktische Garantien.

Szenarien sollen **keine freie Texteingabe** voraussetzen.

## Replay- vs. Simulated-Szenarien

### Simulated
- Prompt, Tokens und Ausgabe sind vorgegeben
- Zwischenwerte werden intern simuliert (seeded)
- Weniger Pflegeaufwand

### Replay
- Attention-Gewichte und Generationsschritte sind explizit vorgegeben
- Maximale Reproduzierbarkeit
- Ideal für Vorträge, Schulungen und Erklärvideos

Beide Varianten können gemischt verwendet werden.

## Gute Szenarien erkennen

Ein gutes Szenario:

- ist kurz und fokussiert  
- erklärt *warum* etwas passiert, nicht nur *dass*  
- vermeidet unnötige Komplexität  
- lässt sich in wenigen Minuten erklären  

Wenn ein Szenario mehrere Effekte gleichzeitig erklären soll,  
ist es meist besser, es aufzuteilen.

## Weiterführende Dokumentation

- `docs/json-schema.md` – vollständige Feldbeschreibung
- `docs/concept.md` – didaktisches Gesamtkonzept
- `docs/guided-vs-sandbox.md` – Modus-Erklärung

*Die Szenarien sind bewusst kuratiert – Qualität geht vor Quantität.*
