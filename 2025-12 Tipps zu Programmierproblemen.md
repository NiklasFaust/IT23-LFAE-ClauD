# 🎓 IHK Prüfungsvorbereitung: Algorithmen & Pseudocode
**Cheat Sheet für Anwendungsentwickler (AP2 Teip 2)**

Dieses Dokument fasst die häufigsten Fehlerquellen zusammen, die in Prüfungen Punkte kosten, und zeigt, wie man sie vermeidet.

---

## 🛑 Die 5 häufigsten Fehler (und wie man sie löst)

### 1. Der "Harakiri-Pilot" (Absturz bei leeren Listen)
**Situation:** Du sollst das Minimum/Maximum finden (z. B. "Bester Tisch").
**Der Fehler:** Du greifst sofort auf das erste Element zu, ohne zu prüfen, ob die Liste überhaupt Einträge hat.

❌ **Falsch (Gefährlich):**
```java
Tisch bester = freieTische.get(0); // 💥 Bumm! Absturz, wenn Liste leer ist.
For (i = 1; i < freieTische.size(); i++) { ... }

✅ Richtig (Safe):
// Die "Türsteher"-Methode (Guard Clause)
If (freieTische.size() == 0) {
    Return null; // Oder leere Liste, je nach Aufgabe
}
Tisch bester = freieTische.get(0); // Jetzt ist es sicher!

2. Die "Verschachtelungs-Falle" (Zu früh hinzugefügt)
Situation: Du hast zwei Listen (z. B. Tische und Reservierungen) und willst prüfen, ob ein Tisch frei ist.
Der Fehler: Du nutzt else in der inneren Schleife. Das führt dazu, dass ein Tisch fälschlicherweise mehrfach oder zu früh hinzugefügt wird.
❌ Falsch:
For (tisch in alleTische) {
    For (res in reservierungen) {
        If (tisch.nr == res.nr) {
            Break; // Tisch ist belegt
        } Else {
            // 💥 FEHLER! Der Tisch wird für JEDE Reservierung,
            // die NICHT passt, hinzugefügt (Duplikate!).
            ergebnisListe.add(tisch); 
        }
    }
}

✅ Richtig (Das Flag-Prinzip):
For (tisch in alleTische) {
    Boolean istReserviert = false; // 🚩 Wir nehmen erstmal an, er ist frei

    For (res in reservierungen) {
        If (tisch.nr == res.nr && res.datum == datum) {
            istReserviert = true; // 🚩 Treffer! Flag setzen
            Break; // Wir wissen Bescheid, raus hier.
        }
    }

    // Erst NACH der inneren Schleife entscheiden!
    If (istReserviert == false) {
        ergebnisListe.add(tisch);
    }
}

3. Der "Mathe-Flüchtigkeitsfehler" (Randbedingungen)
Situation: Textaufgaben wie "Der Tisch muss mindestens zur Hälfte besetzt sein".
Der Fehler: Es wird nur geprüft, ob die Gruppe reinpasst, aber nicht, ob der Tisch zu groß ist.
❌ Falsch:
If (tisch.maxPersonen >= gruppenGrosse) { ... }
// Erlaubt: 2 Personen an einem 20er Tisch. Unwirtschaftlich!

✅ Richtig:
// 1. Passt die Gruppe rein? (Kapazität)
// 2. Ist der Tisch voll genug? (Wirtschaftlichkeit / >= 50%)
If (tisch.maxPersonen >= gruppenGrosse AND gruppenGrosse >= tisch.maxPersonen / 2) { 
    ... 
}

4. Der "Schnittstellen-Ignorant" (Falsche Datentypen)
Situation: Die Aufgabe verlangt als Rückgabe List<Tisch>, aber du arbeitest mit Nummern.
Der Fehler: Du gibst List<Integer> oder einen einzelnen String zurück.
❌ Falsch:
// Aufgabe verlangt Objekte!
Return tisch.getNr(); 

✅ Richtig:
// Objekt zur Liste hinzufügen und Liste zurückgeben
ergebnisListe.add(tischObject);
Return ergebnisListe;

🛠 Das "Universal-Rezept" für Filter-Aufgaben
Fast jede IHK-Aufgabe folgt dem Muster: "Nimm Liste A, filtere alles raus, was in Liste B steht oder Bedingung X nicht erfüllt."
Hier ist die Musterlösung, die fast immer funktioniert:
Funktion filtereObjekte(listeA, listeB, kriterien)
    
    // 1. Ergebnis-Liste erstellen
    ergebnisListe = neu Liste()

    // 2. Hauptschleife über die Kandidaten
    Für jedes (objektA in listeA) tue:

        // 3. Einfache Kriterien zuerst prüfen (Performance!)
        Wenn (objektA.groesse < kriterium) Dann
            Continue // Nächster Durchlauf
        Ende Wenn

        // 4. Das Flag für die Prüfung gegen Liste B
        istBlockiert = falsch

        // 5. Innere Schleife (Abgleich mit "Verbots-Liste")
        Für jedes (objektB in listeB) tue:
            Wenn (objektA.id == objektB.id) Dann
                istBlockiert = wahr
                Break // Sofort raus, wir haben einen Blocker gefunden
            Ende Wenn
        Ende Für

        // 6. Entscheidung: Nur hinzufügen, wenn NICHT blockiert
        Wenn (istBlockiert == falsch) Dann
            ergebnisListe.add(objektA)
        Ende Wenn

    Ende Für

    // 7. Rückgabe
    Return ergebnisListe

Ende Funktion

🚀 Checkliste für die letzten 5 Minuten der Prüfung
Bevor du abgibst, prüfe diese 4 Punkte:
 * [ ] Leere Liste? Habe ich if size == 0 bedacht?
 * [ ] Rückgabetyp? Gebe ich das zurück, was im Methodenkopf steht (z.B. List<Tisch> statt Tisch)?
 * [ ] Grenzwerte? Habe ich < oder <= benutzt? (Bei "mindestens" immer >=).
 * [ ] Schleifen-Logik? Füge ich wirklich nur nach der Prüfung hinzu und nicht in der Schleife?


