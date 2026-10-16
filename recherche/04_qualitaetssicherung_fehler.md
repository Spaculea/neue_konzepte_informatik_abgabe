# Gruppe 4: Qualitätssicherung und Fehlermuster

Für **IV.C** im Ergebnisteil. Leitfrage: Wie sichert man die Qualität von Agentencode, und woran scheitern Agenten?

Rote Linie der Gruppe: **Verifikation ist der Hebel.** Sie muss aber unabhängig und gründlich sein; oberflächliche Prüfungen reichen nicht.

---

## huang2023agentcoder — AgentCoder: Multi-Agent Code Generation with Effective Testing and Self-optimisation

- **Typ / Venue:** Systembeschreibung mit Benchmark-Evaluation, arXiv-Preprint (2312.13010, v3 Mai 2024)
- **Gegenstand:** Drei Agenten:
  - **Programmer**
  - **Test Designer**: schreibt Tests *nur aus der Anforderung*, ohne den Code zu sehen
  - **Test Executor**: führt die Tests aus und meldet Fehler an den Programmer zurück

  Das wiederholt sich, bis alle Tests bestehen oder das Budget aufgebraucht ist.
- **Kernidee:** Tests, die im selben Verlauf direkt nach dem Code entstehen, sind durch den Code voreingenommen. **Code und Tests getrennt zu erzeugen** macht die Tests objektiver und vielfältiger.
- **Kernbefunde:** Mit GPT-4 **96,3 %** pass@1 auf HumanEval und **91,8 %** auf MBPP, bei 56,9K bzw. 66,3K Tokens. Der vorherige Bestwert lag bei 90,2 % bzw. 78,9 % mit 138,2K bzw. 206,5K Tokens. Evaluiert mit 14 LLMs und 16 Vergleichsansätzen. Wenige, klar getrennte Rollen schlagen große Multi-Agenten-Systeme wie MetaGPT (5 Agenten) oder ChatDev (7 Agenten).
- **Wirkung:** *Qualität:* höhere Korrektheit. *Kosten:* weniger Tokens.
- **Nutzen fürs Paper:** Beleg für **unabhängige Tests als Leitplanke** und für eine schlanke Rollenteilung.
- **Grenzen:** Nur Funktionsebene (HumanEval, MBPP), keine Repository-Aufgaben. Älteste Quelle der Sammlung (Preprint Dez. 2023), nach Absprache aber zulässig.

---

## cemri2025mast — Why Do Multi-Agent LLM Systems Fail?

- **Typ / Venue:** Empirische Fehleranalyse und Taxonomie, NeurIPS 2025 (Datasets & Benchmarks Track). UC Berkeley.
- **Methode:**
  - Grounded Theory auf 150 Traces, jeweils im Schnitt über 15.000 Zeilen, Übereinstimmung zwischen Annotatoren κ = 0,88
  - Danach Annotation von **1.642 Traces aus 7 Multi-Agenten-Frameworks** (z. B. ChatDev, MetaGPT) über ein LLM-as-a-Judge-Verfahren
  - Aufgaben aus Coding, Mathematik und allgemeinen Agentenaufgaben
- **Kernbefunde:**
  - Fehlerraten von **41 % bis 86,7 %** bei aktuellen Open-Source-Multi-Agenten-Systemen
  - **Taxonomie MAST** mit 14 Fehlermodi in drei Kategorien:
    1. **Systemdesign (44,2 %)**, z. B. Aufgabenspezifikation missachtet (11,8 %), Schritte wiederholt (15,7 %), Abbruchbedingung nicht erkannt (12,4 %)
    2. **Fehlabstimmung zwischen Agenten (32,3 %)**, z. B. Reasoning und Handlung passen nicht zusammen (13,2 %), keine Rückfrage bei Unklarheit
    3. **Verifikation (23,5 %)**: vorzeitiger Abbruch (6,2 %), keine oder unvollständige Prüfung (8,2 %), falsche Prüfung (9,1 %)
  - Verifizierer prüfen oft nur oberflächlich, etwa ob der Code kompiliert oder TODOs übrig sind. Ein ChatDev-Schachprogramm besteht die Prüfung und verletzt trotzdem die Spielregeln.
  - Eingriffe: Bessere Rollenbeschreibungen bringen +9,4 %, ein **zusätzlicher Prüfschritt gegen das übergeordnete Ziel +15,6 %** Erfolgsrate (ChatDev). Einfache Prompt-Korrekturen reichen aber nicht aus.
- **Wirkung:** *Qualität:* Fehler entstehen vor allem durch Systemdesign und fehlende Verifikation, nicht durch schwache Modelle.
- **Nutzen fürs Paper:** Liefert eine Fehlertaxonomie für IV.C. Zeigt, dass mehr Agenten nicht mehr Qualität bedeuten. Belegt eine **mehrstufige Verifikation**: technische Korrektheit *und* Erfüllung des Ziels.
- **Grenzen:** Allgemeine Multi-Agenten-Systeme, nicht speziell Coding-Agenten wie Claude Code. Programmieraufgaben sind meist kleine Programme (ProgramDev).

---

## sajadi2025patchsecurity — How Safe Are AI-Generated Patches? Security Risks in LLM and Agentic APR on SWE-bench

- **Typ / Venue:** Großangelegte Sicherheitsanalyse, arXiv-Preprint (2507.02976, v3 Dez. 2025)
- **Methode:**
  - Über 20.000 GitHub-Issues aus SWE-bench (Train und Test)
  - Verglichen werden Patches von Entwicklern, einem Einzel-LLM (Llama 3.3 70B) und drei Agenten-Frameworks (**OpenHands, AutoCodeRover, HoneyComb**)
  - Statische Analyse u. a. mit CodeQL und Semgrep, Mehrheitsentscheid, manuelle Validierung
- **Kernbefunde:**
  - Llama erzeugt **11× mehr neue Schwachstellen** als Entwickler (135 vs. 12 bestätigte). Es sind andere Typen, z. B. Eval-Injection (CWE-95) und unsichere Deserialisierung (CWE-502); das Modell kopiert also nicht einfach menschliche Fehler.
  - Alle drei Agenten erzeugen Schwachstellen. **OpenHands, der Agent mit der meisten Kontrolle über die Codebasis, erzeugt eine Größenordnung mehr** als AutoCodeRover und HoneyComb. **Mehr Autonomie heißt hier mehr Sicherheitsrisiko**, besonders bei neuen Features und dateiübergreifenden Änderungen.
  - Risikofaktoren:
    - **viele geänderte Dateien** und Dateitypen
    - Bug- und Konfigurations-Issues, bei denen **erwartetes Verhalten, Reproduktionsschritte oder Code-Snippets fehlen**
  - Faktoren auf Projektebene wie Größe oder Anzahl der Beitragenden spielen keine signifikante Rolle.
- **Wirkung:** *Qualität (Sicherheit):* deutlich negativ, umso stärker, je mehr Autonomie der Agent hat und je schlechter die Aufgabe beschrieben ist.
- **Nutzen fürs Paper:** Zentrale Quelle für Sicherheit. Verbindet alle drei Dimensionen: Autonomie (mehr Kontrolle, mehr Risiko), Kontext (fehlende Issue-Informationen) und Qualitätssicherung (Sicherheitsprüfung muss in den Workflow). Stützt **kleine Änderungen** und **risikobasiertes Review**.
- **Grenzen:** Die Agenten wurden nur auf dem kleineren Test-Split untersucht. Statische Analyse liefert Fehlalarme und übersieht Schwachstellen. Nur Python.
