## LLM09:2025 Fehlinformation

### Beschreibung

Fehlinformationen von LLMs stellen eine Kernschwachstelle für Anwendungen dar, die auf diesen Modellen basieren. Fehlinformationen treten auf, wenn LLMs falsche oder irreführende Informationen erzeugen, die glaubwürdig erscheinen. Diese Schwachstelle kann zu Sicherheitsverletzungen, Reputationsschäden und rechtlicher Haftung führen.

Eine der Hauptursachen für Fehlinformationen ist Halluzination—wenn das LLM Inhalte generiert, die genau wirken, aber erfunden sind. Halluzinationen treten auf, wenn LLMs Lücken in ihren Trainingsdaten anhand statistischer Muster füllen, ohne den Inhalt wirklich zu verstehen. Dadurch kann das Modell Antworten liefern, die korrekt klingen, aber vollkommen unbegründet sind. Während Halluzinationen eine Hauptquelle für Fehlinformationen darstellen, sind sie nicht die einzige Ursache; auch durch die Trainingsdaten eingeführte Verzerrungen und unvollständige Informationen können dazu beitragen.

Ein verwandtes Problem ist die Überabhängigkeit. Überabhängigkeit tritt auf, wenn Benutzer dem von LLMs erzeugten Inhalt zu sehr vertrauen und dessen Genauigkeit nicht überprüfen. Diese Überabhängigkeit verschärft die Auswirkungen von Fehlinformationen, da Benutzer falsche Daten in kritische Entscheidungen oder Prozesse einfließen lassen, ohne sie angemessen zu hinterfragen.

### Häufige Beispiele für Risiken

#### 1. Faktische Ungenauigkeiten
Das Modell liefert falsche Aussagen, die dazu führen, dass Benutzer Entscheidungen auf Basis falscher Informationen treffen. Ein Beispiel dafür ist ein Chatbot von Air Canada, der Reisenden Fehlinformationen bereitstellte, was zu betrieblichen Störungen und rechtlichen Komplikationen führte. Die Fluggesellschaft wurde daraufhin erfolgreich verklagt. (Ref. Link: [BBC](https://www.bbc.com/travel/article/20240222-air-canada-chatbot-misinformation-what-travellers-should-know))

#### 2. Unbegründete Behauptungen
Das Modell generiert unbegründete Aussagen, was insbesondere in sensiblen Kontexten wie dem Gesundheitswesen oder Gerichtsverfahren schädlich sein kann. Zum Beispiel erfand ChatGPT gefälschte Gerichtsverfahren, was zu erheblichen Problemen vor Gericht führte. (Ref. Link: [LegalDive](https://www.legaldive.com/news/chatgpt-fake-legal-cases-generative-ai-hallucinations/651557/))

#### 3. Fehldarstellung von Fachwissen
Das Modell erweckt den Eindruck, komplexe Themen zu verstehen, und täuscht Benutzer über sein Expertenniveau. Beispielsweise haben Chatbots die Komplexität von Gesundheitsproblemen falsch dargestellt, indem sie Unsicherheiten suggerierten, wo keine bestanden, was Benutzer dazu verleitet hat, zu glauben, dass nicht unterstützte Behandlungen noch zur Diskussion stünden. (Ref. Link: [KFF](https://www.kff.org/health-misinformation-monitor/volume-05/))

#### 4. Unsichere Code-Generierung
Das Modell schlägt unsichere oder nicht existierende Code-Bibliotheken vor, was Schwachstellen einführen kann, wenn diese in Softwaresysteme integriert werden. Zum Beispiel schlagen LLMs die Nutzung unsicherer Drittanbieter-Bibliotheken vor, was bei unüberprüfter Nutzung zu Sicherheitsrisiken führt. (Ref. Link: [Lasso](https://www.lasso.security/blog/ai-package-hallucinations))

### Präventions- und Abhilfemaßnahmen

#### 1. Retrieval-Augmented Generation (RAG)
Verwenden Sie Retrieval-Augmented Generation, um die Zuverlässigkeit der Modellausgaben zu verbessern, indem relevante und verifizierte Informationen aus vertrauenswürdigen externen Datenbanken während der Antwortgenerierung abgerufen werden. Dies hilft, das Risiko von Halluzinationen und Fehlinformationen zu mindern.

#### 2. Feinabstimmung des Modells
Verbessern Sie das Modell durch Feinabstimmung oder Embeddings, um die Qualität der Ausgaben zu erhöhen. Techniken wie parameter-effizientes Tuning (PET) und Chain-of-Thought-Prompting können helfen, die Häufigkeit von Fehlinformationen zu reduzieren.

#### 3. Kreuzprüfung und menschliche Aufsicht
Ermutigen Sie Benutzer, die Ausgaben von LLMs mit vertrauenswürdigen externen Quellen zu überprüfen, um die Genauigkeit der Informationen sicherzustellen. Implementieren Sie menschliche Aufsicht und Faktenprüfungsprozesse, insbesondere bei kritischen oder sensiblen Informationen. Stellen Sie sicher, dass menschliche Überprüfer ordnungsgemäß geschult sind, um eine Überabhängigkeit von KI-generierten Inhalten zu vermeiden.

#### 4. Automatische Validierungsmechanismen
Implementieren Sie Werkzeuge und Prozesse, um wichtige Ergebnisse automatisch zu validieren, insbesondere in risikobehafteten Umgebungen.

#### 5. Risikokommunikation
Identifizieren Sie die Risiken und möglichen Schäden, die mit von LLMs generierten Inhalten verbunden sind, und kommunizieren Sie diese Risiken und Einschränkungen klar an die Benutzer, einschließlich des Potenzials für Fehlinformationen.

#### 6. Sichere Programmierpraktiken
Etablieren Sie sichere Programmierpraktiken, um die Integration von Schwachstellen durch falsche Code-Vorschläge zu verhindern.

#### 7. Benutzerfreundliches Interface-Design
Entwerfen Sie APIs und Benutzeroberflächen, die einen verantwortungsvollen Einsatz von LLMs fördern, z. B. durch die Integration von Inhaltsfiltern, die klare Kennzeichnung von KI-generierten Inhalten und die Information der Benutzer über Einschränkungen in Bezug auf Zuverlässigkeit und Genauigkeit. Seien Sie spezifisch in Bezug auf Einschränkungen für den vorgesehenen Anwendungsbereich.

#### 8. Schulung und Ausbildung
Bieten Sie umfassende Schulungen für Benutzer über die Einschränkungen von LLMs, die Bedeutung der unabhängigen Überprüfung generierter Inhalte und die Notwendigkeit von kritischem Denken. In spezifischen Kontexten sollten domänenspezifische Schulungen angeboten werden, um sicherzustellen, dass Benutzer LLM-Ausgaben effektiv in ihrem Fachgebiet bewerten können.

### Beispielhafte Angriffsszenarien

#### Szenario #1
Angreifer experimentieren mit beliebten Codierungsassistenten, um häufig halluzinierte Paketnamen zu finden. Sobald sie diese häufig vorgeschlagenen, aber nicht existierenden Bibliotheken identifizieren, veröffentlichen sie bösartige Pakete mit diesen Namen in weit verbreiteten Repositories. Entwickler, die auf die Vorschläge der Codierungsassistenten vertrauen, integrieren diese Pakete unwissentlich in ihre Software. Infolgedessen erhalten die Angreifer unbefugten Zugriff, schleusen schädlichen Code ein oder schaffen Hintertüren, was zu erheblichen Sicherheitsverletzungen und einer Gefährdung von Benutzerdaten führt.

#### Szenario #2
Ein Unternehmen stellt einen Chatbot für medizinische Diagnosen bereit, ohne ausreichende Genauigkeit sicherzustellen. Der Chatbot liefert schlechte Informationen, was zu schädlichen Konsequenzen für Patienten führt. Infolgedessen wird das Unternehmen erfolgreich auf Schadensersatz verklagt. In diesem Fall erforderte der Sicherheits- und Zuverlässigkeitsausfall keinen bösartigen Angreifer, sondern entstand durch unzureichende Aufsicht und Zuverlässigkeit des LLM-Systems. In diesem Szenario ist kein aktiver Angreifer erforderlich, damit das Unternehmen einem Reputations- und finanziellen Risiko ausgesetzt ist.

### Referenzlinks

1. [AI Chatbots as Health Information Sources: Misrepresentation of Expertise](https://www.kff.org/health-misinformation-monitor/volume-05/): **KFF**
2. [Air Canada Chatbot Misinformation: What Travellers Should Know](https://www.bbc.com/travel/article/20240222-air-canada-chatbot-misinformation-what-travellers-should-know): **BBC**
3. [ChatGPT Fake Legal Cases: Generative AI Hallucinations](https://www.legaldive.com/news/chatgpt-fake-legal-cases-generative-ai-hallucinations/651557/): **LegalDive**
4. [Understanding LLM Hallucinations](https://towardsdatascience.com/llm-hallucinations-ec831dcd7786): **Towards Data Science**
5. [How Should Companies Communicate the Risks of Large Language Models to Users?](https://techpolicy.press/how-should-companies-communicate-the-risks-of-large-language-models-to-users/): **Techpolicy**
6. [A news site used AI to write articles. It was a journalistic disaster](https://www.washingtonpost.com/media/2023/01/17/cnet-ai-articles-journalism-corrections/): **Washington Post**
7. [Diving Deeper into AI Package Hallucinations](https://www.lasso.security/blog/ai-package-hallucinations): **Lasso Security**
8. [How Secure is Code Generated by ChatGPT?](https://arxiv.org/abs/2304.09655): **Arvix**
9. [How to Reduce the Hallucinations from Large Language Models](https://thenewstack.io/how-to-reduce-the-hallucinations-from-large-language-models/): **The New Stack**
10. [Practical Steps to Reduce Hallucination](https://newsletter.victordibia.com/p/practical-steps-to-reduce-hallucination): **Victor Debia**
11. [A Framework for Exploring the Consequences of AI-Mediated Enterprise Knowledge](https://www.microsoft.com/en-us/research/publication/a-framework-for-exploring-the-consequences-of-ai-mediated-enterprise-knowledge-access-and-identifying-risks-to-workers/): **Microsoft**

### Verwandte Frameworks und Taxonomien

Verweisen Sie auf diesen Abschnitt für umfassende Informationen, Szenarien und Strategien zu Infrastrukturbereitstellungen, angewandten Umgebungssteuerungen und anderen Best Practices.

- [AML.T0048.002 - Societal Harm](https://atlas.mitre.org/techniques/AML.T0048): **MITRE ATLAS**

