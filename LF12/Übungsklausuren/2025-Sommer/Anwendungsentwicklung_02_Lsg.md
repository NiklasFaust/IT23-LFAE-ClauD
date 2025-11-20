# IHK Abschlussprüfung - Lösungen
**Fach:** Anwendungsentwicklung  
**Datum:** 7. Mai 2025

---

## Aufgabe 1 (25 Punkte): Bettenauslastung ermitteln

**Pseudocode-Lösung:**

```
Funktion ermittleAuslastungsTage(belegung : Belegung[], 
                                   startDatum : Date, 
                                   endDatum : Date, 
                                   station : Station) : Integer
    
    // Initialisierung
    tageUeber80Prozent := 0
    aktuellesDatum := startDatum
    stationId := station.getStationId()
    gesamtBetten := station.getAnzahlBetten()
    schwellwert := gesamtBetten * 0.8  // 80% der Betten
    
    // Iteration über alle Tage im Zeitraum
    Solange aktuellesDatum <= endDatum
        
        // Zähler für belegte Betten an diesem Tag und Station
        belegteBetten := 0
        
        // Prüfe alle Belegungseinträge
        Für i := 0 bis belegung.length - 1
            aktuelleBelegung := belegung[i]
            
            // Prüfe ob Belegung zur gesuchten Station gehört
            Wenn aktuelleBelegung.getStationId() = stationId Dann
                
                belegungsStart := aktuelleBelegung.getDatumVon()
                belegungsEnde := aktuelleBelegung.getDatumBis()
                
                // Prüfe ob aktuellesDatum im Belegungszeitraum liegt
                // datumBis zählt NICHT als Belegungstag
                Wenn aktuellesDatum >= belegungsStart UND 
                   aktuellesDatum < belegungsEnde Dann
                    
                    belegteBetten := belegteBetten + 1
                Ende Wenn
            Ende Wenn
        Ende Für
        
        // Prüfe ob Schwellwert überschritten
        Wenn belegteBetten > schwellwert Dann
            tageUeber80Prozent := tageUeber80Prozent + 1
        Ende Wenn
        
        // Nächster Tag
        aktuellesDatum := aktuellesDatum + 1
    Ende Solange
    
    Rückgabe tageUeber80Prozent
Ende Funktion
```

**Alternative Version mit Parameter stationId : Integer, anzahlBetten : Integer:**

```
Funktion ermittleAuslastungsTage(belegung : Belegung[], 
                                   startDatum : Date, 
                                   endDatum : Date, 
                                   stationId : Integer, 
                                   anzahlBetten : Integer) : Integer
    
    tageUeber80Prozent := 0
    aktuellesDatum := startDatum
    schwellwert := anzahlBetten * 0.8
    
    Solange aktuellesDatum <= endDatum
        belegteBetten := 0
        
        Für i := 0 bis belegung.length - 1
            Wenn belegung[i].getStationId() = stationId Dann
                belegungsStart := belegung[i].getDatumVon()
                belegungsEnde := belegung[i].getDatumBis()
                
                Wenn aktuellesDatum >= belegungsStart UND 
                   aktuellesDatum < belegungsEnde Dann
                    belegteBetten := belegteBetten + 1
                Ende Wenn
            Ende Wenn
        Ende Für
        
        Wenn belegteBetten > schwellwert Dann
            tageUeber80Prozent := tageUeber80Prozent + 1
        Ende Wenn
        
        aktuellesDatum := aktuellesDatum + 1
    Ende Solange
    
    Rückgabe tageUeber80Prozent
Ende Funktion
```

---

## Aufgabe 2 (25 Punkte): Medikationsplan und Testing

### a) Sequenzdiagramm (19 Punkte)

```plaintext
                       ┌─────────┐             ┌──────────────────┐             ┌───────────────────────┐
                       │  UI     │             │  Medikation      │             │ MedikamentenVerwaltung│
                       └────┬────┘             └────────┬─────────┘             └──────────┬────────────┘
                            │                           │                                  │
ausgabeMedikationsplan()     │                           │                                  │
   ───────────────────────>  │                           │                                  │
                            │                           │                                  │
                            │                           │ getMedikamente(patient)          │
		                    │                           │────────────────────────────────> │
		                    │                           │                                  │
		                    │                           │      [Rückgabe: Medikament[]]    │
		                    │                           │<──────────────────────────────── │
		                    │                           │                                  │
		                    │                           │ LOOP für jedes Medikament        │
		                    │                           │                                  │
		                    │                           │ getEinnahme(medikament, patient) │
		                    │                           │────────────────────────────────> │
		                    │                           │                                  │
		                    │                           │ [Prüfung: String leer?]          │
		                    │                           │<-------------------------------- │
		                    │                           │                                  │
		                    │      [String = ""]        │                                  │
		                    │─────────────────────>     │ getStandardMedikation(medikament)│
		                    │                           │────────────────────────────────> │
		                    │                           │                                  │
		                    │                           │ [Rückgabe: Standard-Einnahme]    │
		                    │                           │<──────────────────────────────── │
		                    │                           │                                  │
		                    │                           │ [Ermittelte Einnahme]            │
		                    │                           │<──────────────────────────────── │
		                    │                           │                                  │
		                    │                           │ ausgabeMedikation(medikation)    │
		                    │                           │─────────────────────────────────>│
		                    │                           │                                  │
		                    │                           │ END LOOP                         │
		                    │                           │                                  │
		                    │                           │                                  │
```

**Notation:** Das Sequenzdiagramm zeigt:
1. UI ruft `ausgabeMedikationsplan()` auf
2. Abruf der Medikamentenliste via `getMedikamente()`
3. Loop über alle Medikamente
4. Pro Medikament: `getEinnahme()` abrufen
5. Wenn Return-Wert leer: `getStandardMedikation()` als Alternative
6. Ausgabe via `ausgabeMedikation()`

### b) Testing (6 Punkte)

**ba) Überdeckungstest (2 Punkte):**
Geeignete Art: **Branch Coverage (Zweigüberdeckung)**
- Begründung: Die Methode enthält bedingte Verzweigungen (IF-ELSE-Struktur: Arzt-Vorgabe vs. Standard-Medikation). Branch Coverage stellt sicher, dass jede Entscheidung (beide Zweige) mindestens einmal durchlaufen wird, was kritische Fehler bei der Logik aufdeckt.

**bb) Whiteboxtest (2 Punkte):**
Merkmale:
- Tester kennt den internen Programmcode/Algorithmus
- Testfälle basieren auf Code-Struktur (Anweisungen, Zweige, Pfade)
- Ziel: Prüfung derinneren Logik, Datenflüsse und Bedingungen
- Gegensatz zu Blackbox-Tests: hier nur Schnittstelle bekannt

**bc) Leerzeichen-Problem (2 Punkte):**
Vorgehensweise:
1. **Trimmen** des Strings (entfernen führender/nachfolgender Leerzeichen)
2. **Prüfen** ob resultierender String leer ist
3. **Entscheidung**: Wenn nach Trim nicht leer → behalten; wenn leer → als "keine Vorgabe" behandeln → Fallback auf Standard-Medikation
4. **Fehlerbehandlung**: Optional Logging für Administratoren

---

## Aufgabe 3 (23 Punkte): Datenmodell Erweiterung

**Erweitertes relationales Datenmodell (3NF):**

```sql
-- Bestehende Tabellen (vereinfacht)
Patient (Pat_ID [PK], Name, ...)
Arzt (Art_ID [PK], Name, ...)
OP_Saal (OPS_ID [PK], Bezeichnung)
Medikament (Med_ID [PK], Name)

-- NEU: Tabelle Operation
CREATE TABLE Operation (
    OP_ID INT PRIMARY KEY,
    Datum DATE NOT NULL,
    Uhrzeit TIME NOT NULL,
    Pat_ID INT NOT NULL FOREIGN KEY REFERENCES Patient(Pat_ID),
    OPS_ID INT NOT NULL FOREIGN KEY REFERENCES OP_Saal(OPS_ID),
    OP_Art_ID INT NOT NULL FOREIGN KEY REFERENCES Operationsart(OP_Art_ID),
    Anaesthesie_ID INT FOREIGN KEY REFERENCES Anaesthesie(Anaesthesie_ID),
    Besonderheiten TEXT
);

-- NEU: Tabelle Operationsart
CREATE TABLE Operationsart (
    OP_Art_ID INT PRIMARY KEY,
    Bezeichnung VARCHAR(100) NOT NULL,
    Kurzbeschreibung TEXT
);

-- NEU: Tabelle Funktion
CREATE TABLE Funktion (
    F_ID INT PRIMARY KEY,
    Bezeichnung VARCHAR(100) NOT NULL,
    Kurzbeschreibung TEXT
);

-- NEU: Zuordnungstabelle Operation_Arzt (M:N)
CREATE TABLE Operation_Arzt (
    OP_ID INT FOREIGN KEY REFERENCES Operation(OP_ID),
    Art_ID INT FOREIGN KEY REFERENCES Arzt(Art_ID),
    F_ID INT NOT NULL FOREIGN KEY REFERENCES Funktion(F_ID),
    PRIMARY KEY (OP_ID, Art_ID)
);
-- Kardinalität: Operation 1:N Operation_Arzt, Arzt 1:N Operation_Arzt
-- Funktion: jeder Arzt hat genau eine Funktion pro Operation

-- NEU: Tabelle Anaesthesie
CREATE TABLE Anaesthesie (
    Anaesthesie_ID INT PRIMARY KEY,
    Geplante_Dauer_Minuten INT NOT NULL,
    Med_ID INT FOREIGN KEY REFERENCES Medikament(Med_ID),
    Bezeichnung VARCHAR(100)
);
-- Kardinalität: Anaesthesie 1:N Operation (pro Operation max. 1 Anaesthesie, 
-- aber gleiche Anaesthesie kann bei mehreren Operationen verwendet werden)
```

**Kardinalitäten und Schlüssel:**
- **Operation**: 1:N zu Patient, OP_Saal, Operationsart, Anaesthesie (jeweils Fremdschlüssel)
- **Operation_Arzt**: M:N zwischen Operation und Arzt aufgelöst, mit zusätzlichem Fremdschlüssel zu Funktion
- **Funktion**: 1:N zu Operation_Arzt
- **Operationsart**: 1:N zu Operation
- **Anaesthesie**: 1:N zu Operation (optional)
- **Medikament**: 1:N zu Anaesthesie

---

## Aufgabe 4 (27 Punkte): SQL-Anweisungen

### a) Neuen Arzt hinzufügen (3 Punkte)
```sql
INSERT INTO Aerzte (Vorname, Nachname, Fachgebiet, Email)
VALUES ('Hugo', 'Horner', 'Allgemeinmedizin', 'hhorner@fit.de');
```

### b) Schreibrechte gewähren (3 Punkte)
```sql
GRANT INSERT, UPDATE, DELETE ON NotaufnahmeManagement.Verschreibungen TO hhorner;
```

### c) Schreibrechte entziehen (3 Punkte)
```sql
REVOKE INSERT, UPDATE, DELETE ON NotaufnahmeManagement.Verschreibungen FROM skinkel;
```

### d) Email-Pflichtfeld mit Default (5 Punkte)
```sql
-- Schritt 1: Fehlende Email-Adressen ergänzen
UPDATE Aerzte 
SET Email = 'info@fit.de' 
WHERE Email IS NULL;

-- Schritt 2: Spalte auf NOT NULL setzen
ALTER TABLE Aerzte 
MODIFY COLUMN Email VARCHAR(255) NOT NULL;
```

### e) Patienten mit >= 3 Verschreibungen (8 Punkte)
```sql
SELECT 
    p.PID,
    p.Nachname,
    p.Vorname,
    COUNT(v.VID) AS Anzahl_Verschreibungen
FROM Patienten p
JOIN Verschreibungen v ON p.PID = v.PID
GROUP BY p.PID, p.Nachname, p.Vorname
HAVING COUNT(v.VID) >= 3
ORDER BY Anzahl_Verschreibungen DESC;
```

### f) Durchschnitt Verschreibungen pro Patient (5 Punkte)
```sql
SELECT 
    AVG(Anzahl_Verschreibungen) AS Durchschnitt_Verschreibungen_pro_Patient
FROM (
    SELECT 
        p.PID,
        COUNT(v.VID) AS Anzahl_Verschreibungen
    FROM Patienten p
    JOIN Verschreibungen v ON p.PID = v.PID
    GROUP BY p.PID
) AS Patienten_Verschreibungen;
```

