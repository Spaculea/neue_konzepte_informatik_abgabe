# Recherche: 22 Quellen für das Short Paper

Grundlage für das Short Paper *Gestaltungsprinzipien für Entwickler-Workflows mit KI-Coding-Agenten*. Von allen 22 Einträgen aus `../references.bib` wurden Abstract, Einleitung, Ergebnisse und Fazit gelesen, zusammengefasst und inhaltlich gruppiert. Grundlage waren die arXiv-Fassungen, bei Cui et al. das Working Paper vom Feb. 2025; Stand 16.10.2026. Vor dem Zitieren einzelner Zahlen bitte im Original gegenprüfen, besonders bei Preprints mit mehreren Versionen.

## Dateien

| Datei | Inhalt | Paper-Abschnitt |
|---|---|---|
| [00_uebersicht.md](00_uebersicht.md) | Tabelle aller 22 Quellen (Typ, Venue, Kernbefund, Wirkung auf Qualität und Produktivität), Matrix Quelle × Dimension | III, IV (Übersichtstabelle) |
| [01_agentensysteme_ueberblick.md](01_agentensysteme_ueberblick.md) | Survey, SWE-agent, OpenHands, AutoCodeRover | II Hintergrund |
| [02_autonomie_mensch.md](02_autonomie_mensch.md) | Agentless, HULA, Copilot vs. Agent, Oversight-Interviews | IV.A |
| [03_kontext_steuerung.md](03_kontext_steuerung.md) | CLAUDE.md-/AGENTS.md-Studien | IV.B |
| [04_qualitaetssicherung_fehler.md](04_qualitaetssicherung_fehler.md) | AgentCoder, MAST-Fehlertaxonomie, Patch-Sicherheit | IV.C |
| [05_praxis_produktivitaet.md](05_praxis_produktivitaet.md) | GitHub-PR-Studien, Verbreitung, RCTs zur Produktivität | IV (Produktivität), VI |
| [06_benchmarks_grenzen.md](06_benchmarks_grenzen.md) | SWE-bench und seine Schwächen | II, VI |
| [07_synthese.md](07_synthese.md) | Querbezüge, Kandidaten für die Prinzipien P1–P6 mit Belegen, Widersprüche, Forschungslücken, To-dos für `references.bib` | V, VI |

## Inhaltliche Gruppierung auf einen Blick

```
                    ┌─────────────────────────────────────┐
  Grundlagen        │ 1 Agentensysteme   6 Benchmarks     │  → II Hintergrund
                    └─────────────────────────────────────┘
                    ┌───────────────┬───────────────┬─────────────────┐
  Dimensionen       │ 2 Autonomie & │ 3 Kontext &   │ 4 Qualitäts-    │  → IV.A / B / C
  (Ergebnisteil)    │   Mensch      │   Steuerung   │   sicherung     │
                    └───────────────┴───────────────┴─────────────────┘
                    ┌─────────────────────────────────────┐
  Wirkung           │ 5 Praxis & Produktivität            │  → IV (Produktivität), VI
                    └─────────────────────────────────────┘
```

Jede Zusammenfassung hat dieselbe Struktur: Typ/Venue · Gegenstand/Methode · Kernbefunde mit Zahlen · Wirkung auf Qualität und Produktivität · Nutzen fürs Paper · Grenzen.

## Wichtigste Hinweise vorab

1. **cui2025genai untersucht reine Code-Completion (Copilot), keine Agenten.** Laut Ausschlusskriterium in `PLAN.md` gehört die Studie nicht zu den Ergebnis-Studien. Sie eignet sich nur als Kontrast in Einleitung oder Diskussion.
2. **Altersregel: Alle 22 Quellen sind zulässig** (nach Absprache: ab 2024, Dez. 2023 wird ebenfalls akzeptiert). Die älteste Quelle ist huang2023agentcoder (Preprint Dez. 2023). jimenez2024swebench erschien im Okt. 2023 auf arXiv, steht aber mit dem ICLR-Jahr 2024 in der Bib.
3. **watanabe2025agenticprs** ist inzwischen bei ACM TOSEM angenommen. Der BibTeX-Eintrag sollte aktualisiert werden (Details in [07_synthese.md](07_synthese.md)).
4. Die Gruppen 3 und 5 bestehen fast nur aus deskriptiven Studien oder Preprints. Die Wirkung wird meist *nicht* direkt gemessen. Das gehört als Grenze in die Diskussion.

Die PDFs wurden nicht ins Repo gelegt; alle Quellen sind über die arXiv-IDs bzw. DOIs in [00_uebersicht.md](00_uebersicht.md) abrufbar.
