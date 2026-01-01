# Expanded Explanations – UX & Content Contract

## Zweck dieses Dokuments
Dieses Dokument beschreibt die **UX- und Content-Regeln** für erweiterte Erklärungen
im Projekt **LLM Simulator by cherware.de**.

Es definiert:
- wie zusätzliche Erklärungen in der App integriert werden
- welche Inhalte in die App gehören – und welche bewusst nicht
- wie v1.0 (Referenzversion) und kommende Versionen sauber getrennt bleiben

Dieses Dokument ist **verbindlich** für alle Erweiterungen ab vNext.
Es richtet sich an Entwickler:innen, UX-Architekt:innen und Content-Autor:innen –
nicht an Endnutzer.

## 1. Grundannahmen

- v1.0 ist didaktisch abgeschlossen und eingefroren
- Die App ist eine **Simulation**, kein echtes LLM
- Ziel ist Orientierung und Verständnis, nicht Vollständigkeit
- Mehr Inhalt bedeutet nicht automatisch bessere Didaktik

## 2. Erklärungsebenen (Layer-Modell)

### Layer A – Core (v1.0)
- Fester Erklärungstext pro Pipeline-Schritt
- Immer sichtbar
- Unverändert und nicht erweiterbar
- Referenzebene für alle Nutzer

### Layer B – Expand (vNext)
- Aufklappbare Zusatzinformationen
- Ergänzen den Core, ersetzen ihn nicht
- Standardmäßig geschlossen
- Klar typisiert (siehe Abschnitt 3)

### Layer C – Linkout (vNext)
- Verweise auf Wiki / Blog / externe Dokumentation
- Öffnen außerhalb der App
- Maximal sparsam einsetzen

## 3. Inhaltstypen für Expand-Blöcke

### detail
- Zweck: präzisieren, nicht vertiefen
- 3–5 Sätze
- Keine Fachbegriffe ohne Erklärung

### misconception
- Zweck: typische Fehlannahmen korrigieren
- Sachlich, ruhig, nicht belehrend
- Fehlannahme implizit, Korrektur explizit

### example
- Zweck: Veranschaulichung
- Genau ein Beispiel
- Kein Code, keine Zahlen
- Ohne Vorwissen verständlich

### boundary
- Zweck: Abgrenzung der Simulation
- Was gilt hier – was nicht?
- Kurz und eindeutig

### why
- Zweck: didaktische Entscheidung erklären
- Transparenz statt Rechtfertigung
- Keine Verteidigung, kein Marketing

## 4. Quantitative Leitplanken

Pro Pipeline-Schritt gilt:

- Max. 3–6 Expand-Blöcke
- Max. 2 externe Links
- Core + Expand müssen zusammen auf Mobile gut lesbar bleiben

Wenn Inhalte darüber hinausgehen, gehören sie **nicht** in die App.

## 5. Tooltips – bewusste Rolle

- Tooltips sind Mikrohilfen
- Erklären Begriffe oder UI-Elemente
- Maximal ein Satz

Sobald ein Tooltip länger wird oder Zusammenhänge erklärt,
gehört der Inhalt in einen Expand-Block oder ins Wiki.

## 6. Mobile-First-Regeln

- Der Core-Text muss alleine ausreichend sein
- Expand-Blöcke sind optional
- Kein Expand-Block darf den gesamten Screen dominieren
- Wir vermeiden „Scroll-Monster“

Wenn sich ein Expand-Block wie ein Artikel liest,
ist er fehl am Platz.

## 7. Abgrenzung v1.0 vs. vNext

### v1.0
- Bestehende Core-Texte
- Bestehende Tooltips
- Keine strukturellen Änderungen

### vNext
- Zusätzliche JSON-Datei für erweiterte Erklärungen
- Accordion-/Expand-Mechanik im Erklärung-Bereich
- Externe Links zu weiterführender Dokumentation

## 8. Governance & Pflege

- Dieses Dokument ist der **UX-Vertrag**
- Änderungen erfolgen nur bewusst und versioniert
- Bei Konflikten gilt: Verständlichkeit vor Vollständigkeit

*LLM Simulator by cherware.de – UX Architecture*
