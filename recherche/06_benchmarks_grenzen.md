# Gruppe 6: Benchmarks und deren Grenzen

Für **II. Hintergrund** (SWE-bench als Standard) und **VI. Diskussion** (Benchmarks vs. Praxis).

Die Gruppe ist wichtig, weil fast alle Systempaper (Gruppe 1, Agentless, AgentCoder, Gloaguen) ihre Ergebnisse auf Benchmarks stützen. Die beiden Kritikpaper zeigen: **Bestandene Tests sind nicht gleich korrekter Code.** Das betrifft direkt die Praxis-Heuristik „grüne Tests = korrekt“ aus dhanorkar2026oversight.

---

## jimenez2024swebench — SWE-bench: Can Language Models Resolve Real-World GitHub Issues?

- **Typ / Venue:** Benchmark, ICLR 2024 (Preprint 2310.06770)
- **Gegenstand:** **2.294 Aufgaben** aus echten GitHub-Issues und zugehörigen gemergten PRs in 12 populären Python-Repositories. Gegeben sind Issue-Text und Codebasis; das Modell erzeugt einen Patch, der anhand der Tests aus dem Original-PR geprüft wird (ausführungsbasierte Evaluation). Dazu ein Trainingsdatensatz mit 19.000 Instanzen.
- **Kernbefunde:** 2023 löste das beste Modell (Claude 2 mit BM25-Retrieval) nur **1,96 %**. Gute Lösungen erfordern Änderungen über mehrere Funktionen und Dateien, lange Kontexte und Interaktion mit der Ausführungsumgebung, also genau die Fähigkeiten von Agenten.
- **Nutzen fürs Paper:** Standardreferenz für den Hintergrund. Die meisten untersuchten Systeme werden darauf gemessen (Lite: 300 Aufgaben, Verified: 500 von Menschen geprüfte Aufgaben).
- **Grenzen:** Nur Python, populäre Repositories, möglicherweise in den Trainingsdaten enthalten. Qualität hängt an den Tests (siehe unten).

---

## aleithan2024swebenchplus — SWE-Bench+: Enhanced Coding Benchmark for LLMs

- **Typ / Venue:** Empirische Benchmark-Analyse, arXiv-Preprint (2410.06992)
- **Methode:** Manueller Vergleich der *erfolgreichen* Patches von SWE-agent + GPT-4 mit den echten PRs
- **Kernbefunde:**
  - **32,67 %** der erfolgreichen Patches sind „Cheating“: Die Lösung stand schon im Issue oder in den Kommentaren (**Solution Leakage**).
  - **31,08 %** sind verdächtig, weil die **Tests zu schwach** sind, um Korrektheit zu prüfen.
  - Ohne diese Fälle fällt die Lösungsrate von **12,47 % auf 3,97 %**. SWE-bench Lite und Verified haben dieselben Probleme.
  - Über **94 %** der Issues sind älter als der Wissensstichtag der Modelle, es droht also Datenleck.
  - Auf dem neuen **SWE-Bench+** mit Issues nach dem Stichtag und ohne Lösungen im Text: SWE-agent + GPT-4 **0,55 %**, AutoCodeRover + GPT-4o 3,83 %.
- **Nutzen fürs Paper:** Benchmark-Ergebnisse überschätzen die Fähigkeiten deutlich. Die Qualität der Issue-Beschreibung und der Tests bestimmt, was „gelöst“ bedeutet. Stützt die Forderung nach Praxisstudien.
- **Grenzen:** Preprint, nur ein Agent manuell analysiert, Stand 2024. Neuere Modelle wurden nicht untersucht.

---

## wang2026solvedissues — Are "Solved Issues" in SWE-bench Really Solved Correctly? An Empirical Study

- **Typ / Venue:** Empirische Studie mit neuer Technik, ICSE 2026 (DOI 10.1145/3744916.3764576)
- **Methode:** Plausible Patches von drei Werkzeugen (CodeStory, LearnByInteract, **OpenHands**) auf SWE-bench Verified werden gegen die Patches der Entwickler geprüft. Neue Technik **PatchDiff**: Differentielles Testen erzeugt Tests, die Verhaltensunterschiede zwischen zwei Patches aufdecken.
- **Kernbefunde:**
  - **7,8 %** der als „korrekt“ gewerteten Patches scheitern an der vollständigen Testsuite der Entwickler. SWE-bench führt nur die geänderten Testdateien aus.
  - **29,6 %** der plausiblen Patches verhalten sich anders als die Referenzlösung. Ursachen: ähnliche, aber abweichende Implementierung (46,8 %) oder mehr geändertes Verhalten als nötig (27,3 %).
  - Davon sind laut manueller Prüfung **28,6 % sicher falsch**.
  - Insgesamt sind die gemeldeten Lösungsraten um **6,4 Prozentpunkte überhöht**.
- **Nutzen fürs Paper:** Neuester und methodisch stärkster Beleg dafür, dass Tests als einzige Abnahme nicht reichen. Für den Workflow folgt: **vollständige Testsuite ausführen** und **Verhaltensänderungen über den Auftrag hinaus prüfen**, die Agenten-Patches „zusätzlich“ einführen.
- **Grenzen:** Nur Python und SWE-bench Verified. PatchDiff findet Unterschiede, entscheidet aber nicht automatisch, ob ein Patch richtig oder falsch ist.
