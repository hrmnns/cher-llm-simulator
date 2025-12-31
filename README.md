# LLM Simulation WebApp – Verstehen statt Beeindrucken

Diese WebApp ist eine **didaktische Simulation**, die zeigt, **wie Large Language Models (LLMs) grundsätzlich arbeiten** –  
vom Texteingang über Tokenisierung, Embeddings und Attention bis zur Ausgabe.

Der Fokus liegt nicht auf Performance oder „intelligenten Antworten“,  
sondern auf **Nachvollziehbarkeit, Transparenz und korrekten mentalen Modellen**.

## Was ist dieses Projekt?

Diese Anwendung simuliert den **internen Verarbeitungsweg eines LLMs** in vereinfachter, erklärbarer Form:

**Text → Tokens → Vektoren → Attention → Wahrscheinlichkeiten → Ausgabe**

Dabei werden die einzelnen Schritte visuell dargestellt und kommentiert, sodass insbesondere IT-affine Nutzer nachvollziehen können:

- warum Tokenisierung notwendig ist  
- warum Wörter nicht gleich Tokens sind  
- wie Attention Kontext gewichtet  
- warum LLMs Token für Token generieren  
- warum Architektur allein kein „Wissen“ erzeugt  

## Was dieses Projekt explizit *nicht* ist

❌ Kein echtes LLM  
❌ Keine Inferenz mit trainierten Gewichten  
❌ Kein Wissensmodell  
❌ Kein Ersatz für ChatGPT, Gemini o. Ä.

> **Wichtig:**  
> Diese App simuliert Mechanik und Abläufe –  
> nicht Bedeutung, Weltwissen oder echte Modellleistung.

Alle Ausgaben im „Guided Mode“ sind **didaktisch vorgegeben**  
und dienen ausschließlich der Erklärung.

## Zentrales Konzept: Szenario-basierte Simulation

Die App ist **datengetrieben**.

Alle erklärten Beispiele werden über eine oder mehrere JSON-Dateien definiert.  
Der Code visualisiert nur – **die Didaktik steckt in den Daten**.

### Ein Szenario kann festlegen:
- den Eingabe-Prompt
- die Tokenisierung (Tokens + IDs)
- die erwartete Ausgabe
- optionale Zwischenschritte (z. B. Attention-Matrizen, Top-K-Wahrscheinlichkeiten)
- erklärende Hinweise („Achte hier auf …“)

Neue Beispiele können hinzugefügt werden, **ohne den Code zu ändern**.


## Guided Simulation vs. Mechanik-Sandbox

Die App kennt zwei bewusst getrennte Modi:

### Guided Simulation (Standard)

- kuratierte, vorgegebene Beispiele
- kontrollierte Tokens und Ausgaben
- klare Lernziele pro Szenario
- reproduzierbare, erklärbare Abläufe

➡️ Dieser Modus dient dem **Verständnis**.

### Mechanik-Sandbox (optional)

- freie Eingabe
- keine Garantie auf sinnvolle Ausgaben
- Fokus auf technische Abläufe

➡️ Dieser Modus zeigt, **was die Architektur tut – unabhängig von Bedeutung**.

## Zielgruppe

- IT-Fachleute, Architekten, Entwickler
- technisch interessierte Leser, die LLMs *wirklich* verstehen wollen
- Vortragende / Trainer / Lehrende
- Leser begleitender Blog-Artikel

## Projektstruktur (v1)

```text
.
├─ index.html              # Single-file WebApp
├─ README.md               # Dieses Dokument
├─ LICENSE
│
├─ scenarios/
│   ├─ scenarios.json      # Kuratierte Beispiel-Szenarien
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
