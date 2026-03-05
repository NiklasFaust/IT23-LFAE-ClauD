### 1. Handlungsschritt (25 Punkte)

**Ausgangssituation:** Die _DriveSmart GmbH_ ist eine stetig wachsende Autovermietung. Bisher bot das Unternehmen nur Standard-Verbrenner an. Nun wurde die Flotte um Elektroautos und kleine Transporter erweitert.

In der bisherigen Software gibt es eine Klasse `Fahrzeug`, in der die Mietkosten über eine unübersichtliche und fehleranfällige Mehrfachauswahl (Switch-Case/If-Else) berechnet werden:

- **"VERBRENNER"**: Regulärer Tagespreis mal Anzahl der Tage.
- **"E-AUTO"**: Bekommt zur Förderung der Elektromobilität 10 % Umweltrabatt auf den Gesamtpreis.
- **"TRANSPORTER"**: Regulärer Tagespreis mal Anzahl der Tage plus eine einmalige Reinigungspauschale von 50,00 EUR.

Ein erfahrener Kollege rät Ihnen, diese Redundanzen und langen Auswahlstrukturen durch **Polymorphie** aufzulösen, um die Wartbarkeit der Software zu verbessern (gemäß ISO/IEC 25010 Qualitätsmerkmale).

**Aufgaben:**

**a)** Erläutern Sie den Begriff _Polymorphie_ im Kontext der objektorientierten Programmierung und nennen Sie einen konkreten Vorteil für die Wartbarkeit in diesem Szenario. _(4 Punkte)_

**b)** Erstellen Sie ein UML-Klassendiagramm für einen polymorphen Ansatz, der die Redundanzen aus dem bestehenden Code auflöst. Die Basisklasse soll eine statische Methode zur Objekterstellung enthalten. Begründen Sie Ihre Designentscheidungen. _(10 Punkte)_

**c)** Implementieren Sie die Fabrikmethode `createFahrzeug` in Pseudocode oder einem Struktogramm. Der Default-Fall (unbekannter Typ) soll `null` zurückgeben. _(6 Punkte)_

**d)** Implementieren Sie in Pseudocode oder einem Struktogramm die überschreibende Methode `berechneMiete` für die Fahrzeug-Kategorie **"E-AUTO"**. _(3 Punkte)_

**e)** Bei der Konzeption diskutiert das Team, ob `Fahrzeug` eine _abstrakte Klasse_ oder ein _Interface_ (Schnittstelle) sein sollte. Erläutern Sie einen wesentlichen konzeptionellen Unterschied zwischen einer abstrakten Klasse und einem Interface. _(2 Punkte)_

---

### Musterlösung und Bewertungshinweise

**a) Erläuterung Polymorphie (4 Punkte)** _Je 2 Punkte für die Definition und den Vorteil. Sinngemäße Antworten sind gültig._

- **Definition:** Polymorphie (Vielgestaltigkeit) bedeutet, dass eine Methode in verschiedenen Klassen einer Vererbungshierarchie die gleiche Signatur besitzt, aber unterschiedlich implementiert ist. Erst zur Laufzeit wird entschieden (dynamisches Binden), welche spezifische Methode des instanziierten Objekts aufgerufen wird.
- **Vorteil Wartbarkeit:** Wenn in Zukunft eine neue Fahrzeugkategorie (z. B. "LKW") hinzugefügt wird, muss der bestehende Code (wie alte Switch-Case-Blöcke) nicht verändert werden. Es wird einfach eine neue Unterklasse erstellt. Dies reduziert das Risiko von Fehlern in bestehendem Code (Open-Closed-Principle).

**b) UML-Klassendiagramm (10 Punkte)** _Punkteverteilung: 2 Punkte für abstrakte Basisklasse inkl. Kennzeichnung, 3 Punkte für korrekt erkannte Unterklassen mit passenden Namen, 2 Punkte für Vererbungspfeile, 2 Punkte für Methodensignaturen in Basisklasse und Unterklassen, 1 Punkt für Factory-Methode._

``` mermaid
classDiagram
    class Fahrzeug {
        <<abstract>>
        +createFahrzeug(typ: String)$ Fahrzeug
        +berechneMiete(tage: Integer, tagesPreis: Double)* Double
    }

    class Verbrenner {
        +berechneMiete(tage: Integer, tagesPreis: Double) Double
    }

    class ElektroAuto {
        +berechneMiete(tage: Integer, tagesPreis: Double) Double
    }

    class Transporter {
        +berechneMiete(tage: Integer, tagesPreis: Double) Double
    }

    Fahrzeug <|-- Verbrenner
    Fahrzeug <|-- ElektroAuto
    Fahrzeug <|-- Transporter
```

_(Hinweis für den Korrektor: Klassennamen können variieren (z.B. "Benziner", "Elektrofahrzeug" etc.), solange sie semantisch passen. Die Factory-Methode ist eine sinnvolle Lösung, muss aber nicht von allen Schülern erkannt werden - hier Punkte nach Qualität der Gesamtlösung vergeben.)_

---

**c) Pseudocode Fabrikmethode (6 Punkte)** _1 Punkt Methodenkopf, 1 Punkt Selektor/Switch, 3 Punkte für korrekte Objekt-Rückgaben, 1 Punkt für Default-Return (null)._

``` java
public static Fahrzeug createFahrzeug(String typ) {
    switch(typ) {
        case "VERBRENNER":
            return new Verbrenner();
        case "E-AUTO":
            return new ElektroAuto();
        case "TRANSPORTER":
            return new Transporter();
        default:
            return null;
    }
}
```

_(Hinweis: Eine If-Else-Kette ist ebenfalls mit voller Punktzahl zu bewerten)._

**d) Pseudocode `berechneMiete` für E-AUTO (3 Punkte)** _1 Punkt Methodenkopf, 1 Punkt korrekte mathematische Logik, 1 Punkt Return._

``` java
@Override
public Double berechneMiete(Integer tage, Double tagesPreis) {
    Double basisMiete = tage * tagesPreis;
    return basisMiete * 0.90; // 10 Prozent Rabatt abziehen
}
```

**e) Unterschied Abstrakte Klasse vs. Interface (2 Punkte)** _2 Punkte für einen korrekten Unterschied. Zum Beispiel:_

- Eine abstrakte Klasse kann bereits ausprogrammierte Methoden und Instanzvariablen (Attribute) enthalten. Ein Interface darf (klassischerweise) nur Konstanten und Methodensignaturen (ohne Rumpf) vorgeben.
- Oder: In vielen Programmiersprachen (wie Java/C#) kann eine Klasse nur _eine_ abstrakte Klasse erben (keine Mehrfachvererbung), aber _beliebig viele_ Interfaces implementieren.
- 