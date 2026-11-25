# Smart Campus

> 🏫 **Smart Campus – IoT FHWN**: Pro Raum ein ESP32 mit Sensoren, der per HTTPS Daten an ein Backend sendet. Das Backend speichert in PostgreSQL, ein Dashboard zeigt Raumzustände live (aktualisiert pro Minute).

## 💬 Zu besprechen / offene Entscheidungen

- [ ] **Backend-Sprache** festlegen (Python?)
- [ ] **FH-Netz klären** (DNS, Ports, Domain, Firewall) + Dashboard nur in FH Netz oder auch von außerhalb zugänglich?
- [ ] **Sensoren final auswählen** (Temperatur, Luftfeuchtigkeit, Helligkeit, Bewegung, optional CO2 oder weitere)
- [ ] **Definition der Berechnungen** festlegen: Wann gilt ein Raum als „belegt“ und wann ein „Fenster offen“? (Welche Sensoren, welche Schwellwerte?)
- [ ] **Datenformat und Datenmodell der Sensormeldung (API)** abstimmen, da Firmware und Backend davon abhängen

## ✅ Festgelegt

- ESP-Seite: C++
- Datenbank: PostgreSQL auf eigenem DB-Server (Docker-Container)
- Dashboard: im Campusnetz, lesend öffentlich?

## 🛠️ Aufgaben (in sinnvoller Reihenfolge)

### 1. Grundlagen

- [ ] Programmiersprachen abklären (ESP: C++, DB: PostgreSQL, Backend: offen)
- [ ] IoT-Netz der FH, DNS, Ports und Domain abklären
- [ ] Datenformat und Datenmodell der Sensormeldung (API) festlegen
- [ ] Sensoren auswählen

### 2. ESP / Firmware

- [ ] Pro Sensor Code schreiben und den jeweiligen Sensor auslesen
- [ ] Einzelne Codes zu **einem gemeinsamen ESP-Programm** zusammenführen, das alle Sensoren ausliest
- [ ] Logik für HTTPS-Requests und Token-Versand an den Ingest-Endpunkt
- [ ] Skript zum Flashen eines Geräts und zur Token-Erstellung

### 3. Infrastruktur

- [ ] Docker-Container aufsetzen:
  - DB-Server in eigenem Container
  - API und Logik (Cache, Ingest) in einem Container
  - Frontend in eigenem Container

### 4. Backend

- [ ] Datenbankschema erstellen
- [ ] Ingest mit Token-Prüfung, Validierung und Statuscodes
- [ ] Geräteregistrierung mit Token und Verifizierung
- [ ] Cache aus der Datenbank laden
- [ ] Methoden für die Berechnung von „Raum belegt“ und „Fenster offen“
- [ ] Admin-API mit Login
- [ ] Datenbank-Backups mit Archivierung
- [ ] Health-Checks und Logs

### 5. Frontend

- [ ] Dashboard mit Live-Updates (pro Minute aus Cache/DB)
- [ ] Raum-Detailansicht mit Verlauf
- [ ] Admin-Oberfläche für Geräte und Raumzuteilung
- [ ] Fehlerzustände darstellen
- [ ] Wartungsmeldung bei Backend-Ausfall
- [ ] Proxy mit TLS konfigurieren

### 6. Deployment

- [ ] Auf FH-Netz deployen
- [ ] Verbesserungen und Feinschliff nach dem Rollout
