# Reporting-Automatisierung-KIS-Daten-

Diese Dokumentation beschreibt ein Projekt zur Automatisierung des klinischen Reportings, welches die Aufbereitung und Visualisierung von Behandlungsdaten mittels Power Query und Power BI zum Ziel hat.

1. Datenquellen und Vorbereitung
Die Grundlage bilden CSV-Dateien aus einem Krankenhausinformationssystem (KIS), die folgende Informationen enthalten
:
• Falldaten: Fallnummer, Patientenpseudonym, Aufnahme- und Entlassungsdatum, Fachabteilung, Station, Erlös, Entlassungsart und Arzt-ID
.
• Stammdaten: Eine separate Arzttabelle (KIS Arzt), die Arzt-IDs den entsprechenden Klarnamen zuordnet
.
• Zeittabelle: In Power BI wird zusätzlich eine Datumstabelle für optimierte Filterfunktionen genutzt
.

--------------------------------------------------------------------------------
2. ETL-Prozess mit Power Query
Die Datenaufbereitung erfolgt automatisiert über den Power Query Editor
:
• Datenimport: Die Dateien werden über die Funktion „Daten abrufen aus Ordner“ geladen, wodurch alle im Verzeichnis befindlichen Jahresdateien (2023, 2024, 2025) kombiniert werden
,
.
• Berechnete Spalten: Es wird eine benutzerdefinierte Spalte „Verweildauer“ erstellt, die sich aus der Differenz zwischen dem Entlassungs- und dem Aufnahmedatum ergibt ([Entlassdatum] - [Aufnahmedatum])
,. Der Datentyp wird anschließend als ganze Zahl formatiert
.
• Zusammenführen von Abfragen: Um Klarnamen statt IDs anzuzeigen, wird ein Inner Join zwischen der Falltabelle und der Arzttabelle über das Feld „Arzt-ID“ durchgeführt
.
• Automatisierung: Alle Transformationsschritte werden in Power Query gespeichert
. Sobald neue Dateien im Quellordner abgelegt werden, reicht ein Klick auf „Alle aktualisieren“, um das gesamte Reporting inklusive aller Berechnungen zu erneuern,
.

--------------------------------------------------------------------------------
3. Visualisierung
Die Ergebnisse werden auf zwei Wegen präsentiert:
Excel-Lösung
In Excel werden Pivot-Tabellen und Pivot-Charts genutzt, um die Verweildauer als Mittelwert darzustellen
. Hierbei kann die Entwicklung über Jahre, Quartale oder Monate hinweg visualisiert werden
.
Power BI Dashboard
Das Power BI Dashboard bietet eine interaktive Plattform für die Geschäftsleitung und andere Nutzer
,
:
• Datenmodell: Die Tabellen sind über die Arzt-ID und Datumsfelder miteinander verknüpft
.
• Interaktive Filter (Slicer): Nutzer können nach Zeitraum, spezifischen Ärzten (z. B. Anna Feldmann) oder Fachabteilungen (z. B. Innere Medizin) filtern
,
.
• Key Performance Indicators (KPIs): Wichtige Kennzahlen und Trends der Verweildauer werden grafisch aufbereitet, um beispielsweise saisonale Schwankungen direkt zu identifizieren
,
.
