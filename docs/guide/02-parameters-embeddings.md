# Parameter – Embeddings & frühe Pipeline-Wirkungen

Diese Datei beschreibt die **Wirkung von Parametern im Embedding-Schritt** des *LLM Simulator by cherware.de*  
(Referenzstand **v1.3.40**).

Der Fokus liegt darauf, **beobachtbar zu machen**, was sich technisch ändert, **wo** sich diese Änderung in der App zeigt  
und **wie** sie sich auf nachgelagerte Schritte auswirkt.

## Überblick

Betrachtete Parameter:

- `d_model`
- Positional Encoding (an / aus)

Diese Parameter wirken **früh** in der Pipeline und beeinflussen **alle folgenden Schritte** (Attention, MLP, Logits, Decoding).

## 1. d_model – Dimension der Embeddings

### Was wird verändert
`d_model` bestimmt die **Länge des Zahlenvektors**, mit dem jedes Token repräsentiert wird.  
Formal:  
Ein Token wird von einer diskreten ID auf einen Vektor der Dimension *d_model* abgebildet.

### Wo wirkt es zuerst
- **Embeddings**: Länge und Struktur der Vektoren
- indirekt in **Attention** (größere Matrizen)
- indirekt im **MLP** (größere Eingabedimension)

### Was siehst du in der App
- Dropdown-Auswahl: `d_model = 8 | 16 | 32`
- Barcode-Visualisierung pro Token:
  - mehr Balken bei höherem `d_model`
  - gleiche Token behalten ihre Position, aber mit mehr Dimensionen

### Was kannst du beobachten
- Bei größerem `d_model`:
  - feinere numerische Struktur
  - visuell „ruhigere“ Attention-Muster
- Bei kleinerem `d_model`:
  - gröbere Unterschiede
  - stärkere Ausschläge in Attention und MLP

### Typische Fehlinterpretationen
- Mehr Dimensionen bedeuten **nicht** automatisch „mehr Wissen“.
- Einzelne Dimensionen haben **keine semantische Bedeutung**.

## 2. Positional Encoding

### Was wird verändert
Zum Token-Embedding wird ein **positionsabhängiger Vektor addiert**, damit das Modell Token-Reihenfolgen unterscheiden kann.

In der App erfolgt dies **additiv und vereinfacht** (sin/cos-ähnlich, didaktisch).

### Wo wirkt es zuerst
- **Embeddings**: gleicher Token an unterschiedlicher Position → anderer Vektor
- besonders sichtbar in **Attention**

### Was siehst du in der App
- Checkbox: *Positional Encoding*
- Veränderung der Barcode-Ansicht bei gleichem Token an anderer Position
- Veränderte Muster in der Attention-Heatmap

### Was kannst du beobachten
- Ohne Positional Encoding:
  - Tokens gleichen Typs sind numerisch identisch
  - Attention reagiert schwächer auf Reihenfolge
- Mit Positional Encoding:
  - Reihenfolge wird unterscheidbar
  - Diagonale in Attention wird stabiler

### Typische Fehlinterpretationen
- Positional Encoding ist kein „Zeitverständnis“.
- Es ergänzt Information, ersetzt aber keine Kontextverarbeitung.

## Zusammenspiel: d_model × Positional Encoding

### Beobachtbares Muster
- Kleines `d_model` + Positional Encoding:
  - Position dominiert stärker
- Großes `d_model` + Positional Encoding:
  - Position ist eingebettet, aber weniger dominant

### Didaktische Kernaussage
> Reihenfolge wird **nicht gelernt**, sondern **numerisch kodiert** – und diese Kodierung wirkt nur, wenn nachgelagerte Schritte (Attention, MLP) sie nutzen.

## Abgrenzung / Vereinfachungen

- Embeddings sind **seeded simuliert**
- Keine echten Wort- oder Satzbedeutungen
- Keine Lernprozesse
- Kein Vergleich realer Modellgrößen

## Übergang zu den nächsten Schritten

Die hier beschriebenen Parameter bestimmen die **numerische Ausgangsbasis** für:

- **Attention** (Kontextgewichtung)
- **MLP** (Transformation mit/ohne Kontext)

→ Fortsetzung in: **03-parameters-attention-mlp.md**

**Referenz:** LLM Simulator by cherware.de · Version v1.3.40  
