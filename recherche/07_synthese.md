# Synthese: Querbezüge, Prinzipien, Widersprüche, Lücken

Vorarbeit für **V. Gestaltungsprinzipien** und **VI. Diskussion**. Die Prinzipien sind *Vorschläge* zum Diskutieren im Team. PLAN.md verlangt, dass jedes Prinzip durch mindestens zwei Quellen gestützt ist; das ist bei allen erfüllt.

---

## 1. Kernaussagen je Dimension

### A) Autonomiegrad und menschliche Beteiligung

- **Mehr Autonomie ist nicht automatisch besser.**
  - Ein fester Ablauf schlägt komplexe Agenten (xia2025agentless).
  - Mehr Kontrolle über die Codebasis bringt mehr Schwachstellen (sajadi2025patchsecurity).
- **Menschliche Freigabe an definierten Punkten funktioniert:** 82 % Plan-Freigabe bei HULA. Über die gesamte Kette sinkt die Erfolgsquote aber stark: Nur 25 % der Code-Ergebnisse werden zum PR, davon 59 % gemergt (takerngsaksiri2025hula).
- **Agenten helfen besonders bei unbekannten Aufgaben bzw. Codebasen** (chen2025codewithme). In vertrauten, komplexen Repositories bremsen KI-Werkzeuge erfahrene Entwickler eher (becker2025metr).
- **Aufsicht findet vor, während und nach der Ausführung statt** (dhanorkar2026oversight). Im Alltag wird sie über riskante Heuristiken abgekürzt.

### B) Kontext und Steuerung

- Kontextdateien sind verbreitet, haben aber keine feste Struktur (chatlatanagulchai2025manifests, mohsenimofidi2026context). **Ihre Wirkung auf die Lösungsrate ist nicht nachgewiesen.** Sie kosten über 20 % mehr, werden aber befolgt (gloaguen2026agentsmd).
- **Weniger, gezielter Kontext ist besser als mehr:** Repository-Übersichten helfen nicht (gloaguen2026agentsmd), und ein Dateibetrachter mit 100 Zeilen schlägt die ganze Datei (yang2024sweagent).
- **Die Aufgabenbeschreibung ist der wichtigste Kontext.**
  - Kurze Issues senken die Leistung (takerngsaksiri2025hula).
  - Unvollständige Issues führen zu falschen Patches (zhang2024autocoderover).
  - Fehlende Reproduktionsschritte bzw. Snippets erhöhen das Risiko für Schwachstellen (sajadi2025patchsecurity).
  - Implizites Projektwissen fehlt der KI (becker2025metr).

### C) Qualitätssicherung und Fehlermuster

- **Ausführbare Verifikation verbessert Ergebnisse:** Linter als Leitplanke (yang2024sweagent), unabhängige Tests (huang2023agentcoder), SBFL (zhang2024autocoderover), Prüfung gegen das übergeordnete Ziel mit +15,6 % (cemri2025mast).
- **Bestandene Tests sind nicht gleich korrekter Code:**
  - 31 % schwache Tests (aleithan2024swebenchplus)
  - 29,6 % Verhaltensabweichungen bei plausiblen Patches (wang2026solvedissues)
  - 34,6 % Overfitting (zhang2024autocoderover)
  - Trotzdem gilt „grüne Tests = korrekt“ in der Praxis als Heuristik (dhanorkar2026oversight).
- **Sicherheit muss eigens geprüft werden.** Agenten erzeugen andere Schwachstellentypen als Menschen (sajadi2025patchsecurity), und Kontextdateien behandeln Sicherheit selten (mohsenimofidi2026context).
- **Ein Viertel der Fehler in Multi-Agenten-Systemen sind Verifikationsfehler** (cemri2025mast).

### Produktivität

| Befund | Quelle | Umfeld |
|---|---|---|
| +26 % abgeschlossene Aufgaben | cui2025genai | Code-Completion, große Firmen, eher Junioren |
| +35 % Korrektheit bei ~50 % Aufwand | chen2025codewithme | Agent vs. Copilot, Studierende, Laboraufgaben |
| 4 min vs. 2,68 Tage pro Issue | zhang2024autocoderover | Benchmark (unfairer Vergleich) |
| PRs 10× schneller geschlossen; 164 PRs in 5 Tagen | li2025aidev | Open Source, aber geringere Akzeptanz |
| geringerer Aufwand wahrgenommen | takerngsaksiri2025hula | Umfrage, Industrie |
| **−19 % (langsamer)**, gefühlt +20 % | becker2025metr | Experten, eigene große Repositories |
| +20 % Inferenzkosten durch Kontextdateien | gloaguen2026agentsmd | Benchmark |

**Lesart:** Der Nutzen hängt vom Umfeld ab. Er ist hoch bei unbekanntem Code, einfachen bzw. klar umrissenen Aufgaben und weniger erfahrenen Personen. Er ist niedrig oder negativ bei Experten in großen Codebasen mit viel implizitem Wissen. Selbsteinschätzungen überschätzen den Nutzen systematisch (becker2025metr). Das schwächt alle Studien, die nur Umfragen nutzen.

---

## 2. Kandidaten für die Gestaltungsprinzipien P1–P6

### P1: Planen vor Ausführen, mit menschlicher Freigabe des Plans

Der Agent erstellt zuerst einen Plan; der Mensch prüft und korrigiert ihn, erst dann wird Code geschrieben.

- **Belege:** takerngsaksiri2025hula (82 % Freigabe, Feedback reichert Kontext an) · dhanorkar2026oversight (Co-Planning als vorbeugende Aufsicht) · xia2025agentless (feste Phasen statt freier Planung) · chen2025codewithme (Transparenz, Checkpoints)
- **Wirkung:** Qualität + (früh Fehlrichtungen erkennen), Produktivität + (geringerer Einstiegsaufwand)
- **Einschränkung:** Der Plan ist kein Beweis für die Umsetzung (dhanorkar2026oversight, Heuristik 1). Die Freigabe des Plans ersetzt also nicht das Review des Codes.

### P2: Autonomie nach Aufgabentyp und Risiko staffeln

Hohe Autonomie bei Doku, Tests, Refactoring und unbekanntem Code. Enge Führung bei Features bzw. Bugfixes mit dateiübergreifender Logik und bei sicherheitsrelevantem Code.

- **Belege:** li2025aidev (Doku 86–89 % Akzeptanz, Features/Fixes deutlich niedriger) · watanabe2025agenticprs (Einsatz bei Refactoring, Doku, Tests) · sajadi2025patchsecurity (mehr Autonomie und mehr Dateien, mehr Schwachstellen) · chen2025codewithme vs. becker2025metr (unbekannter vs. vertrauter Code)
- **Wirkung:** Qualität + (weniger riskante Autonomie), Produktivität + (Agent dort, wo er hilft)

### P3: Kontext knapp, gezielt und aufgabenbezogen

Kontextdateien enthalten nur, was nicht im Code oder README steht (Konventionen, Verbote, Build-/Test-Befehle), werden von Menschen geschrieben und gepflegt. Die Aufgabenbeschreibung enthält erwartetes Verhalten, Reproduktionsschritte und Code-Bezüge.

- **Belege:** gloaguen2026agentsmd (Übersichten nutzlos, LLM-generiert schlechter, +20 % Kosten) · yang2024sweagent (zu viel Kontext schadet) · mohsenimofidi2026context / chatlatanagulchai2025manifests (Praxis: Befehle, Konventionen; Stile präskriptiv/prohibitiv) · takerngsaksiri2025hula, zhang2024autocoderover, sajadi2025patchsecurity (Qualität der Issue-Beschreibung) · watanabe2025agenticprs (Projektregeln festhalten)
- **Wirkung:** Qualität + (Konventionen werden befolgt, weniger Fehlinterpretation), Produktivität ± (mehr Schritte und Kosten)
- **Hinweis:** Schwach belegt, was die Lösungsrate angeht; gut belegt, was die Einhaltung von Anweisungen angeht. So formulieren.

### P4: Ausführbare, unabhängige Verifikation als Leitplanke

Linter, Typprüfung und Tests laufen automatisch nach jeder Änderung. Tests entstehen möglichst unabhängig vom generierten Code oder liegen schon vor. Die vollständige Testsuite läuft, nicht nur die neuen Tests. Zusätzlich wird geprüft, ob das übergeordnete Ziel erfüllt ist.

- **Belege:** yang2024sweagent (Linter-Guardrail) · huang2023agentcoder (unabhängige Tests) · cemri2025mast (Verifikation auf Ziel-Ebene +15,6 %, oberflächliche Verifizierer) · zhang2024autocoderover (SBFL) · wang2026solvedissues (vollständige Suite, Verhaltensabweichungen) · aleithan2024swebenchplus (schwache Tests)
- **Wirkung:** Qualität ++, Produktivität + (weniger Nacharbeit), aber höhere Laufzeit und Kosten

### P5: Menschliches Review bleibt verbindlich, auch für Sicherheit

Agenten-Code durchläuft ein normales Code-Review und dazu eine statische Sicherheitsanalyse. Das Review darf sich nicht allein auf grüne Tests oder Überfliegen stützen; Automation Bias ist ein bekanntes Risiko.

- **Belege:** watanabe2025agenticprs (45 % brauchen Nacharbeit) · li2025aidev (58 % ohne explizites Review, sehr kurze Review-Zeiten, Bots vom selben Anbieter) · sajadi2025patchsecurity (11× mehr Schwachstellen, neue CWE-Typen) · dhanorkar2026oversight (Heuristiken, Automation Bias, EU AI Act) · takerngsaksiri2025hula (Codequalität bleibt Thema)
- **Wirkung:** Qualität ++, Produktivität − (Review-Aufwand). Hier liegt der zentrale Zielkonflikt.

### P6: Kleine, nachvollziehbare Änderungen

PRs klein und auf eine Aufgabe beschränkt halten. Agentenbeiträge als solche kennzeichnen (Co-Author). Agentenaktionen sichtbar machen und in einer Sandbox ausführen.

- **Belege:** watanabe2025agenticprs (kleine PRs reduzieren Review-Reibung) · sajadi2025patchsecurity (mehr geänderte Dateien, mehr Schwachstellen) · li2025aidev (fehlende Urheberschaft) · wang2025openhands (Sandbox, sichtbare Aktionen) · dhanorkar2026oversight (A-priori-Kontrolle: Berechtigungen, Deny-Listen) · chen2025codewithme (Transparenz)
- **Spannung:** robbes2026agenticmuch zeigt, dass Agenten-Commits in der Praxis *größer* sind. Das Prinzip steht damit gegen die gängige Praxis.

**Mögliche Verdichtung auf 4 Prinzipien** für die Seitengrenze: P1 + P2 → „Gestufte Autonomie mit Plan-Freigabe“ · P3 · P4 + P5 → „Mehrstufige Verifikation: automatisch und menschlich“ · P6.

**Vorschlag für die Abbildung (Workflow-Schema):**
`Kontext vorbereiten (P3) → Planen + Freigabe (P1/P2) → Ausführen in Sandbox (P6) → Automatische Verifikation (P4) → Review + Sicherheitsprüfung (P5) → kleiner PR (P6)`

---

## 3. Widersprüche und Spannungen (für VI. Diskussion)

1. **Produktivität: +26 % vs. −19 %.** Anderes Werkzeug (Completion vs. Agent bzw. Chat), andere Personen (Junioren vs. Experten), andere Messgröße (Output-Zahl vs. Zeit pro Aufgabe). → Es kommt auf Umfeld und Workflow an. Das stützt den Ansatz des Papers.
2. **Benchmark-Erfolg vs. Praxisakzeptanz.** Agenten werden auf Benchmarks immer besser. In der Praxis ist die Akzeptanz geringer als bei Menschen (li2025aidev, watanabe2025agenticprs), und Benchmark-Werte sind überhöht (aleithan2024swebenchplus, wang2026solvedissues).
3. **Kontextdateien:** Anbieter und Praxis empfehlen sie (Verbreitung 5 % → wachsend), ihr messbarer Nutzen ist aber nicht belegt (gloaguen2026agentsmd).
4. **Tests als Garantie:** Tests sind der wichtigste Hebel (Gruppe 4), aber zugleich die größte Schwachstelle der Evaluation (Gruppe 6) und eine riskante Review-Heuristik (dhanorkar2026oversight).
5. **Geschwindigkeit des Reviews:** Schnelle Merges wirken produktiv (li2025aidev), deuten aber auf flache Reviews hin. Das passt zu den Sicherheitsbefunden (sajadi2025patchsecurity).

---

## 4. Forschungslücken (für VI. Diskussion)

- **Keine Langzeitstudien** zu Wartbarkeit, technischer Schuld und Kompetenzverlust. Alle Studien sind Momentaufnahmen von 2024–2026.
- **Kaum kontrollierte Studien zu Workflow-Varianten.** Fast nichts vergleicht etwa mit vs. ohne Plan-Freigabe oder kleine vs. große Aufgaben *im selben Setting*. HULA und Chen kommen am nächsten.
- **Wirkung von Kontext auf Qualitätsmerkmale jenseits der Lösungsrate** (Konventionen, Wartbarkeit) ist ungemessen.
- **Sicherheit** wird nur in einer Studie systematisch untersucht (sajadi2025patchsecurity, Preprint).
- **Die Rolle der Entwickler verändert sich** (Developer-Manager, dhanorkar2026oversight). Folgen für Ausbildung und Kompetenzen sind offen.
- **Sprachen und Domänen:** fast alles Python bzw. Open Source; Industrie nur bei HULA (Atlassian) und Cui.

## 5. Grenzen der eigenen Literaturbasis (Threats to Validity)

- 9 von 22 Quellen sind Preprints ohne Peer Review (Stand 16.10.2026).
- Eine Quelle (cui2025genai) untersucht keine Agenten. huang2023agentcoder (Dez. 2023) ist die älteste Quelle und testet nur auf Funktionsebene.
- Interessenkonflikte: Chen et al. sind OpenHands-Entwickler, HULA kommt von Atlassian, Dhanorkar et al. sind bei Microsoft.
- Viele Studien beruhen auf demselben Benchmark (SWE-bench), dessen Schwächen in Gruppe 6 belegt sind.
- Der Bereich ändert sich schnell: Ergebnisse mit Modellen von 2024 (GPT-4, Claude 3) gelten nur eingeschränkt für heutige Agenten.

---

## 6. To-dos für `references.bib`

| Eintrag | Änderung |
|---|---|
| watanabe2025agenticprs | Laut arXiv v3 bei **ACM Transactions on Software Engineering and Methodology (TOSEM)** angenommen → `@article`, `journal = {ACM TOSEM}`, Hinweis „accepted“ bzw. DOI, sobald vorhanden |
| zhang2024autocoderover | DOI ergänzen: `10.1145/3650212.3680384` |
| mohsenimofidi2026context | DOI ergänzen: `10.1145/3793302.3793350` |
| wang2026solvedissues | DOI ergänzen: `10.1145/3744916.3764576` |
| cemri2025mast | `booktitle` präzisieren: NeurIPS 2025, *Datasets and Benchmarks Track* |
| gloaguen2026agentsmd | Autor im PDF als „Mündler-Sasahara, Niels“ geschrieben. Prüfen, welche Schreibweise die Venue verwendet. |
| cui2025genai | Inhaltlich prüfen: Ausschlusskriterium Code-Completion (siehe oben) |
