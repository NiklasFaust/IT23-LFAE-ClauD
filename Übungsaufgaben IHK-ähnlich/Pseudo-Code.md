### 4. Handlungsschritt (25 Punkte)

**Ausgangssituation:** Die _ChargeSmart GmbH_ betreibt in einer Großstadt ein Netz von 50 E-Ladesäulen (die Ladesäulen-IDs sind fortlaufend von 0 bis 49 vergeben). Um die Auslastung zu analysieren, werden alle Ladevorgänge in einem System protokolliert.

Die Daten liegen in einem eindimensionalen Array `logs` vor. Jedes Element in diesem Array ist ein Objekt der Klasse `Ladevorgang`.

Ihnen liegt folgende Klassendokumentation vor:

**Klasse: Ladevorgang**

- **Attribute:**
    - `stationID : Integer` (ID der Ladesäule, Werte von 0 bis 49)
    - `geladeneKWh : Double` (Geladene Energiemenge in Kilowattstunden)
    - `dauerMinuten : Integer` (Dauer des Ladevorgangs in Minuten)
    - `monat : Integer` (Monat des Ladevorgangs, 1 = Januar ... 12 = Dezember)
- **Methoden:**
    - Für jedes Attribut existiert eine entsprechende, öffentliche Getter-Methode (z. B. `getStationID() : Integer`, `getGeladeneKWh() : Double`, etc.).

**Aufgabe:** Das Management benötigt eine Auswertung, welche Ladesäule in einem bestimmten Monat die **meiste Energie (in kWh) insgesamt** abgegeben hat. Um Fehlmessungen und abgebrochene Ladevorgänge herauszufiltern, dürfen nur Ladevorgänge in die Berechnung einfließen, die eine **bestimmte Mindestdauer** erreicht oder überschritten haben.

Entwerfen Sie einen Algorithmus für die Funktion: `ermittleTopStation(logs: Ladevorgang[], suchMonat: Integer, minDauer: Integer) : Integer`

Der Algorithmus soll:

1. Nur Ladevorgänge berücksichtigen, die im übergebenen `suchMonat` stattgefunden haben und deren Dauer mindestens `minDauer` Minuten beträgt.
2. Die geladenen Kilowattstunden für jede gültige `stationID` aufsummieren.
3. Die `stationID` der Ladesäule ermitteln und zurückgeben, die in der Summe den höchsten gültigen Energieumsatz erzielt hat. (Gehen Sie davon aus, dass es einen eindeutigen Spitzenreiter gibt).

Stellen Sie den Algorithmus in Pseudocode dar. Nutzen Sie die klassische, sprachunabhängige Notation. Für die Array-Länge können Sie `logs.length` oder `laenge(logs)` verwenden. _(25 Punkte)_

---

---
🔐β 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 🔐
