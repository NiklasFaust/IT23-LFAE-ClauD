### Aufgabe 1: Einführung in die Normalisierung

**Musterlösung:**

- **Erste Normalform (1NF):** Eine Tabelle ist in der Ersten Normalform, wenn alle Spalten atomar sind, das heißt, jede Zelle enthält nur einen Wert und alle Einträge einer Spalte den gleichen Datentyp haben.


| Vorname | Nachname | PLZ   | Ort       |
| ------- | -------- | ----- | --------- |
| Peter   | Lustig   | 24768 | Rendsburg |


- **Zweite Normalform (2NF):** Eine Tabelle ist in der Zweiten Normalform, wenn sie bereits in der 1NF ist und alle Nicht-Schlüsselattribute vollständig funktional abhängig vom Primärschlüssel sind. Das bedeutet, dass keine Teilschlüsselabhängigkeiten vorhanden sind.


| Vorname | Nachname | PLZ   | Ort       | Automarke | FarbeAuto |
| ------- | -------- | ----- | --------- | --------- | --------- |
| Peter   | Lustig   | 24768 | Rendsburg | Toyota    | silber    |
| Ursula  | Übel     | 24112 | Kiel      | VW        | gelb      |


- **Dritte Normalform (3NF):** Eine Tabelle ist in der Dritten Normalform, wenn sie bereits in der 2NF ist und keine Nicht-Schlüsselattribute transitiv abhängig vom Primärschlüssel sind. Das bedeutet, dass keine indirekten Abhängigkeiten existieren.



- **Vorteile der Normalisierung:**
  1. Reduzierung von Datenredundanz.
  2. Verbesserung der Datenintegrität.
  3. Effiziente Nutzung des Speicherplatzes.
  
- **Probleme bei nicht normalisierten Datenbanken:**
  - Dateninkonsistenzen durch redundante Datenspeicherung.
  - Schwierigkeiten bei der Pflege und Aktualisierung von Daten.
  - Ineffiziente Abfragen aufgrund unnötiger Komplexität.

### Aufgabe 2: Anwendung der Ersten Normalform

**Musterlösung:**

Die gegebene Tabelle hat mehrere Artikelspalten (`Artikel1`, `Artikel2`, `Artikel3`), was gegen die Regel verstößt, dass jede Zelle nur einen Wert enthalten sollte.

Um die Tabelle in die Erste Normalform zu bringen:
- Erzeugen Sie eine neue Zeile für jeden Artikel pro Bestellung:
  
```
Bestellnummer | Kunde | Artikel
--------------------------------
1001          | Schmidt | Artikel A
1001          | Schmidt | Artikel B
1001          | Schmidt | Artikel C
```

Hier wird jeder Artikel als separate Zeile dargestellt.

### Aufgabe 3: Übergang zur Zweiten Normalform

**Musterlösung:**

Identifizierte funktionale Abhängigkeiten:
- `Bestellnummer` → `Kunde`, `KundenAdresse`
- `ArtikelID` → `ArtikelName`

Um die Tabelle in die Zweite Normalform zu bringen:
- Zerlegen Sie die Tabelle basierend auf den funktionalen Abhängigkeiten:

Tabelle Bestellungen:
```
Bestellnummer | Kunde | KundenAdresse
--------------------------------------
1001          | Müller   | Straße A 
```

Tabelle Bestellpositionen:
```
Bestellnummer | ArtikelID | Menge
---------------------------------
1001          | A123      | 10   
```

Tabelle Artikel:
```
ArtikelID     | ArtikelName 
---------------------------
A123          | Stuhl      
```

### Aufgabe 4: Dritte Normalform erreichen

**Musterlösung:**

Funktionale Abhängigkeiten identifizieren:
- `ArtikelID` → `ArtikelName`
- `LieferantID` → `LieferantName`, `LieferantAdresse`

Um die Struktur in die Dritte Normalform zu bringen:

Tabelle Artikel:
```
ArtikelID     | ArtikelName 
---------------------------
A123          | Stuhl      
```

Tabelle Lieferanten:
```
LieferantID   | LieferantName    | LieferantAdresse
--------------------------------------------------
L001          | Lieferant GmbH   | Hauptstraße B   
```

Tabelle Lieferung:
```
ArtikelID     | LieferantID 
----------------------------
A123          | L001        
``` 

### Aufgabe 5: Analyse eines bestehenden Systems

**Musterlösung:**

Ein einfaches Shop-System analysieren:

Aktuelle Struktur (fiktives Beispiel):
- Produkte(Product_ID, Name, Preis)
- Bestellungen(Order_ID, Product_IDs[], Kunde)

Analyse zeigt fehlende Trennung von Produkten und Bestellungen sowie redundante Speicherung von Kundendaten.

Vorschläge für Verbesserungen zur Erreichung mindestens der dritten NF:

Neues Schema:

Tabelle Produkte bleibt unverändert.
Zusätzlich erstellen Sie eine separate Tabelle für Kunden und eine Join-Tabelle für Bestellungen und Produkte. Nachteile könnten zahlreiche Joins bei komplexen Abfragen sein.

### Aufgabe 6: Praktische Implementierung

**Musterlösung:** 

Schrittweises Schema für ein Bibliothekssystem:

#### Schritt zur Erstellung des Schemas bis zur Dritten NF

Erste Version des Schemas:

Bücher(Titel, Autor(en), ISBN, Genre)
Mitglieder(Name, Adresse, Telefonnummer)
Ausleihen(Buch_ISBN[], Mitglied_Name[], Datum_Ausleihe)

Nach Analyse von funktionalen Abhängigkeiten führen wir folgende Änderungen durch:

Bücher(ISBN PK , Titel, Genre)
Autoren(Autor_ID PK , Name)
Buch_Autoren(ISBN FK , Autor_ID FK )
Mitglieder(Mitglieds_ID PK , Name, Adresse)
Ausleihen(Ausleihe_ID PK , Buch_ISBN FK , Mitglieds_ID FK , Datum_Ausleihe)

Diese Struktur stellt sicher, dass alle Tabellen bis zur dritten NF normalisiert sind.