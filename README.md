# LLM Simulator by cherware.de

**Erklärbare Simulation von LLM-Grundprinzipien für IT-affine Nutzer.**

Diese WebApp ist eine **didaktische Simulation**, die zeigt, wie Large Language Models (LLMs) grundsätzlich arbeiten –
vom Texteingang über Tokenisierung, Embeddings und Attention bis hin zur Ausgabe.

Der Fokus liegt nicht auf „intelligenten Antworten“, sondern auf **Nachvollziehbarkeit, Transparenz und korrekten mentalen Modellen**.

## Ziel & Einordnung

Der *LLM Simulator by cherware.de* visualisiert den typischen Verarbeitungsweg eines LLMs in vereinfachter, erklärbarer Form:

**Text → Tokens → Vektoren → Attention → Wahrscheinlichkeiten → Ausgabe**

Die Anwendung richtet sich an technisch interessierte Nutzer, die verstehen möchten,

- warum Tokenisierung notwendig ist
- warum Wörter nicht gleich Tokens sind
- wie Attention Kontext gewichtet
- warum LLMs Token für Token generieren
- warum Architektur allein kein „Wissen“ erzeugt

Die Simulation ersetzt **keine echten Modelle**, sondern macht deren grundlegende Mechanik nachvollziehbar.

## Was dieses Projekt explizit *nicht* ist

❌ Kein echtes LLM  
❌ Keine Inferenz mit trainierten Gewichten  
❌ Kein Wissensmodell  
❌ Kein Ersatz für ChatGPT, Gemini oder ähnliche Systeme  

> **Hinweis:**  
> Diese Anwendung simuliert ausschließlich **Mechanik und Abläufe**.  
> Bedeutung, Weltwissen und Modellqualität realer LLMs werden bewusst nicht abgebildet.

Alle Ausgaben im *Guided Mode* sind **didaktisch vorgegeben** und dienen ausschließlich der Erklärung.

## Referenzszenarien (v1)

Die Version v1 des LLM Simulators enthält sogenannte **Referenzszenarien**.
Diese Szenarien sind didaktisch eingefroren und dienen als stabile Grundlage
für die Erklärung zentraler LLM-Grundprinzipien.

Referenzszenarien sind keine Tests und keine realistischen Modellläufe.
Sie stellen bewusst vereinfachte, deterministische Abläufe dar, um
bestimmte Konzepte gezielt sichtbar zu machen.

### Zweck der Referenzszenarien

Referenzszenarien erfüllen drei Aufgaben:

- didaktische Orientierung (Was soll hier verstanden werden?)
- strukturelle Vorlage für weitere Szenarien
- Vergleichsbasis für spätere Versionen des Simulators

Sie bilden damit den inhaltlichen und konzeptionellen Ausgangspunkt von v1.

### Enthaltene Referenzszenarien

**Baseline – Einfache Begriffsabfrage**  
Zeigt die grundlegende Verarbeitung eines einfachen Prompts:
tokenbasierte Verarbeitung und probabilistische Textgenerierung.

**Komposita – Subword-Zerlegung am Beispiel „Hundeleine“**  
Vertieft das Verständnis von Tokenisierung anhand zusammengesetzter Begriffe
und zeigt, warum Wörter intern häufig in Teilstücke zerlegt werden.

### Einordnung

Referenzszenarien sind bewusst stabil gehalten und ändern sich innerhalb von v1 nicht.
Neue Szenarien oder Erweiterungen orientieren sich an diesen Referenzen,
ersetzen sie jedoch nicht.

Weiterentwicklungen erfolgen in nachfolgenden Versionen.

## Guided Simulation vs. Mechanik-Sandbox

Die App unterscheidet bewusst zwei Modi mit unterschiedlicher Zielsetzung.

### Guided Simulation (Standard)

- kuratierte, vorgegebene Szenarien
- kontrollierte Tokenisierung und Ausgabe
- klar definierte Lernziele pro Szenario
- reproduzierbare, erklärbare Abläufe

➡️ Dieser Modus dient dem **strukturierten Verständnis** zentraler Konzepte.

### Mechanik-Sandbox (v1)

Die Mechanik-Sandbox ist in v1 bewusst als **technischer Experimentierraum** angelegt.

Sie dient dazu, die **reinen Abläufe der Architektur** sichtbar zu machen –
unabhängig von didaktisch kuratierten Szenarien oder inhaltlich sinnvollen Antworten.

#### Aktueller Stand (v1)

In der aktuellen Version ermöglicht die Sandbox:

- freie Texteingabe
- Durchlaufen der technischen Pipeline
- Visualisierung der Verarbeitungsschritte

Dabei gilt ausdrücklich:

- keine semantische Garantie
- keine konsistente oder „richtige“ Ausgabe
- keine inhaltliche Reproduzierbarkeit

Die Sandbox ist damit **kein LLM-Ersatz** und kein Modus zur Bewertung von Antworten.

#### Einordnung

Die Sandbox zeigt, **was die Architektur technisch tut**, nicht,
was sie „bedeutet“ oder „weiß“.

Sie ist bewusst roh gehalten und bildet den Gegenpol zur Guided Simulation:
Während dort Didaktik im Vordergrund steht, zeigt die Sandbox
die Mechanik ohne didaktische Leitplanken.

#### Ausblick

Die Sandbox ist als Ausbaupunkt für spätere Versionen vorgesehen, z. B. für:

- konfigurierbares Sampling
- reproduzierbare Läufe
- gezielte Variation einzelner Parameter

Diese Funktionen sind **nicht Teil von v1**.

## Zielgruppe

- IT-Fachleute, Architekten und Entwickler
- technisch interessierte Leser, die LLMs verstehen möchten
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
│   ├─ scenarios.json
│   └─ v1/
│      ├─ baseline.reference.json
│      └─ komposita.reference.json
│
├─ docs/
│   ├─ concept.md
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
2. `index.html` im Browser öffnen  
3. Szenario auswählen oder Sandbox aktivieren  
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
- `docs/architecture.md` – App- und State-Architektur
- `docs/json-schema.md` – Szenario-Format

## Lizenz

Dieses Projekt steht unter einer offenen Lizenz.
Details siehe `LICENSE` im Repository.

*Simulation statt Magie. Erklärung statt Show.*
