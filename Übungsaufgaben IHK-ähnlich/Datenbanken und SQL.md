### 2. Handlungsschritt (25 Punkte)

**Ausgangssituation:** Die _FlexDesk GmbH_ bietet in verschiedenen Städten moderne Co-Working-Räume an. Für die Verwaltung der Standorte, Kunden und Buchungen wurde eine relationale Datenbank erstellt.

Ihnen liegen die folgenden Tabellenauszüge der Datenbank vor:

**Tabelle: Standort** 

| St_ID (PK) | St_Stadt | St_Adresse       |
| :--------- | :------- | :--------------- |
| 1          | Berlin   | Alexanderplatz 4 |
| 2          | Hamburg  | Reeperbahn 10    |
| 3          | München  | Marienplatz 1    |

**Tabelle: Kunde** 

| Kd_ID (PK) | Kd_Name       | Kd_Firma          |
| :--------- | :------------ | :---------------- |
| 101        | Müller, Jan   | WebSolutions GmbH |
| 102        | Schmidt, Anna | NULL              |
| 103        | Kaya, Ali     | TechCorp AG       |

**Tabelle: Raum** 

| Rm_ID (PK) | Rm_StID (FK) | Rm_Bezeichnung  | Rm_Tagespreis | Rm_MaxPersonen |
| :--------- | :----------- | :-------------- | :------------ | :------------- |
| 50         | 1            | Meetingraum A   | 120.00        | 8              |
| 51         | 1            | Konferenzraum B | 250.00        | 20             |
| 52         | 2            | Kreativ-Space   | 90.00         | 5              |

**Tabelle: Buchung** 

| Bu_ID (PK) | Bu_KdID (FK) | Bu_RmID (FK) | Bu_Datum   | Bu_Tage | Bu_Storniert |
| :--------- | :----------- | :----------- | :--------- | :------ | :----------- |
| 5001       | 101          | 50           | 2024-03-15 | 2       | 0            |
| 5002       | 103          | 51           | 2024-04-10 | 1       | 0            |
| 5003       | 101          | 52           | 2024-05-02 | 3       | 1            |

_(Hinweis: Das Feld_ _Bu_Storniert_ _ist als Boolean / numerisch umgesetzt: 1 = storniert, 0 = nicht storniert)._

Zur Abfrage und Pflege der Daten sollen nachfolgende SQL-Anweisungen erstellt werden. Nutzen Sie dafür die übliche IHK-SQL-Syntax.

**Aufgaben:**

**a)** Erstellen Sie eine SQL-Anweisung, die eine Liste aller Räume am Standort "Hamburg" ausgibt, deren Tagespreis unter 100,00 EUR liegt. Ausgegeben werden sollen die Bezeichnung des Raums, der Tagespreis sowie die maximale Personenanzahl. _(5 Punkte)_

**b)** Erstellen Sie eine SQL-Anweisung, die eine Liste mit dem Namen und dem Firmennamen aller Kunden ausgibt, die im Jahr 2024 eine Buchung für mehr als 2 Tage getätigt haben. Die Liste darf **keine doppelten** Einträge enthalten. _(8 Punkte)_

**c)** Die Geschäftsführung benötigt eine Umsatzstatistik pro Stadt. Erstellen Sie eine SQL-Anweisung, die für jede Stadt die **Anzahl der Buchungen** sowie den berechneten **Gesamtumsatz** (Berechnung: `Bu_Tage * Rm_Tagespreis`) ausgibt. Stornierte Buchungen (`Bu_Storniert = 1`) dürfen dabei **nicht** in die Berechnung einfließen. _(8 Punkte)_

**d)** Aufgrund eines Systemfehlers müssen alte Daten korrigiert werden. Erstellen Sie eine SQL-Anweisung, die bei allen Buchungen des Kunden mit der ID `101` den Status `Bu_Storniert` auf `1` (wahr) setzt, sofern das Buchungsdatum (`Bu_Datum`) _vor_ dem 01.01.2024 liegt. _(4 Punkte)_

--------------------------------------------------------------------------------

### Musterlösung und Bewertungshinweise

🔐β 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 🔐