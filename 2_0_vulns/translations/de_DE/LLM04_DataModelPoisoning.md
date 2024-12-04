## LLM04: Daten- und Modellvergiftung

### Beschreibung

Data Poisoning tritt auf, wenn Daten für das Pre-Training, Fine-Tuning oder Embeddings manipuliert werden, um Schwachstellen, Backdoors oder Verzerrungen einzuführen. Diese Manipulation kann die Modellsicherheit, Leistung oder ethisches Verhalten kompromittieren und zu schädlichen Ausgaben oder beeinträchtigten Fähigkeiten führen. Zu den häufigen Risiken gehören verschlechterte Modellleistung, verzerrte oder toxische Inhalte und die Ausnutzung nachgelagerter Systeme.

Data Poisoning kann verschiedene Phasen des LLM-Lebenszyklus betreffen, einschließlich Pre-Training (Lernen aus allgemeinen Daten), Fine-Tuning (Anpassung von Modellen an spezifische Aufgaben) und Embedding (Umwandlung von Text in numerische Vektoren). Das Verständnis dieser Phasen hilft dabei, potenzielle Schwachstellen zu identifizieren. Data Poisoning wird als Integritätsangriff betrachtet, da die Manipulation von Trainingsdaten die Fähigkeit des Modells zu präzisen Vorhersagen beeinträchtigt. Die Risiken sind besonders hoch bei externen Datenquellen, die nicht verifizierte oder schädliche Inhalte enthalten können.

Darüber hinaus können Modelle, die über geteilte Repositories oder Open-Source-Plattformen verteilt werden, über das Data Poisoning hinausgehende Risiken bergen, wie etwa Malware, die durch Techniken wie Malicious Pickling eingebettet wird und bei Laden des Modells schädlichen Code ausführen kann. Beachten Sie auch, dass Poisoning die Implementierung einer Backdoor ermöglichen kann. Solche Backdoors können das Verhalten des Modells unverändert lassen, bis ein bestimmter Trigger eine Änderung bewirkt. Dies kann solche Änderungen schwer zu testen und zu erkennen machen und effektiv die Möglichkeit schaffen, dass ein Modell zu einem Sleeper Agent wird.

### Häufige Beispiele für Schwachstellen

1. Böswillige Akteure führen während des Trainings schädliche Daten ein, die zu verzerrten Ausgaben führen. Techniken wie "Split-View Data Poisoning" oder "Frontrunning Poisoning" nutzen die Dynamik des Modelltrainings aus.
  (Ref. link: [Split-View Data Poisoning](https://github.com/GangGreenTemperTatum/speaking/blob/main/dc604/hacker-summer-camp-23/Ads%20_%20Poisoning%20Web%20Training%20Datasets%20_%20Flow%20Diagram%20-%20Exploit%201%20Split-View%20Data%20Poisoning.jpeg))
  (Ref. link: [Frontrunning Poisoning](https://github.com/GangGreenTemperTatum/speaking/blob/main/dc604/hacker-summer-camp-23/Ads%20_%20Poisoning%20Web%20Training%20Datasets%20_%20Flow%20Diagram%20-%20Exploit%202%20Frontrunning%20Data%20Poisoning.jpeg))
2. Angreifer können schädliche Inhalte direkt in den Trainingsprozess einschleusen und die Ausgabequalität des Modells kompromittieren.
3. Benutzer fügen unwissentlich sensible oder proprietäre Informationen während der Interaktionen ein, die in nachfolgenden Ausgaben exponiert werden könnten.
4. Nicht verifizierte Trainingsdaten erhöhen das Risiko von verzerrten oder fehlerhaften Ausgaben.
5. Fehlende Ressourcenzugriffsbeschränkungen können die Aufnahme unsicherer Daten ermöglichen, was zu verzerrten Ausgaben führt.

### Präventions- und Mitigationsstrategien

1. Verfolgen Sie Datenursprünge und -transformationen mit Tools wie OWASP CycloneDX oder ML-BOM. Verifizieren Sie die Datenlegitimität während aller Modellentwicklungsphasen.
2. Überprüfen Sie Datenanbieter gründlich und validieren Sie Modellausgaben gegen vertrauenswürdige Quellen, um Anzeichen von Poisoning zu erkennen.
3. Implementieren Sie striktes Sandboxing, um die Modellexposition gegenüber nicht verifizierten Datenquellen zu begrenzen. Nutzen Sie Anomalie-Erkennungstechniken, um schädliche Daten herauszufiltern.
4. Passen Sie Modelle für verschiedene Anwendungsfälle durch spezifische Datensätze beim Fine-Tuning an. Dies hilft, genauere Ausgaben basierend auf definierten Zielen zu produzieren.
5. Stellen Sie ausreichende Infrastrukturkontrollen sicher, um zu verhindern, dass das Modell auf unbeabsichtigte Datenquellen zugreift.
6. Verwenden Sie Data Version Control (DVC), um Änderungen in Datensätzen zu verfolgen und Manipulationen zu erkennen. Versionierung ist entscheidend für die Aufrechterhaltung der Modellintegrität.
7. Speichern Sie von Benutzern bereitgestellte Informationen in einer Vektordatenbank, die Anpassungen ohne erneutes Training des gesamten Modells ermöglicht.
8. Testen Sie die Modellrobustheit mit Red-Team-Kampagnen und adversarialen Techniken wie Federated Learning, um die Auswirkungen von Datenperturbationen zu minimieren.
9. Überwachen Sie den Trainingsverlust und analysieren Sie das Modellverhalten auf Anzeichen von Poisoning. Verwenden Sie Schwellenwerte, um anomale Ausgaben zu erkennen.
10. Integrieren Sie während der Inferenz Retrieval-Augmented Generation (RAG) und Grounding-Techniken, um die Risiken von Halluzinationen zu reduzieren.

### Beispiel-Angriffsszenarien

#### Szenario #1
Ein Angreifer verzerrt die Modellausgaben durch Manipulation von Trainingsdaten oder durch Verwendung von Prompt-Injection-Techniken und verbreitet dadurch Fehlinformationen.

#### Szenario #2
Toxische Daten ohne angemessene Filterung können zu schädlichen oder verzerrten Ausgaben führen und gefährliche Informationen verbreiten.

#### Szenario #3
Ein böswilliger Akteur oder Konkurrent erstellt gefälschte Dokumente für das Training, was zu Modellausgaben führt, die diese Ungenauigkeiten widerspiegeln.

#### Szenario #4
Unzureichende Filterung ermöglicht es einem Angreifer, irreführende Daten über Prompt Injection einzufügen, was zu kompromittierten Ausgaben führt.

#### Szenario #5
Ein Angreifer verwendet Poisoning-Techniken, um einen Backdoor-Trigger in das Modell einzufügen. Dies könnte zu Authentifizierungsumgehung, Datenexfiltration oder versteckter Befehlsausführung führen.

### Referenz-Links

1. [How data poisoning attacks corrupt machine learning models](https://www.csoonline.com/article/3613932/how-data-poisoning-attacks-corrupt-machine-learning-models.html): **CSO Online**
2. [MITRE ATLAS (framework) Tay Poisoning](https://atlas.mitre.org/studies/AML.CS0009/): **MITRE ATLAS**
3. [PoisonGPT: How we hid a lobotomized LLM on Hugging Face to spread fake news](https://blog.mithrilsecurity.io/poisongpt-how-we-hid-a-lobotomized-llm-on-hugging-face-to-spread-fake-news/): **Mithril Security**
4. [Poisoning Language Models During Instruction](https://arxiv.org/abs/2305.00944): **Arxiv White Paper 2305.00944**
5. [Poisoning Web-Scale Training Datasets - Nicholas Carlini | Stanford MLSys #75](https://www.youtube.com/watch?v=h9jf1ikcGyk): **Stanford MLSys Seminars YouTube Video**
6. [ML Model Repositories: The Next Big Supply Chain Attack Target](https://www.darkreading.com/cloud-security/ml-model-repositories-next-big-supply-chain-attack-target) **OffSecML**
7. [Data Scientists Targeted by Malicious Hugging Face ML Models with Silent Backdoor](https://jfrog.com/blog/data-scientists-targeted-by-malicious-hugging-face-ml-models-with-silent-backdoor/) **JFrog**
8. [Backdoor Attacks on Language Models](https://towardsdatascience.com/backdoor-attacks-on-language-models-can-we-trust-our-models-weights-73108f9dcb1f): **Towards Data Science**
9. [Never a dill moment: Exploiting machine learning pickle files](https://blog.trailofbits.com/2021/03/15/never-a-dill-moment-exploiting-machine-learning-pickle-files/) **TrailofBits**
10. [arXiv:2401.05566 Sleeper Agents: Training Deceptive LLMs that Persist Through Safety Training](https://www.anthropic.com/news/sleeper-agents-training-deceptive-llms-that-persist-through-safety-training) **Anthropic (arXiv)**
11. [Backdoor Attacks on AI Models](https://www.cobalt.io/blog/backdoor-attacks-on-ai-models) **Cobalt**

### Verwandte Frameworks und Taxonomien

Siehe diesen Abschnitt für umfassende Informationen, Szenarien und Strategien zu Infrastrukturbereitstellung, angewandten Umgebungskontrollen und anderen Best Practices.

- [AML.T0018 | Backdoor ML Model](https://atlas.mitre.org/techniques/AML.T0018) **MITRE ATLAS**
- [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework): Strategien zur Gewährleistung der KI-Integrität. **NIST**

