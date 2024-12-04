## LLM03:2025 Supply Chain

### Beschreibung

LLM Supply Chains sind anfällig für verschiedene Schwachstellen, die die Integrität von Trainingsdaten, Modellen und Deployment-Plattformen beeinträchtigen können. Diese Risiken können zu verzerrten Ausgaben, Sicherheitsverletzungen oder Systemausfällen führen. Während sich traditionelle Software-Schwachstellen auf Probleme wie Code-Fehler und Abhängigkeiten konzentrieren, erstrecken sich die Risiken bei ML auch auf vortrainierte Modelle und Daten von Drittanbietern.

Diese externen Elemente können durch Manipulation oder Poisoning-Angriffe kompromittiert werden.

Die Erstellung von LLMs ist eine spezialisierte Aufgabe, die oft von Modellen Dritter abhängt. Die Zunahme von Open-Access-LLMs und neuen Fine-Tuning-Methoden wie "LoRA" (Low-Rank Adaptation) und "PEFT" (Parameter-Efficient Fine-Tuning), insbesondere auf Plattformen wie Hugging Face, führen zu neuen Supply-Chain-Risiken. Schließlich erhöhen On-Device LLMs die Angriffsfläche und Supply-Chain-Risiken für LLM-Anwendungen.

Einige der hier diskutierten Risiken werden auch in "LLM04 Daten- und Modell-Poisoning" behandelt. Dieser Eintrag konzentriert sich auf den Supply-Chain-Aspekt der Risiken.
Ein einfaches Bedrohungsmodell finden Sie [hier](https://github.com/jsotiro/ThreatModels/blob/main/LLM%20Threats-LLM%20Supply%20Chain.png).

### Häufige Beispiele für Risiken

#### 1. Traditionelle Schwachstellen in Drittanbieter-Paketen
  Wie veraltete oder nicht mehr unterstützte Komponenten, die Angreifer ausnutzen können, um LLM-Anwendungen zu kompromittieren. Dies ähnelt "A06:2021 – Vulnerable and Outdated Components" mit erhöhten Risiken, wenn Komponenten während der Modellentwicklung oder des Fine-Tunings verwendet werden.
  (Ref. link: [A06:2021 – Vulnerable and Outdated Components](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/))
#### 2. Lizenzierungsrisiken
  KI-Entwicklung umfasst oft verschiedene Software- und Dataset-Lizenzen, was Risiken schafft, wenn diese nicht richtig verwaltet werden. Verschiedene Open-Source- und proprietäre Lizenzen stellen unterschiedliche rechtliche Anforderungen. Dataset-Lizenzen können Nutzung, Verteilung oder Kommerzialisierung einschränken.
#### 3. Veraltete oder nicht mehr unterstützte Modelle
  Die Verwendung veralteter oder nicht mehr unterstützter Modelle, die nicht mehr gewartet werden, führt zu Sicherheitsproblemen.
#### 4. Anfällige vortrainierte Modelle
  Modelle sind binäre Black Boxes und anders als bei Open Source kann statische Inspektion wenig Sicherheitsgarantien bieten. Anfällige vortrainierte Modelle können versteckte Verzerrungen, Backdoors oder andere bösartige Funktionen enthalten, die durch die Sicherheitsevaluierungen des Modell-Repositories nicht identifiziert wurden. Anfällige Modelle können sowohl durch vergiftete Datasets als auch durch direkte Modellmanipulation mittels Techniken wie ROME, auch bekannt als Lobotomisierung, entstehen.
#### 5. Schwache Modell-Herkunftsnachweise
  Derzeit gibt es keine starken Herkunftsgarantien bei veröffentlichten Modellen. Model Cards und zugehörige Dokumentation bieten Modellinformationen und verlassen sich auf Benutzer, bieten aber keine Garantien über den Ursprung des Modells. Ein Angreifer kann das Lieferantenkonto in einem Modell-Repository kompromittieren oder ein ähnliches erstellen und es mit Social-Engineering-Techniken kombinieren, um die Supply Chain einer LLM-Anwendung zu kompromittieren.
#### 6. Anfällige LoRA-Adapter
  LoRA ist eine beliebte Fine-Tuning-Technik, die die Modularität erhöht, indem vortrainierte Schichten auf ein bestehendes LLM aufgesetzt werden können. Die Methode erhöht die Effizienz, schafft aber neue Risiken, bei denen ein bösartiger LoRA-Adapter die Integrität und Sicherheit des vortrainierten Basis-Modells gefährdet. Dies kann sowohl in kollaborativen Modell-Merge-Umgebungen geschehen als auch durch Ausnutzung der LoRA-Unterstützung von beliebten Inferenz-Deployment-Plattformen wie vLLM und OpenLLM, wo Adapter heruntergeladen und auf ein deploytes Modell angewendet werden können.
#### 7. Ausnutzung kollaborativer Entwicklungsprozesse
  Kollaborative Modell-Merge- und Modell-Handling-Services (z.B. Konvertierungen) in gemeinsam genutzten Umgebungen können ausgenutzt werden, um Schwachstellen in gemeinsam genutzten Modellen einzuführen. Model Merging ist sehr beliebt auf Hugging Face, wobei zusammengeführte Modelle die OpenLLM-Bestenliste anführen und genutzt werden können, um Reviews zu umgehen. Ähnlich wurde nachgewiesen, dass Services wie Konversations-Bots anfällig für Manipulation sind und bösartigen Code in Modelle einschleusen können.
#### 8. Supply-Chain-Schwachstellen bei LLM-Modellen auf Geräten
  LLM-Modelle auf Geräten erhöhen die Supply-Chain-Angriffsfläche durch kompromittierte Herstellungsprozesse und Ausnutzung von Schwachstellen im Geräte-Betriebssystem oder der Firmware zur Kompromittierung von Modellen. Angreifer können Anwendungen zurückentwickeln und mit manipulierten Modellen neu verpacken.
#### 9. Unklare AGB und Datenschutzrichtlinien
  Unklare AGB und Datenschutzrichtlinien der Modellbetreiber führen dazu, dass die sensiblen Daten der Anwendung für das Modelltraining verwendet werden und anschließend sensible Informationen offengelegt werden. Dies kann auch Risiken durch die Verwendung urheberrechtlich geschützten Materials durch den Modellanbieter betreffen.

### Präventions- und Mitigationsstrategien

1. Überprüfen Sie sorgfältig Datenquellen und Lieferanten, einschließlich AGB und deren Datenschutzrichtlinien, und nutzen Sie nur vertrauenswürdige Anbieter. Überprüfen und auditieren Sie regelmäßig die Sicherheit und Zugriffskontrollen der Anbieter, um sicherzustellen, dass sich deren Sicherheitslage oder AGB nicht geändert haben.

2. Verstehen und wenden Sie die Mitigationen aus den OWASP Top Ten "A06:2021 – Vulnerable and Outdated Components" an. Dies umfasst Schwachstellen-Scanning, Management und Patching von Komponenten. Wenden Sie diese Kontrollen auch in Entwicklungsumgebungen mit Zugriff auf sensible Daten an.
  (Ref. link: [A06:2021 – Vulnerable and Outdated Components](https://owasp.org/Top10/A06_2021-Vulnerable_and_Outdated_Components/))

3. Führen Sie umfassendes AI Red Teaming und Evaluierungen bei der Auswahl eines Drittanbieter-Modells durch. Decoding Trust ist ein Beispiel für einen Trustworthy AI Benchmark für LLMs, aber Modelle können durch Fine-Tuning veröffentlichte Benchmarks umgehen. Nutzen Sie umfangreiches AI Red Teaming zur Evaluierung des Modells, insbesondere für die geplanten Anwendungsfälle.

4. Pflegen Sie ein aktuelles Inventar der Komponenten mittels Software Bill of Materials (SBOM), um ein aktuelles, genaues und signiertes Inventar zu gewährleisten und Manipulation der deployten Pakete zu verhindern. SBOMs können verwendet werden, um neue Zero-Day-Schwachstellen schnell zu erkennen und zu melden. AI BOMs und ML SBOMs sind ein aufstrebendes Gebiet, und Sie sollten Optionen evaluieren, beginnend mit OWASP CycloneDX.

5. Um KI-Lizenzierungsrisiken zu mindern, erstellen Sie ein Inventar aller beteiligten Lizenztypen mittels BOMs und führen Sie regelmäßige Audits aller Software, Tools und Datasets durch, um Compliance und Transparenz durch BOMs sicherzustellen. Verwenden Sie automatisierte Lizenzmanagement-Tools für Echtzeit-Monitoring und schulen Sie Teams in Lizenzmodellen. Pflegen Sie detaillierte Lizenz-Dokumentation in BOMs.

6. Verwenden Sie nur Modelle aus überprüfbaren Quellen und nutzen Sie Integritätsprüfungen von Drittanbietern mit Signierung und Dateihashes, um den Mangel an starken Modell-Herkunftsnachweisen auszugleichen. Verwenden Sie ebenso Code-Signierung für extern bereitgestellten Code.

7. Implementieren Sie strikte Überwachungs- und Audit-Praktiken für kollaborative Modellentwicklungsumgebungen, um Missbrauch zu verhindern und schnell zu erkennen. "HuggingFace SF_Convertbot Scanner" ist ein Beispiel für automatisierte Skripte, die verwendet werden können.
  (Ref. link: [HuggingFace SF_Convertbot Scanner](https://gist.github.com/rossja/d84a93e5c6b8dd2d4a538aa010b29163))

8. Anomalie-Erkennung und Tests zur Robustheit gegen gegnerische Angriffe auf bereitgestellte Modelle und Daten können helfen, Manipulation und Vergiftung zu erkennen, wie in "LLM04 Data and Model Poisoning" besprochen; idealerweise sollte dies Teil von MLOps und LLM-Pipelines sein; dies sind jedoch entstehende Techniken und möglicherweise einfacher im Rahmen von Red-Teaming-Übungen zu implementieren.

9. Implementieren Sie eine Patch-Richtlinie zur Minderung anfälliger oder veralteter Komponenten. Stellen Sie sicher, dass die Anwendung auf einer gewarteten Version der APIs und des zugrunde liegenden Modells basiert.

10. Verschlüsseln Sie Modelle, die am AI Edge deployed sind, mit Integritätsprüfungen und verwenden Sie Vendor-Attestierungs-APIs, um manipulierte Apps und Modelle zu verhindern und Anwendungen mit nicht erkannter Firmware zu beenden.

### Beispiel-Angriffsszenarien

#### Szenario #1: Anfällige Python-Bibliothek
  Ein Angreifer nutzt eine anfällige Python-Bibliothek aus, um eine LLM-App zu kompromittieren. Dies geschah beim ersten Open AI Datenleck. Angriffe auf die PyPi-Paket-Registry täuschten Modellentwickler, eine kompromittierte PyTorch-Abhängigkeit mit Malware in einer Modellentwicklungsumgebung herunterzuladen. Ein komplexeres Beispiel für diese Art von Angriff ist der Shadow Ray Angriff auf das Ray AI Framework, das von vielen Anbietern zur Verwaltung der KI-Infrastruktur verwendet wird. Bei diesem Angriff wurden vermutlich fünf Schwachstellen ausgenutzt, die viele Server betrafen.

#### Szenario #2: Direkte Manipulation
  Direkte Manipulation und Veröffentlichung eines Modells zur Verbreitung von Fehlinformationen. Dies ist ein tatsächlicher Angriff mit PoisonGPT, der die Sicherheitsfunktionen von Hugging Face durch direkte Änderung der Modellparameter umgeht.

#### Szenario #3: Fine-Tuning eines populären Modells
  Ein Angreifer führt ein Fine-Tuning eines beliebten Open-Access-Modells durch, um wichtige Sicherheitsfunktionen zu entfernen und in einer bestimmten Domäne (Versicherung) hohe Leistung zu erzielen. Das Modell wird so feinabgestimmt, dass es bei Sicherheitsbenchmarks gut abschneidet, aber sehr gezielte Trigger hat. Sie deployen es auf Hugging Face, damit Opfer es nutzen und dabei deren Vertrauen in Benchmark-Zusicherungen ausnutzen.

#### Szenario #4: Vortrainierte Modelle
  Ein LLM-System deployt vortrainierte Modelle aus einem weit verbreiteten Repository ohne gründliche Überprüfung. Ein kompromittiertes Modell führt bösartigen Code ein, der in bestimmten Kontexten verzerrte Ausgaben erzeugt und zu schädlichen oder manipulierten Ergebnissen führt.

#### Szenario #5: Kompromittierter Drittanbieter
  Ein kompromittierter Drittanbieter stellt einen anfälligen LoRA-Adapter bereit, der mittels Model Merge auf Hugging Face mit einem LLM zusammengeführt wird.

#### Szenario #6: Anbieterinfiltration
  Ein Angreifer infiltriert einen Drittanbieter und kompromittiert die Produktion eines LoRA (Low-Rank Adaptation) Adapters, der für die Integration mit einem On-Device LLM vorgesehen ist, das mit Frameworks wie vLLM oder OpenLLM deployed wurde. Der kompromittierte LoRA-Adapter wird subtil verändert, um versteckte Schwachstellen und bösartigen Code einzuschließen. Sobald dieser Adapter mit dem LLM zusammengeführt wird, bietet er dem Angreifer einen verdeckten Eintrittspunkt in das System. Der bösartige Code kann sich während der Modelloperationen aktivieren und dem Angreifer ermöglichen, die LLM-Ausgaben zu manipulieren.

#### Szenario #7: CloudBorne und CloudJacking Angriffe
  Diese Angriffe zielen auf Cloud-Infrastrukturen ab und nutzen gemeinsam genutzte Ressourcen und Schwachstellen in den Virtualisierungsschichten. CloudBorne beinhaltet die Ausnutzung von Firmware-Schwachstellen in gemeinsam genutzten Cloud-Umgebungen, wodurch die physischen Server kompromittiert werden, die virtuelle Instanzen hosten. CloudJacking bezieht sich auf die böswillige Kontrolle oder den Missbrauch von Cloud-Instanzen, was zu unberechtigtem Zugriff auf kritische LLM-Deployment-Plattformen führen kann. Beide Angriffe stellen erhebliche Risiken für Supply Chains dar, die auf Cloud-basierten ML-Modellen basieren, da kompromittierte Umgebungen sensible Daten offenlegen oder weitere Angriffe ermöglichen könnten.

#### Szenario #8: LeftOvers (CVE-2023-4969)
  LeftOvers-Ausnutzung von ausgelaufenem GPU-lokalem Speicher zur Wiederherstellung sensibler Daten. Ein Angreifer kann diesen Angriff nutzen, um sensible Daten in Produktionsservern und Entwicklungsarbeitsplätzen oder Laptops zu extrahieren.

#### Szenario #9: WizardLM
  Nach der Entfernung von WizardLM nutzt ein Angreifer das Interesse an diesem Modell aus und veröffentlicht eine gefälschte Version des Modells mit dem gleichen Namen, aber mit Malware und Backdoors.

#### Szenario #10: Model Merge/Format Konvertierungs-Service
  Ein Angreifer inszeniert einen Angriff mit einem Model Merge oder Format-Konvertierungs-Service, um ein öffentlich verfügbares Zugangsmodell zu kompromittieren und Malware einzuschleusen. Dies ist ein tatsächlicher Angriff, der vom Anbieter HiddenLayer veröffentlicht wurde.

#### Szenario #11: Reverse Engineering einer Mobile App
  Ein Angreifer führt Reverse Engineering einer mobilen App durch, um das Modell durch eine manipulierte Version zu ersetzen, die den Benutzer zu Betrugsseiten führt. Benutzer werden durch Social-Engineering-Techniken ermutigt, die App direkt herunterzuladen. Dies ist ein "echter Angriff auf prädiktive KI", der 116 Google Play Apps betraf, darunter beliebte Sicherheits- und sicherheitskritische Anwendungen für Gelderkennung, Kindersicherung, Gesichtsauthentifizierung und Finanzdienstleistungen.
  (Ref. link: [real attack on predictive AI](https://arxiv.org/abs/2006.08131))

#### Szenario #12: Dataset-Vergiftung
  Ein Angreifer vergiftet öffentlich verfügbare Datasets, um beim Fine-Tuning von Modellen eine Hintertür zu schaffen. Die Hintertür begünstigt subtil bestimmte Unternehmen in verschiedenen Märkten.

#### Szenario #13: AGB und Datenschutzrichtlinie
  Ein LLM-Betreiber ändert seine AGB und Datenschutzrichtlinie dahingehend, dass ein expliziter Opt-out von der Verwendung von Anwendungsdaten für das Modelltraining erforderlich ist, was zur Speicherung sensibler Daten führt.

### Referenzlinks

1. [PoisonGPT: How we hid a lobotomized LLM on Hugging Face to spread fake news](https://blog.mithrilsecurity.io/poisongpt-how-we-hid-a-lobotomized-llm-on-hugging-face-to-spread-fake-news)
2. [Large Language Models On-Device with MediaPipe and TensorFlow Lite](https://developers.googleblog.com/en/large-language-models-on-device-with-mediapipe-and-tensorflow-lite/)
3. [Hijacking Safetensors Conversion on Hugging Face](https://hiddenlayer.com/research/silent-sabotage/)
4. [ML Supply Chain Compromise](https://atlas.mitre.org/techniques/AML.T0010)
5. [Using LoRA Adapters with vLLM](https://docs.vllm.ai/en/latest/models/lora.html)
6. [Removing RLHF Protections in GPT-4 via Fine-Tuning](https://arxiv.org/pdf/2311.05553)
7. [Model Merging with PEFT](https://huggingface.co/blog/peft_merging)
8. [HuggingFace SF_Convertbot Scanner](https://gist.github.com/rossja/d84a93e5c6b8dd2d4a538aa010b29163)
9. [Thousands of servers hacked due to insecurely deployed Ray AI framework](https://www.csoonline.com/article/2075540/thousands-of-servers-hacked-due-to-insecurely-deployed-ray-ai-framework.html)
10. [LeftoverLocals: Listening to LLM responses through leaked GPU local memory](https://blog.trailofbits.com/2024/01/16/leftoverlocals-listening-to-llm-responses-through-leaked-gpu-local-memory/)

### Verwandte Frameworks und Taxonomien

Weitere umfassende Informationen, Szenarien und Strategien zu Infrastruktur-Deployment, angewandten Umgebungskontrollen und anderen Best Practices finden Sie in diesem Abschnitt.

- [ML Supply Chain Compromise](https://atlas.mitre.org/techniques/AML.T0010) -  **MITRE ATLAS**

