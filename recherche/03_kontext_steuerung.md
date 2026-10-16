# Gruppe 3: Kontext und Steuerung

Für **IV.B** im Ergebnisteil. Leitfrage: Wie wird dem Agenten Projektwissen mitgegeben (CLAUDE.md, AGENTS.md, Issue-Beschreibung), und hilft das?

Zwei der drei Arbeiten beschreiben nur, *was* in Kontextdateien steht (Repository-Mining). Nur gloaguen2026agentsmd misst, *ob es wirkt*. Diese Asymmetrie ist selbst ein Befund für die Diskussion.

---

## chatlatanagulchai2025manifests — On the Use of Agentic Coding Manifests: An Empirical Study of Claude Code

- **Typ / Venue:** Repository-Mining, PROFES 2025 (Kurzpaper, DOI 10.1007/978-3-032-12089-2_40)
- **Methode:** 253 `CLAUDE.md`-Dateien aus 242 GitHub-Repositories, Struktur automatisch und Inhalte manuell analysiert
- **Kernbefunde:**
  - **Flache Struktur:** typischerweise eine Hauptüberschrift und eine mittlere Anzahl an Unterabschnitten
  - Häufigste Inhalte:
    1. **Build- und Run-Befehle** (operative Kommandos)
    2. Implementierungsdetails
    3. Architekturbeschreibung
  - Viele Dateien definieren zusätzlich eine **Rolle für die KI**.
  - Die Dateien sind zugleich Ausführungsanleitung und Rahmen für die Zusammenarbeit von Mensch und KI.
  - Offizielle Dokumentation zum Schreiben solcher Dateien fehlt weitgehend, daher arbeiten Entwickler nach Versuch und Irrtum.
- **Wirkung:** nicht gemessen
- **Nutzen fürs Paper:** Beschreibt die Praxis der Kontextsteuerung. Gut für den Hintergrund und als Kontrast zu gloaguen2026agentsmd: Was üblich ist, muss nicht wirken.
- **Grenzen:** Nur Claude Code, rein deskriptiv, kurzes Paper.

---

## mohsenimofidi2026context — Context Engineering for AI Agents in Open-Source Software

- **Typ / Venue:** Repository-Mining (Vorstudie), MSR 2026 (DOI 10.1145/3793302.3793350)
- **Begriff:** **Context Engineering** steuert, *welche* Informationen das Modell erhält. Prompt Engineering steuert, *wie* die Aufgabe formuliert ist.
- **Methode:** 10.000 GitHub-Repositories auf Kontextdateien gescannt (Copilot-Instructions, CLAUDE.md, AGENTS.md, GEMINI.md), dann 155 AGENTS.md-Dateien qualitativ analysiert, Commit-Historie eingeschlossen
- **Kernbefunde:**
  - *Verbreitung:* Nur **466 Projekte (5 %)** nutzen überhaupt eine Kontextdatei (Stand Okt. 2025), die Verbreitung steht also noch am Anfang.
  - *Inhalte:* häufig Code-Konventionen und Best Practices, Beitragsrichtlinien, Architektur; **selten Troubleshooting oder Sicherheit**
  - *Fünf Schreibstile:* deskriptiv, präskriptiv, prohibitiv („Never commit to main“), erklärend (Regel mit Begründung), konditional („Wenn …, dann …“)
  - *Weiterentwicklung:* 50 % der AGENTS.md-Dateien wurden nie geändert, 23 % einmal, 21 % zwei- bis siebenmal.
  - Es gibt **noch keine etablierte Struktur.** Kontextdateien sind gepflegte Software-Artefakte, die versioniert und reviewt werden.
- **Wirkung:** nicht gemessen. Die Autoren fordern ausdrücklich zu untersuchen, wie sich Inhalt, Struktur und Stil auf das Agentenverhalten auswirken.
- **Nutzen fürs Paper:** Liefert Definition und Begriff „Context Engineering“. Die Taxonomie der Schreibstile ist ein konkreter Ansatzpunkt für ein Gestaltungsprinzip (prohibitive und erklärende Regeln). Die Sicherheitslücke in den Dateien passt zu sajadi2025patchsecurity.
- **Grenzen:** Vorstudie, nur englischsprachige Projekte, Fokus auf vier Werkzeuge.

---

## gloaguen2026agentsmd — Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?

- **Typ / Venue:** Benchmark-Experiment, ICLR 2026 (Preprint arXiv:2602.11988, gelesen in v3 vom Sep. 2026). ETH Zürich und LogicStar.ai.
- **Methode:**
  - Neuer Benchmark **CTXBENCH**: 138 Aufgaben aus 12 neueren, weniger bekannten Repositories, die von Entwicklern geschriebene Kontextdateien enthalten
  - Zusätzlich SWE-bench mit LLM-generierten Kontextdateien
  - Vier Coding-Agenten in drei Bedingungen: ohne Kontextdatei, mit LLM-generierter Datei, mit der Datei der Entwickler
- **Kernbefunde:**
  - **Kontextdateien verbessern die Lösungsrate nicht signifikant.**
    - LLM-generierte Dateien: −0,5 % (SWE-bench) bzw. −2 % (CTXBENCH), nicht signifikant
    - Von Entwicklern geschriebene Dateien: +2,4 % im Schnitt (p = 0,21), aber **signifikant besser als LLM-generierte** (p = 0,038)
  - **Die Kosten steigen um über 20 %** und die Zahl der Schritte wächst, weil die Agenten die Anweisungen befolgen: Sie testen mehr, suchen und lesen mehr Dateien und nutzen repo-spezifische Werkzeuge.
  - **Repository-Übersichten helfen nicht**, obwohl die Anbieter sie empfehlen.
  - Empfehlung: LLM-generierte Kontextdateien vorerst weglassen. Von Hand geschriebene Dateien sollen **nur enthalten, was nicht schon im Code oder README steht**, etwa abweichende Konventionen oder nicht-funktionale Anforderungen. Jede Änderung soll vor dem Einsatz evaluiert werden.
- **Wirkung:** *Qualität:* kein messbarer Gewinn bei der Lösungsrate, Anweisungen werden aber befolgt. *Produktivität und Kosten:* über 20 % mehr Inferenzkosten.
- **Nutzen fürs Paper:** Wichtigster Gegenbefund zur verbreiteten Praxis. Daraus folgt das Prinzip **„Kontext knapp und gezielt statt umfassend“**, passend zu yang2024sweagent (zu viel Kontext schadet).
- **Grenzen:** Gemessen wird nur die Lösungsrate im Benchmark. Ob Konventionen eingehalten werden und wie gut der Code wartbar ist, wird nicht erfasst, obwohl gerade dafür Kontextdateien gedacht sind. Nur Python.
