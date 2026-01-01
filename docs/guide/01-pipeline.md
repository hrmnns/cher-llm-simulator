# Pipeline – Verarbeitungsweg im LLM Simulator

Diese Datei beschreibt die **Pipeline des LLM Simulator by cherware.de** im Referenzstand **v1.3.40**.  
Sie erläutert jeden einzelnen Schritt so, dass klar wird,

- was technisch (vereinfacht) passiert,
- was in der App sichtbar ist,
- und was konkret beobachtet oder ausprobiert werden kann.

Die Pipeline ist didaktisch aufgebaut und bildet **keine vollständige Transformer-Architektur** ab.

## Überblick

**Eingabe → Tokenisierung → Embeddings → Attention → MLP → Logits → Decoding → Zusammenfassung**

Jeder Schritt kann in der App **direkt angewählt** werden. Es existiert kein fortlaufender Modellzustand – jeder Schritt ist eine erklärbare Momentaufnahme.

## 1. Eingabe

### Was passiert
Der gesamte **Prompt-Kontext** wird zusammengestellt. Er besteht aus drei Teilen:
**System**, **Instruktion** und **User**. Dieser Stack bildet die vollständige Texteingabe für alle weiteren Schritte.

### Was ist sichtbar
- Prompt-Stack mit drei Textfeldern (read-only im Guided-Modus)
- Hinweis zur Kuratierung im Guided Mode

### Was kann beobachtet werden
- Szenarien verändern den Prompt-Stack konsistent
- Reihenfolge und Trennung der Rollen bleiben stabil

### Typische Missverständnisse
- Noch keine Bedeutung, kein „Verstehen“
- Sandbox erlaubt Texteingabe, garantiert aber keine sinnvolle Weiterverarbeitung

## 2. Tokenisierung

### Was passiert
Der Text wird in **Token** zerlegt. Tokens sind Einheiten aus dem Modellvokabular und entsprechen nicht zwingend ganzen Wörtern (Subwords, Leerzeichen, Satzzeichen).

### Was ist sichtbar
- Token-Chips mit Token-Text und Token-ID
- Rekonstruktion des Textes aus Tokens (Kontrolle)

### Was kann beobachtet werden
- Subword-Zerlegung bei Komposita
- Führende Leerzeichen in Token-Texten
- Feste, szenariobasierte Tokenisierung im Guided Mode

### Typische Missverständnisse
- Token ≠ Wort
- Tokenisierung ist hier nicht dynamisch berechnet

## 3. Embeddings

### Was passiert
Jedes Token wird auf einen **Zahlenvektor** abgebildet. Optional wird **Positional Encoding** additiv ergänzt, um die Position im Kontext zu berücksichtigen.

### Was ist sichtbar
- Auswahl der Vektordimension (**d_model**)
- Checkbox für Positional Encoding
- Vektor-Darstellung pro Token (Barcode-Ansicht)

### Was kann beobachtet werden
- Größere d_model-Werte erzeugen längere Vektoren
- Positional Encoding verändert Vektoren positionsabhängig
- Änderungen wirken sich auf Attention und MLP aus

### Typische Missverständnisse
- Dimensionen haben keine semantische Bedeutung
- Werte sind seeded simuliert

## 4. Attention

### Was passiert
Attention berechnet, **wie stark Tokens einander gewichten**. Mit Causal Mask darf ein Token nur auf sich selbst und frühere Tokens achten.

### Was ist sichtbar
- Attention-Heatmap (Token × Token)
- Auswahl von Layer und Head
- Toggle für Causal Mask

### Was kann beobachtet werden
- Maskierte Bereiche oberhalb der Diagonalen
- Unterschiedliche Gewichtungsmuster je Head/Layer
- Stabil reproduzierbare Muster

### Typische Missverständnisse
- Attention ist keine Logik oder Schlussfolgerung
- Gewichte sind didaktische Näherungen

## 5. MLP

### Was passiert
Das MLP (Feedforward-Netz) transformiert Token-Repräsentationen nichtlinear. Die App zeigt den Unterschied **mit und ohne Kontext** (Attention).

### Was ist sichtbar
- Auswahl eines Tokens (Index i)
- Vergleichsansicht: ohne vs. mit Attention
- Optional: Delta-Ansicht

### Was kann beobachtet werden
- Kontext verändert die Repräsentation sichtbar
- Delta zeigt den Beitrag des Kontexts

### Typische Missverständnisse
- Kein echtes Transformer-Block-MLP
- Werte sind nicht interpretierbar im Sinne von Features

## 6. Logits

### Was passiert
Aus der MLP-Ausgabe entstehen **Logits** – Rohwerte für mögliche nächste Tokens. Nach Softmax ergeben sich Wahrscheinlichkeiten.

### Was ist sichtbar
- Top-K-Liste möglicher Tokens pro Schritt
- Slider für Generationsschritte
- Hervorhebung des gewählten Tokens

### Was kann beobachtet werden
- Verteilungen verändern sich durch Filterung
- Logits sind nicht normiert

### Typische Missverständnisse
- Logits ≠ Wahrscheinlichkeiten
- Werte stammen aus Simulation bzw. Rekonstruktion

## 7. Decoding

### Was passiert
Beim Decoding wird aus der Verteilung ein Token ausgewählt (Greedy oder Sampling). Dieser Prozess wird iterativ wiederholt.

### Was ist sichtbar
- Feste Ausgabe im Guided Mode
- Interaktive Decoding-Demo:
  - Greedy / Sampling
  - Temperature
  - Top-K
  - Top-P
  - Seed

### Was kann beobachtet werden
- Temperature steuert Varianz
- Top-K / Top-P beschneiden den Kandidatenraum
- Seed macht Sampling reproduzierbar

### Typische Missverständnisse
- Demo beeinflusst nicht die feste Guided-Ausgabe
- Greedy ignoriert Seed

## 8. Zusammenfassung

### Was passiert
Kein Modellschritt, sondern eine **strukturierte Rückschau** auf den gesamten Lauf.

### Was ist sichtbar
- Ergebnis (Prompt + Output)
- Kurzüberblick Pipeline
- Zentrale Erkenntnisse
- Run-Snapshot (JSON)

### Was kann beobachtet werden
- Snapshot enthält Decoding-Demo-Parameter
- Snapshot dient der Dokumentation, nicht der Modellrekonstruktion

### Typische Missverständnisse
- Snapshot ist kein Trainings- oder Modellzustand

**Referenz:** LLM Simulator by cherware.de · Version v1.3.40  
