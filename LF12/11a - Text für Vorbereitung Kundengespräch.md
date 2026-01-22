### Leitfaden zur Gesprächsvorbereitung (30 Minuten)

Fokus auf den **Requirements (Anforderungen)** und dem **Prozess**.

#### 1. Rollenverteilung & Setup (5 Minuten)

Damit das Gespräch nicht chaotisch verläuft, müssen Verantwortlichkeiten geklärt werden:

- **Moderator:** Begrüßt die Kundin, führt durch die Agenda, achtet auf die Zeit.
- **Protokollant:** Schreibt _alles_ mit (Requirements, Wünsche, No-Gos).
- **Fragesteller:** 1-2 Personen, die die Hauptfragen stellen (vermeidet, dass alle durcheinander reden).
- **Zielsetzung klären:** Was wollen wir am Ende des Gesprächs haben? (Ziel: Ein grobes Verständnis der **User Stories** und der **rechtlichen Rahmenbedingungen**).
#### 2. Domain-Check & Rechtliches (5-10 Minuten)

Bevor man den Kunden fragt, muss man wissen, worum es geht. Ein digitales Verbandsbuch ist kein normales CRUD-Projekt.
- **Recherche (Kurz!):** Was _muss_ in einem Verbandsbuch stehen? (Stichwort: **DGUV Information 204-022**).
    - _Tipp für die Azubis:_ Nicht die Kundin fragen "Was soll da rein?", sondern fragen: "Wir wissen, dass gesetzlich Ort, Zeit, Unfallhergang, Art der Verletzung und Name des Ersthelfers erfasst werden müssen. Gibt es darüber hinaus schulspezifische Daten, die Sie brauchen?" Das wirkt viel kompetenter.
        
- **Das Elefanten-Thema (Datenschutz):** Gesundheitsdaten sind nach DSGVO Art. 9 "besonderer Kategorie".
    - Fragen vorbereiten zu: Wer darf das lesen? Wie lange darf es gespeichert werden (Löschfristen)? Wer darf exportieren?

#### 3. Fragenkatalog erstellen (10 Minuten)

Fragen in Kategorien clustern. Hier sind die wichtigsten Blöcke für das Verbandsbuch:

**A. Der Prozess (Workflow)**

- Wo passiert die Eintragung? (Im Sekretariat? Am Unfallort per Tablet? Im Lehrerzimmer?)
- Wer trägt ein? (Nur Schulsanitäter? Jede Lehrkraft? Das Sekretariat?)
- Was passiert nach dem Eintrag? (Muss jemand benachrichtigt werden? BGM-Beauftragte? Schulleitung?)

**B. Die Benutzer (User Experience)**
- Wie technikaffin sind die Nutzer? (Muss die Oberfläche extrem simpel sein?)
- Wie schnell muss es gehen? (In Panik-Situationen darf kein langes Login-Verfahren stören).

**C. Reporting & Auswertung**
- Was macht die BGM-Beauftragte mit den Daten?
- Braucht sie eine Statistik (z. B. "Wo passieren die meisten Unfälle?")?
- Muss ein Export für die Unfallkasse generiert werden?

**D. Migration (Altlasten)**
- Was passiert mit den alten Heften? (Bleiben die im Schrank oder sollen Daten übertragen werden? -> _Hoffentlich nicht, das sprengt meist den Rahmen_).

#### 4. Visualisierung vorbereiten (5 Minuten)

Wenn noch Zeit ist:
- Ein Blatt Papier nehmen und eine ganz grobe **Skizze (Wireframe)** machen, wie das Formular aussehen könnte.
- Das hilft im Gespräch ungemein: "Meinen Sie so ungefähr? Oder fehlen hier Felder?"

## Spickzettel

| **Do (Machen)**                                                                                        | **Don't (Vermeiden)**                                                                                |
| ------------------------------------------------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------- |
| **Offene Fragen stellen** ("Wie sieht Ihr aktueller Ablauf aus?", "Was stört Sie am Heft am meisten?") | **Fachchinesisch nutzen** ("Wollen Sie eine REST-API?", "Soll das Frontend in React sein?")          |
| **Zuhören & Bestätigen** ("Habe ich Sie richtig verstanden, dass nur Sie die Einträge lesen dürfen?")  | **Lösungen vorwegnehmen** ("Wir machen da einfach eine App, die alles kann.")                        |
| **Schmerzpunkte finden** ("Warum wollen Sie weg vom Papier? Was läuft schief?")                        | **Feature-Creep** (Dem Kunden Dinge versprechen, die er gar nicht verlangt hat, z.B. KI-Auswertung.) |