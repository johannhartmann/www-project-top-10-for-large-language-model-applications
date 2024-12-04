## LLM07:2025 System Prompt Leakage

### Beschreibung

Die System Prompt Leakage-Schwachstelle in LLMs bezieht sich auf das Risiko, dass die System-Prompts oder Anweisungen, die zur Steuerung des Modellverhaltens verwendet werden, auch sensible Informationen enthalten können, die nicht entdeckt werden sollten. System-Prompts sind darauf ausgelegt, die Ausgabe des Modells basierend auf den Anforderungen der Anwendung zu steuern, können aber unbeabsichtigt Geheimnisse enthalten. Wenn diese Informationen entdeckt werden, können sie für weitere Angriffe genutzt werden.

Es ist wichtig zu verstehen, dass der System-Prompt nicht als Geheimnis betrachtet werden sollte und auch nicht als Sicherheitskontrolle verwendet werden sollte. Dementsprechend sollten keine sensiblen Daten wie Zugangsdaten, Verbindungszeichenfolgen usw. in der Sprache des System-Prompts enthalten sein.

Wenn ein System-Prompt Informationen über verschiedene Rollen und Berechtigungen oder sensible Daten wie Verbindungszeichenfolgen oder Passwörter enthält, liegt das grundlegende Sicherheitsrisiko nicht in deren Offenlegung, sondern darin, dass die Anwendung die Umgehung von starkem Session-Management und Autorisierungsprüfungen durch Delegierung an das LLM ermöglicht und dass sensible Daten an einer Stelle gespeichert werden, an der sie nicht sein sollten.

Kurz gesagt: Die Offenlegung des System-Prompts selbst stellt nicht das eigentliche Risiko dar - das Sicherheitsrisiko liegt bei den zugrundeliegenden Elementen, sei es die Offenlegung sensibler Informationen, die Umgehung von System-Guardrails, unangemessene Trennung von Privilegien usw. Selbst wenn der genaue Wortlaut nicht offengelegt wird, werden Angreifer, die mit dem System interagieren, fast sicher viele der Guardrails und Formatierungseinschränkungen bestimmen können, die in der System-Prompt-Sprache vorhanden sind, indem sie die Anwendung nutzen, Äußerungen an das Modell senden und die Ergebnisse beobachten.

### Häufige Beispiele für Risiken

#### 1. Offenlegung sensibler Funktionalität
Der System-Prompt der Anwendung kann sensible Informationen oder Funktionalitäten offenlegen, die vertraulich bleiben sollen, wie zum Beispiel sensible Systemarchitektur, API-Schlüssel, Datenbank-Zugangsdaten oder Benutzer-Tokens. Diese können von Angreifern extrahiert oder verwendet werden, um unbefugten Zugriff auf die Anwendung zu erhalten. Zum Beispiel könnte ein System-Prompt, der den verwendeten Datenbanktyp eines Tools enthält, dem Angreifer ermöglichen, diesen für SQL-Injection-Angriffe zu nutzen.

#### 2. Offenlegung interner Regeln
Der System-Prompt der Anwendung offenbart Informationen über interne Entscheidungsprozesse, die vertraulich bleiben sollten. Diese Informationen ermöglichen es Angreifern, Einblicke in die Funktionsweise der Anwendung zu gewinnen, was es ihnen ermöglichen könnte, Schwachstellen auszunutzen oder Kontrollen in der Anwendung zu umgehen. Zum Beispiel - Es gibt eine Banking-Anwendung mit einem Chatbot, deren System-Prompt Informationen wie 
  >"Das Transaktionslimit ist auf $5000 pro Tag für einen Benutzer festgelegt. Der Gesamtkreditbetrag für einen Benutzer beträgt $10.000" 
enthält.

#### 3. Offenlegung von Filterkriterien
Ein System-Prompt könnte das Modell auffordern, sensible Inhalte zu filtern oder abzulehnen. Zum Beispiel könnte ein Modell einen System-Prompt haben wie
  >"Wenn ein Benutzer Informationen über einen anderen Benutzer anfordert, antworte immer mit 'Tut mir leid, ich kann bei dieser Anfrage nicht helfen'".

#### 4. Offenlegung von Berechtigungen und Benutzerrollen
Der System-Prompt könnte die internen Rollenstrukturen oder Berechtigungsstufen der Anwendung offenlegen. Zum Beispiel könnte ein System-Prompt offenbaren:
  >"Die Admin-Benutzerrolle gewährt vollen Zugriff auf die Änderung von Benutzerdatensätzen."
Wenn die Angreifer von diesen rollenbasierten Berechtigungen erfahren, könnten sie nach einer Möglichkeit zur Privilegien-Eskalation suchen.

### Präventions- und Mitigationsstrategien

#### 1. Trennung sensibler Daten von System-Prompts
Vermeiden Sie die direkte Einbettung sensibler Informationen (z.B. API-Schlüssel, Auth-Keys, Datenbanknamen, Benutzerrollen, Berechtigungsstruktur der Anwendung) in die System-Prompts. Stattdessen sollten solche Informationen in Systeme ausgelagert werden, auf die das Modell keinen direkten Zugriff hat.

#### 2. Vermeidung der Abhängigkeit von System-Prompts für strikte Verhaltenskontrolle
Da LLMs anfällig für andere Angriffe wie Prompt-Injections sind, die den System-Prompt verändern können, wird empfohlen, System-Prompts wenn möglich nicht zur Kontrolle des Modellverhaltens zu verwenden. Stattdessen sollten Sie sich auf Systeme außerhalb des LLM verlassen, um dieses Verhalten sicherzustellen. Zum Beispiel sollte die Erkennung und Verhinderung schädlicher Inhalte in externen Systemen erfolgen.

#### 3. Implementierung von Guardrails
Implementieren Sie ein System von Guardrails außerhalb des LLM selbst. Während das Training bestimmter Verhaltensweisen in ein Modell effektiv sein kann, wie zum Beispiel das Training, seinen System-Prompt nicht preiszugeben, ist dies keine Garantie dafür, dass das Modell sich immer daran halten wird. Ein unabhängiges System, das die Ausgabe überprüfen kann, um festzustellen, ob das Modell den Erwartungen entspricht, ist System-Prompt-Anweisungen vorzuziehen.

#### 4. Sicherstellung der unabhängigen Durchsetzung von Sicherheitskontrollen vom LLM
Kritische Kontrollen wie Privilegientrennung, Autorisierungsprüfungen und ähnliches dürfen nicht an das LLM delegiert werden, weder durch den System-Prompt noch anderweitig. Diese Kontrollen müssen auf deterministische, überprüfbare Weise erfolgen, und LLMs sind dafür (derzeit) nicht geeignet. In Fällen, in denen ein Agent Aufgaben ausführt, die unterschiedliche Zugriffsebenen erfordern, sollten mehrere Agenten verwendet werden, die jeweils mit den geringsten Privilegien konfiguriert sind, die zur Ausführung der gewünschten Aufgaben erforderlich sind.

### Beispiel-Angriffsszenarien

#### Szenario #1
Ein LLM hat einen System-Prompt, der einen Satz von Zugangsdaten für ein Tool enthält, auf das es Zugriff erhalten hat. Der System-Prompt wird einem Angreifer zugespielt, der diese Zugangsdaten dann für andere Zwecke nutzen kann.

#### Szenario #2
Ein LLM hat einen System-Prompt, der die Generierung von anstößigen Inhalten, externen Links und Code-Ausführung verbietet. Ein Angreifer extrahiert diesen System-Prompt und verwendet dann einen Prompt-Injection-Angriff, um diese Anweisungen zu umgehen und ermöglicht damit einen Remote Code Execution-Angriff.

### Referenz-Links

1. [SYSTEM PROMPT LEAK](https://x.com/elder_plinius/status/1801393358964994062): Pliny the prompter
2. [Prompt Leak](https://www.prompt.security/vulnerabilities/prompt-leak): Prompt Security
3. [chatgpt_system_prompt](https://github.com/LouisShark/chatgpt_system_prompt): LouisShark
4. [leaked-system-prompts](https://github.com/jujumilk3/leaked-system-prompts): Jujumilk3
5. [OpenAI Advanced Voice Mode System Prompt](https://x.com/Green_terminals/status/1839141326329360579): Green_Terminals

### Verwandte Frameworks und Taxonomien

Siehe diesen Abschnitt für umfassende Informationen, Szenarien und Strategien zur Infrastrukturbereitstellung, angewandten Umgebungskontrollen und anderen Best Practices.

- [AML.T0051.000 - LLM Prompt Injection: Direct (Meta Prompt Extraction)](https://atlas.mitre.org/techniques/AML.T0051.000) **MITRE ATLAS**

