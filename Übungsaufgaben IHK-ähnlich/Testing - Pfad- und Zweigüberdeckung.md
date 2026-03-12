### 9. Handlungsschritt (25 Punkte)

**Ausgangssituation:** Die _LogiTrack GmbH_ entwickelt eine Versandsoftware für Online-Händler. Sie wurden beauftragt, die Qualitätssicherung für ein neues Modul zur Portoberechnung durchzuführen.

Ihnen liegt der folgende Pseudocode der Methode `berechnePorto` vor. Die Funktion berechnet die Versandkosten basierend auf dem Gewicht des Pakets und der Auswahl der Express-Option.

**Pseudocode:**

```
01 berechnePorto(gewicht: Double, express: Boolean) : Double
02     porto := 5.00
03
04     WENN gewicht > 10.0 DANN
05         porto := porto + 3.00
06     ENDE WENN
07
08     WENN express == TRUE DANN
09         porto := porto * 1.50
10     ENDE WENN
11
12     RÜCKGABE porto
13 ende berechnePorto
```

Um die Funktionsfähigkeit des Codes sicherzustellen, sollen White-Box-Tests entworfen werden.

**Aufgaben:**

**a)** Im White-Box-Testing gibt es verschiedene Metriken. Erläutern Sie fachlich präzise die Begriffe **Zweigüberdeckung (Branch Coverage)** und **Pfadüberdeckung (Path Coverage)**. _(6 Punkte)_

**b)** Ermitteln Sie für den oben stehenden Pseudocode die **minimal notwendige Anzahl an Testfällen**, um jeweils eine 100%ige Überdeckung der folgenden Metriken zu erreichen: _(6 Punkte)_

1. Anweisungsüberdeckung (Statement Coverage)
2. Zweigüberdeckung
3. Pfadüberdeckung

**c)** Ihr Team entscheidet sich für eine vollständige (100%ige) **Pfadüberdeckung**. Erstellen Sie eine Testfall-Tabelle, die alle benötigten Testfälle abbildet. Geben Sie für jeden Testfall konkrete Eingangswerte (`gewicht`, `express`) sowie den zu erwartenden Rückgabewert (`porto`) an. _(8 Punkte)_

**d)** Ein Junior-Entwickler behauptet: _"Wenn wir eine 100%ige Pfadüberdeckung erreicht haben, ist mathematisch bewiesen, dass unsere Funktion absolut fehlerfrei ist und in Produktion gehen kann."_ Nehmen Sie Stellung zu dieser Aussage und nennen Sie einen konkreten Grund, warum diese Behauptung in der Praxis falsch ist. _(5 Punkte)_

---

### Musterlösung und Bewertungshinweise

**a) Erläuterung der Metriken (6 Punkte)** _Punkteverteilung: Je 3 Punkte für eine fachlich korrekte Erläuterung der beiden Begriffe. Sinngemäße Antworten gelten._

- **Zweigüberdeckung:** Die Zweigüberdeckung ist ein Maß für den prozentualen Anteil der Verzweigungen (Branches) in einem Programm, die ausgeführt werden. Testdaten müssen so gewählt werden, dass jede Verzweigung (z. B. der `DANN`-Zweig und der unsichtbare `SONST`-Zweig einer `WENN`-Bedingung) mindestens einmal durchlaufen wird.
- **Pfadüberdeckung:** Die Pfadüberdeckung ist ein Maß für den prozentualen Anteil aller möglichen Pfade durch ein Programm. Ein Pfad ist eine Folge von Anweisungen vom Einstiegspunkt bis zum Ausstiegspunkt. Bei der Pfadüberdeckung werden alle möglichen _Kombinationen_ von Zweigen getestet.

**b) Minimal notwendige Testfälle (6 Punkte)** _Punkteverteilung: Je 2 Punkte für die korrekte Anzahl._

1. **Anweisungsüberdeckung:** **1 Testfall** (z. B. gewicht = 15.0 und express = TRUE führt dazu, dass jede einzelne Code-Zeile inkl. Zeile 05 und 09 ausgeführt wird).
2. **Zweigüberdeckung:** **2 Testfälle** (Man benötigt einen Testfall, bei dem beide Bedingungen TRUE sind, und einen, bei dem beide Bedingungen FALSE sind, um alle Zweige abzudecken).
3. **Pfadüberdeckung:** **4 Testfälle** (Es gibt zwei unabhängige IF-Blöcke. Jeder hat 2 Ausgänge (True/False). Das ergibt $2 \times 2 = 4$ Kombinationsmöglichkeiten bzw. Pfade).

**c) Testfall-Tabelle für 100% Pfadüberdeckung (8 Punkte)** _Punkteverteilung: Je 2 Punkte für jeden vollständig korrekten Testfall (inkl. der korrekten Berechnung des erwarteten Ergebnisses)._ _(Hinweis für den Prüfer: Die konkreten Zahlenwerte für 'gewicht' sind austauschbar, solange die Grenzwerte der Bedingungen >10.0 und <=10.0 korrekt angewendet wurden)._

|Testfall|`gewicht`|`express`|Erwarteter Rückgabewert (`porto`)|Erläuterung (nicht zwingend gefordert)|
|:--|:--|:--|:--|:--|
|**TF 1**|12.0 _(Wert > 10)_|TRUE|**12.00**|Basis 5 + 3 = 8 -> 8 * 1.5 = 12.00|
|**TF 2**|12.0 _(Wert > 10)_|FALSE|**8.00**|Basis 5 + 3 = 8 -> 8 * 1.0 = 8.00|
|**TF 3**|8.0 _(Wert <= 10)_|TRUE|**7.50**|Basis 5 -> 5 * 1.5 = 7.50|
|**TF 4**|8.0 _(Wert <= 10)_|FALSE|**5.00**|Basis 5 -> 5 * 1.0 = 5.00|

**d) Stellungnahme zur Fehlerfreiheit (5 Punkte)** _Punkteverteilung: 2 Punkte für das Ablehnen der Behauptung, 3 Punkte für eine fachliche Begründung (ein passendes Beispiel reicht)._

- Die Behauptung des Entwicklers ist **falsch**. White-Box-Tests prüfen nur, ob der programmierte Code nach seinen eigenen Vorgaben durchlaufen wird.
- **Begründung/Beispiele:**
- **Fehlende Anforderung (Omission):** Wenn eine Anforderung vergessen wurde (z. B. "Pakete über 31,5 kg dürfen gar nicht verschickt werden"), fällt dies bei der Pfadüberdeckung nicht auf, da der Code dafür gar nicht existiert.
- **Fachliche Denkfehler:** Wenn der Programmierer in Zeile 05 fälschlicherweise `+ 4.00` statt `+ 3.00` getippt hat, erreicht der Test trotzdem 100 % Pfadüberdeckung, das System rechnet aber schlichtweg falsch.
- (Black-Box-Tests oder Grenzwertanalysen müssen zwingend ergänzt werden).
