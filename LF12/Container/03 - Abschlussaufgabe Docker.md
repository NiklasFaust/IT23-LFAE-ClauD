# Praxisaufgabe: Containerisierte Bibliotheksverwaltung für die Stadtbibliothek Rendsburg

## Ausgangssituation

Die Stadtbibliothek Rendsburg möchte ihr veraltetes Bibliotheksverwaltungssystem modernisieren. Als erster Schritt soll eine containerisierte Prototyp-Lösung entwickelt werden, die die Grundfunktionen der Medienverwaltung abbildet. Das System soll später einfach skalierbar und wartbar sein.

**Deine Aufgabe:** Entwickle eine containerisierte Bibliotheksverwaltung bestehend aus einem Datenbank-Container und einem Web-Frontend-Container.

## Anforderungen

### Teil 1: Datenbank-Container erstellen

1. **Erstelle ein eigenes Docker-Image** basierend auf `mariadb:latest`
   
2. **Das Image soll automatisch beim Start:**
   - Eine Datenbank namens `bibliothek_db` anlegen
   - Eine Tabelle `medien` mit folgender Struktur erstellen:
     - `id` (INT, AUTO_INCREMENT, PRIMARY KEY)
     - `titel` (VARCHAR(255))
     - `autor` (VARCHAR(255))
     - `isbn` (VARCHAR(20))
     - `kategorie` (VARCHAR(100))
     - `verfuegbar` (BOOLEAN, Standard: TRUE)
     - `ausgeliehen_am` (DATE, kann NULL sein)
   
3. **Füge Testdaten ein:**
   - Mindestens 5 verschiedene Medien (Bücher, DVDs, etc.)
   - Unterschiedliche Kategorien (Roman, Sachbuch, Film, etc.)
   - Mindestens ein Medium soll als ausgeliehen markiert sein

4. **Technische Anforderungen:**
   - Verwende ein Initialization-Script (`.sql`-Datei), das beim ersten Start ausgeführt wird
   - Setze ein Root-Passwort und erstelle einen dedizierten Datenbankbenutzer `bibliothek_user` mit entsprechenden Rechten
   - Dokumentiere deine Konfiguration im Dockerfile

### Teil 2: Datenbank-Container starten

5. **Starte den Container mit:**
   - Persistenter Datenspeicherung über ein Docker-Volume
   - Geeigneter Port-Freigabe für externe Zugriffe
   - Aussagekräftigem Container-Namen

### Teil 3: Web-Frontend-Container einrichten

6. **Erstelle einen zweiten Container** mit einem Web-Frontend:
   - Verwende `phpmyadmin/phpmyadmin:latest` als Basis-Image
   - Konfiguriere die Verbindung zum Datenbank-Container
   - Der Container soll automatisch mit dem Datenbank-Container kommunizieren können

7. **Starte den Frontend-Container:**
   - Verbinde ihn mit dem Datenbank-Container (über Docker-Netzwerk oder Container-Linking)
   - Mache das Frontend über Port 8080 auf dem Host erreichbar

### Teil 4: Funktionstest und Dokumentation

8. **Teste die Lösung:**
   - Greife über `http://localhost:8080` auf das Frontend zu
   - Logge dich mit den konfigurierten Credentials ein
   - Führe eine SQL-Abfrage aus, die alle verfügbaren Medien anzeigt
   - Ändere den Status eines Mediums von "verfügbar" auf "ausgeliehen"

8. **Erstelle eine kurze Dokumentation** (`DOKUMENTATION.md`) **mithilfe eines KI-Tools (Achtung, Ergebnis überprüfen), die enthält**:
   - Verwendete Befehle zum Bauen und Starten der Container
   - Zugangsdaten für das System
   - Beschreibung des verwendeten Datenmodells
   - Anleitung zur Verwendung des Systems
   - Mögliche Erweiterungen für ein produktives System

## Erwartete Deliverables

- [ ] `Dockerfile` für den Datenbank-Container
- [ ] SQL-Initialisierungsskript (`init.sql`)
- [ ] Dokumentation mit allen verwendeten Docker-Befehlen

## Hilfestellung

**Docker-Tipps:**
- MariaDB führt automatisch `.sql`-Dateien aus dem Verzeichnis `/docker-entrypoint-initdb.d/` beim ersten Start aus
- Umgebungsvariablen für MariaDB: `MYSQL_ROOT_PASSWORD`, `MYSQL_DATABASE`, `MYSQL_USER`, `MYSQL_PASSWORD`
- Verwende `docker network create` für ein dediziertes Netzwerk zwischen den Containern
- Das Cheat Sheet: [[01b - Docker Cheat Sheet|01b - Docker Cheat Sheet]] hilft dir bei den grundlegenden Befehlen

**Bonus-Aufgabe (optional):**
Erstelle eine `docker-compose.yml`-Datei, die beide Container mit einem Befehl startet und konfiguriert.

---

**Zeitrahmen:** 120-180 Minuten  
**Schwierigkeitsgrad:** Mittel  
**Lernziele:** Dockerfile-Erstellung, Container-Networking, Persistente Datenspeicherung, Praktische Anwendung von Datenbank-Containern