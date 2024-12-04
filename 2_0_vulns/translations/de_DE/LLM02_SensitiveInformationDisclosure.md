## LLM02:2025 Offenlegung sensibler Informationen

### Beschreibung

Sensible Informationen können sowohl das LLM als auch seinen Anwendungskontext betreffen. Dies umfasst personenbezogene Daten (PII), Finanzdaten, Gesundheitsakten, vertrauliche Geschäftsdaten, Sicherheitsanmeldeinformationen und rechtliche Dokumente. Proprietäre Modelle können auch einzigartige Trainingsmethoden und Quellcode enthalten, die als sensibel eingestuft werden, insbesondere bei geschlossenen oder Foundation Models.

LLMs, insbesondere wenn sie in Anwendungen eingebettet sind, riskieren die Offenlegung sensibler Daten, proprietärer Algorithmen oder vertraulicher Details durch ihre Ausgabe. Dies kann zu unberechtigtem Datenzugriff, Verletzungen der Privatsphäre und Verstößen gegen geistiges Eigentum führen. Anwender sollten wissen, wie sie sicher mit LLMs interagieren können. Sie müssen die Risiken verstehen, die mit der unbeabsichtigten Bereitstellung sensibler Daten verbunden sind, die später in der Ausgabe des Modells offengelegt werden könnten.

Um dieses Risiko zu reduzieren, sollten LLM-Anwendungen eine angemessene Datensanitisierung durchführen, um zu verhindern, dass Benutzerdaten in das Trainingsmodell gelangen. Anwendungsbesitzer sollten auch klare Nutzungsbedingungen bereitstellen, die es Benutzern ermöglichen, der Aufnahme ihrer Daten in das Trainingsmodell zu widersprechen. Das Hinzufügen von Einschränkungen innerhalb des System-Prompts bezüglich der Datentypen, die das LLM zurückgeben soll, kann eine Abschwächung gegen die Offenlegung sensibler Informationen bieten. Solche Einschränkungen werden jedoch möglicherweise nicht immer eingehalten und könnten durch Prompt Injection oder andere Methoden umgangen werden.

### Häufige Beispiele für Schwachstellen

#### 1. PII-Leakage
  Personenbezogene Daten (PII) können während der Interaktionen mit dem LLM offengelegt werden.
#### 2. Offenlegung proprietärer Algorithmen
  Schlecht konfigurierte Modellausgaben können proprietäre Algorithmen oder Daten offenlegen. Die Offenlegung von Trainingsdaten kann Modelle für Inversionsangriffe anfällig machen, bei denen Angreifer sensible Informationen extrahieren oder Eingaben rekonstruieren können. Zum Beispiel ermöglichte, wie im 'Proof Pudding'-Angriff (CVE-2019-20634) demonstriert, die Offenlegung von Trainingsdaten die Modellextraktion und -inversion, wodurch Angreifer Sicherheitskontrollen in Machine-Learning-Algorithmen umgehen und E-Mail-Filter umgehen konnten.
#### 3. Offenlegung sensibler Geschäftsdaten
  Generierte Antworten könnten unbeabsichtigt vertrauliche Geschäftsinformationen enthalten.

### Präventions- und Mitigationsstrategien

###@ Sanitisierung:

#### 1. Integration von Datensanitisierungstechniken
  Implementieren Sie Datensanitisierung, um zu verhindern, dass Benutzerdaten in das Trainingsmodell gelangen. Dies umfasst das Bereinigen oder Maskieren sensibler Inhalte vor deren Verwendung im Training.
#### 2. Robuste Eingabevalidierung
  Wenden Sie strenge Eingabevalidierungsmethoden an, um potenziell schädliche oder sensible Dateneingaben zu erkennen und zu filtern und sicherzustellen, dass sie das Modell nicht kompromittieren.

###@ Zugriffskontrolle:

#### 1. Durchsetzung strenger Zugriffskontrollen
  Beschränken Sie den Zugriff auf sensible Daten basierend auf dem Prinzip der geringsten Privilegien. Gewähren Sie nur Zugriff auf Daten, die für den spezifischen Benutzer oder Prozess notwendig sind.
#### 2. Einschränkung von Datenquellen
  Begrenzen Sie den Modellzugriff auf externe Datenquellen und stellen Sie sicher, dass die Laufzeit-Datenorchestrierung sicher verwaltet wird, um unbeabsichtigte Datenlecks zu vermeiden.

###@ Federated Learning und Datenschutztechniken:

#### 1. Nutzung von Federated Learning
  Trainieren Sie Modelle mit dezentralisierten Daten, die über mehrere Server oder Geräte verteilt sind. Dieser Ansatz minimiert die Notwendigkeit einer zentralisierten Datenerfassung und reduziert Expositionsrisiken.
#### 2. Integration von Differential Privacy
  Wenden Sie Techniken an, die den Daten oder Ausgaben Rauschen hinzufügen, wodurch es für Angreifer schwierig wird, einzelne Datenpunkte zurückzuverfolgen.

###@ Benutzeraufklärung und Transparenz:

#### 1. Benutzer über sichere LLM-Nutzung aufklären
  Bieten Sie Anleitungen zur Vermeidung der Eingabe sensibler Informationen. Bieten Sie Schulungen zu Best Practices für die sichere Interaktion mit LLMs an.
#### 2. Transparenz bei der Datennutzung sicherstellen
  Pflegen Sie klare Richtlinien zur Datenspeicherung, -nutzung und -löschung. Ermöglichen Sie Benutzern, der Aufnahme ihrer Daten in Trainingsprozesse zu widersprechen.

###@ Sichere Systemkonfiguration:

#### 1. System-Präambel verbergen
  Beschränken Sie die Möglichkeit für Benutzer, die ursprünglichen Systemeinstellungen zu überschreiben oder darauf zuzugreifen, um das Risiko einer Offenlegung interner Konfigurationen zu reduzieren.
#### 2. Best Practices für Sicherheitsfehlkonfigurationen beachten
  Befolgen Sie Richtlinien wie "OWASP API8:2023 Security Misconfiguration", um die Offenlegung sensibler Informationen durch Fehlermeldungen oder Konfigurationsdetails zu verhindern.
  (Ref. link:[OWASP API8:2023 Security Misconfiguration](https://owasp.org/API-Security/editions/2023/en/0xa8-security-misconfiguration/))

###@ Fortgeschrittene Techniken:

#### 1. Homomorphe Verschlüsselung
  Verwenden Sie homomorphe Verschlüsselung, um sichere Datenanalyse und datenschutzfreundliches maschinelles Lernen zu ermöglichen. Dies stellt sicher, dass Daten während der Verarbeitung durch das Modell vertraulich bleiben.
#### 2. Tokenisierung und Redaktierung
  Implementieren Sie Tokenisierung zur Vorverarbeitung und Sanitisierung sensibler Informationen. Techniken wie Pattern Matching können vertrauliche Inhalte vor der Verarbeitung erkennen und redigieren.

### Beispiel-Angriffsszenarien

#### Szenario #1: Unbeabsichtigte Datenoffenlegung
  Ein Benutzer erhält eine Antwort, die die persönlichen Daten eines anderen Benutzers enthält, aufgrund unzureichender Datensanitisierung.
#### Szenario #2: Gezielte Prompt Injection
  Ein Angreifer umgeht Eingabefilter, um sensible Informationen zu extrahieren.
#### Szenario #3: Datenleck über Trainingsdaten
  Nachlässige Dateneinbindung im Training führt zur Offenlegung sensibler Informationen.

### Referenzlinks

1. [Lessons learned from ChatGPT's Samsung leak](https://cybernews.com/security/chatgpt-samsung-leak-explained-lessons/): **Cybernews**
2. [AI data leak crisis: New tool prevents company secrets from being fed to ChatGPT](https://www.foxbusiness.com/politics/ai-data-leak-crisis-prevent-company-secrets-chatgpt): **Fox Business**
3. [ChatGPT Spit Out Sensitive Data When Told to Repeat 'Poem' Forever](https://www.wired.com/story/chatgpt-poem-forever-security-roundup/): **Wired**
4. [Using Differential Privacy to Build Secure Models](https://neptune.ai/blog/using-differential-privacy-to-build-secure-models-tools-methods-best-practices): **Neptune Blog**
5. [Proof Pudding (CVE-2019-20634)](https://avidml.org/database/avid-2023-v009/) **AVID** (`moohax` & `monoxgas`)

### Verwandte Frameworks und Taxonomien

Weitere umfassende Informationen, Szenarien und Strategien zu Infrastruktur-Deployment, angewandten Umgebungskontrollen und anderen Best Practices finden Sie in diesem Abschnitt.

- [AML.T0024.000 - Infer Training Data Membership](https://atlas.mitre.org/techniques/AML.T0024.000) **MITRE ATLAS**
- [AML.T0024.001 - Invert ML Model](https://atlas.mitre.org/techniques/AML.T0024.001) **MITRE ATLAS**
- [AML.T0024.002 - Extract ML Model](https://atlas.mitre.org/techniques/AML.T0024.002) **MITRE ATLAS**

