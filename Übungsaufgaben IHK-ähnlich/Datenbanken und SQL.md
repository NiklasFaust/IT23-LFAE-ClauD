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