## LLM10:2025 Unkontrollierter Verbrauch

### Beschreibung

Unkontrollierter Verbrauch bezieht sich auf den Prozess, bei dem ein Large Language Model (LLM) Ausgaben auf Basis von Eingabeabfragen oder -anweisungen erzeugt. Die Inferenz ist eine kritische Funktion von LLMs, die erlernte Muster und Wissen anwenden, um relevante Antworten oder Vorhersagen zu liefern.

Angriffe, die darauf abzielen, den Dienst zu stören, die finanziellen Ressourcen des Ziels zu erschöpfen oder sogar geistiges Eigentum zu stehlen, indem das Verhalten eines Modells geklont wird, beruhen auf einer gemeinsamen Klasse von Sicherheitslücken, um erfolgreich zu sein. Unkontrollierter Verbrauch tritt auf, wenn eine LLM-Anwendung es Benutzern ermöglicht, exzessive und unkontrollierte Inferenzoperationen durchzuführen, was zu Risiken wie Denial-of-Service (DoS), wirtschaftlichen Verlusten, Modell-Diebstahl und Dienstverschlechterung führen kann. Die hohen Rechenanforderungen von LLMs, insbesondere in Cloud-Umgebungen, machen sie anfällig für Ressourcenausbeutung und unbefugte Nutzung.

### Häufige Beispiele für Schwachstellen

#### 1. Variable Eingabelängen-Überflutung
Angreifer können das LLM mit zahlreichen Eingaben unterschiedlicher Länge überlasten und dabei Verarbeitungsschwächen ausnutzen. Dies kann Ressourcen erschöpfen und das System möglicherweise unresponsive machen, was die Dienstverfügbarkeit erheblich beeinträchtigt.

#### 2. Denial of Wallet (DoW)
Durch die Einleitung eines hohen Volumens an Operationen nutzen Angreifer das Kosten-pro-Nutzung-Modell von cloudbasierten KI-Diensten aus, was zu untragbaren finanziellen Belastungen für den Anbieter und einem Risiko des finanziellen Ruins führt.

#### 3. Kontinuierlicher Eingabeüberfluss
Das kontinuierliche Senden von Eingaben, die das Kontextfenster des LLM überschreiten, kann zu einem übermäßigen Verbrauch von Rechenressourcen führen, was zu Dienstverschlechterungen und betrieblichen Störungen führt.

#### 4. Ressourcenintensive Anfragen
Das Einreichen von ungewöhnlich anspruchsvollen Anfragen mit komplexen Sequenzen oder komplizierten Sprachmustern kann Systemressourcen erschöpfen, was zu verlängerten Verarbeitungszeiten und möglichen Systemausfällen führt.

#### 5. Modellauszug über API
Angreifer können die Modell-API mit sorgfältig gestalteten Eingaben und Prompt-Injection-Techniken abfragen, um genügend Ausgaben zu sammeln, um ein partielles Modell zu replizieren oder ein Schattenmodell zu erstellen. Dies birgt nicht nur Risiken eines Diebstahls geistigen Eigentums, sondern untergräbt auch die Integrität des Originalmodells.

#### 6. Funktionale Modellreplikation
Durch die Nutzung des Zielmodells zur Generierung synthetischer Trainingsdaten können Angreifer ein anderes Basis-Modell feinabstimmen und eine funktionale Äquivalenz schaffen. Dies umgeht traditionelle abfragebasierte Extraktionsmethoden und stellt erhebliche Risiken für proprietäre Modelle und Technologien dar.

#### 7. Side-Channel-Angriffe
Böswillige Angreifer können Eingabefiltertechniken des LLM ausnutzen, um Side-Channel-Angriffe auszuführen und Modellgewichte sowie Architekturinformationen zu erlangen. Dies könnte die Sicherheit des Modells kompromittieren und weitere Angriffe ermöglichen.

### Präventions- und Abhilfemaßnahmen

#### 1. Eingabevalidierung
Implementieren Sie eine strikte Eingabevalidierung, um sicherzustellen, dass Eingaben keine angemessenen Größenlimits überschreiten.

#### 2. Einschränkung von Logits und Logprobs
Beschränken oder verschleiern Sie die Offenlegung von `logit_bias` und `logprobs` in API-Antworten. Stellen Sie nur die notwendigen Informationen bereit, ohne detaillierte Wahrscheinlichkeiten offenzulegen.

#### 3. Ratenbegrenzung
Setzen Sie Ratenbegrenzungen und Benutzerkontingente ein, um die Anzahl der Anfragen, die eine einzelne Entität in einem bestimmten Zeitraum stellen kann, einzuschränken.

#### 4. Ressourcenmanagement
Überwachen und verwalten Sie die Ressourcenzuweisung dynamisch, um zu verhindern, dass ein einzelner Benutzer oder eine einzelne Anfrage übermäßige Ressourcen verbraucht.

#### 5. Zeitüberschreitungen und Drosselung
Setzen Sie Zeitlimits und drosseln Sie die Verarbeitung ressourcenintensiver Operationen, um anhaltenden Ressourcenverbrauch zu verhindern.

#### 6. Sandbox-Techniken
Beschränken Sie den Zugriff des LLM auf Netzwerkressourcen, interne Dienste und APIs.
- Dies ist besonders wichtig für alle gängigen Szenarien, da es Insider-Risiken und Bedrohungen umfasst. Darüber hinaus steuert es das Ausmaß des Zugriffs, den die LLM-Anwendung auf Daten und Ressourcen hat, und dient damit als entscheidender Kontrollmechanismus zur Abschwächung oder Verhinderung von Side-Channel-Angriffen.

#### 7. Umfassende Protokollierung, Überwachung und Anomalieerkennung
Überwachen Sie kontinuierlich den Ressourcenverbrauch und implementieren Sie Protokollierung, um ungewöhnliche Muster im Ressourcenverbrauch zu erkennen und darauf zu reagieren.

#### 8. Wasserzeichen
Implementieren Sie Wasserzeichen-Frameworks, um die unbefugte Nutzung von LLM-Ausgaben einzubetten und zu erkennen.

#### 9. Graceful Degrade
Entwerfen Sie das System so, dass es unter hoher Last graceful degradiert, sodass eine Teilfunktionalität erhalten bleibt, anstatt komplett auszufallen.

#### 10. Begrenzung von Warteschlangenaktionen und skalierbare Infrastruktur
Begrenzen Sie die Anzahl der Warteschlangenaktionen und Gesamtaktionen, während Sie dynamische Skalierung und Lastverteilung integrieren, um variable Anforderungen zu bewältigen und eine konsistente Systemleistung sicherzustellen.

#### 11. Robustheitstraining gegen Angriffe
Trainieren Sie Modelle, um adversarielle Anfragen und Extraktionsversuche zu erkennen und abzumildern.

#### 12. Glitch-Token-Filterung
Erstellen Sie Listen bekannter Glitch-Token und scannen Sie Ausgaben, bevor sie dem Kontextfenster des Modells hinzugefügt werden.

#### 13. Zugriffskontrollen
Implementieren Sie starke Zugriffskontrollen, einschließlich rollenbasierter Zugriffskontrolle (RBAC) und des Prinzips der geringsten Privilegien, um unbefugten Zugriff auf LLM-Modell-Repositories und Trainingsumgebungen zu begrenzen.

#### 14. Zentralisierte ML-Modell-Inventarisierung
Nutzen Sie ein zentralisiertes Inventar oder ein zentrales Register für Modelle, die in der Produktion verwendet werden, um eine ordnungsgemäße Governance und Zugriffskontrolle sicherzustellen.

#### 15. Automatisierte MLOps-Bereitstellung
Implementieren Sie automatisierte MLOps-Bereitstellungen mit Governance-, Verfolgungs- und Genehmigungs-Workflows, um Zugriffs- und Bereitstellungskontrollen innerhalb der Infrastruktur zu verschärfen.

### Beispielhafte Angriffsszenarien

#### Szenario #1: Unkontrollierte Eingabegröße
Ein Angreifer reicht eine ungewöhnlich große Eingabe an eine LLM-Anwendung ein, die Textdaten verarbeitet. Dies führt zu einem übermäßigen Speicherverbrauch und hoher CPU-Auslastung, was das System möglicherweise abstürzen lässt oder den Dienst erheblich verlangsamt.

#### Szenario #2: Wiederholte Anfragen
Ein Angreifer übermittelt ein hohes Volumen von Anfragen an die LLM-API, was zu einem übermäßigen Verbrauch von Rechenressourcen führt und den Dienst für legitime Benutzer unzugänglich macht.

#### Szenario #3: Ressourcenintensive Anfragen
Ein Angreifer gestaltet spezifische Eingaben, die die rechenintensivsten Prozesse des LLM auslösen, was zu verlängerten CPU-Auslastungen und möglichen Systemausfällen führt.

#### Szenario #4: Denial of Wallet (DoW)
Ein Angreifer generiert exzessive Operationen, um das Pay-per-Use-Modell von cloudbasierten KI-Diensten auszunutzen und dadurch untragbare Kosten für den Dienstanbieter zu verursachen.

#### Szenario #5: Funktionale Modellreplikation
Ein Angreifer nutzt die API des LLM, um synthetische Trainingsdaten zu generieren und ein anderes Modell zu feinabstimmen. Dies schafft eine funktionale Äquivalenz und umgeht traditionelle Einschränkungen bei der Modellausgabe.

#### Szenario #6: Umgehung von Eingabefiltern
Ein böswilliger Angreifer umgeht Eingabefiltertechniken und Voranweisungen des LLM, um einen Side-Channel-Angriff durchzuführen und Modellinformationen an eine kontrollierte Ressource zu exfiltrieren.

### Referenzlinks

1. [Proof Pudding (CVE-2019-20634)](https://avidml.org/database/avid-2023-v009/) **AVID** (`moohax` & `monoxgas`)
2. [arXiv:2403.06634 Stealing Part of a Production Language Model](https://arxiv.org/abs/2403.06634) **arXiv**
3. [Runaway LLaMA | How Meta's LLaMA NLP model leaked](https://www.deeplearning.ai/the-batch/how-metas-llama-nlp-model-leaked/): **Deep Learning Blog**
4. [I Know What You See:](https://arxiv.org/pdf/1803.05847.pdf): **Arxiv White Paper**
5. [A Comprehensive Defense Framework Against Model Extraction Attacks](https://ieeexplore.ieee.org/document/10080996): **IEEE**
6. [Alpaca: A Strong, Replicable Instruction-Following Model](https://crfm.stanford.edu/2023/03/13/alpaca.html): **Stanford Center on Research for Foundation Models (CRFM)**
7. [How Watermarking Can Help Mitigate The Potential Risks Of LLMs?](https://www.kdnuggets.com/2023/03/watermarking-help-mitigate-potential-risks-llms.html): **KD Nuggets**
8. [Securing AI Model Weights Preventing Theft and Misuse of Frontier Models](https://www.rand.org/content/dam/rand/pubs/research_reports/RRA2800/RRA2849-1/RAND_RRA2849-1.pdf)
9. [Sponge Examples: Energy-Latency Attacks on Neural Networks: Arxiv White Paper](https://arxiv.org/abs/2006.03463) **arXiv**
10. [Sourcegraph Security Incident on API Limits Manipulation and DoS Attack](https://about.sourcegraph.com/blog/security-update-august-2023) **Sourcegraph**

### Verwandte Frameworks und Taxonomien

Verweisen Sie auf diesen Abschnitt für umfassende Informationen, Szenarien und Strategien zu Infrastrukturbereitstellungen, angewandten Umgebungssteuerungen und anderen Best Practices.

- [MITRE CWE-400: Uncontrolled Resource Consumption](https://cwe.mitre.org/data/definitions/400.html) **MITRE Common Weakness Enumeration**
- [AML.TA0000 ML Model Access: Mitre ATLAS](https://atlas.mitre.org/tactics/AML.TA0000) & [AML.T0024 Exfiltration via ML Inference API](https://atlas.mitre.org/techniques/AML.T0024) **MITRE ATLAS**
- [AML.T0029 - Denial of ML Service](https://atlas.mitre.org/techniques/AML.T0029) **MITRE ATLAS**
- [AML.T0034 - Cost Harvesting](https://atlas.mitre.org/techniques/AML.T0034) **MITRE ATLAS**
- [AML.T0025 - Exfiltration via Cyber Means](https://atlas.mitre.org/techniques/AML.T0025) **MITRE ATLAS**
- [OWASP Machine Learning Security Top Ten - ML05:2023 Model Theft](https://owasp.org/www-project-machine-learning-security-top-10/docs/ML05_2023-Model_Theft.html) **OWASP ML Top 10**
- [API4:2023 - Unrestricted Resource Consumption](https://owasp.org/API-Security/editions/2023/en/0xa4-unrestricted-resource-consumption/) **OWASP Web Application Top 10**
- [OWASP Resource Management](https://owasp.org/www-project-secure-coding-practices-quick-reference-guide/) **OWASP Secure Coding Practices**

