# Plan: Short Paper „Gestaltungsprinzipien für Entwickler-Workflows mit KI-Coding-Agenten“

Baut auf `abstract.tex` auf. Annahmen, die vor dem Start zu klären sind, stehen ganz unten unter „Offene Punkte“.

## 1. Rahmen

| Punkt | Annahme |
|---|---|
| Format | IEEE Conference (`IEEEtran`), zweispaltig |
| Umfang | 4 Seiten Text + Literaturverzeichnis (Short Paper) |
| Sprache | Deutsch |
| Autoren | 3 |
| Forschungsfrage | Welche Gestaltungsprinzipien für Entwickler-Workflows mit KI-Coding-Agenten lassen sich aus der aktuellen Forschung ableiten, und wie wirken sie sich auf Codequalität und Produktivität aus? |

## 2. Gliederung und Seitenbudget

| Abschnitt | Seiten | Inhalt |
|---|---|---|
| I. Einleitung | 0,5 | Motivation (Wandel von Code-Completion zu Agenten), Problem (Workflow-Gestaltung statt Werkzeugwahl), Forschungsfrage, Beitrag des Papers, Aufbau |
| II. Hintergrund | 0,4 | Begriffe: KI-Coding-Agent, Autonomiestufen, Workflow, Human-in-the-Loop; Abgrenzung zu reiner Code-Completion |
| III. Methodik | 0,6 | Datenquellen, Suchstring, Zeitraum, Ein-/Ausschlusskriterien, Auswahlprozess (Zahlen je Schritt), Kategorienschema, Extraktionsbogen |
| IV. Ergebnisse | 1,5 | A) Autonomiegrad und menschliche Beteiligung, B) Kontext und Steuerung, C) Qualitätssicherung und Fehlermuster. In jedem Teil die Wirkung auf **Qualität** und **Produktivität** getrennt benennen. Eine Übersichtstabelle: Studie × Dimension × Studientyp × Befund |
| V. Gestaltungsprinzipien | 0,5 | 4–6 Prinzipien (P1–Pn), jeweils mit Begründung und den stützenden Quellen |
| VI. Diskussion | 0,4 | Forschungslücken (Benchmarks vs. Praxis, fehlende Langzeitstudien, Sicherheit, Rolle der Entwickler), Grenzen der eigenen Analyse (Threats to Validity) |
| VII. Fazit | 0,1 | Antwort auf die Forschungsfrage in 3–4 Sätzen, Ausblick |

Abbildungen: maximal eine Abbildung (z. B. Workflow-Schema „Planen → Prüfen → Ausführen → Verifizieren“ oder Auswahlprozess der Literatur) und eine Tabelle. Mehr passt auf 4 Seiten nicht.

## 3. Methodik der Literaturanalyse

### Quellen
- ACM Digital Library, IEEE Xplore, arXiv (Preprints im Paper kennzeichnen)
- Konferenzen: ICSE, FSE, ASE, CHI, NeurIPS, ICLR (ergänzend: MSR, ICML)
- Zeitraum: 01/2024 bis Stichtag (Stichtag festlegen und im Paper nennen)

### Suchstring (Vorschlag, je Datenbank anpassen)
```
("coding agent" OR "software engineering agent" OR "agentic coding"
  OR "LLM-based agent" OR "AI pair programmer")
AND
(workflow OR "human-in-the-loop" OR autonomy OR "code review"
  OR testing OR productivity OR "code quality")
```

### Einschlusskriterien
- Untersucht LLM-basierte Agenten, die mehrschrittig arbeiten und Werkzeuge nutzen (Dateien bearbeiten, Befehle ausführen, Tests laufen lassen)
- Enthält eine empirische Evaluation (Nutzerstudie, Benchmark oder Feldstudie) oder eine Systembeschreibung mit Evaluation
- Veröffentlicht ab 2024, auf Englisch oder Deutsch

### Ausschlusskriterien
- Reine Code-Completion ohne agentisches Verhalten
- Positionspapiere ohne eigene Daten (höchstens für Einleitung oder Diskussion)
- Kein Bezug zu Workflow, Qualität oder Produktivität

### Auswahlprozess
1. Suche → Treffer je Datenbank notieren
2. Duplikate entfernen
3. Screening nach Titel und Abstract (jede Arbeit von einer Person, unklare Fälle von zweiter Person)
4. Volltext-Screening
5. Rückwärtssuche über die Literaturverzeichnisse der eingeschlossenen Arbeiten (Snowballing)

Die Zahlen jedes Schritts in einer gemeinsamen Tabelle (z. B. Spreadsheet) festhalten. Sie kommen in Abschnitt III und ersetzen das `[n]` im Abstract.

### Extraktionsbogen (je Arbeit)
- Bibliografische Angaben, Venue, Jahr, Preprint ja/nein
- Studientyp: Nutzerstudie / Benchmark / Systembeschreibung / Feldstudie
- Untersuchte Agenten bzw. Werkzeuge
- Dimension(en): Autonomie / Kontext & Steuerung / Qualitätssicherung
- Untersuchte Workflow-Elemente (z. B. Planungsschritt, Kontextdateien, Tests als Leitplanke, Review)
- Gemessene Wirkung auf Qualität (Metrik + Ergebnis)
- Gemessene Wirkung auf Produktivität (Metrik + Ergebnis)
- Berichtete Fehlermuster
- Limitationen laut Autoren

### Einstiegsliteratur (vor Aufnahme prüfen, ob die Kriterien erfüllt sind)
- SWE-bench (Jimenez et al., ICLR 2024): Standard-Benchmark, relevant für die Benchmark-Kritik
- SWE-agent (Yang et al., NeurIPS 2024): Einfluss der Agent-Computer-Schnittstelle
- OpenHands (Wang et al., ICLR 2025): offene Agentenplattform
- Agentless (Xia et al., 2024): einfacher, fest vorgegebener Workflow als Gegenposition zu autonomen Agenten
- METR-Studie zur Produktivität erfahrener Open-Source-Entwickler mit KI-Werkzeugen (2025): Gegenbefund zur erwarteten Produktivitätssteigerung

## 4. Zeitplan

Wochen relativ zum Start. An die Abgabefrist anpassen.

| Woche | Phase | Ergebnis |
|---|---|---|
| 1 | Protokoll | Suchstring, Kriterien und Extraktionsbogen festgelegt; `references.bib` und Grundgerüst `paper.tex` angelegt |
| 2 | Suche und Screening | Liste der eingeschlossenen Arbeiten mit Zahlen je Schritt |
| 3 | Extraktion | Extraktionsbogen für alle Arbeiten ausgefüllt |
| 4 | Synthese | Befunde je Dimension, Entwurf der Prinzipien P1–Pn, Übersichtstabelle |
| 4–5 | Schreiben | Erstfassung aller Abschnitte |
| 5 | Abstract finalisieren | Platzhalter in `abstract.tex` mit echten Zahlen und Befunden ersetzt |
| 6 | Review und Abgabe | Gegenseitiges Lesen, Seitenlimit prüfen, Literaturverzeichnis prüfen, Abgabe |

## 5. Aufgabenverteilung (Vorschlag)

| Person | Dimension (Extraktion + Ergebnisteil) | Weitere Abschnitte |
|---|---|---|
| A | Autonomiegrad und menschliche Beteiligung | Einleitung, Hintergrund |
| B | Kontext und Steuerung | Methodik |
| C | Qualitätssicherung und Fehlermuster | Diskussion, Fazit |
| Alle | | Gestaltungsprinzipien, Abstract, finales Review |

Suche und Screening werden gemeinsam gemacht, damit alle die gleiche Literaturbasis haben.

## 6. Repo-Struktur

```
abstract.tex        # Einreichung Abstract
paper.tex           # Short Paper (IEEEtran)
sections/           # ein .tex pro Abschnitt, per \input eingebunden → weniger Merge-Konflikte
references.bib      # gemeinsame BibTeX-Datei, Stil IEEEtran
figures/            # Abbildungen
```

Ein Abschnitt pro Datei erlaubt paralleles Arbeiten ohne Konflikte. Build-Artefakte sind per `.gitignore` ausgeschlossen.

## 7. Qualitätscheckliste vor der Abgabe

- [ ] Forschungsfrage wird im Fazit explizit beantwortet (Qualität **und** Produktivität)
- [ ] Jedes Prinzip in Abschnitt V ist durch mindestens zwei Quellen gestützt oder als schwach belegt markiert
- [ ] Preprints sind als solche gekennzeichnet
- [ ] Zahlen im Abstract stimmen mit Abschnitt III überein
- [ ] Keine roten `\todo{}`-Platzhalter mehr im PDF
- [ ] Seitenlimit eingehalten
- [ ] Einheitliche Begriffe (z. B. immer „KI-Coding-Agent“)

## 8. Offene Punkte

- Genaues Seitenlimit und ob das Literaturverzeichnis mitzählt
- Abgabefrist(en) für Abstract und Paper
- Sind arXiv-Preprints als Quellen zugelassen?
- Vorgaben zu Mindestanzahl an Quellen oder Zitierstil
