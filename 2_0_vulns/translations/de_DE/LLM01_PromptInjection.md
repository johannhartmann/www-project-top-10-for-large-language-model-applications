## LLM01:2025 Prompt Injection

### Beschreibung

Eine Prompt Injection Schwachstelle tritt auf, wenn Benutzereingaben das Verhalten oder die Ausgabe des LLM in unbeabsichtigter Weise verändern. Diese Eingaben können das Modell beeinflussen, auch wenn sie für Menschen nicht wahrnehmbar sind. Daher müssen Prompt Injections nicht für Menschen sichtbar/lesbar sein, solange der Inhalt vom Modell verarbeitet wird.

Prompt Injection Schwachstellen existieren in der Art und Weise, wie Modelle Prompts verarbeiten und wie Eingaben das Modell dazu bringen können, Prompt-Daten fälschlicherweise an andere Teile des Modells weiterzuleiten. Dies kann dazu führen, dass Richtlinien verletzt, schädliche Inhalte generiert, unberechtigter Zugriff ermöglicht oder kritische Entscheidungen beeinflusst werden. Während Techniken wie Retrieval Augmented Generation (RAG) und Fine-Tuning darauf abzielen, LLM-Ausgaben relevanter und präziser zu machen, zeigt die Forschung, dass sie Prompt Injection Schwachstellen nicht vollständig mindern können.

Während Prompt Injection und Jailbreaking verwandte Konzepte in der LLM-Sicherheit sind, werden sie oft synonym verwendet. Prompt Injection beinhaltet die Manipulation von Modellantworten durch spezifische Eingaben, um dessen Verhalten zu ändern, was auch das Umgehen von Sicherheitsmaßnahmen einschließen kann. Jailbreaking ist eine Form der Prompt Injection, bei der der Angreifer Eingaben bereitstellt, die dazu führen, dass das Modell seine Sicherheitsprotokolle vollständig missachtet. Entwickler können Schutzmaßnahmen in System-Prompts und die Eingabeverarbeitung einbauen, um Prompt Injection Angriffe abzuschwächen. Eine effektive Prävention von Jailbreaking erfordert jedoch kontinuierliche Aktualisierungen des Trainings und der Sicherheitsmechanismen des Modells.

### Arten von Prompt Injection Schwachstellen

#### Direkte Prompt Injections
  Direkte Prompt Injections treten auf, wenn die Prompt-Eingabe eines Benutzers das Verhalten des Modells direkt in unbeabsichtigter oder unerwarteter Weise verändert. Die Eingabe kann entweder absichtlich (d.h. ein böswilliger Akteur erstellt gezielt einen Prompt, um das Modell auszunutzen) oder unbeabsichtigt (d.h. ein Benutzer stellt versehentlich eine Eingabe bereit, die unerwartetes Verhalten auslöst) erfolgen.

#### Indirekte Prompt Injections
  Indirekte Prompt Injections treten auf, wenn ein LLM Eingaben aus externen Quellen wie Websites oder Dateien akzeptiert. Der Inhalt in den externen Daten kann, wenn er vom Modell interpretiert wird, das Verhalten des Modells in unbeabsichtigter oder unerwarteter Weise verändern. Wie direkte Injections können auch indirekte Injections absichtlich oder unbeabsichtigt sein.

Die Schwere und Art der Auswirkungen eines erfolgreichen Prompt Injection Angriffs kann stark variieren und hängt weitgehend sowohl vom geschäftlichen Kontext, in dem das Modell operiert, als auch von der Agency ab, mit der das Modell entwickelt wurde. Im Allgemeinen kann Prompt Injection jedoch zu unbeabsichtigten Ergebnissen führen, einschließlich, aber nicht beschränkt auf:

- Offenlegung sensibler Informationen
- Preisgabe sensibler Informationen über die AI-Systeminfrastruktur oder System-Prompts
- Manipulation von Inhalten, die zu falschen oder verzerrten Ausgaben führt
- Gewährung unberechtigten Zugriffs auf dem LLM zur Verfügung stehende Funktionen
- Ausführung beliebiger Befehle in verbundenen Systemen
- Manipulation kritischer Entscheidungsprozesse

Der Aufstieg multimodaler KI, die mehrere Datentypen gleichzeitig verarbeitet, führt zu einzigartigen Prompt Injection Risiken ein. Böswillige Akteure könnten Interaktionen zwischen Modalitäten ausnutzen, wie zum Beispiel das Verstecken von Anweisungen in Bildern, die harmlosen Text begleiten. Die Komplexität dieser Systeme erweitert die Angriffsfläche. Multimodale Modelle können auch anfällig für neuartige Cross-Modal-Angriffe sein, die mit aktuellen Techniken schwer zu erkennen und zu mindern sind. Robuste multimodal-spezifische Verteidigungsmechanismen sind ein wichtiger Bereich für weitere Forschung und Entwicklung.

### Präventions- und Mitigationsstrategien

Prompt Injection Schwachstellen sind aufgrund der Natur der generativen KI möglich. Angesichts des stochastischen Einflusses im Kern der Funktionsweise von Modellen ist unklar, ob es absolut sichere Methoden zur Prävention von Prompt Injection gibt. Die folgenden Maßnahmen können jedoch die Auswirkungen von Prompt Injections abschwächen:

#### 1. Modellverhalten einschränken
  Stellen Sie spezifische Anweisungen über die Rolle, Fähigkeiten und Einschränkungen des Modells innerhalb des System-Prompts bereit. Erzwingen Sie strikte Kontexteinschränkungen, begrenzen Sie Antworten auf spezifische Aufgaben oder Themen und weisen Sie das Modell an, Versuche zur Änderung der Kernanweisungen zu ignorieren.
#### 2. Erwartete Ausgabeformate definieren und validieren
  Spezifizieren Sie klare Ausgabeformate, fordern Sie detaillierte Begründungen und Quellenangaben an und verwenden Sie deterministische Code zur Validierung der Einhaltung dieser Formate.
#### 3. Eingabe- und Ausgabefilterung implementieren
  Definieren Sie sensible Kategorien und erstellen Sie Regeln zur Identifizierung und Behandlung solcher Inhalte. Wenden Sie semantische Filter an und verwenden Sie String-Überprüfung zum Scannen nach nicht erlaubten Inhalten. Bewerten Sie Antworten mit der RAG-Triade: Bewerten Sie Kontextrelevanz, Grundierung und Frage/Antwort-Relevanz, um potenziell bösartige Ausgaben zu identifizieren.
#### 4. Berechtigungskontrolle und Prinzip der geringsten Privilegien durchsetzen
  Stellen Sie der Anwendung eigene API-Tokens für erweiterbare Funktionalität zur Verfügung und behandeln Sie diese Funktionen im Code, anstatt sie dem Modell zur Verfügung zu stellen. Beschränken Sie die Zugriffsrechte des Modells auf das für die beabsichtigten Operationen notwendige Minimum.
#### 5. Menschliche Genehmigung für Hochrisiko-Aktionen erforderlich machen
  Implementieren Sie Human-in-the-Loop-Kontrollen für privilegierte Operationen, um unberechtigte Aktionen zu verhindern.
#### 6. Externe Inhalte trennen und identifizieren
  Trennen und kennzeichnen Sie nicht vertrauenswürdige Inhalte deutlich, um ihren Einfluss auf Benutzer-Prompts zu begrenzen.
#### 7. Gegnerisches Testen und Angriffssimulationen durchführen
  Führen Sie regelmäßige Penetrationstests und Breach-Simulationen durch, behandeln Sie das Modell als nicht vertrauenswürdigen Benutzer, um die Effektivität von Vertrauensgrenzen und Zugriffskontrolle zu testen.

### Beispiel-Angriffsszenarien

#### Szenario #1: Direkte Injection
  Ein Angreifer injiziert einen Prompt in einen Kundenservice-Chatbot und weist ihn an, vorherige Richtlinien zu ignorieren, private Datenspeicher abzufragen und E-Mails zu versenden, was zu unberechtigtem Zugriff und Rechteausweitung führt.
#### Szenario #2: Indirekte Injection
  Ein Benutzer verwendet ein LLM zur Zusammenfassung einer Webseite, die versteckte Anweisungen enthält, die das LLM dazu veranlassen, ein Bild mit einem URL-Link einzufügen, was zur Exfiltration der privaten Konversation führt.
#### Szenario #3: Unbeabsichtigte Injection
  Ein Unternehmen fügt einer Stellenbeschreibung eine Anweisung hinzu, KI-generierte Bewerbungen zu identifizieren. Ein Bewerber, der sich dieser Anweisung nicht bewusst ist, verwendet ein LLM zur Optimierung seines Lebenslaufs und löst unbeabsichtigt die KI-Erkennung aus.
#### Szenario #4: Beabsichtigte Modellbeeinflussung
  Ein Angreifer modifiziert ein Dokument in einem Repository, das von einer Retrieval-Augmented Generation (RAG) Anwendung verwendet wird. Wenn die Abfrage eines Benutzers den modifizierten Inhalt zurückgibt, verändern die bösartigen Anweisungen die LLM-Ausgabe und erzeugen irreführende Ergebnisse.
#### Szenario #5: Code Injection
  Ein Angreifer nutzt eine Schwachstelle (CVE-2024-5184) in einem LLM-gestützten E-Mail-Assistenten aus, um bösartige Prompts zu injizieren, die Zugriff auf sensible Informationen und Manipulation von E-Mail-Inhalten ermöglichen.
#### Szenario #6: Payload-Splitting
  Ein Angreifer lädt einen Lebenslauf mit aufgeteilten bösartigen Prompts hoch. Wenn ein LLM zur Bewertung des Kandidaten verwendet wird, manipulieren die kombinierten Prompts die Modellantwort und führen zu einer positiven Empfehlung trotz des tatsächlichen Lebenslaufinhalts.
#### Szenario #7: Multimodale Injection
  Ein Angreifer bettet einen bösartigen Prompt in ein Bild ein, das harmlosen Text begleitet. Wenn eine multimodale KI das Bild und den Text gleichzeitig verarbeitet, verändert der versteckte Prompt das Verhalten des Modells, was möglicherweise zu unberechtigten Aktionen oder der Offenlegung sensibler Informationen führt.
#### Szenario #8: Adversarial Suffix
  Ein Angreifer fügt einem Prompt eine scheinbar bedeutungslose Zeichenkette hinzu, die die LLM-Ausgabe in bösartiger Weise beeinflusst und Sicherheitsmaßnahmen umgeht.
#### Szenario #9: Mehrsprachiger/Verschleierter Angriff
  Ein Angreifer verwendet mehrere Sprachen oder codiert bösartige Anweisungen (z.B. mit Base64 oder Emojis), um Filter zu umgehen und das Verhalten des LLM zu manipulieren.


### Referenzlinks

1. [ChatGPT Plugin Vulnerabilities - Chat with Code](https://embracethered.com/blog/posts/2023/chatgpt-plugin-vulns-chat-with-code/) **Embrace the Red**
2. [ChatGPT Cross Plugin Request Forgery and Prompt Injection](https://embracethered.com/blog/posts/2023/chatgpt-cross-plugin-request-forgery-and-prompt-injection./) **Embrace the Red**
3. [Not what you've signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection](https://arxiv.org/pdf/2302.12173.pdf) **Arxiv**
4. [Defending ChatGPT against Jailbreak Attack via Self-Reminder](https://www.researchsquare.com/article/rs-2873090/v1) **Research Square**
5. [Prompt Injection attack against LLM-integrated Applications](https://arxiv.org/abs/2306.05499) **Cornell University**
6. [Inject My PDF: Prompt Injection for your Resume](https://kai-greshake.de/posts/inject-my-pdf) **Kai Greshake**
8. [Not what you've signed up for: Compromising Real-World LLM-Integrated Applications with Indirect Prompt Injection](https://arxiv.org/pdf/2302.12173.pdf) **Cornell University**
9. [Threat Modeling LLM Applications](https://aivillage.org/large%20language%20models/threat-modeling-llm/) **AI Village**
10. [Reducing The Impact of Prompt Injection Attacks Through Design](https://research.kudelskisecurity.com/2023/05/25/reducing-the-impact-of-prompt-injection-attacks-through-design/) **Kudelski Security**
11. [Adversarial Machine Learning: A Taxonomy and Terminology of Attacks and Mitigations (nist.gov)](https://nvlpubs.nist.gov/nistpubs/ai/NIST.AI.100-2e2023.pdf)
12. [2407.07403 A Survey of Attacks on Large Vision-Language Models: Resources, Advances, and Future Trends (arxiv.org)](https://arxiv.org/abs/2407.07403)
13. [Exploiting Programmatic Behavior of LLMs: Dual-Use Through Standard Security Attacks](https://ieeexplore.ieee.org/document/10579515)
14. [Universal and Transferable Adversarial Attacks on Aligned Language Models (arxiv.org)](https://arxiv.org/abs/2307.15043)
15. [From ChatGPT to ThreatGPT: Impact of Generative AI in Cybersecurity and Privacy (arxiv.org)](https://arxiv.org/abs/2307.00691)

### Verwandte Frameworks und Taxonomien

Weitere umfassende Informationen, Szenarien und Strategien zu Infrastruktur-Deployment, angewandten Umgebungskontrollen und anderen Best Practices finden Sie in diesem Abschnitt.

- [AML.T0051.000 - LLM Prompt Injection: Direct](https://atlas.mitre.org/techniques/AML.T0051.000) **MITRE ATLAS**
- [AML.T0051.001 - LLM Prompt Injection: Indirect](https://atlas.mitre.org/techniques/AML.T0051.001) **MITRE ATLAS**
- [AML.T0054 - LLM Jailbreak Injection: Direct](https://atlas.mitre.org/techniques/AML.T0054) **MITRE ATLAS**

