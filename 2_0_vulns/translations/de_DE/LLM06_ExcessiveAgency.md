## LLM06:2025 Übermäßige Handlungsfähigkeit

### Beschreibung

Einem LLM-basierten System wird oft vom Entwickler ein gewisser Grad an Handlungsfähigkeit (Agency) gewährt - die Fähigkeit, Funktionen aufzurufen oder über Erweiterungen (manchmal auch als Tools, Skills oder Plugins von verschiedenen Anbietern bezeichnet) mit anderen Systemen zu interagieren, um Aktionen als Reaktion auf einen Prompt auszuführen. Die Entscheidung darüber, welche Erweiterung aufgerufen werden soll, kann auch an einen LLM-'Agent' delegiert werden, der dies dynamisch basierend auf dem Eingabe-Prompt oder der LLM-Ausgabe bestimmt. Agent-basierte Systeme rufen typischerweise wiederholt ein LLM auf und nutzen die Ausgabe vorheriger Aufrufe, um nachfolgende Aufrufe zu steuern.

Übermäßige Handlungsfähigkeit ist die Schwachstelle, die schädliche Aktionen als Reaktion auf unerwartete, mehrdeutige oder manipulierte Ausgaben eines LLM ermöglicht, unabhängig davon, was die Fehlfunktion des LLM verursacht. Häufige Auslöser sind:
* Halluzinationen/Konfabulationen, verursacht durch schlecht konstruierte gutartige Prompts oder einfach ein schlecht performendes Modell;
* direkte/indirekte Prompt-Injection von einem böswilligen Benutzer, einem früheren Aufruf einer böswilligen/kompromittierten Erweiterung oder (in Multi-Agent/kollaborativen Systemen) einem böswilligen/kompromittierten Peer-Agent.

Die Hauptursache für übermäßige Handlungsfähigkeit ist typischerweise einer oder mehrere der folgenden Punkte:
* übermäßige Funktionalität;
* übermäßige Berechtigungen;
* übermäßige Autonomie.

Übermäßige Handlungsfähigkeit kann zu einem breiten Spektrum an Auswirkungen auf die Vertraulichkeit, Integrität und Verfügbarkeit führen und hängt davon ab, mit welchen Systemen eine LLM-basierte App interagieren kann.

Hinweis: Übermäßige Handlungsfähigkeit unterscheidet sich von unsachgemäßer Ausgabebehandlung, die sich mit unzureichender Überprüfung von LLM-Ausgaben befasst.

### Häufige Beispiele für Risiken

#### 1. Übermäßige Funktionalität
Ein LLM-Agent hat Zugriff auf Erweiterungen, die Funktionen enthalten, die für den beabsichtigten Betrieb des Systems nicht benötigt werden. Zum Beispiel muss ein Entwickler einem LLM-Agent die Fähigkeit gewähren, Dokumente aus einem Repository zu lesen, aber die von ihnen gewählte Drittanbieter-Erweiterung enthält auch die Möglichkeit, Dokumente zu ändern und zu löschen.

#### 2. Übermäßige Funktionalität
Eine Erweiterung wurde möglicherweise während einer Entwicklungsphase getestet und zugunsten einer besseren Alternative verworfen, aber das ursprüngliche Plugin bleibt für den LLM-Agent verfügbar.

#### 3. Übermäßige Funktionalität
Ein LLM-Plugin mit offener Funktionalität filtert die Eingabeanweisungen nicht angemessen auf Befehle, die über das für den beabsichtigten Betrieb der Anwendung Notwendige hinausgehen. Beispiel: Eine Erweiterung zur Ausführung eines bestimmten Shell-Befehls verhindert nicht ausreichend die Ausführung anderer Shell-Befehle.

#### 4. Unnötige Berechtigungen
Eine LLM-Erweiterung verfügt über Berechtigungen für nachgelagerte Systeme, die für den beabsichtigten Betrieb der Anwendung nicht erforderlich sind. Z.B. verbindet sich eine zum Lesen von Daten vorgesehene Erweiterung mit einem Datenbankserver unter Verwendung einer Identität, die nicht nur SELECT-Berechtigungen, sondern auch UPDATE-, INSERT- und DELETE-Berechtigungen hat.

#### 5. Übermäßige Berechtigungen
Eine LLM-Erweiterung, die für die Durchführung von Operationen im Kontext eines einzelnen Benutzers konzipiert ist, greift mit einer generischen hochprivilegierten Identität auf nachgelagerte Systeme zu. Z.B. verbindet sich eine Erweiterung zum Lesen des Dokumentenspeichers des aktuellen Benutzers mit dem Dokumenten-Repository unter einem privilegierten Konto, das Zugriff auf Dateien aller Benutzer hat.

#### 6. Übermäßige Autonomie
Eine LLM-basierte Anwendung oder Erweiterung versäumt es, Aktionen mit hoher Auswirkung unabhängig zu überprüfen und zu genehmigen. Z.B. führt eine Erweiterung, die das Löschen von Benutzerdokumenten ermöglicht, Löschungen ohne Bestätigung durch den Benutzer durch.

### Präventions- und Mitigationsstrategien
Die folgenden Maßnahmen können übermäßige Handlungsfähigkeit verhindern:

#### 1. Erweiterungen minimieren
Beschränken Sie die Erweiterungen, die LLM-Agenten aufrufen dürfen, auf das absolut Notwendige. Wenn ein LLM-basiertes System beispielsweise keine Möglichkeit benötigt, den Inhalt einer URL abzurufen, sollte dem LLM-Agent eine solche Erweiterung nicht angeboten werden.

#### 2. Erweiterungsfunktionalität minimieren
Beschränken Sie die in LLM-Erweiterungen implementierten Funktionen auf das Notwendigste. Beispielsweise benötigt eine Erweiterung, die auf das Postfach eines Benutzers zugreift, um E-Mails zusammenzufassen, möglicherweise nur die Fähigkeit, E-Mails zu lesen, daher sollte die Erweiterung keine anderen Funktionen wie das Löschen oder Senden von Nachrichten enthalten.

#### 3. Offene Erweiterungen vermeiden
Vermeiden Sie nach Möglichkeit die Verwendung von offenen Erweiterungen (z.B. Shell-Befehle ausführen, URLs abrufen usw.) und verwenden Sie stattdessen Erweiterungen mit granularerer Funktionalität. 

#### 4. Erweiterungsberechtigungen minimieren
Beschränken Sie die Berechtigungen, die LLM-Erweiterungen für andere Systeme erhalten, auf das Notwendigste, um den Umfang unerwünschter Aktionen zu begrenzen.

#### 5. Erweiterungen im Benutzerkontext ausführen
Verfolgen Sie Benutzerautorisierung und Sicherheitsbereich, um sicherzustellen, dass Aktionen im Namen eines Benutzers in nachgelagerten Systemen im Kontext dieses spezifischen Benutzers und mit den minimal erforderlichen Privilegien ausgeführt werden.

#### 6. Benutzerbestätigung erforderlich
Nutzen Sie Human-in-the-Loop-Kontrolle, um zu verlangen, dass ein Mensch Aktionen mit hoher Auswirkung genehmigt, bevor sie ausgeführt werden.

#### 7. Vollständige Mediation
Implementieren Sie Autorisierung in nachgelagerten Systemen, anstatt sich darauf zu verlassen, dass ein LLM entscheidet, ob eine Aktion erlaubt ist oder nicht.

#### 8. LLM-Ein- und Ausgaben bereinigen
Befolgen Sie Best Practices für sicheres Programmieren, wie z.B. die Empfehlungen von OWASP im ASVS (Application Security Verification Standard), mit besonderem Fokus auf Eingabebereinigung. Verwenden Sie Static Application Security Testing (SAST) und Dynamic and Interactive Application Testing (DAST, IAST) in Entwicklungspipelines.

### Beispiel-Angriffsszenarien

Eine LLM-basierte persönliche Assistenz-App erhält über eine Erweiterung Zugriff auf das Postfach einer Person, um den Inhalt eingehender E-Mails zusammenzufassen. Um diese Funktionalität zu erreichen, benötigt die Erweiterung die Fähigkeit, Nachrichten zu lesen, jedoch enthält das vom Systementwickler gewählte Plugin auch Funktionen zum Senden von Nachrichten. Zusätzlich ist die App anfällig für einen indirekten Prompt-Injection-Angriff, bei dem eine böswillig erstellte eingehende E-Mail das LLM dazu bringt, dem Agenten zu befehlen, den Posteingang des Benutzers nach sensiblen Informationen zu durchsuchen und an die E-Mail-Adresse des Angreifers weiterzuleiten. Dies könnte vermieden werden durch:
* Eliminierung übermäßiger Funktionalität durch Verwendung einer Erweiterung, die nur Lesefunktionen implementiert,
* Eliminierung übermäßiger Berechtigungen durch Authentifizierung beim E-Mail-Service des Benutzers über eine OAuth-Sitzung mit reinem Lesezugriff, und/oder
* Eliminierung übermäßiger Autonomie durch Anforderung einer manuellen Überprüfung und Bestätigung des Benutzers für jede vom LLM-Plugin erstellte E-Mail.

Alternativ könnten die verursachten Schäden durch Implementierung von Rate Limiting auf der E-Mail-Sende-Schnittstelle reduziert werden.

### Referenz-Links

1. [Slack AI data exfil from private channels](https://promptarmor.substack.com/p/slack-ai-data-exfiltration-from-private): **PromptArmor**
2. [Rogue Agents: Stop AI From Misusing Your APIs](https://www.twilio.com/en-us/blog/rogue-ai-agents-secure-your-apis): **Twilio**
3. [Embrace the Red: Confused Deputy Problem](https://embracethered.com/blog/posts/2023/chatgpt-cross-plugin-request-forgery-and-prompt-injection./): **Embrace The Red**
4. [NeMo-Guardrails: Interface guidelines](https://github.com/NVIDIA/NeMo-Guardrails/blob/main/docs/security/guidelines.md): **NVIDIA Github**
6. [Simon Willison: Dual LLM Pattern](https://simonwillison.net/2023/Apr/25/dual-llm-pattern/): **Simon Willison**

