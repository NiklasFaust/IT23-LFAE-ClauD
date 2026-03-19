# Infoblatt: ER-Diagramm und Relationale Datenmodelle
**Für Fachinformatiker Anwendungsentwicklung (3. Ausbildungsjahr)**

---

## 1. Datenbankmodelle - Übersicht

Es gibt vier Hauptdatenbankmodelle:

| Modell | Merkmal | Einsatzgebiet |
|--------|---------|---------------|
| **Netzwerkmodell** | Datensätze können mehrere Vorgänger haben | Leistungsoptimierte Anwendungen |
| **Hierarchisches Modell** | Baumschema, genau ein Vorgänger pro Datensatz | Legacy-Systeme |
| **Objektorientiertes Modell** | Objektkapselung mit Methoden | OO-Softwareentwicklung |
| **Relationales Modell** ⭐ | Tabellen mit Schlüsselbeziehungen | **Standard für kleine bis große Projekte** |

---

## 2. ER-Diagramm (Entity-Relationship-Modell)

### Definition
Das ER-Modell ist ein **abstraktes Datenmodell** und **Modellierungsinstrument** – es zählt **nicht** zu den Datenbankmodellen.

**siehe auch [[07 - Entity Relationship Modell und Diagramm (ERM und ERD)|07 - Entity Relationship Modell und Diagramm (ERM und ERD)]]**
### Bestandteile

**Entitäten (Entity)**
- Rechteck dargestellt
- Objekte der realen Welt (z.B. Kunde, Fahrzeug)

**Attribute**
- Ovale Darstellung
- Eigenschaften einer Entität (z.B. Name, Geburtsdatum)
- **Primärschlüssel**: Unterstrichen, eindeutige Identifikation

**Beziehungen (Relationship)**
- Raute dargestellt
- Verbindungen zwischen Entitäten

### Kardinalitäten

| Notation | Bedeutung | Beispiel |
|----------|-----------|----------|
| 1:1 | Ein Datensatz zu einem anderen | Ehepartner |
| 1:n | Ein Datensatz zu mehreren | Kunde → Bestellungen |
| n:m | Viele zu vielen | Schüler ↔ Kurse |

---

## 3. Relationales Datenbankmodell

### Grundkonzept
- Daten werden in **Tabellen (Relationen)** gespeichert
- Tabellen werden über **Schlüsselattribute** verknüpft
- Keine Hierarchie zwischen Tabellen

### Schlüsselkonzepte

**Primärschlüssel (PK - Primary Key)**
- Eindeutige Identifikation jedes Datensatzes
- Beispiel: `Kunde_PK`, `Fahrzeug_PK`

**Fremdschlüssel (FK - Foreign Key)**
- Verweis auf Primärschlüssel einer anderen Tabelle
- Beispiel: `Berater_FK` in Tabelle `Chef` → `Berater_PK` in Tabelle `Berater`

### Begriffe

| Begriff | Erklärung |
|---------|-----------|
| **Tabelle** | Relation, strukturierte Datensammlung |
| **Attribut** | Spalte einer Tabelle |
| **Tupel** | Zeile einer Tabelle (Datensatz) |
| **Datentyp** | Festlegung der Attributswerte (text, integer, date, etc.) |

---

## 4. Transformation: ER-Modell → Relationales Modell

### Regeln

1. **Jede Entität** → Eine Tabelle
2. **Attribute der Entität** → Spalten der Tabelle
3. **Primärschlüssel** → Unterstrichenes Attribut wird PK
4. **1:n-Beziehung** → Fremdschlüssel in der Tabelle der "n-Seite"
5. **n:m-Beziehung** → Zwischentabelle mit zwei Fremdschlüsseln

### Beispiel: Chef und Berater

**ER-Modell:**
- Entität: Chef (mit Attributen)
- Entität: Berater (mit Attributen)
- Beziehung: 1:n (ein Berater berät mehrere Chefs)

**Relationales Modell:**
```
Tabelle: Chef
- Chef_PK (Primärschlüssel)
- Vorname, Nachname, Geburtsdatum
- Berater_FK (Fremdschlüssel → Berater.Berater_PK)

Tabelle: Berater
- Berater_PK (Primärschlüssel)
- Vorname, Nachname, Geburtsdatum
```

---

## 5. Praxisbeispiel: Autovermietung "Car4You"

### Kernentitäten

```
Kunde
├── Kunde_PK
├── Name, Adresse
├── Kundenstatus (VIP, Standard)
└── Geburtsdatum (für Altersprüfung)

Fahrzeug
├── Fahrzeug_PK
├── Kennzeichen, Kilometerstand
├── Erstzulassung, Farbe
└── Modell_FK → Fahrzeugmodell

Fahrzeugmodell
├── Modell_PK
├── Bezeichnung, Preis_pro_Tag
└── Klasse_FK → Fahrzeugklasse

Vermietung
├── Vermietung_PK
├── Startdatum, Enddatum
├── Status (reserviert/aktiv/abgeschlossen)
├── Kunde_FK → Kunde
└── Fahrzeug_FK → Fahrzeug
```

---

## 6. Wichtige Hinweise für die Prüfung

### Normalisierung
- Vermeidung von Redundanzen
- 1NF, 2NF, 3NF kennen

### Designprinzipien
✓ Jede Tabelle hat einen Primärschlüssel
✓ Fremdschlüssel referenzieren korrekt
✓ Datentypen sinnvoll wählen
✓ NULL-Werte vermeiden wo möglich

### Häufige Fehler
✗ n:m-Beziehungen ohne Zwischentabelle
✗ Fehlende Fremdschlüssel
✗ Inkonsistente Namenskonventionen

---

## 7. Vergleich der Modelle

| Kriterium | Netzwerk | Hierarchisch | Objektorientiert | Relational |
|-----------|----------|--------------|------------------|------------|
| Struktur | Netz | Baum | Objekte | Tabellen |
| n:m-Beziehungen | ✓ Direkt | ✗ Nicht möglich | ✓ | ✓ Über Zwischentabelle |
| Verbreitung | Gering | Rückläufig | Gering | **Hoch** |
| Komplexität | Mittel | Niedrig | Hoch | Mittel |

---

**Quelle:** Basierend auf der Website "Der Wirtschaftsingenieur" und Fachwissen für Fachinformatiker

Quelle: https://www.der-wirtschaftsingenieur.de/index.php/datenbankmodelle/