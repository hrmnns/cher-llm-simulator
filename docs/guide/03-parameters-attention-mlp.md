# Parameter – Attention & MLP (FFN)

Diese Datei beschreibt Parameter und Ansichten im Bereich **Attention** und **MLP/FFN** des  
*LLM Simulator by cherware.de* (Referenzstand **v1.3.40**).

Ziel ist es, verständlich zu machen,

- **was** sich durch eine Einstellung ändert,
- **wo** du den Effekt in der App siehst,
- **warum** es bestimmte Schalter überhaupt gibt.

Die App ist eine **didaktische Simulation** – kein echtes LLM und keine reale Modellinferenz.

## Überblick

In diesem Kapitel:

- **Attention**: Auswahl von *Layer* und *Head*, optional *Causal Mask*
- **MLP/FFN**: Token-Auswahl (*Token i*), *Vergleich anzeigen* (ohne vs. mit Attention), *Delta anzeigen*

## Wichtige Vorbemerkung: Warum gibt es hier nur 2 Layer und 2 Heads?

Die Auswahl von **Layer** und **Head** dient in dieser App **nicht dazu, ein echtes Modell nachzubilden**.
Sie ist ein **didaktisches Hilfsmittel**, um Unterschiede sichtbar zu machen.

### Vereinfacht gesagt

- **Heads** zeigen, dass ein Modell **gleichzeitig auf unterschiedliche Dinge achten kann**
- **Layer** zeigen, dass ein Text **mehrmals hintereinander weiterverarbeitet** wird

In der App gibt es davon **bewusst nur zwei Varianten**, um vergleichen zu können,
ohne die Oberfläche zu überladen.

### Was bedeutet „Head“ hier konkret?

Ein **Head** ist eine mögliche Art, wie Tokens auf andere Tokens schauen.

In der App bedeutet:

- **Head 1**: eine Variante der Kontextgewichtung
- **Head 2**: eine andere Variante der Kontextgewichtung

Beide sehen denselben Text, setzen aber **unterschiedliche Schwerpunkte**.

> Merksatz:  
> Ein Head ist eine **Blickrichtung auf den Text**.

### Was bedeutet „Layer“ hier konkret?

Ein **Layer** ist ein weiterer Verarbeitungsschritt auf dem Weg durch die Pipeline.

In der App bedeutet:

- **Layer 1**: erste Kontextbildung
- **Layer 2**: weiterverarbeitete Kontextbildung

Layer 2 arbeitet also **auf dem Ergebnis von Layer 1**, nicht erneut auf dem Originaltext.

> Merksatz:  
> Ein Layer ist ein **weiterer Verarbeitungsschritt**.

### Warum genau zwei?

- Mit **nur einem** Head oder Layer gäbe es **keinen Vergleich**
- Zwei Varianten sind die **kleinste sinnvolle Anzahl**, um Unterschiede zu sehen
- Mehr Varianten würden die App komplexer machen, ohne zusätzlichen Erkenntnisgewinn

> Wichtig:  
> Mehr Heads oder Layer bedeuten hier **nicht** „besser“ oder „schlauer“.

## Begriffsklärung: Was bedeutet MLP (FFN)?

**MLP** steht für **Multi-Layer Perceptron**.  
**FFN** steht für **Feed-Forward Network**.

Im Kontext von Transformer-Modellen bezeichnen beide Begriffe denselben Baustein:
eine kleine, mehrstufige Rechenfunktion, die **jeden Token-Vektor für sich** weiterverarbeitet.

Wichtig dabei:

- Ein MLP/FFN „schaut“ **nicht erneut** auf andere Tokens (das ist die Aufgabe der Attention).
- Es verarbeitet die bereits vorhandene Token-Repräsentation **weiter** (Zahlen → andere Zahlen).
- In echten Modellen ist das ein wesentlicher Teil der nichtlinearen Transformation.

> Merksatz:  
> **Attention** bestimmt, *worauf* ein Token schaut.  
> **MLP (FFN)** bestimmt, *wie* der so entstandene Zustand weiterverarbeitet wird.

## 1) Attention – Kontextgewichtung per Heatmap

### Was sehe ich?

Im Schritt **Attention** siehst du eine **Heatmap**, die zeigt,
**welche Tokens auf welche anderen Tokens achten**.

Zeilen und Spalten stehen für Tokens,
die Farbintensität für die Stärke der Aufmerksamkeit.

### Wozu ist es da?

Attention macht aus einer Token-Liste einen **kontextabhängigen Zustand**:
Ein Token wird nicht isoliert betrachtet, sondern im Zusammenhang mit anderen Tokens.

### Wie nutze ich es?

- Wechsle zwischen **Layer 1** und **Layer 2**
- Wechsle zwischen **Head 1** und **Head 2**
- Aktiviere **Causal Mask**, um Attention auf frühere Tokens zu begrenzen
- Beobachte:
  - wie sich Muster verändern
  - ob die Heatmap eher diagonal oder breit verteilt ist

### Typische Missverständnisse

- Attention ist **kein Sprachverständnis**
- Ein anderer Head ist **keine bessere Meinung**
- Die Heatmap zeigt **Gewichtung**, keine Bedeutung

## 2) MLP/FFN – Transformation nach der Attention

### Was sehe ich?

Im Schritt **MLP** siehst du,
wie ein Token-Vektor **nach der Attention weiterverarbeitet** wird.

Du kannst:

- ein Token auswählen (**Token i**)
- den Zustand **ohne Kontext** und **mit Kontext** vergleichen
- die Differenz (**Delta**) anzeigen

### Wozu ist es da?

Das MLP verändert die Vektoren weiter.
Hier wird sichtbar, dass **Kontext die Grundlage der Transformation verändert**.

### Wie nutze ich es?

- Wähle ein Token mit **Token i**
- Aktiviere **Vergleich anzeigen**
- Aktiviere **Delta anzeigen**
- Wechsle ggf. den Attention-Layer/Head und beobachte die Auswirkungen

### Typische Missverständnisse

- Das Delta ist **kein Fehler**
- MLP ist **keine Entscheidungsinstanz**
- Ohne Attention sieht man nur einen Teil des Effekts

## Ausführliches Beispiel: „Der Hund beißt den Mann“

Dieses Beispiel ist bewusst einfach gewählt, damit man den Übergang von **Attention** zu **MLP** gut nachvollziehen kann.

Prompt:
```
Der Hund beißt den Mann
```

Das Ziel des Experiments ist **nicht**, eine „richtige“ sprachliche Interpretation zu erzwingen,
sondern zu verstehen, was technisch passiert:

1. **Attention** erzeugt Kontext, indem Tokens unterschiedliche Gewichte füreinander erhalten.
2. **MLP/FFN** verarbeitet anschließend **jeden Token-Vektor einzeln weiter** – aber auf Basis dieses Kontexts.

### Schritt A: Vor der Attention (nur Embeddings)

Vor der Attention sind Tokens im Modell zunächst nur als Vektoren vorhanden,
die primär ihren Token-Inhalt (und ggf. Position) repräsentieren.

Wichtig:

- Das Token „Hund“ ist zunächst nur „Hund“.
- Es hat noch keinen Hinweis darauf, dass es im Satz z. B. als Handelnder auftaucht.
- Ebenso ist „Mann“ zunächst nur „Mann“.

In diesem Zustand sind Tokens **nebeneinander**, aber noch nicht „miteinander verbunden“.

> Merksatz:  
> **Embeddings sind Ausgangspunkte – noch kein Kontext.**

### Schritt B: Attention erzeugt einen Kontext-Vektor

In der Attention-Heatmap kannst du nun beobachten, dass Tokens nicht gleich „wichtig“ füreinander sind.

Typische Beobachtung (abhängig von Layer/Head):

- Das Verb-Token (z. B. „beißt“) legt Aufmerksamkeit auf inhaltlich relevante Tokens („Hund“, „Mann“).
- Tokens in der Nähe haben oft stärkere Gewichte als weit entfernte Tokens (Positionsinformation vorausgesetzt).
- Mit aktivierter **Causal Mask** sind Gewichte zu „zukünftigen“ Tokens eingeschränkt.

Wichtig ist nicht, dass du die Heatmap „sprachlich“ deutest,
sondern dass du erkennst:

- Ein Token bekommt Informationen **aus anderen Tokens** zugemischt.
- Dadurch entsteht pro Token ein **Kontext-Vektor**.

Man kann sich das so vorstellen:

- Vorher: „Hund“ (isoliert)
- Nachher: „Hund + Kontext aus dem Satz“

> Merksatz:  
> **Attention liefert den Kontext – sie bestimmt, welche anderen Tokens Einfluss haben.**

### Schritt C: MLP/FFN verarbeitet den Kontext weiter

Jetzt kommt das MLP (FFN). Hier ist die wichtigste didaktische Aussage:

> Das MLP erzeugt den Kontext nicht selbst.  
> Es verarbeitet die durch Attention bereits veränderten Vektoren weiter.

In der App kannst du das besonders gut sehen, wenn du den Vergleich nutzt.

#### 1) Token auswählen

Gehe in den Schritt **MLP** und wähle mit **Token i** z. B.:

- Token i = „Hund“
- Token i = „beißt“
- Token i = „Mann“

(Je nach Token siehst du andere Vektorformen.)

#### 2) Vergleich anzeigen

Aktiviere **Vergleich anzeigen**.

Damit siehst du zwei Wege:

- **ohne Attention**: MLP verarbeitet das reine Embedding
- **mit Attention**: MLP verarbeitet den Kontext-Vektor (Embedding + Kontextwirkung)

Das ist der zentrale Vergleich. Er zeigt:

- Der Eingang in das MLP ist **anders**, sobald Kontext berücksichtigt wird.
- Das Ergebnis der MLP-Transformation ist dadurch ebenfalls anders.

> Merksatz:  
> **MLP rechnet pro Token weiter – aber auf Basis dessen, was Attention geliefert hat.**

#### 3) Delta anzeigen

Aktiviere zusätzlich **Delta anzeigen**.

Delta ist hier didaktisch als Differenz gemeint:

- **Kontext − Embedding**

Du siehst also: *„Was hat Attention an diesem Token verändert?“*

Das ist nützlich, um zu verstehen, dass Kontext nicht „magisch“ ist,
sondern als **konkrete Verschiebung im Zahlenraum** sichtbar gemacht werden kann.

> Merksatz:  
> Delta ist keine Bewertung und kein Fehlermaß – es zeigt nur **die Veränderung durch Kontext**.

### Was du aus dem Beispiel mitnehmen solltest

- Attention erzeugt Kontext: Tokens werden abhängig vom restlichen Satz verändert.
- MLP/FFN verarbeitet diesen Zustand weiter: Zahlen werden nichtlinear transformiert.
- Ohne Attention wäre MLP nur eine Weiterverarbeitung isolierter Embeddings.
- Mit Attention wird MLP zu einer Weiterverarbeitung **kontextualisierter** Vektoren.

Kurz gesagt:

> **Attention verbindet Tokens – MLP verarbeitet das Ergebnis weiter.**

## Abgrenzung und Vereinfachungen

- Layer und Heads sind **didaktische Umschalter**
- Keine Aussage über reale Modellgrößen
- Keine Trainings- oder Optimierungslogik
- Die gezeigten Werte sind **simuliert**, um Effekte sichtbar zu machen

**Referenz:** LLM Simulator by cherware.de · Version v1.3.40
