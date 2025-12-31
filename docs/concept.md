# Didaktisches Konzept – cher-llm-simulator

## Ziel dieses Dokuments

Dieses Dokument beschreibt das **didaktische Gesamtkonzept** des Projekts *cher-llm-simulator*.

Es dient als **langfristige Referenz** für:
- die Weiterentwicklung der WebApp
- die Erstellung neuer Szenarien
- die Einordnung des Projekts nach außen (z. B. Blog, Vorträge, Schulungen)

Das Konzept ist bewusst **technisch präzise**, aber **didaktisch reduziert**.

## Grundidee

Der *cher-llm-simulator* ist keine Demo zur Beeindruckung,  
sondern ein Werkzeug zum **Verstehen der grundlegenden Mechanik von Large Language Models (LLMs)**.

Ziel ist es, beim Nutzer ein **korrektes mentales Modell** aufzubauen:

> Ein LLM ist kein Wissensspeicher,  
> sondern ein statistisches Modell zur **Next-Token-Vorhersage**  
> auf Basis von Vektorrepräsentationen und Kontextgewichtung.

## Zentrale didaktische Leitlinien

### 1. Ehrlichkeit vor Wow-Effekt

- Keine „scheinbar intelligenten“ Antworten ohne echtes Modell
- Keine implizite Gleichsetzung von Simulation und Realität
- Klare Kennzeichnung von Vereinfachungen

Verständlichkeit geht vor Show.

### 2. Mechanik vor Bedeutung

Der Simulator erklärt:
- **wie** etwas berechnet wird

nicht:
- **warum** eine Antwort inhaltlich richtig ist

Bedeutung und Weltwissen entstehen durch Training –  
nicht durch Architektur allein.

### 3. Kontrollierte Beispiele statt freier Eingabe

Freie Eingaben erzeugen falsche Erwartungen.

Deshalb basiert der Guided Mode auf:
- kuratierten Prompts
- vorgegebener Tokenisierung
- erklärbaren Ausgaben

Der Fokus liegt auf **vergleichenden Beispielen**, nicht auf Vollständigkeit.

### 4. Ein Lernziel pro Szenario

Jedes Szenario soll genau **einen Hauptaspekt** vermitteln.

Beispiele:
- Subword-Tokenisierung
- Mehrdeutigkeit ohne Kontext
- Einfluss von Instruktionen
- Iterative Generierung

Komplexe Effekte werden bewusst auf mehrere Szenarien verteilt.

## Szenario-basierter Ansatz

Die App folgt einem **datengetriebenen Ansatz**:

- Code = Visualisierung & Ablaufsteuerung
- Szenarien = Didaktik & Inhalt

Ein Szenario definiert:
- den Prompt-Stack
- die Tokenisierung
- die erwartete Ausgabe
- optionale Replay-Daten
- erklärende Hinweise

Dadurch ist das System:
- erweiterbar
- reproduzierbar
- dokumentierbar

## Guided Simulation vs. Mechanik-Sandbox

### Guided Simulation

Ziel:
- strukturiertes Verständnis

Eigenschaften:
- feste Szenarien
- kontrollierte Ausgaben
- klare Lernziele

Dieser Modus ist der **primäre Lernpfad**.

### Mechanik-Sandbox

Ziel:
- Entzauberung
- technisches Experimentieren

Eigenschaften:
- freie Eingabe
- keine semantische Garantie
- Fokus auf Zahlen und Abläufe

Dieser Modus ist **optional** und klar gekennzeichnet.

## Vereinfachungen (bewusst)

Um Verständlichkeit zu gewährleisten, werden u. a. folgende Vereinfachungen vorgenommen:

- stark reduzierte Modellgrößen
- vereinfachte Tokenisierung
- abstrahierte Attention-Darstellung
- keine echten Trainingsgewichte

Diese Vereinfachungen sind **kein Mangel**,  
sondern Voraussetzung für Erklärbarkeit.

## Zielgruppe

Der Simulator richtet sich primär an:
- IT-affine Nutzer
- Entwickler, Architekten, technische Entscheider
- Lehrende und Vortragende

Er ist **nicht** als Endnutzer-Chatbot gedacht.

## Abgrenzung zu echten LLMs

Der Simulator:
- erklärt Prinzipien
- vermittelt Struktur
- schafft Orientierung

Er ersetzt:
- kein echtes LLM
- keine Forschung
- keine produktive Nutzung

## Langfristige Perspektive

Das Projekt ist bewusst offen angelegt für:
- zusätzliche Szenarien
- tiefere technische Ansichten
- didaktische Erweiterungen

Das Grundprinzip bleibt jedoch stabil:
> **Simulation statt Magie. Erklärung statt Show.**

*Dieses Dokument ist Teil der offiziellen Projektdokumentation und dient als Referenz für alle weiteren Erweiterungen.*
