# Automatisierung des klinischen Reportings (Verweildauer-Analyse)

---

## Projektziel und Anwendungsbereich
Das Ziel dieses Projekts ist die Überführung manueller Berichtsprozesse in ein **skalierbares, automatisiertes Reporting-System**.  
Im Fokus steht die Analyse der **durchschnittlichen Verweildauer von Patienten**, basierend auf Daten aus einem Krankenhausinformationssystem (KIS).  
Das System ermöglicht Auswertungen über:
- verschiedene Zeiträume  
- Fachabteilungen  
- einzelne Ärzte  

<br>

<img width="2527" height="1225" alt="Beispielzahlen_1" src="https://github.com/user-attachments/assets/2d3b8731-aa3c-4b98-9194-de0f848d140e" />

*Abbildung 1: Beispieldaten*

<br>

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

<br>

<img width="1728" height="828" alt="Daten_2" src="https://github.com/user-attachments/assets/c79da5df-16bd-4273-9621-ae57530d67b7" />

*Abbildung 2: Datenquellenübersicht*

<br>

---

## Der ETL-Prozess (Extraktion, Transformation, Laden)
Die Datenaufbereitung bildet das Herzstück der Automatisierung und erfolgt im **Power Query Editor**.

### A. Dynamischer Datenimport
Anstelle einzelner Dateien wird die Funktion **„Daten abrufen aus Ordner“** verwendet.  
So werden neue Datensätze (z. B. für 2025) automatisch beim nächsten Aktualisierungsvorgang integriert – ohne zusätzliche Anpassungen.

<br>

<img width="4400" height="2253" alt="Daten_laden_3" src="https://github.com/user-attachments/assets/9c014b16-ddeb-4730-bd67-a08c2d370c96" />

*Abbildung 3: Dynamischer Datenimport über Ordnerstruktur*

<br>

### B. Datenbereinigung und Transformation

- **Kombination:**  
  Mehrere Jahresdateien werden strukturbasiert zusammengeführt.

<br>

<img width="4400" height="2315" alt="Kombinieren_transformieren_4" src="https://github.com/user-attachments/assets/22142eea-8463-4b89-9cbd-1da2a52c90d6" />

*Abbildung 4: Kombinieren und Transformieren der Jahresdaten*

<br>

- **Berechnung der Verweildauer:**  
  Erstellung einer benutzerdefinierten Spalte:  
  `Verweildauer = [Entlassdatum] - [Aufnahmedatum]`

<br>

<img width="4400" height="2314" alt="Neue_Spalte_5" src="https://github.com/user-attachments/assets/f0748712-45bb-4c08-94cb-b5b118d47ea4" />

*Abbildung 5: Anlegen der Verweildauer-Spalte*

<br>

<img width="2556" height="1353" alt="Verweildauer_6" src="https://github.com/user-attachments/assets/15ab5274-a89b-45c7-8ebd-7bf4031a4b02" />

*Abbildung 6: Formel der Verweildauerberechnung*

<br>

- **Typkonvertierung:**  
  Umwandlung in Datentyp *Ganze Zahl* zur korrekten Mittelwertberechnung.

<br>

<img width="4400" height="2331" alt="Typkonvertierung_7" src="https://github.com/user-attachments/assets/2302fe05-6743-429e-9f83-dc08eaec5d04" />

*Abbildung 7: Typkonvertierung für Berechnungsstabilität*

<br>

- **Daten-Merging (Join):**  
  Inner Join der Falldaten mit der Arzttabelle über die Arzt-ID.  
  IDs werden durch Klarnamen ersetzt → bessere Lesbarkeit und Interpretation.

<br>

<img width="4400" height="2330" alt="KIS_Aertzte_hinzufügen_8" src="https://github.com/user-attachments/assets/13ba3c70-e7ac-4f16-a2b4-bf56549b8c5b" />

*Abbildung 8: Einbindung der Ärztetabelle*

<br>

<img width="4400" height="2325" alt="9_Abfragen_zusammenführen" src="https://github.com/user-attachments/assets/5adeee3b-6b2e-4f09-a3f3-276ced7cb0a0" />

*Abbildung 9: Zusammenführen der Abfragen*

<br>

<img width="2559" height="1357" alt="10_Join" src="https://github.com/user-attachments/assets/477c4f04-3b90-4323-904b-ed9a58a0b84f" />

*Abbildung 10: Join über Arzt-ID*

<br>

<img width="4400" height="2333" alt="11_Name" src="https://github.com/user-attachments/assets/83f76066-1852-4074-8f07-49e2c01a693a" />

*Abbildung 11: Anzeige der Arztnamen*

<br>

<img width="4403" height="2332" alt="12_Schliessen_laden" src="https://github.com/user-attachments/assets/56ba1eef-4c7b-4d76-b5ba-05cba7771b33" />

*Abbildung 12: Laden der bereinigten Daten*

<br>

---

## Visualisierungsoptionen

### Lösung 1: Excel Pivot-Reporting
- Berechnung der durchschnittlichen Verweildauer  
- Gruppierung nach Jahren, Quartalen und Monaten  
- Darstellung zeitlicher Entwicklungen und Trends  

<br>

<img width="4400" height="2330" alt="13_Pivot" src="https://github.com/user-attachments/assets/5900b5b2-3e09-4a81-a2a7-c793055140b2" />

*Abbildung 13: Pivot-Auswertung*

<br>

<img width="2559" height="1355" alt="14_Pivot_Auswahl" src="https://github.com/user-attachments/assets/c004eab7-8239-4d1f-be87-317e425bb183" />

*Abbildung 14: Auswahl relevanter Kennzahlen*

<br>

<img width="2556" height="1355" alt="15_Grafik_Excel" src="https://github.com/user-attachments/assets/cacc780d-c683-464e-a3df-caede4bc94b4" />

*Abbildung 15: Visualisierte Verweildauerentwicklung pro Arzt/Ärztin*

<br>

---

### Lösung 2: Power BI Dashboard
Interaktive Reporting-Oberfläche für Geschäftsleitung und Fachbereiche:

- **Datenmodell:** Tabellen sind relational verknüpft (z. B. über Arzt-ID)

<br>

<img width="2547" height="1351" alt="16_Datenmodell" src="https://github.com/user-attachments/assets/1ffc6d7b-45be-4040-9b6c-e0dbb7597c8e" />

*Abbildung 16: Power BI Datenmodell*

<br>
- **Interaktive Slicer:** Filterung nach Zeitraum (z. B. nur 2025) oder Fachabteilungen (z. B. Innere Medizin)
<br>

<img width="2794" height="1573" alt="17_Slicer" src="https://github.com/user-attachments/assets/43a50e37-8e81-4fe0-8729-280598ffe8a9" />

*Abbildung 17: Interaktive Filterung per Slicer*

<br>
- **Personalisierte Ansichten:** Analyse individueller Ärzt:innen über Zeit (z. B. „Anna Feldmann“)
<br>

<img width="3555" height="1995" alt="18_Feldmann" src="https://github.com/user-attachments/assets/7bddc2d8-30c9-44a3-bc7e-79825ac659b1" />

*Abbildung 18: Arztbezogene Detailanalyse*

<br>

---

## Wartung und Skalierbarkeit
Die Wartung ist minimal:
- Neue CSV-Dateien in den Quellordner ablegen  
- Klick auf **„Alle aktualisieren“** genügt  
- Power Query übernimmt Import, Transformation, Merging und Berechnung automatisch

<br>

<img width="4400" height="2333" alt="19_Alle_aktualisieren" src="https://github.com/user-attachments/assets/85a9b22b-3a47-4656-9182-ff06d51a725b" />

*Abbildung 19: Vollautomatische Aktualisierung*

<br>

---

Ergebnis: Ein **robustes, automatisiertes Reporting-System**, das Transparenz schafft, manuelle Arbeit reduziert und datengetriebene Entscheidungen unterstützt.
