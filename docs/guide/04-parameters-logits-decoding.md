# Parameter – Logits & Decoding

Diese Datei beschreibt die **letzten Schritte der Pipeline** im  
*LLM Simulator by cherware.de* (Referenzstand **v1.3.40**):

- **Logits**: numerische Bewertungen möglicher nächster Tokens
- **Decoding**: Auswahlstrategie, wie aus diesen Bewertungen ein Token gewählt wird

Ziel ist eine **verständliche, entmystifizierende Erklärung**:
Nicht „das Modell entscheidet“, sondern **Parameter steuern die Auswahl**.

Die App ist eine **didaktische Simulation** – kein echtes LLM, keine echte Inferenz.

## Überblick

In diesem Kapitel:

- Was sind **Logits**?
- Warum Logits noch **keine Wahrscheinlichkeiten** sind
- Was bedeutet **Decoding**?
- Wirkung der Parameter:
  - Temperature
  - Top‑P (Nucleus Sampling)
  - Top‑K
  - Seed
- Ein ausführliches Beispiel zum Ausprobieren

## 1) Logits – Bewertungen, keine Entscheidungen

### Was sind Logits?

**Logits** sind rohe, numerische **Scores** für mögliche nächste Tokens.

Man kann sie sich vorstellen als:

> „Wie gut passt dieses Token *jetzt* als nächstes?“

Wichtig:
- Logits sind **nur Zahlen**
- Sie sind **nicht normiert**
- Sie sind **keine Wahrscheinlichkeiten**
- Sie sind **keine Entscheidung**

### Anschauliches Bild

Stell dir eine Rangliste vor:

- Token A: Score 12.3  
- Token B: Score 11.9  
- Token C: Score 4.2  

Das Modell hat hier **noch nichts ausgewählt**.
Es hat nur bewertet.

> Merksatz:  
> **Logits sagen, was möglich ist – nicht, was passiert.**

## 2) Von Logits zur Auswahl – warum Decoding nötig ist

Aus Logits allein folgt **keine eindeutige Ausgabe**.

Erst das **Decoding** legt fest:

- welche Tokens überhaupt in Betracht kommen
- wie stark Unterschiede gewichtet werden
- ob die Auswahl deterministisch oder zufallsbasiert ist

> Merksatz:  
> **Decoding ist die Regel, nach der aus Bewertungen eine Auswahl wird.**

Im Simulator ist Decoding der Punkt,
an dem die Parameter **sichtbar Einfluss auf die Ausgabe** haben.

## 3) Decoding-Parameter im Überblick

### Temperature

**Temperature** steuert,
wie stark Unterschiede zwischen Logits wirken.

- niedrige Temperature:
  - große Unterschiede dominieren
  - Auswahl wirkt stabil und vorhersehbar
- hohe Temperature:
  - Unterschiede werden abgeflacht
  - mehr Variation, mehr Zufall

> Merksatz:  
> Niedrige Temperature = vorsichtig  
> Hohe Temperature = experimentierfreudig

### Top‑K

**Top‑K** begrenzt die Auswahl auf die **K bestbewerteten Tokens**.

- K = 1:
  - immer das bestbewertete Token
- K = 5:
  - Auswahl nur aus den 5 besten Kandidaten

> Merksatz:  
> Top‑K bestimmt, **wie viele Optionen überhaupt erlaubt sind**.

### Top‑P (Nucleus Sampling)

**Top‑P** begrenzt die Auswahl auf so viele Tokens,
bis eine bestimmte **kumulative Wahrscheinlichkeit** erreicht ist.

Vereinfacht:

- Tokens werden nach Score sortiert
- so viele Tokens werden zugelassen,
  bis die Summe „ausreichend groß“ ist

> Merksatz:  
> Top‑P bestimmt, **wie breit der Wahrscheinlichkeitsraum ist**.

Top‑P passt sich damit **dynamisch** an:
- manchmal wenige Tokens
- manchmal mehr

### Seed

Der **Seed** steuert den Zufallsstartpunkt.

- gleicher Seed + gleiche Parameter → gleiche Ausgabe
- anderer Seed → andere Auswahl (bei zufallsbasiertem Decoding)

Wichtig:
- Seed erzeugt **keinen Inhalt**
- Er macht Zufall **reproduzierbar**

> Merksatz:  
> Seed macht Ergebnisse **wiederholbar**, nicht besser.

## 4) Ausführliches Beispiel: „Der Hund ist ein …“

Dieses Beispiel zeigt besonders gut,
wie Decoding-Parameter die Ausgabe beeinflussen.

Prompt:
```
Der Hund ist ein
```

Nach den bisherigen Pipeline-Schritten liegen Logits vor,
z. B. für Tokens wie:

- „Tier“
- „Haustier“
- „Säugetier“
- „Hund“
- …

Diese Tokens sind **alle plausibel**.
Welche gewählt wird, entscheidet **nicht der Text allein**, sondern das Decoding.

### Schritt A: Niedrige Temperature, kleines Top‑K

Einstellungen (Beispiel):

- Temperature: niedrig
- Top‑K: 1 oder 2
- Top‑P: aus oder hoch
- Seed: beliebig

Beobachtung:

- Die Ausgabe ist sehr stabil
- Meist wird immer derselbe Token gewählt
- Variation ist kaum sichtbar

Interpretation:

> Die Auswahl folgt streng der höchsten Bewertung.

### Schritt B: Höhere Temperature, größeres Top‑K

Einstellungen:

- Temperature: höher
- Top‑K: 5
- Top‑P: aktiv
- Seed: variieren

Beobachtung:

- Unterschiedliche, aber sinnvolle Fortsetzungen
- Mehr Abwechslung zwischen Läufen
- Trotzdem kein „Chaos“

Interpretation:

> Mehrere gut bewertete Optionen dürfen zum Zug kommen.

### Schritt C: Gleiche Parameter, unterschiedlicher Seed

Einstellungen:

- gleiche Temperature
- gleiches Top‑K / Top‑P
- Seed ändern

Beobachtung:

- unterschiedliche Ausgaben
- aber aus **demselben erlaubten Token-Raum**

Interpretation:

> Der Seed beeinflusst *welche* Option gewählt wird,
> nicht *welche Optionen möglich sind*.

## 5) Wichtige Klarstellungen

- Logits sind **keine Bedeutung**
- Decoding ist **keine Intelligenz**
- Parameter sind **keine Kreativitätsregler im menschlichen Sinn**
- Unterschiedliche Ausgaben entstehen,
  obwohl die zugrunde liegenden Bewertungen gleich sein können

> Zentrale Aussage:  
> **Variation entsteht durch Auswahlregeln, nicht durch neues Wissen.**

## Abgrenzung und Vereinfachungen

- Logits und Wahrscheinlichkeiten sind **vereinfacht dargestellt**
- Keine echten Softmax-Berechnungen
- Kein echtes Sampling
- Ziel ist **Beobachtbarkeit**, nicht mathematische Korrektheit

## Übergang

Nach dem Decoding entsteht eine **konkrete Ausgabe**.

→ Fortsetzung in: **05-summary-verarbeitungsweg-erkenntnisse.md**

**Referenz:** LLM Simulator by cherware.de · Version v1.3.40
