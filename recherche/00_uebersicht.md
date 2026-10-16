# Übersicht aller 22 Quellen

**Legende Typ:** SYS = Systembeschreibung mit Evaluation · BENCH = Benchmark bzw. Benchmark-Experiment · NUTZ = kontrollierte Nutzerstudie · FELD = Feldstudie bzw. Repository-Mining · QUAL = qualitative Interviews · SURV = Survey

**Legende Wirkung:** + positiv · − negativ · ○ kein bzw. nicht signifikanter Effekt · – nicht gemessen

## Tabelle

| # | Bibkey | Gr. | Typ | Venue / Status | Kernbefund (eine Zeile) | Qualität | Produkt. |
|---|---|---|---|---|---|---|---|
| 1 | liu2024agentsurvey | 1 | SURV | arXiv 2409.02977 | 124 Paper; Agent = Planung, Memory, Wahrnehmung, Aktion; Agenten > reines LLM | + | – |
| 2 | yang2024sweagent | 1 | SYS | NeurIPS 2024 | Agentengerechte Schnittstelle (ACI) bringt +10,7 pp; Linter-Leitplanke und knappes Feedback | + | – |
| 3 | wang2025openhands | 1 | SYS | ICLR 2025 | Offene Plattform mit Docker-Sandbox und Event-Stream; 26 % SWE-bench Lite | – | – |
| 4 | zhang2024autocoderover | 1 | SYS | ISSTA 2024 | AST-Suche + SBFL; 19 % Lite in ~4 min; nur 65,4 % der „gelösten“ Patches korrekt | ± | + |
| 5 | xia2025agentless | 2 | SYS | FSE 2025 | Fester 3-Phasen-Ablauf ohne Autonomie: 32 % Lite, 0,70 USD; besser als komplexe Agenten | + | + (Kosten) |
| 6 | takerngsaksiri2025hula | 2 | SYS+FELD | ICSE-SEIP 2025 | Human-in-the-Loop in JIRA: 82 % Pläne freigegeben, 59 % der PRs gemergt; Codequalität bleibt Thema | ± | + (subjektiv) |
| 7 | chen2025codewithme | 2 | NUTZ | arXiv 2507.08149 | Agent vs. Copilot (n = 20): +35 % Korrektheit, ~50 % Aufwand; Verständnis des Agenten fehlt | + | + |
| 8 | dhanorkar2026oversight | 2 | QUAL | arXiv 2606.05391 | 17 Interviews: 4 Formen der Aufsicht; riskante Heuristiken (Plan, Tests, Überfliegen, Automation Bias) | − (Risiko) | – |
| 9 | chatlatanagulchai2025manifests | 3 | FELD | PROFES 2025 | 253 CLAUDE.md: flach; Build/Run-Befehle, Implementierung, Architektur | – | – |
| 10 | mohsenimofidi2026context | 3 | FELD | MSR 2026 | 5 % von 10.000 Repos mit Kontextdatei; keine feste Struktur; 5 Schreibstile; selten Sicherheit | – | – |
| 11 | gloaguen2026agentsmd | 3 | BENCH | ICLR 2026 | Kontextdateien: Lösungsrate ○, Kosten +20 %; LLM-generiert schlechter als von Hand geschrieben | ○ | − (Kosten) |
| 12 | huang2023agentcoder | 4 | SYS | arXiv 2312.13010 | Unabhängig erzeugte Tests: 96,3 % HumanEval mit weniger Tokens | + | + (Kosten) |
| 13 | cemri2025mast | 4 | FELD (Traces) | NeurIPS 2025 D&B | 1.642 Traces, 14 Fehlermodi: Systemdesign 44 %, Fehlabstimmung 32 %, Verifikation 24 % | − | – |
| 14 | sajadi2025patchsecurity | 4 | BENCH/FELD | arXiv 2507.02976 | LLM 11× mehr Schwachstellen als Entwickler; mehr Autonomie, mehr Risiko; fehlende Issue-Infos | − | – |
| 15 | watanabe2025agenticprs | 5 | FELD | TOSEM (angenommen) | 567 Claude-Code-PRs: 83,8 % gemergt (Menschen 91 %); 45 % brauchen Nacharbeit | ± | + |
| 16 | li2025aidev | 5 | FELD | arXiv 2507.15003 | 456K Agenten-PRs: geringere Akzeptanz außer bei Doku; sehr schnell; oft kein Review | − | + |
| 17 | robbes2026agenticmuch | 5 | FELD | arXiv 2601.18341 | 22–29 % von 128K Projekten nutzen Agenten; größere Commits, oft Features und Fixes | – | – |
| 18 | cui2025genai | 5 | RCT (Feld) | Management Science 2025 | ⚠ Code-Completion: +26 % Aufgaben, Junioren profitieren stärker | – | + |
| 19 | becker2025metr | 5 | RCT | arXiv 2507.09089 | Erfahrene Entwickler in eigenen Repos 19 % *langsamer* mit KI, fühlen sich aber 20 % schneller | ○ | − |
| 20 | jimenez2024swebench | 6 | BENCH | ICLR 2024 | 2.294 echte GitHub-Issues; ausführungsbasierte Evaluation | – | – |
| 21 | aleithan2024swebenchplus | 6 | BENCH-Analyse | arXiv 2410.06992 | 33 % Solution Leakage, 31 % schwache Tests; 12,47 % → 3,97 % → 0,55 % | − | – |
| 22 | wang2026solvedissues | 6 | BENCH-Analyse | ICSE 2026 | 29,6 % plausibler Patches verhalten sich anders; Lösungsraten um 6,4 pp überhöht | − | – |

## Matrix Quelle × Dimension

● = Hauptbeitrag · ○ = Nebenbefund

| Bibkey | A Autonomie & Mensch | B Kontext & Steuerung | C Qualitätssicherung | Produktivität | Benchmark-Kritik |
|---|:-:|:-:|:-:|:-:|:-:|
| liu2024agentsurvey | ○ | ○ | | | |
| yang2024sweagent | | ● | ● | | |
| wang2025openhands | ○ | | ○ | | |
| zhang2024autocoderover | ○ | ● | ● | ○ | ○ |
| xia2025agentless | ● | | ○ | ○ | ● |
| takerngsaksiri2025hula | ● | ● | ○ | ● | |
| chen2025codewithme | ● | | | ● | ○ |
| dhanorkar2026oversight | ● | ○ | ● | | |
| chatlatanagulchai2025manifests | | ● | | | |
| mohsenimofidi2026context | | ● | | | |
| gloaguen2026agentsmd | | ● | | ○ | |
| huang2023agentcoder | | | ● | ○ | |
| cemri2025mast | ○ | | ● | | |
| sajadi2025patchsecurity | ● | ● | ● | | |
| watanabe2025agenticprs | ○ | ○ | ● | ● | |
| li2025aidev | ○ | | ● | ● | ● |
| robbes2026agenticmuch | | | | ○ | |
| cui2025genai | | | | ● | |
| becker2025metr | | ○ | | ● | ● |
| jimenez2024swebench | | | | | ● |
| aleithan2024swebenchplus | | ○ | ○ | | ● |
| wang2026solvedissues | | | ● | | ● |

## Verteilung nach Studientyp

- **Praxis bzw. Feld** (FELD, QUAL, RCT im Feld): 9 → HULA, Dhanorkar, Chatlatanagulchai, Mohsenimofidi, Watanabe, Li, Robbes, Cui, Becker
- **Kontrollierte Nutzerstudien:** 2 → Chen, Becker (Becker ist zugleich Feldsetting)
- **Benchmark bzw. System:** 9 → SWE-agent, OpenHands, AutoCodeRover, Agentless, AgentCoder, Gloaguen, Sajadi, MAST, SWE-bench
- **Benchmark-Kritik:** 2 → Aleithan, Wang 2026
- **Survey:** 1 → Liu
- **Preprints ohne Venue (Stand 16.10.2026):** 9 → liu, chen, dhanorkar, huang, sajadi, li, robbes, becker, aleithan; watanabe ist inzwischen angenommen

## Links

arXiv: `https://arxiv.org/abs/<ID>`

| Bibkey | arXiv-ID / DOI |
|---|---|
| liu2024agentsurvey | 2409.02977 |
| yang2024sweagent | 2405.15793 |
| wang2025openhands | 2407.16741 |
| zhang2024autocoderover | 2404.05427 · DOI 10.1145/3650212.3680384 |
| xia2025agentless | 2407.01489 |
| takerngsaksiri2025hula | 2411.12924 |
| chen2025codewithme | 2507.08149 |
| dhanorkar2026oversight | 2606.05391 |
| chatlatanagulchai2025manifests | 2509.14744 · DOI 10.1007/978-3-032-12089-2_40 |
| mohsenimofidi2026context | 2510.21413 · DOI 10.1145/3793302.3793350 |
| gloaguen2026agentsmd | 2602.11988 |
| huang2023agentcoder | 2312.13010 |
| cemri2025mast | 2503.13657 |
| sajadi2025patchsecurity | 2507.02976 |
| watanabe2025agenticprs | 2509.14745 |
| li2025aidev | 2507.15003 |
| robbes2026agenticmuch | 2601.18341 |
| cui2025genai | DOI 10.1287/mnsc.2025.00535 |
| becker2025metr | 2507.09089 |
| jimenez2024swebench | 2310.06770 |
| aleithan2024swebenchplus | 2410.06992 |
| wang2026solvedissues | 2503.15223 · DOI 10.1145/3744916.3764576 |
