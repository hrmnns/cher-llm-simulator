# Parameter – Embeddings & Positionsinformation

Diese Datei beschreibt die **Wirkung früher Parameter im Embedding-Schritt** des  
*LLM Simulator by cherware.de* (Referenzstand **v1.3.40**).

Der Fokus liegt darauf, **transparent und nachvollziehbar** zu erklären,

- was sich technisch ändert,
- wo diese Änderung in der App sichtbar wird,
- und welche Konsequenzen sich für die weitere Pipeline ergeben.

Die beschriebenen Effekte sind **didaktische Simulationen** und keine reale Modellinferenz.

## Überblick

Behandelte Parameter:

- `d_model` (Dimension der Embeddings)
- Positional Encoding (additiv, an/aus)

Diese Parameter wirken **am Anfang der Pipeline** und beeinflussen alle nachfolgenden Schritte
(**Attention, MLP, Logits, Decoding**).

## 1. `d_model` – Dimension der Token-Embeddings

### Was wird verändert

`d_model` legt fest, **wie viele numerische Dimensionen** ein Token-Embedding besitzt.
Jedes Token wird von einer diskreten ID auf einen Vektor der Länge `d_model` abgebildet.

Formal (vereinfacht):
```
Token → ℝ^d_model
```

### Wo wirkt es

- **Embeddings:** Länge und Struktur der Vektoren
- **Attention:** Größe der beteiligten Matrizen
- **MLP:** Eingabedimension der Transformation

### Was siehst du in der App

- Auswahl: `d_model = 8 | 16 | 32`
- Barcode-Darstellung der Token-Embeddings:
  - höhere Werte → mehr Balken
  - gleiche Token behalten ihre Position im Vektorraum

### Was kannst du beobachten

- kleines `d_model`:
  - gröbere numerische Unterschiede
  - stärker vereinfachte Attention-Muster
- größeres `d_model`:
  - feinere numerische Struktur
  - stabilere, gleichmäßigere Muster in Attention und MLP

### Typische Missverständnisse

- Mehr Dimensionen bedeuten **nicht automatisch** mehr Wissen.
- Einzelne Dimensionen sind **nicht semantisch interpretierbar**.

## 2. Positional Encoding – Positionsinformation für Tokens

### Was passiert technisch

Zum reinen **Token-Embedding** wird ein **positionsabhängiger Zahlenvektor addiert**, damit das Modell erkennen kann,
**an welcher Stelle im Text** ein Token steht.

Formal (vereinfacht):
```
Eingabe-Vektor = Token-Embedding + Positions-Vektor
```

- Der Positions-Vektor hängt **nur von der Token-Position** ab, nicht vom Token-Inhalt.
- Gleiche Tokens an unterschiedlichen Positionen erhalten dadurch **unterschiedliche Eingabe-Vektoren**.

> Das Token sagt dem Modell, was dort steht. Die Positionsinformation sagt dem Modell, wo es steht. Erst zusammen ergibt das eine unterscheidbare Eingabe.

In der App wird dieser Mechanismus **vereinfacht simuliert**:
- additiv
- deterministisch (reproduzierbar)
- ohne Lernprozess

Die Positionswerte folgen dabei einem **regelmäßigen, wellenartigen Zahlenmuster**
(sinus-/cosinus-ähnlich), das sich mit der Token-Position systematisch verändert.

Wichtig dabei:
- Die Werte sind **nicht zufällig** und **nicht gelernt**
- Benachbarte Positionen erzeugen **ähnliche**, weiter entfernte **unterschiedlichere** Muster
- Ziel ist eine **stabile numerische Positionsmarkierung**, keine exakte mathematische Nachbildung

### Warum ist Positional Encoding notwendig?

Ohne Positionsinformation kennt das Modell:

- **welche Tokens** vorhanden sind,
- aber nicht, **in welcher Reihenfolge** sie stehen.

Beispiel:
> „Der Hund beißt den Mann.“  
> „Der Mann beißt den Hund.“

Ohne Positionsinformation sind beide Sätze für das Modell **nahezu identisch**, da sie aus denselben Tokens bestehen.

Positional Encoding liefert daher **keine Bedeutung**, sondern eine **numerische Orientierung**,
die es nachgelagerten Schritten (insbesondere Attention) erlaubt,
Reihenfolge und Nähe zu berücksichtigen.

### Bedeutung des Schalters „additiv“

Der Schalter **Positional Encoding (additiv)** entscheidet,
ob Positionsinformation überhaupt in die Pipeline eingebracht wird.

#### Positional Encoding **aktiv**

- Token-Embeddings enthalten zusätzlich Positionsinformation
- gleiche Tokens unterscheiden sich je nach Position
- Attention kann Reihenfolge berücksichtigen
- Rollen (z. B. handelnd / betroffen) werden numerisch unterscheidbar

#### Positional Encoding **deaktiviert**

- **keine Positionsinformation vorhanden**
- gleiche Tokens haben überall identische Vektoren
- Reihenfolge geht vollständig verloren
- unterschiedliche Interpretationen wären theoretisch gleich plausibel

> Hinweis:  
> In v1 bleibt die Textausgabe im Guided Mode bewusst stabil.
> Die mögliche Mehrdeutigkeit ohne Positionsinformation wird im Verarbeitungsweg sichtbar gemacht,
> nicht durch unterschiedliche Textausgaben.

### Was siehst du konkret in der App?

- **Embeddings-Ansicht (Barcode):**
  - mit Positional Encoding: gleiche Tokens → unterschiedliche Muster
  - ohne Positional Encoding: gleiche Tokens → identische Muster
- **Attention-Heatmap:**
  - mit Positional Encoding: stabilere Diagonalen, positionsabhängige Struktur
  - ohne Positional Encoding: symmetrischere, weniger gerichtete Muster

### Typische Fehlinterpretationen

- Positional Encoding bedeutet **kein Sprachverständnis**.
- Es ersetzt **keine Grammatik** und **keine Logik**.
- Es liefert lediglich eine **Positionsmarkierung**, die genutzt werden kann – oder auch nicht.

## Zusammenspiel: `d_model` × Positional Encoding

### Beobachtbare Muster

- kleines `d_model` + Positional Encoding:
  - Positionsinformation dominiert stärker
- großes `d_model` + Positional Encoding:
  - Positionsinformation ist eingebettet, aber weniger dominant

### Didaktische Kernaussage

> Reihenfolge wird nicht „verstanden“, sondern **numerisch kodiert**.
> Ob diese Kodierung wirkt, entscheidet erst die weitere Verarbeitung.

## Abgrenzung und Vereinfachungen

- Alle Embeddings sind **simuliert**
- Keine echten Wortbedeutungen
- Keine Lern- oder Trainingsprozesse
- Keine Aussage über reale Modellarchitekturen

## Übergang

Die hier beschriebenen Parameter bestimmen die **numerische Ausgangsbasis** für:

- **Attention** (Kontextgewichtung)
- **MLP** (Transformation mit/ohne Kontext)

→ Fortsetzung in: **03-parameters-attention-mlp.md**

**Referenz:** LLM Simulator by cherware.de · Version v1.3.40
