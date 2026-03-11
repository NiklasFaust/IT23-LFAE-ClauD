### 5. Handlungsschritt (25 Punkte)

**Ausgangssituation:** Die _PhysioVital GmbH_ betreibt ein großes Zentrum für Physiotherapie. Bislang wurden alle Behandlungstermine in einer einfachen Tabellenkalkulation (Excel) verwaltet. Um Auswertungen zu erleichtern und Fehler zu vermeiden, soll dieses System durch eine relationale Datenbank abgelöst werden.

Ihnen liegt ein Auszug aus der bisherigen, fehleranfälligen Tabelle vor:

**Tabelle: Behandlungsübersicht**

|Termin_ID|Datum|Uhrzeit|Pat_Nr|Pat_Name|Pat_Krankenkasse|Ther_Nr|Ther_Name|Raum_Nr|Raum_Ausstattung|
|:--|:--|:--|:--|:--|:--|:--|:--|:--|:--|
|1001|12.05.2024|09:00|5012|Müller, Jan|TK|12|Schmidt, Anna|R1|Massageliege|
|1002|12.05.2024|10:00|8334|Kaya, Ali|AOK|12|Schmidt, Anna|R2|Schlingentisch|
|1003|13.05.2024|09:00|5012|Müller, Jan|TK|18|Weber, Tom|R1|Massageliege|

In einem Vorgespräch wurden folgende Sachverhalte und Annahmen für das neue System festgelegt:

- Ein Patient kann im Laufe der Zeit beliebig viele Termine wahrnehmen.
- Ein Therapeut führt viele Termine durch.
- In einem Raum finden nacheinander viele Termine statt.
- Pro Termin (eindeutig identifiziert über die `Termin_ID`) gibt es immer genau einen bestimmten Patienten, genau einen Therapeuten und genau einen Raum.

**Aufgaben:**

**a)** Die dargestellte Tabelle ist nicht normalisiert. Benennen Sie **ein** konkretes Problem (Anomalie), das bei der fortgeführten Nutzung dieser unnormalisierten Tabelle bei Datenänderungen auftreten kann, und erläutern Sie dieses anhand eines Beispiels aus der Tabelle. _(4 Punkte)_

**b)** Erstellen Sie für die geforderte Datenbank ein relationales Datenmodell in der **dritten Normalform (3NF)**.

- Geben Sie den Tabellen und Attributen selbsterklärende Namen.
- Nennen Sie je Tabelle alle erforderlichen Attribute.
- Kennzeichnen Sie Primärschlüssel mit PK und Fremdschlüssel mit FK.
- Zeichnen Sie die Beziehungen mit deren Kardinalitäten (z. B. 1, n, m) ein. _(21 Punkte)_

---

---

### Musterlösung und Bewertungshinweise

🔐β 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 🔐
