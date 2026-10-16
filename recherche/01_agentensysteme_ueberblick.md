# Gruppe 1: Überblick und Agentensysteme

Grundlagen für **II. Hintergrund**: Was ist ein KI-Coding-Agent, wie ist er aufgebaut, welche Architekturen gibt es? Die drei Systempaper liefern außerdem erste Hinweise zur Gestaltung der Werkzeugschnittstelle und zur Prüfung von Patches.

---

## liu2024agentsurvey — Large Language Model-Based Agents for Software Engineering: A Survey

- **Typ / Venue:** Systematischer Survey, arXiv-Preprint (2409.02977, v2 Dez. 2025)
- **Gegenstand:** 124 Paper zu LLM-basierten Agenten im Software Engineering, aus zwei Blickwinkeln geordnet:
  - *SE-Perspektive:* Anforderungen, Codegenerierung, statische Prüfung, Testen, Debugging, IT-Betrieb, End-to-End-Entwicklung und -Wartung
  - *Agenten-Perspektive:* die vier Komponenten **Planung, Gedächtnis (Memory), Wahrnehmung, Aktion**, dazu Multi-Agenten-Systeme (Rollen, Kooperation, Informationsfluss) und Mensch-Agent-Kollaboration
- **Kernaussagen:**
  - Agenten erreichen gegenüber dem reinen LLM durchgängig höhere pass@1-Werte, von Methoden- bis Repository-Ebene. Grund: Sie nehmen Rückmeldungen aus der Umgebung wahr und passen ihren Plan an.
  - Reine LLMs sind leichter einzusetzen, scheitern aber an umgebungsabhängigen Aufgaben wie End-to-End-Entwicklung.
- **Nutzen fürs Paper:** Definition „KI-Coding-Agent“ und das Komponentenmodell für den Hintergrund. Die Abgrenzung Agent vs. Code-Completion lässt sich damit belegen.
- **Grenzen:** Literaturstand Mitte 2024. Die Praxisstudien von 2025/26 sind nicht enthalten.

---

## yang2024sweagent — SWE-agent: Agent-Computer Interfaces Enable Automated Software Engineering

- **Typ / Venue:** Systembeschreibung mit Benchmark-Evaluation, NeurIPS 2024
- **Gegenstand:** Führt den Begriff **Agent-Computer Interface (ACI)** ein. Sprachmodelle gelten als eigene Nutzergruppe und brauchen andere Schnittstellen als Menschen.
- **Methode:** SWE-bench (2.294 Aufgaben), Ablationsstudien auf SWE-bench Lite (300 Aufgaben), Modelle GPT-4 Turbo und Claude 3 Opus
- **Kernbefunde:**
  - 12,47 % gelöste SWE-bench-Aufgaben gegenüber 3,8 % beim vorherigen nicht-interaktiven RAG-Ansatz. HumanEvalFix: 87,7 %.
  - Mit eigener ACI löst der Agent **10,7 Prozentpunkte** mehr Aufgaben als ein Agent mit reiner Linux-Shell.
  - Vier Gestaltungsprinzipien für ACIs:
    1. einfache Aktionen mit wenigen Optionen
    2. kompakte Aktionen
    3. informatives, aber knappes Feedback
    4. **Leitplanken (Guardrails)**: Ein integrierter Linter verwirft fehlerhafte Edits. Ohne ihn sinkt die Lösungsrate um 3 Prozentpunkte.
  - Zu viel Kontext schadet: Ein Dateibetrachter mit 100 Zeilen schlägt sowohl 30 Zeilen als auch die ganze Datei.
- **Wirkung:** *Qualität:* Leitplanken senken Folgefehler. *Produktivität:* nicht mit Menschen gemessen.
- **Nutzen fürs Paper:** Belegt, dass die Gestaltung von Werkzeugen und Workflow die Leistung beeinflusst, ohne dass sich das Modell ändert. Stützt die Prinzipien „Leitplanken einbauen“ und „Kontext knapp halten“.
- **Grenzen:** Nur Benchmark, keine Nutzerstudie. Für die Schwächen von SWE-bench siehe Gruppe 6.

---

## wang2025openhands — OpenHands: An Open Platform for AI Software Developers as Generalist Agents

- **Typ / Venue:** Systembeschreibung / Plattform, ICLR 2025
- **Gegenstand:** Offene Plattform (früher OpenDevin, MIT-Lizenz, über 2.100 Beiträge von 188 Mitwirkenden) mit
  - einer Event-Stream-Architektur aus Aktionen und Beobachtungen,
  - einer **Docker-Sandbox** mit Bash, Browser und IPython,
  - Delegation an mehrere Agenten und einer Evaluation über 15 Benchmarks.
- **Kernbefunde:** CodeActAgent v1.8 mit Claude 3.5 Sonnet löst **26 %** von SWE-bench Lite. Die Weboberfläche zeigt Dateien, Befehle und Browseraktivität, und Nutzer können jederzeit eingreifen.
- **Wirkung:** Keine direkte Messung von Qualität oder Produktivität. OpenHands ist aber der Agent in mehreren anderen Studien: chen2025codewithme, sajadi2025patchsecurity, wang2026solvedissues.
- **Nutzen fürs Paper:** Referenz für die Ausführung in einer **isolierten Umgebung (Sandbox)** als Sicherheitsmaßnahme und für die Sichtbarkeit von Agentenaktionen.
- **Grenzen:** Plattformpaper. Sicherheit und Zuverlässigkeit werden nur als offene Herausforderung genannt.

---

## zhang2024autocoderover — AutoCodeRover: Autonomous Program Improvement

- **Typ / Venue:** Systembeschreibung mit Benchmark-Evaluation, ISSTA 2024 (DOI 10.1145/3650212.3680384)
- **Gegenstand:** Agent für GitHub-Issues, der das Projekt als Programmstruktur (AST mit Klassen und Methoden) behandelt statt als Dateisammlung.
  - Er sucht iterativ Kontext über Code-Such-APIs.
  - Optional verfeinert eine **spektrumbasierte Fehlerlokalisierung (SBFL)** auf Basis vorhandener Tests die Suche.
- **Kernbefunde:**
  - 19 % auf SWE-bench Lite, rund **4 Minuten** pro Issue gegenüber durchschnittlich **2,68 Tagen** bei Entwicklern, Kosten etwa 0,43 USD pro Issue.
  - Manuelle Prüfung der Patches, die die Tests bestehen: nur **65,4 % (51 von 78) sind tatsächlich korrekt**, der Rest überangepasst (Overfitting).
  - Ursachen: zu wenig Kontext und Issue-Beschreibungen, die die Anforderung unvollständig beschreiben, etwa wenn ein vorgeschlagener Patch im Issue in die Irre führt.
  - Tests als zusätzliche Signalquelle (SBFL) verbessern die Lokalisierung.
- **Wirkung:** *Produktivität:* große Zeitersparnis im Benchmark. *Qualität:* Ein Drittel der „gelösten“ Aufgaben ist falsch gelöst.
- **Nutzen fürs Paper:** Belege für „Tests als Leitplanke“ und für „Issue- bzw. Aufgabenbeschreibung ist Teil des Kontexts“. Die Autoren fordern selbst eine **Schnittstelle für menschliche Beteiligung**, da alle Entscheidungen beim LLM liegen.
- **Grenzen:** Der Zeitvergleich (4 Minuten vs. 2,68 Tage) ist unfair, weil die Tage Wartezeiten und Diskussion enthalten. Ausschließlich Benchmark.
