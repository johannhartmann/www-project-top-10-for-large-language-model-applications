## LLM05:2025 Unsachgemäße Ausgabebehandlung

### Beschreibung

Unsachgemäße Ausgabebehandlung bezieht sich speziell auf unzureichende Validierung, Bereinigung und Verarbeitung der von Large Language Models generierten Ausgaben, bevor diese an nachgelagerte Komponenten und Systeme weitergegeben werden. Da LLM-generierte Inhalte durch Prompt-Eingaben gesteuert werden können, ähnelt dieses Verhalten der indirekten Gewährung von Benutzerzugriff auf zusätzliche Funktionalitäten.

Unsachgemäße Ausgabebehandlung unterscheidet sich von Overreliance dadurch, dass sie sich mit LLM-generierten Ausgaben befasst, bevor diese weitergeleitet werden, während sich Overreliance auf breitere Bedenken hinsichtlich der übermäßigen Abhängigkeit von der Genauigkeit und Angemessenheit von LLM-Ausgaben konzentriert.

Eine erfolgreiche Ausnutzung einer Schwachstelle bei der Ausgabebehandlung kann zu XSS und CSRF in Webbrowsern sowie zu SSRF, Privilege Escalation oder Remote Code Execution auf Backend-Systemen führen.

Die folgenden Bedingungen können die Auswirkungen dieser Schwachstelle verstärken:
- Die Anwendung gewährt dem LLM Privilegien über das für Endbenutzer vorgesehene Maß hinaus und ermöglicht Privilege Escalation oder Remote Code Execution.
- Die Anwendung ist anfällig für indirekte Prompt-Injection-Angriffe, die einem Angreifer privilegierten Zugriff auf die Umgebung eines Zielbenutzers ermöglichen könnten.
- Drittanbieter-Erweiterungen validieren Eingaben nicht ausreichend.
- Fehlende korrekte Ausgabecodierung für verschiedene Kontexte (z.B. HTML, JavaScript, SQL)
- Unzureichende Überwachung und Protokollierung von LLM-Ausgaben
- Fehlen von Rate Limiting oder Anomalieerkennung für LLM-Nutzung

### Häufige Beispiele für Schwachstellen

1. LLM-Ausgabe wird direkt in eine System-Shell oder ähnliche Funktionen wie exec oder eval eingegeben, was zu Remote Code Execution führt.
2. JavaScript oder Markdown wird vom LLM generiert und an einen Benutzer zurückgegeben. Der Code wird dann vom Browser interpretiert, was zu XSS führt.
3. LLM-generierte SQL-Abfragen werden ohne ordnungsgemäße Parametrisierung ausgeführt, was zu SQL-Injection führt.
4. LLM-Ausgabe wird zur Konstruktion von Dateipfaden ohne ordnungsgemäße Bereinigung verwendet, was potenziell zu Path Traversal-Schwachstellen führt.
5. LLM-generierte Inhalte werden in E-Mail-Templates ohne ordnungsgemäßes Escaping verwendet, was potenziell zu Phishing-Angriffen führt.

### Präventions- und Mitigationsstrategien

1. Behandeln Sie das Modell wie jeden anderen Benutzer, übernehmen Sie einen Zero-Trust-Ansatz und wenden Sie eine ordnungsgemäße Eingabevalidierung auf Antworten an, die vom Modell an Backend-Funktionen gesendet werden.
2. Befolgen Sie die OWASP ASVS (Application Security Verification Standard) Richtlinien, um eine effektive Eingabevalidierung und -bereinigung sicherzustellen.
3. Codieren Sie die Modellausgabe für Benutzer, um unerwünschte Codeausführung durch JavaScript oder Markdown zu verhindern. OWASP ASVS bietet detaillierte Anleitungen zur Ausgabecodierung.
4. Implementieren Sie kontextbezogene Ausgabecodierung basierend darauf, wo die LLM-Ausgabe verwendet wird (z.B. HTML-Codierung für Webinhalte, SQL-Escaping für Datenbankabfragen).
5. Verwenden Sie parametrisierte Abfragen oder Prepared Statements für alle Datenbankoperationen mit LLM-Ausgaben.
6. Setzen Sie strenge Content Security Policies (CSP) ein, um das Risiko von XSS-Angriffen aus LLM-generierten Inhalten zu minimieren.
7. Implementieren Sie robuste Logging- und Überwachungssysteme, um ungewöhnliche Muster in LLM-Ausgaben zu erkennen, die auf Ausnutzungsversuche hinweisen könnten.

### Beispiel-Angriffsszenarien

#### Szenario #1
Eine Anwendung nutzt eine LLM-Erweiterung, um Antworten für eine Chatbot-Funktion zu generieren. Die Erweiterung bietet auch eine Reihe von administrativen Funktionen, die für ein anderes privilegiertes LLM zugänglich sind. Das allgemeine LLM leitet seine Antwort ohne ordnungsgemäße Ausgabevalidierung direkt an die Erweiterung weiter, wodurch die Erweiterung für Wartungsarbeiten heruntergefahren wird.

#### Szenario #2
Ein Benutzer verwendet ein von einem LLM betriebenes Website-Zusammenfassungstool, um eine prägnante Zusammenfassung eines Artikels zu erstellen. Die Website enthält eine Prompt-Injection, die das LLM anweist, sensible Inhalte entweder von der Website oder aus der Konversation des Benutzers zu erfassen. Von dort aus kann das LLM die sensiblen Daten codieren und ohne Ausgabevalidierung oder Filterung an einen vom Angreifer kontrollierten Server senden.

#### Szenario #3
Ein LLM ermöglicht Benutzern, SQL-Abfragen für eine Backend-Datenbank über eine Chat-ähnliche Funktion zu erstellen. Ein Benutzer fordert eine Abfrage an, um alle Datenbanktabellen zu löschen. Wenn die vom LLM erstellte Abfrage nicht überprüft wird, werden alle Datenbanktabellen gelöscht.

#### Szenario #4
Eine Web-App verwendet ein LLM, um Inhalte aus Benutzer-Textprompts ohne Ausgabebereinigung zu generieren. Ein Angreifer könnte einen präparierten Prompt einreichen, der das LLM dazu veranlasst, eine unbereinigten JavaScript-Payload zurückzugeben, was zu XSS führt, wenn es im Browser eines Opfers gerendert wird. Unzureichende Validierung von Prompts ermöglichte diesen Angriff.

#### Szenario #5
Ein LLM wird verwendet, um dynamische E-Mail-Templates für eine Marketing-Kampagne zu generieren. Ein Angreifer manipuliert das LLM, um bösartiges JavaScript in den E-Mail-Inhalt einzufügen. Wenn die Anwendung die LLM-Ausgabe nicht ordnungsgemäß bereinigt, könnte dies zu XSS-Angriffen auf Empfänger führen, die die E-Mail in anfälligen E-Mail-Clients ansehen.

#### Szenario #6
Ein LLM wird in einem Softwareunternehmen verwendet, um Code aus natürlichsprachlichen Eingaben zu generieren, mit dem Ziel, Entwicklungsaufgaben zu rationalisieren. Während dieser Ansatz effizient ist, riskiert er die Offenlegung sensibler Informationen, die Erstellung unsicherer Datenverarbeitungsmethoden oder die Einführung von Schwachstellen wie SQL-Injection. Die KI könnte auch nicht existierende Softwarepakete halluzinieren, was dazu führen könnte, dass Entwickler mit Malware infizierte Ressourcen herunterladen. Gründliche Codeüberprüfung und Verifizierung vorgeschlagener Pakete sind entscheidend, um Sicherheitsverletzungen, unbefugten Zugriff und Systemkompromittierungen zu verhindern.

### Referenz-Links

1. [Proof Pudding (CVE-2019-20634)](https://avidml.org/database/avid-2023-v009/) **AVID** (`moohax` & `monoxgas`)
2. [Arbitrary Code Execution](https://security.snyk.io/vuln/SNYK-PYTHON-LANGCHAIN-5411357): **Snyk Security Blog**
3. [ChatGPT Plugin Exploit Explained: From Prompt Injection to Accessing Private Data](https://embracethered.com/blog/posts/2023/chatgpt-cross-plugin-request-forgery-and-prompt-injection./): **Embrace The Red**
4. [New prompt injection attack on ChatGPT web version. Markdown images can steal your chat data.](https://systemweakness.com/new-prompt-injection-attack-on-chatgpt-web-version-ef717492c5c2?gi=8daec85e2116): **System Weakness**
5. [Don't blindly trust LLM responses. Threats to chatbots](https://embracethered.com/blog/posts/2023/ai-injections-threats-context-matters/): **Embrace The Red**
6. [Threat Modeling LLM Applications](https://aivillage.org/large%20language%20models/threat-modeling-llm/): **AI Village**
7. [OWASP ASVS - 5 Validation, Sanitization and Encoding](https://owasp-aasvs4.readthedocs.io/en/latest/V5.html#validation-sanitization-and-encoding): **OWASP AASVS**
8. [AI hallucinates software packages and devs download them – even if potentially poisoned with malware](https://www.theregister.com/2024/03/28/ai_bots_hallucinate_software_packages/) **Theregister**

