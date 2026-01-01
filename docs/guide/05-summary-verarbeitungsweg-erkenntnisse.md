# Summary – Verarbeitungsweg & Erkenntnisse

Diese Datei fasst den **gesamten Verarbeitungsweg** des  
*LLM Simulator by cherware.de* zusammen (Referenzstand **v1.3.40**).

Sie dient als **abschließender Überblick** der Version **v1.0**:
kein neues Wissen, sondern Einordnung, Zusammenführung und Orientierung.

Die App ist eine **didaktische Simulation** – kein echtes LLM.

## Überblick: Was hier zusammengeführt wird

Diese Summary beantwortet drei Fragen:

1. **Was passiert Schritt für Schritt in der Pipeline?**
2. **Was kann ich in der App konkret beobachten?**
3. **Welche zentralen Erkenntnisse sollte ich mitnehmen?**

## Der Verarbeitungsweg in einem Durchlauf

### 1) Eingabe

- Der Nutzer gibt einen Text ein.
- Der Text ist zunächst **reine Zeichenfolge**, ohne Bedeutung für das Modell.

> Erkenntnis:  
> Bedeutung entsteht nicht durch den Text selbst, sondern durch Verarbeitung.

### 2) Tokenisierung

- Der Text wird in **Tokens** zerlegt.
- Tokens sind **keine Wörter**, sondern technische Einheiten
  (inkl. Subwords und Komposita).

> Beobachtbar in der App:  
> Zerlegung des Textes in eine Token-Liste.

### 3) Embeddings

- Jedes Token wird in einen **numerischen Vektor** übersetzt.
- Mit aktiviertem Positional Encoding:
  - identische Tokens an unterschiedlichen Positionen werden unterscheidbar.

> Zentrale Erkenntnis:  
> Ohne Positionsinformation gibt es **keine Reihenfolge**.

### 4) Attention

- Tokens gewichten andere Tokens unterschiedlich stark.
- Dadurch entsteht pro Token ein **Kontext-Vektor**.
- Heads zeigen unterschiedliche mögliche Blickrichtungen.
- Layer zeigen aufeinanderfolgende Verarbeitungsschritte.

> Wichtig:  
> Attention erzeugt **Kontext**, aber kein Sprachverständnis.

### 5) MLP (FFN)

- Jeder Token-Vektor wird **für sich** weiterverarbeitet.
- Das MLP nutzt den durch Attention entstandenen Kontext,
  erzeugt ihn aber nicht selbst.

> Zentrale Einsicht:  
> Attention verbindet Tokens – MLP verarbeitet das Ergebnis weiter.

### 6) Logits

- Das Modell erzeugt **numerische Bewertungen**
  für mögliche nächste Tokens.
- Logits sind keine Entscheidungen und keine Wahrscheinlichkeiten.

> Merksatz:  
> Logits sagen, was möglich ist – nicht, was passiert.

### 7) Decoding

- Decoding bestimmt, **wie aus Bewertungen eine Auswahl wird**.
- Parameter wie Temperature, Top-K, Top-P und Seed
  steuern Variation und Reproduzierbarkeit.

> Zentrale Erkenntnis:  
> Unterschiedliche Ausgaben entstehen durch Auswahlregeln,
> nicht durch neues Wissen.

### 8) Ausgabe & Zusammenfassung

- Das gewählte Token wird zur Ausgabe.
- In der App bleibt die Textausgabe im Guided Mode bewusst stabil.
- Der Fokus liegt auf dem **Verarbeitungsweg**, nicht auf Kreativität.

## Zentrale Erkenntnisse (Takeaways)

1. **LLMs arbeiten mit Zahlen, nicht mit Bedeutung.**
2. **Reihenfolge muss explizit kodiert werden.**
3. **Kontext entsteht durch Attention, nicht durch Wörter.**
4. **MLP verarbeitet Kontext weiter, trifft aber keine Entscheidungen.**
5. **Variation entsteht durch Decoding-Parameter, nicht durch Intelligenz.**

## Typische Fehlannahmen – und was die App zeigt

| Häufige Annahme | Was die App tatsächlich zeigt |
|-----------------|-------------------------------|
| „Das Modell versteht den Text“ | Es verarbeitet numerische Repräsentationen |
| „Attention = Verständnis“ | Attention = Kontextgewichtung |
| „MLP entscheidet“ | MLP transformiert Vektoren |
| „Parameter machen kreativ“ | Parameter steuern Auswahlregeln |
| „Gleiche Eingabe = gleiche Ausgabe“ | Nur bei gleichen Parametern & Seed |

## Was diese App bewusst **nicht** zeigt

- kein Training
- kein Lernen
- kein Gedächtnis
- keine echte Sprachmodell-Architektur
- keine Aussage über Qualität realer Modelle

> Ziel der App ist **Verständnis**, nicht Leistungsbewertung.

## Einordnung: Version 1.0

Version **v1.0** des LLM Simulators ist eine **didaktische Referenzversion**.

Sie fokussiert sich auf:

- Transparenz statt Vollständigkeit
- Beobachtbarkeit statt Optimierung
- Mechanik statt Mystifizierung

Erweiterungen (z. B. JSON-basierte Erklärungstexte, UI-Details, weitere Szenarien)
sind bewusst **nicht Teil von v1.0**.

## Einladung zum Erkunden

Nutze die App, um:

- einzelne Schritte gezielt zu vergleichen,
- Parameterwirkungen sichtbar zu machen,
- eigene Fragen zur Funktionsweise von LLMs zu entwickeln.

Es geht nicht darum, „die richtige Antwort“ zu finden,
sondern zu verstehen, **wie Antworten entstehen**.

**Referenz:** LLM Simulator by cherware.de · Version v1.3.40  
**Dokument:** Summary & Erkenntnisse · Version v1.0
