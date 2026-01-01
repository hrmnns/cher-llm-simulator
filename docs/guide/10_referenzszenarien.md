# Referenzszenarien – Didaktische Testfälle für den LLM Simulator (v1.0)

Diese Seite beschreibt die **offiziellen Referenzszenarien** des  
*LLM Simulator by cherware.de* (Version **v1.0**, Referenzstand App **v1.3.40**).

Die Szenarien sind **nicht zufällig gewählt**.  
Jedes Szenario ist gezielt darauf ausgelegt, **bestimmte Mechanismen der Pipeline sichtbar zu machen**.

Ziel ist **Verständnis**, nicht Optimierung und nicht „richtige Antworten“.

## Didaktisches Grundprinzip

Ein gutes Referenzszenario erfüllt mindestens eine dieser Eigenschaften:

- minimale sprachliche Komplexität
- klar isolierbarer Effekt in der Pipeline
- reproduzierbare Beobachtungen
- keine Abhängigkeit von Weltwissen

> Referenzszenarien sind **Testfälle für Mechanik**, nicht Beispiele für Sprachqualität.

## Überblick: Referenzszenarien v1.0

| Szenario | Primärer Fokus | Pipeline-Stufen |
|--------|----------------|-----------------|
| Hund Hund Hund | Positionsinformation | Tokenisierung, Embeddings |
| Der Hund beißt den Mann | Kontext & Weiterverarbeitung | Attention, MLP |
| Der Hund ist ein … | Auswahlmechanik | Logits, Decoding |
| Mann sieht Hund / Hund sieht Mann | Reihenfolge & Rollen | Positional Encoding, Attention |
| Die Bank ist geschlossen | Grenzen von Kontext | Attention (Grenzen) |

## 1. „Hund Hund Hund“

### Szenario
```
Hund Hund Hund
```

### Warum dieses Szenario besonders geeignet ist

- identische Tokens
- keine semantische Ablenkung
- minimale Struktur

Dieses Szenario isoliert eine zentrale Einsicht:

> **Reihenfolge ist keine Eigenschaft des Textes, sondern der Repräsentation.**

### Prädestinierte Pipeline-Stufen

- **Tokenisierung**  
  identische Wörter → identische Tokens

- **Embeddings**  
  ohne Positional Encoding: identische Vektoren  
  mit Positional Encoding: unterscheidbare Vektoren

- **Attention (indirekt)**  
  ohne Positionsinformation keine differenzierbaren Bezugspunkte

### Didaktischer Wert

- idealer Minimaltestfall
- sehr gut überprüfbar in der App
- entlarvt verbreitete Fehlannahmen

➡️ **Referenzszenario für Embeddings & Positional Encoding**

## 2. „Der Hund beißt den Mann“

### Szenario
```
Der Hund beißt den Mann
```

### Warum dieses Szenario besonders geeignet ist

- einfache Alltagssprache
- klare Rollenverteilung
- kein Fachwissen nötig

Dieses Szenario zeigt:

> **Bedeutung entsteht durch Beziehungen zwischen Tokens.**

### Prädestinierte Pipeline-Stufen

- **Attention**  
  Tokens gewichten andere Tokens unterschiedlich stark  
  das Verb wird zum kontextuellen Knotenpunkt

- **MLP (FFN)**  
  Weiterverarbeitung der kontextualisierten Token-Vektoren  
  Vergleich: mit vs. ohne Attention

### Didaktischer Wert

- trennt klar Kontextbildung und Weiterverarbeitung
- sehr gut erklärbar für nicht IT-affine Nutzer
- vermeidet den Mythos „das Modell versteht“

➡️ **Referenzszenario für Attention & MLP**

## 3. „Der Hund ist ein …“

### Szenario
```
Der Hund ist ein
```

### Warum dieses Szenario besonders geeignet ist

- bewusst offene Fortsetzung
- mehrere plausible nächste Tokens
- keine eindeutige „richtige“ Antwort

Dieses Szenario zeigt:

> **Auswahl ist eine Regelentscheidung, kein Wissensakt.**

### Prädestinierte Pipeline-Stufen

- **Logits**  
  mehrere Tokens erhalten hohe Bewertungen

- **Decoding**  
  Temperature, Top-K, Top-P und Seed steuern die Auswahl

### Didaktischer Wert

- entmystifiziert Kreativität
- macht Parameterwirkungen sichtbar
- ideal für reproduzierbare Experimente

➡️ **Referenzszenario für Logits & Decoding**

## 4. „Der Mann sieht den Hund“ / „Der Hund sieht den Mann“

### Szenario
```
Der Mann sieht den Hund
Der Hund sieht den Mann
```

### Warum dieses Szenario besonders geeignet ist

- identische Tokens
- identische Tokenanzahl
- nur die Reihenfolge ändert sich

Dieses Szenario zeigt:

> **Bedeutungsänderung entsteht allein durch Reihenfolge.**

### Prädestinierte Pipeline-Stufen

- **Positional Encoding**  
  gleiche Tokens, andere Positionen → andere Eingabe-Vektoren

- **Attention**  
  unterschiedliche Gewichtungsmuster und Rollenverteilung

### Didaktischer Wert

- zeigt Zusammenspiel mehrerer Pipeline-Stufen
- sehr stark gegen intuitive Fehlannahmen
- gut vergleichbar in der App

➡️ **Referenzszenario für Reihenfolge & Rollen**

## 5. „Die Bank ist geschlossen“ *(optional)*

### Szenario
```
Die Bank ist geschlossen
```

### Warum dieses Szenario besonders geeignet ist

- echtes Mehrdeutigkeitsproblem
- nicht rein syntaktisch auflösbar
- erfordert implizites Weltwissen

Dieses Szenario zeigt:

> **Kontext ist lokal – Weltwissen ist nicht garantiert.**

### Prädestinierte Pipeline-Stufen

- **Attention**  
  Gewichtung nur vorhandener Tokens

- **Gesamteinordnung**  
  explizite Demonstration von Modellgrenzen

### Didaktischer Wert

- Erwartungskorrektur
- verhindert Überinterpretation von Ausgaben

➡️ **Optionales Szenario zur Einordnung von Grenzen**

## Einordnung für Version 1.0

Die hier beschriebenen Referenzszenarien bilden den **didaktischen Kern** der Version **v1.0**.

Sie sind:
- bewusst begrenzt
- reproduzierbar
- pipeline-orientiert

Erweiterungen oder zusätzliche Szenarien sind **nicht ausgeschlossen**,  
gehören aber in spätere Versionen (z. B. v1.1 oder v2).

**Referenz:** LLM Simulator by cherware.de · App-Version v1.3.40  
**Dokument:** Referenzszenarien · Version v1.0
