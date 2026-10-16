# Gruppe 5: Praxis und Produktivität

Für die Wirkung auf **Produktivität** quer durch IV und für die Diskussion. Zwei Untergruppen:

- **Feldstudien aus GitHub-Daten** (watanabe, li, robbes): Wie werden Agenten real genutzt, und wie oft wird ihr Code angenommen?
- **Kontrollierte Experimente zur Produktivität** (cui, becker): Was bringen KI-Werkzeuge messbar?

Die beiden Experimente widersprechen sich scheinbar (+26 % vs. −19 %). Genau diese Spannung ist ein Diskussionspunkt.

---

## watanabe2025agenticprs — On the Use of Agentic Coding: An Empirical Study of Pull Requests on GitHub

- **Typ / Venue:** Repository-Mining, **angenommen bei ACM TOSEM** (arXiv:2509.14745, v3 Feb. 2026) → BibTeX-Eintrag aktualisieren
- **Methode:** 567 PRs, die mit **Claude Code** erstellt wurden, aus 157 Open-Source-Projekten, verglichen mit menschlichen PRs
- **Kernbefunde:**
  - Agenten werden häufig für **Refactoring, Dokumentation und Tests** eingesetzt.
  - **83,8 % der Agenten-PRs werden gemergt**, bei menschlichen PRs 91,0 %.
  - 54,9 % der gemergten Agenten-PRs gehen **unverändert** durch, 45,1 % brauchen Nacharbeit, vor allem bei Bugfixes, Dokumentation und **projektspezifischen Konventionen**.
  - Wenn nachgearbeitet wird, ist der Umfang nicht größer als bei menschlichen PRs.
  - Empfehlungen der Autoren: **PRs klein halten**, **Projektregeln und Architekturvorgaben für den Agenten festhalten**, projektbezogene CI/CD-Prüfungen einbinden.
- **Wirkung:** *Qualität:* meist akzeptabel, aber auf menschliche Nacharbeit angewiesen. *Produktivität:* guter Ausgangspunkt, der Review-Aufwand ist vergleichbar mit menschlichen PRs.
- **Nutzen fürs Paper:** Praxisbeleg für die Prinzipien „kleine, prüfbare Änderungen“, „Konventionen als Kontext“ und „menschliches Review bleibt nötig“.
- **Grenzen:** Nur Claude Code, nur öffentlich erkennbare PRs (Selektionseffekt), Zeitraum 2025.

---

## li2025aidev — The Rise of AI Teammates in SE 3.0: How Autonomous Coding Agents Are Reshaping Software Engineering (AIDev)

- **Typ / Venue:** Datensatz und Repository-Mining, arXiv-Preprint (2507.15003). Queen's University.
- **Methode:** Datensatz **AIDev** mit über **456.000 PRs** von fünf Agenten (OpenAI Codex, Devin, GitHub Copilot Agent, Cursor, Claude Code) aus 61.000 Repositories mit 47.000 Entwicklern
- **Kernbefunde:**
  - Agenten-PRs werden **deutlich seltener angenommen** als menschliche, besonders bei Features, Bugfixes und Performance. Akzeptanzraten: Codex 64 %, Devin 49 %, Copilot 35 %.
  - **Dokumentation ist eine Stärke:** Codex 88,6 % und Claude Code 85,7 % Akzeptanz gegenüber 76,5 % bei Menschen.
  - **Tempo:**
    - Copilot erledigt 75 % seiner Aufgaben in unter 18,5 Minuten.
    - Angenommene Codex-PRs werden nach median **0,3 h** geschlossen, menschliche nach 3,9 h. Die Autoren stellen deshalb die **Tiefe des Reviews** infrage.
  - 58,2 % der Agenten-PRs erhalten **kein explizites Review**. Review-Bots kommen oft vom selben Anbieter wie der Agent, was einen geschlossenen Kreislauf mit Bias-Risiko ergibt.
  - Fallbeispiel: Ein Entwickler reicht in 5 Tagen 164 Codex-PRs ein, fast so viele wie seine 176 PRs aus 3,5 Jahren davor. Die Beiträge sind aber **strukturell einfacher**.
  - **Urheberschaft** ist oft nicht nachvollziehbar: Codex und Claude Code schreiben Commits den Menschen zu.
  - Die Lücke zwischen Benchmark-Leistung und Akzeptanz in der Praxis stellt die ökologische Validität von SWE-bench und Co. infrage.
- **Wirkung:** *Produktivität:* viel mehr Durchsatz und Tempo. *Qualität:* geringere Akzeptanz bei komplexen Aufgaben, oberflächlicheres Review.
- **Nutzen fürs Paper:** Größte Praxisdatenbasis. Belegt, dass der Agent zur Aufgabe passen muss (Doku ja, komplexe Features vorsichtig) und dass Nachvollziehbarkeit und Review fehlen. Verbindet sich mit Gruppe 6.
- **Grenzen:** Vorläufige Analyse, öffentliche Repositories, Akzeptanz ist nur ein grobes Maß für Qualität.

---

## robbes2026agenticmuch — Agentic Much? Adoption of Coding Agents on GitHub

- **Typ / Venue:** Großangelegtes Repository-Mining, arXiv-Preprint (2601.18341, v2 Apr. 2026)
- **Methode:** **128.018 GitHub-Projekte**. Gesucht wird nach Spuren von Agenten auf Datei- und Commit-Ebene (Konfigurationsdateien, Co-Author-Einträge). Stand 21.02.2026.
- **Kernbefunde:**
  - Geschätzte Verbreitung **22,20 % bis 28,66 %** der Projekte, Tendenz steigend. Der Anstieg erfolgte hauptsächlich zwischen März und Oktober 2025.
  - Die Nutzung ist **breit**: Projekte jeder Reife, etablierte Organisationen, viele Sprachen und Themen. Ein Teil der Projekte nutzt Agenten „konsistent“ (5–20 % der Commits) oder sogar „durchgängig“ (über 20 %).
  - Commits mit Agentenbeteiligung sind **größer** als rein menschliche und betreffen oft **Features und Bugfixes**.
- **Wirkung:** nicht direkt gemessen
- **Nutzen fürs Paper:** Motivation in der Einleitung: Agenten sind bereits Praxis, nicht Zukunft. Die großen Commits stehen in Spannung zu sajadi2025patchsecurity (mehr Dateien, mehr Risiko) und watanabe2025agenticprs (kleine PRs empfohlen).
- **Grenzen:** Agenten ohne Spuren werden nicht erkannt (Untergrenze). Spuren wie Konfigurationsdateien belegen keine intensive Nutzung.

---

## cui2025genai — The Effects of Generative AI on High-Skilled Work: Evidence from Three Field Experiments with Software Developers

- **Typ / Venue:** Drei randomisierte Feldexperimente (RCTs), Management Science 2025 (DOI 10.1287/mnsc.2025.00535)
- **Methode:** Zufällig vergebener Zugang zu **GitHub Copilot (Code-Completion)** bei Microsoft, Accenture und einem anonymen Fortune-100-Unternehmen, **4.867 Entwickler**, 2 bis 8 Monate
- **Kernbefunde:**
  - **+26,08 %** abgeschlossene Aufgaben (PRs) pro Woche (SE 10,3 %), +13,55 % Commits, +38,38 % Builds
  - **Weniger erfahrene Entwickler** nutzen das Werkzeug häufiger und profitieren stärker. Bei langer Betriebszugehörigkeit oder senioren Positionen ist kein signifikanter Effekt messbar.
  - Der Effekt ist kleiner als im Labor (dort 58 % Zeitersparnis), weil Coding nur einen Teil der Arbeit ausmacht.
- **Wirkung:** *Produktivität:* positiv, zumindest im Output gemessen. *Qualität:* nicht gemessen.
- **Nutzen fürs Paper:** Wichtigster Feldbeleg für Produktivitätsgewinne durch KI-Werkzeuge. Gegenpol zu becker2025metr.
- **⚠ Achtung:** Untersucht wird **reine Code-Completion, kein Agent**. Das fällt unter das Ausschlusskriterium in PLAN.md („Reine Code-Completion ohne agentisches Verhalten“). Empfehlung: nur als Kontrast bzw. Ausgangspunkt in Einleitung oder Diskussion nutzen, nicht als Ergebnis-Studie zählen.
- **Grenzen:** Experimente mit viel Rauschen und uneinheitlicher Durchführung. Output-Metriken wie die Zahl der PRs sagen nichts über den Wert der Arbeit.

---

## becker2025metr — Measuring the Impact of Early-2025 AI on Experienced Open-Source Developer Productivity (METR)

- **Typ / Venue:** Randomisierte kontrollierte Studie, arXiv-Preprint (2507.09089)
- **Methode:**
  - **16 erfahrene Open-Source-Entwickler** bearbeiten **246 echte Issues** (Ø 2 h) in ihren eigenen Projekten: Ø 23.000 Sterne, über 1,1 Mio. LOC, Ø 5 Jahre Erfahrung im Projekt.
  - Für jede Aufgabe wird zufällig entschieden, ob KI erlaubt ist; dann meist **Cursor Pro mit Claude 3.5/3.7 Sonnet**, auch im Agenten- und Chat-Modus.
  - 143 h Bildschirmaufnahmen wurden ausgewertet.
- **Kernbefunde:**
  - **Mit KI dauern Aufgaben 19 % länger.**
  - Die Entwickler erwarteten vorher **−24 %** und schätzten nachher **−20 %**. Ökonomen (−39 %) und ML-Experten (−38 %) lagen ebenso daneben.
  - **Die eigene Wahrnehmung des Nutzens ist also unzuverlässig.**
  - Wahrscheinliche Ursachen:
    - übertriebener Optimismus
    - hohe Vertrautheit der Entwickler mit dem Repository
    - große, komplexe Codebasen
    - **geringe Zuverlässigkeit der KI**: unter 44 % der Generierungen übernommen, 9 % der Zeit für Review und Nachbesserung
    - **implizites Projektwissen**, das der KI fehlt
  - Die PR-Qualität ist in beiden Bedingungen qualitativ ähnlich.
- **Wirkung:** *Produktivität:* negativ in diesem Umfeld. *Qualität:* kein erkennbarer Unterschied.
- **Nutzen fürs Paper:** Der stärkste Gegenbefund. Zeigt, dass Kontext und Vertrautheit über den Nutzen entscheiden, und dass Selbsteinschätzung keine Messung ersetzt (methodisch wichtig, da viele Studien auf Umfragen beruhen, z. B. HULA).
- **Grenzen:** Kleine Stichprobe, sehr spezielles Umfeld (Experten in eigenen Großprojekten), Stand Anfang 2025. Die Autoren betonen selbst, dass sich das Ergebnis nicht verallgemeinern lässt.
