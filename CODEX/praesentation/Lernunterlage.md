# Lernunterlage: KI-Coding-Agenten in Entwickler-Workflows

Für die 10-Minuten-Präsentation und die fachliche Abfrage. Grundlage: `CODEX/paper_25.tex` (21 Arbeiten, Literaturstand 16.10.2026), die Folien und die Recherche unter `recherche/`.

**Wichtigste Regel für die Fragerunde:** Antwortet so vorsichtig wie das Paper. Die Recherche-Notizen enthalten an einigen Stellen zugespitzte Aussagen, etwa „11× mehr Schwachstellen“ oder „mehr Autonomie = mehr Risiko“. Diese Zuspitzungen hat das Paper bewusst abgeschwächt (siehe Abschnitt 7).

---

## 1. Die Kernbotschaft in 30 Sekunden

> Wir haben 21 Arbeiten von 2024 bis 2026 ausgewertet und daraus fünf Gestaltungsprinzipien abgeleitet: Planung gemeinsam prüfen, Autonomie nach Risiko staffeln, Kontext gezielt ergänzen, mehrstufig verifizieren und überprüfbar integrieren. Belegt sind nur einzelne, eng begrenzte Maßnahmen, zum Beispiel ein Linter in SWE-agent. Dass die fünf Prinzipien zusammen als Workflow wirken, ist nicht nachgewiesen, und ein allgemeiner Produktivitätsgewinn folgt nicht aus der Literatur. Aktive Arbeitszeit, Gesamtdauer, Testbestehen und funktionale Korrektheit muss man getrennt messen.

**Die drei Sätze, die man nie vergessen darf:**
1. Weniger aktive Arbeit ist keine kürzere Gesamtdauer (Chen: 12,5 min aktiv, mit Agentenlaufzeit 27,9 min).
2. Bestandene Tests sind keine korrekte Lösung (AutoCodeRover 51/78; Wang 29,6 % Verhaltensabweichungen).
3. Die Prinzipien sind begründete Empfehlungen, keine belegten Wirkungsaussagen.

---

## 2. Zeitplan für 10 Minuten

Die Sprechernotizen haben zusammen rund **860 Wörter**. Bei normalem Vortragstempo (120–130 Wörter pro Minute) sind das nur **etwa 7 Minuten**. Rund 3 Minuten fehlen also. Zwei Wege, sie zu füllen:
- langsamer sprechen und nach jeder Kernzahl kurz pausieren (bringt etwa 1 Minute),
- die **Ergänzungen** aus Abschnitt 3 einbauen (bringen zusammen etwa 2–3 Minuten).

Am besten einmal mit Stoppuhr durchsprechen. Zielwerte:

| Folie | Inhalt | Zielzeit | kumuliert |
|---|---|---|---|
| 1 | Titel | 0:20 | 0:20 |
| 2 | Motivation | 0:50 | 1:10 |
| 3 | Forschungsfrage | 0:45 | 1:55 |
| 4 | Vorgehen | 1:00 | 2:55 |
| 5 | Befund 1: Produktivität | 1:15 | 4:10 |
| 6 | Befund 2: Kontext | 1:00 | 5:10 |
| 7 | Befund 3: Verifikation und Integration | 1:15 | 6:25 |
| 8 | Fünf Prinzipien | 1:20 | 7:45 |
| 9 | Evidenzgrenzen | 0:55 | 8:40 |
| 10 | Zielkonflikt und nächster Schritt | 0:45 | 9:25 |
| 11 | Fazit | 0:35 | 10:00 |
| 12 | Quellen | nur zeigen | – |

Kontrollpunkte: Bei **Folie 5 ungefähr bei Minute 3**, bei **Folie 8 ungefähr bei Minute 6:30**. Liegt ihr deutlich darunter, die Ergänzungen nutzen. Liegt ihr darüber, bei Folie 7 den Satz zu Watanabe und bei Folie 9 den Satz zu Python kürzen.

---

## 3. Folie für Folie: Botschaft, Zahlen, Ergänzung, wahrscheinliche Frage

### Folie 2 – Motivation
- **Botschaft:** Agenten sind in der Praxis angekommen, aber Benchmark-Erfolge und PR-Zahlen sagen nichts über Zeitersparnis oder Korrektheit.
- **Zahlen:** 128.018 GitHub-Projekte; **22,20 %** konservativ, **28,66 %** hochgerechnete obere Schätzung (Robbes et al., ACM TOSEM 2026).
- **Ergänzung (+15 s):** „Erkannt wurden die Agenten über Spuren wie Konfigurationsdateien oder Co-Author-Einträge in Commits. Agenten ohne solche Spuren fallen durch, deshalb ist 22,2 % eher eine Untergrenze.“
- **Mögliche Frage:** *Wie wurde die Adoption gemessen?* → über Spuren in Dateien und Commits; das ist eine Untergrenze, und eine Konfigurationsdatei belegt noch keine intensive Nutzung.

### Folie 3 – Forschungsfrage
- **Botschaft:** Die Frage hat zwei Teile: (1) Welche Prinzipien lassen sich ableiten? (2) Was ist belegt, wo liegen die Grenzen? Die drei Dimensionen sind Autonomie, Kontext und Qualitätssicherung.
- **Ergänzung (+15 s):** „Wir haben bewusst nicht gefragt ‚Machen Agenten produktiver?‘. Die Studien messen dafür zu unterschiedliche Dinge. Wir fragen stattdessen, wie man Agenten sinnvoll einbindet und wie belastbar die Belege dafür sind.“

### Folie 4 – Vorgehen
- **Botschaft:** narrative Literaturanalyse, keine systematische Vollerhebung; Evidenzarten werden getrennt.
- **Fakten:** ACM DL, IEEE Xplore, arXiv sowie Rückwärtssuche. Einschluss: ab 2024, Englisch oder Deutsch, mehrschrittige, werkzeugnutzende LLM-Agenten, empirisch oder als System mit Evaluation, Bezug zu Workflow, Qualität oder Produktivität. Ablauf: Duplikate entfernen, dann Titel und Abstract, dann Volltext.
- **Ergänzung (+20 s):** „Ein Beispiel, warum die Trennung wichtig ist: Wenn zwei Agenten-Architekturen verglichen werden, sich aber gleichzeitig Modell, Werkzeuge und Budget unterscheiden, kann man den Unterschied nicht der Autonomie zuschreiben. Deshalb rechnen wir keine Effekte über Studien hinweg zusammen.“
- **Mögliche Frage:** *Warum nicht systematisch?* → siehe Abschnitt 6, Frage M1.

### Folie 5 – Befund 1: Produktivität
- **Botschaft:** Weniger aktive Arbeit heißt nicht kürzere Gesamtdauer; Werkzeugtyp, Population und Zeitmaß muss man trennen.
- **Zahlen Chen et al. (CHI '26):** 20 Studierende, OpenHands gegenüber Copilot. Erfolg **25 % → 60 % (+35 Prozentpunkte)**. Aktive Zeit erfolgreicher Aufgaben **25,1 → 12,5 min**, mit Agentenlaufzeit **27,9 min**.
- **Zahlen Becker et al. (METR, Preprint):** 16 erfahrene Open-Source-Entwickler, 246 Aufgaben in den eigenen Projekten, meist Cursor. **+19 % Bearbeitungszeit** mit KI, geschätzt wurde aber **20 % Ersparnis**.
- **Ergänzung (+30 s):** „Dazu passt Cui et al. in Management Science: drei randomisierte Feldexperimente mit 4.867 Entwicklern, **+26 %** erledigte Aufgaben. Das ist aber Copilot-Codevervollständigung, kein Agent, und gemessen wurden PRs pro Woche, keine Bearbeitungszeit. Deshalb ist +26 % gegenüber −19 % kein echter Widerspruch.“
- **Mögliche Frage:** *Ist +26 % gegen +19 % Zeit ein Widerspruch?* → siehe Abschnitt 6, Frage I1.

### Folie 6 – Befund 2: Kontext
- **Botschaft:** LLM-generierte Kontextdateien kosten mehr, ohne messbar mehr Aufgaben zu lösen.
- **Zahlen Gloaguen et al.:** kein signifikanter Gesamteffekt gegenüber fehlender Kontextdatei; Kosten **+20 % (SWE-bench Lite) / +23 % (CTXBench)**; Schritte **+2,45 / +3,92**. Auf CTXBench sind von Entwicklern geschriebene Dateien signifikant besser als LLM-generierte, aber nicht signifikant besser als gar keine Datei.
- **Ergänzung (+20 s):** „Die Dateien werden durchaus befolgt: Die Agenten testen mehr und lesen mehr Dateien. Das kostet Schritte, verbessert aber die Erfolgsrate nicht messbar. Wie verbreitet die Dateien sind, zeigen Mohsenimofidi et al.: 466 von 10.000 Projekten, also knapp 5 %.“
- **Mögliche Frage:** *Soll man also keine CLAUDE.md schreiben?* → siehe Abschnitt 6, Frage I4.

### Folie 7 – Befund 3: Verifikation und Integration
- **Botschaft:** Testbestehen ist nur ein Näherungsmaß für Korrektheit, und auch gemergte Agenten-PRs brauchen Nacharbeit.
- **Zahlen:**
  - AutoCodeRover: **51 von 78** testbestehenden Patches manuell korrekt = **65,4 %** (im aggregierten @3-Versuch, nicht mit @1 vermischen!).
  - Wang et al. (ICSE 2026): 877 testbestehende Patches auf SWE-bench Verified; **7,8 %** scheitern an der vollständigen Testsuite; **29,6 % (260)** weichen im Verhalten von der Referenz ab; von 77 manuell geprüften verdächtigen Patches: **22 inkorrekt, 4 korrekt, 51 unklar**.
  - Watanabe et al. (TOSEM): **475 von 567** Claude-Code-PRs gemergt, davon **214 (45,1 %)** vor dem Merge revidiert; häufigste Revisionskategorie Bugfix (47,7 %).
- **Ergänzung (+20 s):** „Ein Grund für die 7,8 %: SWE-bench führt nur die Tests aus den geänderten Testdateien aus, nicht die ganze Testsuite. Dazu kommt Aleithan et al.: In manchen Issues steht die Lösung schon im Text, und manche Tests sind zu schwach.“
- **Mögliche Frage:** *Warum ist eine Verhaltensabweichung kein Fehler?* → Ein Patch kann anders implementiert, aber trotzdem korrekt sein. Deshalb sind 51 der 77 Fälle unklar.

### Folie 8 – Fünf Prinzipien
- **Botschaft:** fünf Prinzipien, jeweils mit eigener Handlungsregel; die Regeln sind Empfehlungen, keine belegten Wirkungen.
- Merkhilfe **„P-A-K-V-I“ = Planung, Autonomie, Kontext, Verifikation, Integration**, in der Reihenfolge eines Workflows: vor der Arbeit → während der Arbeit → danach.

| | Prinzip | Handlungsregel | gestützt durch | was NICHT belegt ist |
|---|---|---|---|---|
| P1 | Planung gemeinsam prüfen | Bei unklaren Anforderungen Ziel und Akzeptanzkriterien vorab abstimmen | HULA, Dhanorkar | Zeit- oder Qualitätseffekt; ein freigegebener Plan beweist keine korrekte Umsetzung |
| P2 | Autonomie nach Risiko und Prüfbarkeit staffeln | Sicherheitskritische oder schwer umkehrbare Änderungen menschlich freigeben | Sajadi, Dhanorkar, OpenHands-Sandbox | kausaler Autonomieeffekt; die Sandbox macht den Code nicht sicher |
| P3 | Kontext gezielt ergänzen | Fehlende Build-, Test- und Projektanforderungen gezielt ergänzen | Mohsenimofidi, Gloaguen | dass kürzere Dateien generell die Erfolgsrate steigern |
| P4 | Mehrstufig und am Auftrag verifizieren | Bestandene Tests durch anforderungsbezogene Prüfungen ergänzen | SWE-agent (Linter), Wang 2026, Cemri | dass die Kombination die menschliche Nacharbeit senkt |
| P5 | Überprüfbar integrieren | Änderungen sachlich abgrenzen und vor dem Merge nachvollziehbar prüfen | Watanabe, Sajadi | optimaler Änderungsumfang und Nettozeitgewinn |

- **Ergänzung (+20 s):** pro Prinzip einen Halbsatz dazu sagen, *was nicht belegt ist* (rechte Spalte). Das zeigt methodische Sauberkeit und nimmt Fragen vorweg.

### Folie 9 – Evidenzgrenzen
- **Botschaft:** Belegt sind Einzelmaßnahmen, nicht der Gesamtworkflow.
- **Zahlen:** Linter in SWE-agent **18 statt 15 %** (SWE-bench Lite, Ablation); Cemri et al.: veränderte ChatDev-Topologie **25,0 → 40,6 %** auf 32 ProgramDev-Aufgaben (+15,6 Prozentpunkte, aber durch mehrere Änderungen gleichzeitig).
- **Offen:** Gesamtworkflow, Übertragbarkeit über Python hinaus, Wartbarkeit und Prüfaufwand auf lange Sicht.

### Folie 10 – Zielkonflikt
- **Botschaft:** Mehr Verifikation kostet Zeit und Geld. Sie lohnt sich nur, wenn sie genug Defekte findet.
- **Vorschlag:** kontrollierter Vergleich mit und ohne menschliche Planfreigabe bei gleichem Agenten, Modell und Budget. Gemessen werden getrennt: funktionale Defekte, aktive Arbeitszeit, Gesamtdauer und Review-Aufwand (im Paper außerdem Inferenzkosten und Sicherheitsbefunde).
- **Ergänzung (+20 s):** „Konkret könnte man dieselben Aufgaben zufällig auf zwei Gruppen verteilen. Die eine Gruppe gibt den Plan frei, bevor der Agent loslegt, die andere nicht. Alles andere bleibt gleich. Nur so lässt sich ein Unterschied der Planfreigabe zuschreiben.“

### Folie 11 – Fazit
- Die Antwort hat zwei Teile: Konkrete Empfehlungen sind möglich, ein allgemeiner Gewinn an Qualität oder Produktivität folgt daraus nicht. Dann zur Fragerunde überleiten.

---

## 4. Glossar (Begriffe, nach denen gefragt werden kann)

| Begriff | Erklärung in einem Satz |
|---|---|
| **Coding-Agent** | LLM-basiertes System, das Entwicklungsaktionen mit Werkzeugen ausführt (Dateien ändern, Befehle ausführen, Tests laufen lassen) und die Rückmeldung der Umgebung für die nächsten Schritte nutzt (Definition nach Liu et al.). |
| **Abgrenzung zur Code-Completion** | Copilot-Completion schlägt Code an der Cursorposition vor; ein Agent plant mehrere Schritte, führt sie selbst aus und reagiert auf Ergebnisse. |
| **Komponenten eines Agenten** | Planung, Gedächtnis, Wahrnehmung, Aktion (Liu et al.). |
| **SWE-bench** | Benchmark aus echten GitHub-Issues von 12 Python-Repositories; ein Patch gilt als gelöst, wenn die Tests aus dem Original-PR bestehen. Voll: 2.294 Aufgaben, **Lite: 300**, **Verified: 500** von Menschen geprüfte. |
| **CTXBench** | Benchmark von Gloaguen et al. mit 138 Aufgaben aus 12 neueren Repositories, die echte, von Entwicklern geschriebene Kontextdateien enthalten. |
| **@1 / @3 (pass@k)** | Erfolg im ersten Versuch bzw. in mindestens einem von drei Versuchen. Deshalb darf man die 65,4 % bei AutoCodeRover (@3) nicht mit der @1-Rate vermischen. |
| **Ablation** | Man entfernt gezielt eine Komponente (z. B. den Linter) und misst den Unterschied. So isoliert man deren Effekt. |
| **RCT** | randomisierte kontrollierte Studie; die Zuteilung zu Bedingungen ist zufällig (Cui, Becker). |
| **Within-Subject-Design** | Dieselben Personen erleben beide Bedingungen (Chen: jede Person nutzt Copilot *und* OpenHands). |
| **Endpunkt** | die gemessene Zielgröße, z. B. Erfolgsrate, aktive Zeit, Gesamtdauer, Kosten. |
| **Prozent vs. Prozentpunkte** | 25 % → 60 % sind **+35 Prozentpunkte**, aber +140 Prozent. |
| **Nicht signifikant** | Der Unterschied ist statistisch nicht von Zufall zu trennen. Das ist **kein Nachweis gleicher Leistung**. |
| **Standardfehler** | Unsicherheit einer Schätzung (Cui: 26,08 % ± 10,3 %). |
| **Differenzielles Testen** | Es werden Tests erzeugt, die Verhaltensunterschiede zwischen zwei Patches aufdecken (PatchDiff bei Wang et al.). |
| **Solution Leakage** | Die Lösung steht schon im Issue-Text oder in den Kommentaren (Aleithan et al.). |
| **Linter** | statische Prüfung auf Syntax- und Stilfehler; in SWE-agent verwirft er fehlerhafte Edits. |
| **ACI** | Agent-Computer Interface: eine Werkzeugschnittstelle, die für das Sprachmodell gestaltet ist (SWE-agent). |
| **SBFL** | spektrumbasierte Fehlerlokalisierung: Aus bestehenden und fehlschlagenden Tests wird abgeschätzt, wo der Fehler liegt (AutoCodeRover). |
| **Kontextdatei** | `CLAUDE.md`, `AGENTS.md` usw.: Projektwissen für den Agenten (Konventionen, Build-/Testbefehle, Architektur). |
| **Context Engineering** | steuert, *welche* Informationen das Modell erhält; Prompt Engineering steuert, *wie* die Aufgabe formuliert ist. |
| **Human-in-the-Loop** | Der Mensch greift an festgelegten Stellen ein (HULA: Plan, dann Code). |
| **Sandbox** | isolierte Ausführungsumgebung (bei OpenHands Docker). Sie schützt das System, nicht die Qualität des Codes. |
| **Automation Bias** | übermäßiges Vertrauen in automatische Ergebnisse (Dhanorkar). |
| **Narrative vs. systematische Review** | narrativ: gezielte, begründete Auswahl; systematisch: vollständige, protokollierte und reproduzierbare Suche mit Trefferzahlen (z. B. nach PRISMA). |
| **Preprint** | Veröffentlichung ohne abgeschlossene Begutachtung (z. B. arXiv). |

---

## 5. Die 21 Arbeiten als Steckbriefe

Nach Rolle im Paper gruppiert. **Fett** = auf den Folien genannt, unbedingt sicher können.

**Hintergrund und Definition**
| Arbeit | Typ / Venue | Kern |
|---|---|---|
| **Robbes et al. 2026** | Repository-Mining, ACM TOSEM | 128.018 Projekte, 22,20 % (bis 28,66 %) nutzen Agenten |
| Liu et al. 2024 | Survey, arXiv | Definition des Agenten; 124 Paper; Planung, Gedächtnis, Wahrnehmung, Aktion |
| Xia et al. 2025 (Agentless) | System, FSE | feste Phasen Lokalisierung → Reparatur → Validierung, ohne autonome Steuerung; 32 % auf Lite, 0,70 USD pro Aufgabe |
| **Takerngsaksiri et al. 2025 (HULA)** | System und Feldeinsatz, ICSE-SEIP (Atlassian) | Mensch prüft Plan und Code in JIRA; 82 % der Pläne freigegeben, 59 % der geöffneten PRs gemergt |
| Wang et al. 2025 (OpenHands) | Plattform, ICLR | offene Agentenplattform mit Docker-Sandbox |

**Autonomie und Produktivität**
| Arbeit | Typ / Venue | Kern |
|---|---|---|
| **Chen et al. 2026** | kontrollierte Nutzerstudie, CHI '26 | 20 Studierende; Erfolg 25 → 60 %; aktiv 25,1 → 12,5 min, gesamt 27,9 min |
| Cui et al. 2026 | 3 RCTs im Feld, Management Science | 4.867 Entwickler, Copilot-**Completion**, +26,08 % Aufgaben (SE 10,3 %) |
| **Becker et al. 2025 (METR)** | RCT, arXiv | 16 Experten, 246 Aufgaben, +19 % Zeit, gefühlt −20 % |
| **Dhanorkar et al. 2026** | 17 Interviews, arXiv | 4 Formen der Aufsicht: Vorgaben vorab, gemeinsame Planung, Überwachung, Review; riskante Heuristiken |

**Kontext**
| Arbeit | Typ / Venue | Kern |
|---|---|---|
| Chatlatanagulchai et al. 2025 | Repository-Mining, PROFES | 253 `CLAUDE.md`: Build-/Run-Befehle, Implementierung, Architektur |
| Mohsenimofidi et al. 2026 | Repository-Mining, MSR | 466 von 10.000 Projekten mit Kontextdatei; nur Verbreitung, keine Wirkung |
| **Gloaguen et al. 2026** | Benchmark-Experiment, ICLR-Workshop MemAgents | kein signifikanter Erfolgseffekt; +20/23 % Kosten, +2,45/3,92 Schritte |

**Verifikation, Sicherheit, Integration**
| Arbeit | Typ / Venue | Kern |
|---|---|---|
| **Jimenez et al. 2024** | Benchmark, ICLR | SWE-bench |
| **Zhang et al. 2024 (AutoCodeRover)** | System, ISSTA | 51 von 78 testbestehenden Patches korrekt (65,4 %, @3) |
| Aleithan et al. 2024 (SWE-Bench+) | Benchmark-Analyse, arXiv | Lösungen im Issue-Text, schwache Tests |
| **Wang, Pradel, Liu 2026** | empirische Studie, ICSE | 877 Patches; 7,8 % scheitern an voller Suite; 29,6 % Verhaltensabweichung |
| **Yang et al. 2024 (SWE-agent)** | System, NeurIPS | Linter: 18 statt 15 % auf Lite |
| **Cemri et al. 2025 (MAST)** | Fehlertaxonomie, NeurIPS D&B | ChatDev 25,0 → 40,6 % durch mehrere Änderungen |
| Sajadi et al. 2025 | Sicherheitsanalyse, arXiv | Sicherheitslücken in Agenten-Patches; keine kausale Zuschreibung zum Autonomiegrad |
| **Watanabe et al. 2026** | Repository-Mining, ACM TOSEM | 475/567 gemergt, 214 revidiert (45,1 %) |
| Li et al. 2025 (AIDev) | Repository-Mining, arXiv | kürzere Schließzeiten für Codex-PRs; 58,2 % der Agenten-PRs ohne explizites Review (Menschen 75,3 %) |

---

## 6. Fragenkatalog mit Musterantworten

### Methodik

**M1. Warum keine systematische Literaturanalyse?**
Für ein Short Paper mit begrenztem Umfang haben wir eine gezielte, narrative Analyse gemacht. Die Suche ist dokumentiert (Datenbanken, Suchbegriffe, Einschlusskriterien, Prüfschritte). Die Trefferzahlen pro Schritt berichten wir aber nicht, deshalb beanspruchen wir keine reproduzierbare Vollerhebung. Das steht so auch in den Limitationen.

**M2. Warum gerade 21 Arbeiten? Wie habt ihr ausgewählt?**
Eingeschlossen wurden Arbeiten ab 2024 zu mehrschrittigen, werkzeugnutzenden LLM-Agenten, empirisch oder als System mit Evaluation, mit Bezug zu Workflow, Qualität oder Produktivität. 21 ist das Ergebnis dieser Kriterien und des Umfangs eines Short Papers, keine Zielgröße.

**M3. Warum keine Metaanalyse oder Effektgröße über alle Studien?**
Die Studien messen unterschiedliche Endpunkte (Erfolgsrate, aktive Zeit, Gesamtdauer, PRs pro Woche, Kosten), mit unterschiedlichen Modellen, Budgets und Populationen. Ein gemeinsamer Effekt wäre irreführend. Deshalb ordnen wir nach Evidenzart: kontrolliert, deskriptiv, qualitativ.

**M4. Viele Quellen sind Preprints. Ist das ein Problem?**
Ja, das ist eine Einschränkung, und wir benennen sie. Preprints liefern vor allem Nutzer- und Sicherheitsbefunde (z. B. Becker, Dhanorkar, Sajadi), weil das Feld sehr schnell ist. Wo es eine begutachtete Fassung gibt, zitieren wir diese. Den Status muss man bei der Gewichtung beachten.

**M5. Gibt es Interessenkonflikte in den Studien?**
Ja, und das sollte man kennen: Chen et al. gehören zum Umfeld der OpenHands-Entwickler, HULA kommt von Atlassian, Dhanorkar et al. arbeiten bei Microsoft. Das ist ein Grund mehr, die Ergebnisse vorsichtig einzuordnen. (Im Paper nicht ausdrücklich genannt; ehrlich als zusätzliche Einschränkung nennen.)

**M6. Cui et al. untersucht doch gar keine Agenten. Warum ist die Studie drin?**
Richtig, es geht um Copilot-Codevervollständigung. Wir nutzen sie ausdrücklich nur als angrenzenden Produktivitätsvergleich und sagen in der Tabelle, dass sie keine autonomen Agenten testet. Sie zeigt, dass Werkzeugtyp und Messgröße das Ergebnis stark beeinflussen.

**M7. In eurer Recherche waren 22 Quellen, im Paper 21. Was fehlt?**
AgentCoder (Huang et al.). Die Arbeit stammt von Ende 2023, ist ein Preprint und testet nur einzelne Funktionen (HumanEval, MBPP), keine Repository-Aufgaben. Damit erfüllt sie die Einschlusskriterien nicht.

**M8. Wie aktuell sind die Ergebnisse, wenn sich Modelle so schnell ändern?**
Das ist eine echte Grenze: Viele Studien nutzen Modelle von 2024 oder Anfang 2025 (z. B. Becker: „early-2025 AI“). Absolute Zahlen veralten schnell. Methodische Aussagen bleiben aber gültig, etwa dass Testbestehen nicht Korrektheit ist oder dass aktive Zeit und Gesamtdauer zu trennen sind.

**M9. Warum ist SWE-bench ein Problem für die Übertragbarkeit?**
Nur Python, nur populäre Open-Source-Repositories, möglicherweise in Trainingsdaten enthalten. Dazu kommen Lösungen im Issue-Text und schwache Tests (Aleithan). Industrielle Aufgaben und andere Sprachen sind damit kaum abgedeckt.

### Inhalt

**I1. Cui sagt +26 %, Becker sagt 19 % langsamer. Was stimmt?**
Beides kann stimmen, weil völlig Verschiedenes gemessen wird: Cui misst wöchentliche PRs bei Code-Completion in großen Firmen, Becker misst die Bearbeitungszeit erfahrener Entwickler in ihren eigenen, großen Projekten mit Werkzeugen von Anfang 2025. Werkzeugtyp, Population und Zeitmaß unterscheiden sich, deshalb ist es kein direkter Widerspruch.

**I2. Spart der Agent bei Chen nun Zeit oder nicht?**
Die aktive menschliche Zeit halbiert sich ungefähr (25,1 → 12,5 min). Mit der Laufzeit des Agenten sind es 27,9 min, also nicht kürzer als mit Copilot. Ob das ein Gewinn ist, hängt davon ab, ob der Mensch die Wartezeit anders nutzen kann. Außerdem gelten die Zeiten nur für erfolgreiche Aufgaben, und die Erfolgsquoten unterscheiden sich (25 % gegenüber 60 %).

**I3. Warum schätzen die Entwickler bei Becker eine Ersparnis, obwohl sie langsamer sind?**
Die eigene Wahrnehmung ist unzuverlässig. Mögliche Gründe laut Autoren: übertriebener Optimismus, hohe Vertrautheit mit dem eigenen Repository, große und komplexe Codebasen, geringe Zuverlässigkeit der KI (unter 44 % der Generierungen übernommen, rund 9 % der Zeit für Prüfen und Nachbessern) und fehlendes implizites Projektwissen der KI. Methodische Folge: Umfragen ersetzen keine Zeitmessung.

**I4. Soll man also keine CLAUDE.md/AGENTS.md schreiben?**
Nicht pauschal. Gloaguen zeigt keinen signifikanten Gesamteffekt auf die Erfolgsrate, aber höhere Kosten bei LLM-generierten Dateien. Daraus folgt P3: gezielt nur das ergänzen, was der Agent sonst nicht findet, etwa Build- und Testbefehle oder abweichende Konventionen. Nicht gemessen wurde, ob Kontextdateien Konventionen oder Wartbarkeit verbessern; dafür sind sie eigentlich gedacht.

**I5. Warum reicht es nicht, wenn alle Tests grün sind?**
Tests prüfen nur, was sie abdecken. Bei AutoCodeRover waren nur 51 von 78 testbestehenden Patches korrekt. Bei Wang scheiterten 7,8 % an der vollständigen Suite, und 29,6 % verhielten sich anders als die Referenz. Deshalb fordert P4: vollständige Suite vor der Integration und zusätzliche Prüfungen gegen die Anforderung.

**I6. Ist weniger Autonomie also besser (Agentless)?**
Agentless zeigt, dass ein fester Ablauf auf SWE-bench Lite konkurrenzfähig und günstig sein kann. Ein sauberer Autonomieeffekt folgt daraus nicht, weil sich auch Modell, Werkzeuge und Budget unterscheiden. Deshalb schlagen wir keine minimale, sondern eine *risikogerechte* Autonomie vor (P2).

**I7. Macht eine Sandbox den Agenten sicher?**
Nein. Die Docker-Sandbox bei OpenHands schützt das System vor den Aktionen des Agenten. Der erzeugte Code kann trotzdem Sicherheitslücken enthalten (Sajadi). Deshalb gibt es bei P2 und P5 zusätzlich menschliche Freigabe und Sicherheitsprüfungen.

**I8. Erzeugen autonomere Agenten mehr Sicherheitslücken?**
Vorsicht: Sajadi findet Lücken bei mehreren Agenten, aber Modelle und Bearbeitungsmechanismen unterscheiden sich. Eine kausale Zuschreibung an den Autonomiegrad ist deshalb nicht möglich. Bei Llama-Patches hängen mehr geänderte Dateien mit mehr Sicherheitsproblemen zusammen; dass kleinere Patches schützen, wurde nicht gemessen.

**I9. Warum empfehlt ihr kleine PRs, wenn Agenten-Commits in der Praxis größer sind (Robbes)?**
Genau deshalb: Kleine, abgegrenzte Änderungen sind leichter nachvollziehbar zu prüfen, und Watanabe empfiehlt das ebenfalls. Unser Prinzip steht damit bewusst gegen die gängige Praxis. Den optimalen Umfang hat aber niemand bestimmt.

**I10. Li et al.: Codex-PRs werden schneller geschlossen. Ist das nicht Produktivität?**
Nein, Schließlatenz misst weder menschliche Arbeitszeit noch Durchsatz. Bei 58,2 % der Agenten-PRs fehlt sogar eine explizite GitHub-Reviewaktion (bei Menschen 75,3 %). Ob privat oder gründlich geprüft wurde, lässt sich daraus nicht ablesen.

**I11. 45 % der Claude-Code-PRs werden revidiert. Ist das schlecht?**
Es zeigt, dass menschliche Nacharbeit nötig bleibt, vor allem bei Bugfixes. Der Unterschied im Revisionsumfang zu menschlichen PRs ist nicht signifikant, aber das beweist keinen gleichen Aufwand.

**I12. Was ist der Unterschied zwischen 15,6 % bei Cemri und dem Linter-Befund?**
Der Linter-Befund ist eine Ablation: Nur der Linter wird verändert, deshalb ist er der Linter zuzuschreiben. Bei Cemri wurden mehrere Dinge an der ChatDev-Topologie gleichzeitig geändert; die 15,6 Prozentpunkte sind deshalb kein isolierter Nachweis für eine abschließende Zielprüfung.

**I13. Was bedeutet „Plan freigegeben“ bei HULA für die Qualität?**
Nichts Direktes. Ein freigegebener Plan belegt keine korrekte Umsetzung. Dhanorkar beschreibt sogar das Vertrauen auf den Plan als riskante Prüfheuristik. Deshalb bleibt bei P1 das Code-Review erforderlich.

### Transfer und Meinung

**T1. Was würdet ihr einem Unternehmen konkret raten?**
Die fünf Handlungsregeln: Akzeptanzkriterien vorab klären; Sicherheitskritisches menschlich freigeben; Kontext gezielt ergänzen; zusätzlich zur Testsuite anforderungsbezogen prüfen; kleine PRs mit Review. Und vor allem: den Nutzen im eigenen Team messen, getrennt nach aktiver Zeit, Gesamtdauer, Review-Aufwand und Defekten, statt sich auf Gefühl oder Benchmarks zu verlassen.

**T2. Wie verändert sich die Rolle von Entwicklern?**
Ein Teil der Arbeit verlagert sich zum Spezifizieren, Überwachen und Prüfen (Dhanorkar, in der Recherche als „Developer-Manager“ bezeichnet). Die Folgen für Ausbildung und Kompetenzen, etwa ein möglicher Kompetenzverlust, sind in der Literatur offen.

**T3. Wie würdet ihr euren vorgeschlagenen Versuch konkret aufbauen?**
Gleicher Agent, gleiches Modell, gleiches Budget, dieselben Aufgaben, die zufällig auf zwei Bedingungen verteilt werden: mit gegenüber ohne menschliche Planfreigabe. Endpunkte getrennt erfassen: aktive menschliche Zeit, Gesamtdauer, Inferenzkosten, Review-Aufwand, funktionale Defekte (z. B. per vollständiger Testsuite und Zusatztests), Sicherheitsbefunde; ergänzend später Wartungsaufgaben am selben Code.

**T4. Was war für euch der überraschendste Befund?**
Vorschlag: Becker. Erfahrene Entwickler waren mit KI langsamer, glaubten aber, schneller zu sein. Das zeigt, warum man messen statt schätzen muss. (Alternativ: Kontextdateien ohne messbaren Erfolgseffekt.)

**T5. Wie wichtig ist menschliche Aufsicht regulatorisch?**
Dhanorkar verweist auf die Aufsichtspflicht im EU AI Act (Art. 14). Im Paper ist das nicht Thema; bei einer Nachfrage kurz nennen und sagen, dass die rechtliche Einordnung außerhalb des Fokus liegt.

**T6. Ist der Titel „Evidenzgrenzen“ nicht ein schwaches Ergebnis?**
Nein, es ist ein eigenständiger Beitrag: Wir zeigen, welche Aussagen die Literatur trägt und welche nicht, und welche Endpunkte künftige Studien trennen müssen. Gerade bei einem Hype-Thema ist das nützlich.

### Strategie für Fragen, die man nicht beantworten kann
- Ehrlich sagen: „Das hat die Studie nicht gemessen“ oder „Das liegt außerhalb unseres Korpus“. Das passt zur Grundhaltung des Papers.
- Auf eine der drei Kernaussagen zurückführen (Endpunkte trennen, Tests ≠ Korrektheit, Prinzipien ≠ Wirkungsnachweis).
- Teamkollegen einbinden, wenn jemand den Abschnitt besser kennt.

---

## 7. Fallen: Was ihr NICHT sagen solltet

| Nicht sagen | Stattdessen (wie im Paper) |
|---|---|
| „Agenten machen 35 % produktiver“ | Erfolgsquote **+35 Prozentpunkte** (25 → 60 %), Studierende, Labor |
| „Agenten halbieren die Arbeitszeit“ | *aktive* Zeit halbiert; Gesamtdauer 27,9 min |
| „LLM erzeugt 11× mehr Schwachstellen“ / „mehr Autonomie = mehr Risiko“ | Lücken bei mehreren Agenten; keine kausale Zuschreibung zum Autonomiegrad |
| „Zielprüfung bringt +15,6 %“ | +15,6 PP durch mehrere Änderungen zugleich, nicht isoliert |
| „Kontextdateien bringen nichts“ | kein *signifikanter* Gesamteffekt auf die Erfolgsrate; das ist kein Beweis gleicher Leistung |
| „29,6 % der Patches sind falsch“ | 29,6 % weichen im Verhalten ab; von 77 geprüften waren 22 falsch, 51 unklar |
| „Ein Drittel der gelösten Aufgaben ist falsch“ | 51 von 78 testbestehenden Patches korrekt, im @3-Versuch |
| „Unsere Prinzipien verbessern die Qualität“ | begründete Empfehlungen; Wirkung als Gesamtworkflow nicht nachgewiesen |
| „Wir haben eine systematische Review gemacht“ | narrative Analyse ohne berichtete Trefferzahlen |
| „Gloaguen ist ein ICLR-Hauptkonferenzpaper“ | ICLR-2026-**Workshop** (MemAgents) |

---

## 8. Zahlen-Spickzettel zum Auswendiglernen

| Zahl | Bedeutung | Quelle |
|---|---|---|
| 21 | ausgewertete Arbeiten, 2024–2026, Stand 16.10.2026 | Paper |
| 128.018 / 22,20 % / 28,66 % | Projekte / Adoption konservativ / obere Schätzung | Robbes |
| 25 → 60 % | Erfolg Copilot → OpenHands | Chen |
| 25,1 → 12,5 min / 27,9 min | aktive Zeit / mit Agentenlaufzeit | Chen |
| +26,08 % (SE 10,3 %) | erledigte Aufgaben, Code-Completion, 4.867 Entwickler | Cui |
| +19 % / −20 % gefühlt | Bearbeitungszeit / Schätzung, 16 Entwickler, 246 Aufgaben | Becker |
| 17 | Interviews | Dhanorkar |
| 253 | `CLAUDE.md`-Dateien | Chatlatanagulchai |
| 466 / 10.000 | Projekte mit Kontextdatei | Mohsenimofidi |
| +20 / +23 % | Inferenzkosten Lite / CTXBench | Gloaguen |
| +2,45 / +3,92 | Schritte Lite / CTXBench | Gloaguen |
| 51 / 78 = 65,4 % | korrekte testbestehende Patches (@3) | AutoCodeRover |
| 877 / 7,8 % / 29,6 % (260) | Patches / scheitern an voller Suite / Verhaltensabweichung | Wang 2026 |
| 77 → 22 / 4 / 51 | manuell geprüft → inkorrekt / korrekt / unklar | Wang 2026 |
| 18 vs. 15 % | mit / ohne Linter | SWE-agent |
| 25,0 → 40,6 % (32 Aufgaben) | ChatDev-Topologie | Cemri |
| 475 / 567; 214 = 45,1 %; 47,7 % | gemergt; revidiert; davon Bugfix-Kategorie | Watanabe |
| 58,2 % / 75,3 % | ohne explizite Reviewaktion: Agent / Mensch | Li |

---

## 9. Lernplan bis Montag

1. **Tag 1:** Abschnitte 1 und 3 lesen, Präsentation einmal mit Stoppuhr laut durchsprechen und die Zeit notieren.
2. **Tag 2:** Zahlen-Spickzettel (Abschnitt 8) und Glossar lernen; danach mit abgedeckter rechter Spalte abfragen.
3. **Tag 3:** Fragenkatalog (Abschnitt 6) im Team gegenseitig abfragen, Antworten in eigenen Worten in unter 30 Sekunden geben. Fallen-Tabelle (Abschnitt 7) wiederholen.
4. **Vor dem Termin:** Kernbotschaft (Abschnitt 1) und Fazit noch einmal laut sagen.
