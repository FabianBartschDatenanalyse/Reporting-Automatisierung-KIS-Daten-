# Reporting-Automatisierung-KIS-Daten-

## Dokumentation: Automatisierung des klinischen Reportings (Verweildauer-Analyse)

---

## Projektziel und Anwendungsbereich
Das Ziel dieses Projekts ist die Überführung manueller Berichtsprozesse in ein **skalierbares, automatisiertes Reporting-System**.  
Im Fokus steht die Analyse der **durchschnittlichen Verweildauer von Patienten**, basierend auf Daten aus einem Krankenhausinformationssystem (KIS).  
Das System ermöglicht Auswertungen über:
- verschiedene Zeiträume  
- Fachabteilungen  
- einzelne Ärzte  

---

## Datenstruktur und Quellen
Das Projekt nutzt mehrere Datenquellen, die dynamisch miteinander verknüpft werden:

- **KIS-Falldaten (CSV):**  
  Enthält Fallnummer, Patientenpseudonym, Aufnahme- und Entlassungsdatum, Fachabteilung, Station, Erlös, Entlassungsart und Arzt-ID.  
  Das System kombiniert automatisch mehrere Jahresdateien (z. B. 2023, 2024 und zukünftig 2025).

- **KIS-Arztstamm (CSV/Excel):**  
  Referenztabelle, die Arzt-IDs den Klarnamen der behandelnden Ärzte zuordnet.

- **Datumstabelle:**  
  Ergänzende Tabelle in Power BI zur Optimierung zeitlicher Analysen (Time Intelligence).

---

## Der ETL-Prozess (Extraktion, Transformation, Laden)
Die Datenaufbereitung bildet das Herzstück der Automatisierung und erfolgt im **Power Query Editor**.

### A. Dynamischer Datenimport
Anstelle einzelner Dateien wird die Funktion  
**„Daten abrufen aus Ordner“**  
verwendet.  
So werden neue Datensätze (z. B. für 2025) automatisch beim nächsten Aktualisierungsvorgang integriert – ohne zusätzliche Anpassungen.

### B. Datenbereinigung und Transformation
- **Kombination:**  
  Mehrere Jahresdateien werden strukturbasiert zusammengeführt.
- **Berechnung der Verweildauer:**  
  Erstellung einer benutzerdefinierten Spalte:  
  `Verweildauer = [Entlassdatum] - [Aufnahmedatum]`
- **Typkonvertierung:**  
  Umwandlung in Datentyp *Ganze Zahl* zur korrekten Mittelwertberechnung.
- **Daten-Merging (Join):**  
  Inner Join der Falldaten mit der Arzttabelle über die Arzt-ID.  
  IDs werden durch Klarnamen ersetzt → bessere Lesbarkeit und Interpretation.

---

## Visualisierungsoptionen

### Lösung 1: Excel Pivot-Reporting
- Berechnung der durchschnittlichen Verweildauer  
- Gruppierung nach Jahren, Quartalen und Monaten  
- Darstellung zeitlicher Entwicklungen und Trends

---

### Lösung 2: Power BI Dashboard
Interaktive Reporting-Oberfläche für Geschäftsleitung und Fachbereiche:

- **Datenmodell:**  
  Tabellen sind relational verknüpft (z. B. über Arzt-ID)
- **Interaktive Slicer:**  
  Filterung nach Zeitraum (z. B. nur 2025)  
  oder Fachabteilungen (z. B. Innere Medizin)
- **Personalisierte Ansichten:**  
  Analyse individueller Ärzt:innen über Zeit (z. B. „Anna Feldmann“)

---

## Wartung und Skalierbarkeit
Die Wartung ist minimal:
- Neue CSV-Dateien einfach in den Quellordner ablegen  
- Klick auf **„Alle aktualisieren“** genügt  
- Power Query führt automatisch:
  - Import  
  - Transformation  
  - Merging  
  - Berechnung  
für den gesamten Datensatz aus

---

Ergebnis: Ein **robustes, automatisiertes Reporting-System**, das Transparenz schafft, manuelle Arbeit reduziert und datengetriebene Entscheidungen unterstützt.
lter (Slicer): Nutzer können nach Zeitraum, spezifischen Ärzten (z. B. Anna Feldmann) oder Fachabteilungen (z. B. Innere Medizin) filtern.

