# Gruppe 2: Autonomiegrad und menschliche Beteiligung

Für **IV.A** im Ergebnisteil. Leitfrage: Wie viel Entscheidungsfreiheit sollte der Agent haben, und an welchen Stellen greift der Mensch ein?

Die Gruppe deckt das Spektrum ab:

- **Festgelegter Workflow ohne Agentenautonomie:** Agentless
- **Human-in-the-Loop mit Freigabestellen:** HULA
- **Agent statt Copilot:** Chen et al.
- **Wie Entwickler Agenten in der Praxis beaufsichtigen:** Dhanorkar et al.

---

## xia2025agentless — Agentless: Demystifying LLM-based Software Engineering Agents

- **Typ / Venue:** Systembeschreibung mit Benchmark-Evaluation, FSE 2025 (Preprint arXiv:2407.01489)
- **Gegenstand:** Gegenentwurf zu autonomen Agenten. Ein fest vorgegebener Ablauf in drei Phasen: **Lokalisierung → Reparatur → Patch-Validierung**. Das LLM entscheidet nicht selbst über nächste Schritte und bedient keine komplexen Werkzeuge.
- **Kritik an autonomen Agenten:**
  1. Werkzeugnutzung und -design sind komplex und fehleranfällig.
  2. Bei der Planung fehlt Kontrolle: 30–40 Schritte pro Aufgabe, schwer nachzuvollziehen und zu debuggen.
  3. Der Agent erkennt irreführendes Feedback nur schlecht.
- **Kernbefunde:**
  - **32,00 %** auf SWE-bench Lite (96 Aufgaben) bei 0,70 USD pro Aufgabe, damals bestes Open-Source-Ergebnis. OpenAI nutzte den Ansatz zur Demonstration von GPT-4o und o1.
  - Die manuelle Klassifikation von SWE-bench Lite findet Aufgaben, deren Lösung schon im Issue steht, sowie unklare oder irreführende Beschreibungen. Daraus entsteht das bereinigte **SWE-bench Lite-S**.
- **Wirkung:** *Qualität und Kosten:* Ein einfacher, kontrollierter Ablauf ist mindestens so gut wie komplexe Agenten und günstiger.
- **Nutzen fürs Paper:** Zentrale Quelle für „mehr Autonomie ist nicht automatisch besser“. Spricht für einen **strukturierten Workflow mit festen Phasen**. Liefert außerdem Benchmark-Kritik für Gruppe 6.
- **Grenzen:** Nur Bugfixes in Python (SWE-bench Lite). Offene, explorative Aufgaben deckt der Ansatz nicht ab.

---

## takerngsaksiri2025hula — Human-In-the-Loop Software Development Agents (HULA)

- **Typ / Venue:** Systembeschreibung mit Feldeinsatz und Umfrage, ICSE-SEIP 2025 (Atlassian, Monash University, University of Melbourne)
- **Gegenstand:** Ein Framework mit drei Rollen, eingebaut in Atlassian JIRA: **AI Planner Agent**, **AI Coding Agent** und **Human Agent**. Der Mensch prüft und verfeinert zuerst den Plan, dann den Code.
- **Methode:** Dreistufige Evaluation
  1. offline auf SWE-bench und 369 interne JIRA-Issues
  2. online im Einsatz mit 663 echten JIRA-Issues
  3. Umfrage unter Atlassian-Entwicklern
- **Kernbefunde:**
  - *Offline:* Recall der zu ändernden Dateien 86 % (SWE-bench) gegenüber 30 % (intern). Code-Ähnlichkeit 45 % gegenüber 30 %. Die internen Issues sind kürzer, haben also weniger Kontext.
  - *Online:*
    - Für 527 von 663 Issues entsteht ein Plan, davon werden **433 freigegeben (82 %)**.
    - Für 376 Issues wird Code erzeugt; bei 95 davon (25 %) öffnen die Entwickler einen PR.
    - **56 dieser PRs werden gemergt (59 %)**.
  - *Umfrage:* 41 % finden den Plan passend zum Issue, 61 % halten den Code für gut les- und änderbar. Das spart Zeit vor allem beim Einstieg und bei einfachen Aufgaben.
  - **Die Codequalität bleibt in Teilen ein Problem.** Detaillierte Issue-Beschreibungen sind nötig, was zu besserer Dokumentation führt, aber Aufwand kostet.
- **Fazit der Autoren:**
  1. Die Detailtiefe der Eingabe bestimmt die Leistung stark.
  2. Menschliches Feedback reichert den Kontext an.
  3. Zeit und Aufwand sinken, die Qualität ist aber nicht garantiert.
- **Wirkung:** *Produktivität:* subjektiv geringerer Aufwand. *Qualität:* Plan-Freigabe funktioniert gut, über die ganze Kette bis zum gemergten Code sinkt die Erfolgsquote aber deutlich.
- **Nutzen fürs Paper:** Hauptbeleg für eine **Freigabe nach dem Planungsschritt** (Plan → menschliche Prüfung → Code). Verbindet die Dimensionen Autonomie und Kontext.
- **Grenzen:** Ein Unternehmen, Wahrnehmung per Umfrage statt gemessener Zeit, Industrie-Autoren.

---

## chen2025codewithme — Code with Me or for Me? How Increasing AI Automation Transforms Developer Workflows

- **Typ / Venue:** Kontrollierte Nutzerstudie, arXiv-Preprint (2507.08149). Autoren von CMU und All Hands AI, also selbst OpenHands-Entwickler.
- **Methode:** Within-Subject-Design, **20 Teilnehmende**: Studierende mit Copilot-Erfahrung, 60 % davon mit 3–5 Jahren Berufserfahrung, ohne Agentenerfahrung. Sie lösen realistische Aufgaben (neu entwickeln, Feature einbauen, Bug fixen) einmal mit **GitHub Copilot** und einmal mit **OpenHands**.
- **Kernbefunde:**
  - Mit dem Agenten steigt die Aufgabenkorrektheit im Schnitt um **35 %**, bei etwa **50 % des Nutzeraufwands** (gemessen als Zeit).
  - Signifikant geringere kognitive Belastung. Die Teilnehmenden lösen Aufgaben, die sie sonst nicht geschafft hätten, z. B. in unbekannten Codebasen wie matplotlib.
  - Der Aufwand sinkt vor allem, weil der Agent selbst debuggt und Umgebungen aufsetzt.
  - Probleme: Die Teilnehmenden **verstehen das Agentenverhalten** und die Ausgaben oft nicht ausreichend; die Zufriedenheit ist eingeschränkt.
  - Drei Anforderungen an künftige Agenten: **Transparenz**, **ausgewogene Proaktivität** (z. B. Pausen an Aufgabengrenzen) und **gezielter Einsatz menschlicher Mitarbeit**.
- **Wirkung:** *Produktivität:* positiv, mehr gelöst bei weniger Aufwand. *Qualität:* höhere Korrektheit, aber weniger Verständnis des entstandenen Codes.
- **Nutzen fürs Paper:** Einzige kontrollierte Studie zum direkten Vergleich Copilot vs. Agent. Stützt Transparenz und Checkpoints als Gestaltungsprinzip.
- **Grenzen:** Kleine Stichprobe, Studierende, kurze Laboraufgaben, Interessenkonflikt (OpenHands-Team).

---

## dhanorkar2026oversight — Human Oversight of Agentic Systems in Practice

- **Typ / Venue:** Qualitative Interviewstudie, arXiv-Preprint (2606.05391, Juni 2026). Microsoft-Autoren, der Text verortet die Arbeit im FAccT-Umfeld.
- **Methode:** Interviews mit **17 erfahrenen Entwicklern** (Power User), ausgewertet mit offenem, axialem und selektivem Kodieren.
- **Kernbefunde – vier Formen der Aufsicht (Oversight Work):**
  1. **A-priori-Kontrolle:** Konfiguration vor dem Prompt, z. B. Deny-Listen und Berechtigungen
  2. **Co-Planning:** den Plan gemeinsam mit dem Agenten erarbeiten
  3. **Echtzeit-Monitoring** während der Ausführung
  4. **Post-hoc-Review** des Ergebnisses

  Aufsicht ist also nicht nur reaktiv und rückblickend, sondern auch **vorbeugend und proaktiv**.
- **Vier Heuristiken beim Review.** Effizienz geht dabei vor Vollständigkeit, und alle vier sind riskant:
  1. Der Plan gilt als zuverlässiges Abbild dessen, was der Agent tatsächlich getan hat.
  2. **Grüne Tests gelten als Beweis für korrekten Code.** Das ist nur so gut wie die Tests.
  3. Überfliegen und Stichproben statt vollständiger Prüfung.
  4. In unbekannten Domänen wird dem Agenten vertraut (**Automation Bias**). Stimmen zwei Agenten überein, steigt das Vertrauen weiter.
- **Weitere Punkte:** Code von Agenten zu reviewen ist schwierig, weil es zu viele Informationen sind. Die Rolle verschiebt sich vom „Craftsman“ zum **„Developer-Manager“**. Spannungsfeld mit der Aufsichtspflicht nach EU AI Act, Art. 14.
- **Wirkung:** *Qualität:* Die Heuristiken schaffen blinde Flecken bei der Prüfung. *Produktivität:* Ohne Heuristiken skaliert die Aufsicht nicht.
- **Nutzen fürs Paper:** Liefert die Begriffe für den Human-in-the-Loop-Teil und die Workflow-Phasen (vor, während und nach der Ausführung). Spannt den Bogen zu den Benchmark-Studien: Heuristik 2 scheitert an schwachen Tests (aleithan2024swebenchplus, wang2026solvedissues).
- **Grenzen:** Kleine qualitative Stichprobe von Microsoft-nahen Power-Usern, keine Messung von Wirkungen.
