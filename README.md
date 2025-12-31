# cher-llm-simulator

**Erklärbare Simulation von LLM-Grundprinzipien für IT-affine Nutzer.**

Diese WebApp ist eine **didaktische Simulation**, die zeigt, wie Large Language Models (LLMs) grundsätzlich arbeiten –
vom Texteingang über Tokenisierung, Embeddings und Attention bis hin zur Ausgabe.

Der Fokus liegt nicht auf „intelligenten Antworten“, sondern auf **Nachvollziehbarkeit, Transparenz und korrekten mentalen Modellen**.

## Was ist dieses Projekt?

Der *cher-llm-simulator* visualisiert den typischen Verarbeitungsweg eines LLMs in vereinfachter, erklärbarer Form:

**Text → Tokens → Vektoren → Attention → Wahrscheinlichkeiten → Ausgabe**

Dabei werden die einzelnen Schritte schrittweise dargestellt und kommentiert, sodass insbesondere IT-affine Nutzer nachvollziehen können:

- warum Tokenisierung notwendig ist
- warum Wörter nicht gleich Tokens sind
- wie Attention Kontext gewichtet
- warum LLMs Token für Token generieren
- warum Architektur allein kein „Wissen“ erzeugt

## Was dieses Projekt explizit *nicht* ist

❌ Kein echtes LLM  
❌ Keine Inferenz mit trainierten Gewichten  
❌ Kein Wissensmodell  
❌ Kein Ersatz für ChatGPT, Gemini oder ähnliche Systeme  

> **Wichtig:**  
> Diese Anwendung simuliert ausschließlich **Mechanik und Abläufe**.  
> Bedeutung, Weltwissen und Modellqualität echter LLMs werden nicht abgebildet.

Alle Ausgaben im *Guided Mode* sind **didaktisch vorgegeben** und dienen ausschließlich der Erklärung.

## Zentrales Konzept: Szenario-basierte Simulation

Die App ist **datengetrieben** aufgebaut.

Alle Beispiele und Lernpfade werden über JSON-Szenarien definiert.
Der Code stellt lediglich die Pipeline dar – **die Didaktik steckt in den Daten**.

Ein Szenario kann u. a. festlegen:

- den Eingabe-Prompt (Prompt-Stack)
- die Tokenisierung (Tokens + IDs)
- die erwartete Ausgabe
- optionale Zwischenschritte (z. B. Attention-Matrizen, Top-K-Wahrscheinlichkeiten)
- erklärende Hinweise („Achte hier besonders auf …“)

Neue Beispiele können ergänzt werden, **ohne den Code zu ändern**.

## Guided Simulation vs. Mechanik-Sandbox

Die App unterscheidet bewusst zwei Modi:

### Guided Simulation (Standard)

- kuratierte, vorgegebene Beispiele
- kontrollierte Tokenisierung und Ausgabe
- klar definierte Lernziele pro Szenario
- reproduzierbare, erklärbare Abläufe

➡️ Dieser Modus dient dem **strukturierten Verständnis**.

### Mechanik-Sandbox (optional)

- freie Eingabe
- keine Garantie auf sinnvolle Ausgabe
- Fokus auf technische Abläufe

➡️ Dieser Modus zeigt, **was die Architektur technisch tut – unabhängig von Bedeutung**.

## Zielgruppe

- IT-Fachleute, Architekten und Entwickler
- technisch interessierte Leser, die LLMs wirklich verstehen möchten
- Vortragende, Trainer und Lehrende
- Leser begleitender Blog-Artikel (z. B. im reflectIT-Kontext)

## Projektstruktur (v1)

```
.
├─ index.html              # Single-file WebApp
├─ README.md               # Dieses Dokument
├─ LICENSE
│
├─ scenarios/
│   ├─ scenarios.json      # Kuratierte Guided-Szenarien
│   └─ README.md           # Erklärung des Szenario-Formats
│
├─ docs/
│   ├─ concept.md          # Didaktisches Gesamtkonzept
│   ├─ guided-vs-sandbox.md
│   ├─ architecture.md
│   └─ json-schema.md
│
└─ assets/
    └─ screenshots/
```

## Installation & Nutzung

Keine Installation notwendig.

1. Repository klonen oder herunterladen  
2. index.html im Browser öffnen  
3. Szenario auswählen  
4. Pipeline Schritt für Schritt erkunden  

Die Anwendung ist vollständig **clientseitig** und benötigt keinen Server.

## Motivation & Haltung

Dieses Projekt entstand aus der Beobachtung, dass viele LLM-Demos beeindrucken,
aber wenig erklären.

Ziel ist es, ein **ehrliches, reduziertes und korrektes Modell** zu vermitteln –
auch wenn das bedeutet, auf „Wow-Effekte“ zu verzichten.

**Verstehen ist hier wichtiger als Staunen.**

## Weiterführende Dokumentation

- `docs/concept.md` – didaktische Leitidee
- `docs/guided-vs-sandbox.md` – Erklärung der Modi
- `docs/architecture.md` – App- & State-Architektur
- `docs/json-schema.md` – Szenario-Format

## Lizenz

Dieses Projekt steht unter einer offenen Lizenz.
Details siehe `LICENSE` im Repository.

*Simulation statt Magie. Erklärung statt Show.*
