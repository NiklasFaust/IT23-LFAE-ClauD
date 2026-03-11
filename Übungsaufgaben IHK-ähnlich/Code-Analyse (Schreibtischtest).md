### 8. Handlungsschritt (25 Punkte)

**Ausgangssituation:** Die _SalesPro GmbH_ berechnet den wöchentlichen Leistungsbonus ihrer Vertriebsmitarbeiter durch einen Algorithmus. Dem Algorithmus wird ein eindimensionales Array `vertraege` übergeben, das die Anzahl der täglich abgeschlossenen Verträge einer Arbeitswoche enthält.

Für die Bonusberechnung hat die Geschäftsführung folgende **drei fachliche Vorgaben** definiert:

1. Für jeden Tag mit **20 oder mehr** abgeschlossenen Verträgen erhöht sich der Multiplikator `streak` um 1. Der Bonus für diesen Tag berechnet sich aus `Verträge * streak` und wird dem `gesamtBonus` hinzugefügt.
2. Schließt der Vertriebler an einem Tag **weniger als 10** Verträge ab, reißt die Erfolgsserie und der `streak` fällt sofort wieder auf `0` zurück.
3. An Tagen mit **10 bis 19** Verträgen (inklusive) bleibt der aktuelle `streak`-Wert unverändert erhalten, es wird an diesem Tag jedoch **kein** Betrag dem `gesamtBonus` hinzugefügt.

Ein Auszubildender hat den folgenden Pseudocode entworfen, der jedoch **zwei logische Fehler** enthält, da er die Vorgaben nicht exakt umsetzt.

**Pseudocode:**

```
01  berechneBonus(vertraege: Integer[]) : Integer
02      gesamtBonus := 0
03      streak := 0
04
05      FÜR i := 0 BIS laenge(vertraege) - 1
06          heute := vertraege[i]
07
08          WENN heute > 20 DANN
09              streak := streak + 1
10              gesamtBonus := gesamtBonus + (heute * streak)
11          SONST
12              WENN heute < 10 DANN
13                  streak := 0
14              SONST
15                  gesamtBonus := gesamtBonus + heute
16              ENDE WENN
17          ENDE WENN
18      ENDE FÜR
19
20      RÜCKGABE gesamtBonus
21  ende berechneBonus
```

Zum Testen des fehlerhaften Algorithmus liegt folgendes Array für eine 4-Tage-Woche vor: `vertraege =`

**Aufgaben:**

**a)** Führen Sie für den **fehlerhaften** Pseudocode des Auszubildenden einen Schreibtischtest (Trace Table) mit den gegebenen Testdaten durch. Tragen Sie die Werte der Variablen am **Ende jedes Schleifendurchlaufs** (also nach Ausführung von Zeile 17) in die Verlaufstabelle ein. Die Initialwerte vor der Schleife sind bereits vorgegeben. _(12 Punkte)_

|Iteration|i|heute|streak|gesamtBonus|
|:--|:--|:--|:--|:--|
|Init|-|-|0|0|
|1. Durchlauf|||||
|2. Durchlauf|||||
|3. Durchlauf|||||
|4. Durchlauf|||||

**b)** Vergleichen Sie das Ergebnis Ihres Schreibtischtests mit den fachlichen Vorgaben der Geschäftsführung. Nennen und beschreiben Sie die **zwei** logischen Fehler, die der Auszubildende gemacht hat. Geben Sie dabei die betroffenen Zeilennummern an. _(4 Punkte)_

**c)** Notieren Sie die **korrigierten Zeilen 08 bis 17**, sodass der Pseudocode alle drei Vorgaben der Geschäftsführung fehlerfrei erfüllt. _(5 Punkte)_

**d)** Erläutern Sie den generellen Zweck eines Schreibtischtests in der Softwareentwicklung und nennen Sie einen entscheidenden Nachteil dieser Methode. _(4 Punkte)_

---

### Musterlösung und Bewertungshinweise
🔐β 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 🔐
---
