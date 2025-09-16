# Visualisierung-von-Geodaten I Abschlussaufgabe I SoSe25
**Impressum**<br>
<br>
Autor: Leeroy Life Leffke<br>
Herrausgeber: BHT<br>
Kontakt: lele5111@bht-berlin.de<br>
<br>
<br>
**Inhaltsverzeichnis**<br>
<br>
[EP.01 Dasymetrische Choroplethenkarte](#ep01-dasymetrische-choroplethenkarte)<br>
[EP.02 Gitterchoroplethenkarte](#ep02-gitterchoroplethenkarte)<br>
[EP.03 Punktrasterkarte](#ep03-punktrasterkarte)<br>
[EP.04 Value-by-alpha Mapping](#ep04-value-by-alpha-mapping)<br>
[EP.05 Tilemaps](#ep05-tilemaps)<br>
[EP.06 Flowmaps](#ep06-flowmaps)<br>
[EP.07 Mesh-Daten](#ep07-mesh-daten)<br>
[EP.08 Animationen in QGIS](#ep08-animationen-in-qgis)<br>
[EP.09 3D-Gebäudemodelle](#ep09-3d-gebäudemodelle)<br>

## EP.01 Dasymetrische Choroplethenkarte
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.01.jpg)<br>
<br>
**Arbeitsschritte**<br>
1. Datenbeschaffung<br>
•	LOR-Shapefile (Planungsräume Berlin)<br>
•	Einwohnerzahlen (CSV, Stand 01/2023)<br>
•	CLC-Daten (Corine Land Cover – für bebaute Flächen)<br>
2. Daten vorbereiten<br>
•	CSV in Excel aufräumen (Spalten, Zahlenformate)<br>
•	In QGIS laden und CSV mit Shapefile verknüpfen (Join über PLR-Nummer)<br>
3. Einfache Choroplethenkarte<br>
•	Bevölkerungsdichte berechnen: Einwohner / ($area / 10000)<br>
•	Jenks-Klassifizierung (5 Klassen), Farbschema wählen<br>
4. Dasymetrische Karte erstellen<br>
•	CLC-Daten filtern: Nur bebaute Flächen (Codes 111 + 112)<br>
•	Bebaute Fläche zusammenfassen (Geometrie auflösen)<br>
•	Mit LOR-Flächen verschneiden (bebaute Teilflächen pro Planungsraum)<br>
•	Neue Fläche und Dichte berechnen für die bewohnten Flächen<br>
•	Unbebaute Flächen grau, bebaute Flächen farbig nach Dichte<br>
5. Karte gestalten<br>
•	Beide Karten nebeneinander platzieren<br>
•	Titel, Legende, Maßstab, Nordpfeil, Quellen, Name ergänzen<br>

**Vorteile der Methode**<br>
<br>
Die dasymetrische Choroplethenkarte stellt die Bevölkerung deutlich realistischer dar, da sie die Bevölkerung nur auf tatsächlich bebaute und bewohnte Flächen verteilt. Dadurch entstehen klarere Dichte-Hotspots, etwa in Mitte, Friedrichshain oder Marzahn, während unbewohnte Gebiete wie der Grunewald oder das Tempelhofer Feld korrekt ausgeklammert werden. Im Gegensatz zur einfachen Choroplethenkarte vermeidet sie so Verzerrungen durch große, ungenutzte Flächen und ermöglicht eine bessere Vergleichbarkeit zwischen Stadtteilen wie Wedding und Köpenick. Diese realitätsnahe Darstellung bietet besonders für Stadtplanung, Wohnraumanalyse und Infrastrukturentscheidungen eine deutlich höhere Aussagekraft.<br>
<br>
**Nachteile der Methode**<br>
<br>
Trotz ihrer höheren Genauigkeit ist die dasymetrische Choroplethenkarte aufwändiger in der Erstellung, da sie zusätzliche Daten wie Bebauung, Landnutzung oder Satellitenbilder benötigt. Die Abgrenzung bewohnter Flächen ist nicht immer eindeutig und kann je nach Datenbasis variieren. Dadurch entsteht ein höherer Interpretationsspielraum, der Vergleiche erschweren kann. Zudem ist die Methode komplexer und weniger intuitiv lesbar als klassische Karten, da sie sich nicht an bekannten Verwaltungsgrenzen orientiert.
## EP.02 Gitterchoroplethenkarte
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.02_Leffke_Kirschbl%C3%BCtenb%C3%A4ume.jpeg)<br>
<br>
**Arbeitsschritte**<br>
1. Datenbeschaffung<br>
•	Bezirksgrenzen und Kirschbaumdaten (z. B. vom FIS-Broker oder Geoportal Berlin) und in QGIS laden<br>
2. Hexagon-Gitter erstellen<br>
Menü: Vektor → Recherchewerkzeuge → Gitter erzeugen<br>
• Typ: Hexagon (Polygone)<br>
• Ausdehnung: Bezirksgrenzen<br>
• Seitenlänge: 500 m<br>
• Horizontaler & vertikaler Abstand: 866,025 m<br>
3. Gitter auf Berlin begrenzen<br>
•	Verschneidung mit Bezirksfläche, damit nur Zellen in Berlin bleiben<br>
4. Punkte zählen<br>
Menü: Verarbeitung → Werkzeugkiste → „Attribute nach Position verknüpfen”<br>
•	Ziel: Hexagon-Gitter<br>
•	Join: Kirschbaum-Punkte<br>
•	Ergebnis: Anzahl Bäume pro Zelle<br>
5. Darstellung<br>
•	Symbolisierung: Abgestuft nach Baumanzahl<br>
•	Farbverlauf: Weiß (wenig) nach Rot (viel)<br>
•	Klassen: 5 Klassen nach Jenks<br>
6. Drucklayout<br>
•	Karte, Titel, Legende, Maßstab, Nordpfeil, Quellen & Name einfügen<br>

**Vorteile der Methode**<br>
<br>
Die Gitterchoroplethenkarte bietet eine gleichmäßige Flächenaufteilung, da jedes Rasterelement, wie in diesem Fall ein Hexagon, dieselbe Größe hat. Dadurch lassen sich räumliche Verteilungen objektiver und besser vergleichen. Verzerrungen durch unterschiedlich große Verwaltungsgrenzen, wie sie bei klassischen Choroplethenkarten auftreten, werden vermieden. Besonders gut eignet sich diese Methode für punktbezogene Daten, da sich räumliche Muster, Häufungen oder Cluster deutlich erkennen lassen. Außerdem sorgt das Gitter für eine gewisse Anonymisierung, da keine exakten Adressen oder administrative Einteilungen sichtbar sind.<br>

**Nachteile der Methode**<br>
<br>
Ein Nachteil der Gitterchoroplethenkarte ist, dass die genaue Lage einzelner Objekte durch die Aggregation auf Rasterzellen verloren geht. Wie groß die Gitter sind, spielt eine große Rolle: Bei zu großen Gittern fehlen Details, bei zu kleinen wird die Karte unübersichtlich. Zudem sind die Rasterzellen künstlich und folgen keinen bestehenden Verwaltungsgrenzen, was die Aussagekraft in politischen oder administrativen Kontexten einschränkt. Auch die Datenverarbeitung ist etwas aufwendiger, da die punktuellen Daten zunächst in die Gitterstruktur überführt werden müssen.
## EP.03 Punktrasterkarte
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.03_Leffke.jpg)<br>
<br>
**Arbeitsschritte**<br>

1. Daten herunterladen und Importieren<br>
•	Airbnb-Daten (von InsideAirbnb) als CSV-Datei herunterladen<br>
•	Fehlerhafte oder fehlende Werte entfernen (z. B. NULL-Preise)<br>
•	CSV als Punktdaten importieren und nach Objektart gruppieren (Entire Room, Private Room, Shared Room, Hotel Room)<br>
2. Raster erzeugen und zuschneiden<br> 
•	Gleichmäßiges Raster über das Stadtgebiet erzeugen (Vektor → Recherchewerkzeuge → Gitter)<br>
•	Verschneide das Raster mit der Stadtfläche, damit nur Felder innerhalb der Stadt bleiben<br>
4. Punktdaten laden und zählen<br>
•	Airbnb-Punkte (z. B. nach Unterkunftstyp gefiltert) in QGIS laden<br>
•	Unterkünfte je Typ in jeder Rasterzelle zählen (Menü: Verarbeitung → Werkzeugkiste → „Attribute nach Position verknüpfen”)<br>
5. Visualisierung<br>
In jede Zelle kommt ein Punkt je Objektart (zusätzlich den Durchschnittspreis pro Kategorie berechnen):<br>
•	Punktfarbe = Anzahl der Objekte<br>
•	Punktgröße = Durchschnittspreis<br>
6. Drucklayout erstellen<br>
•	Karte, Titel, Legende, Maßstab, Nordpfeil, Quellenangabe, Name<br>

**Vorteile der Methode**<br>
<br>
Die Punktrasterkarte ist besonders gut geeignet, um räumliche Verteilungen und Häufungen sichtbar zu machen. Jeder Punkt steht für eine bestimmte Anzahl von Objekten, was die Darstellung sehr anschaulich und leicht verständlich macht. Gerade bei größeren Datenmengen lässt sich so schnell erkennen, wo sich Schwerpunkte oder Cluster bilden, zum Beispiel eine hohe Dichte an Airbnb-Angeboten im Berliner Stadtzentrum. Die Methode ist unabhängig von administrativen Grenzen, wodurch alle Flächen gleich behandelt werden. Dadurch eignet sich die Karte gut für vergleichende raumanalytische Darstellungen.<br>

**Nachteile der Methode**<br>
<br>
Ein Nachteil der Punktrasterkarte ist, dass die einzelnen Punkte keine echten Standorte darstellen, sondern zufällig innerhalb eines Rasters platziert werden. Dadurch geht die genaue Lage verloren. Zudem zeigt die Karte nur die Verteilung und nicht exakte Werte pro Gebiet. In sehr dicht besiedelten Bereichen kann die Darstellung schnell überladen und unübersichtlich wirken. Auch die Wahl der Rastergröße spielt eine große Rolle: Ist das Raster zu groß, werden Details verschluckt. Ist das Raster zu klein, wird die Karte schwer lesbar. Insgesamt eignet sich die Methode eher zur Darstellung von Mustern als für genaue Analysen.
## EP.04 Value-by-alpha Mapping
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.04_Leffke.jpg)<br>
<br>
**Arbeitsschritte**<br>
1. Datenbeschaffung<br>
•	Wahlkreis-Shapefile und die Zweitstimmenergebnisse (2021, 2025) von der Bundeswahlleiterin herunterladen<br>
2. Datenaufbereitung<br>
•	In Excel alle irrelevanten Spalten entfernen nur die Zweitstimmen der Parteien SPD, CDU/CSU, Grüne, Linke und AfD behalten<br>
•	CSU-Werte in Bayern zur CDU zusammenfassen und als CSV abspeichern<br>
3. Datenimport in QGIS<br>
•	Shapefile und die CSV in QGIS importieren<br>
•	Sicherstellen, dass die Wahlkreisnummer korrekt definiert und das richtige Trennzeichen gewählt ist<br>
4. Verknüpfung der Daten<br>
•	Join -> CSV mit dem Shapefile über die Wahlkreisnummer<br>
5. Attributberechnung<br>
Erzeuge neue Felder:<br>
•	g_value (Stimmenzahl der Gewinnerpartei) array_max( array( "SPD" , "CDU" , "Gruenen" , "AFD" , "Linke"))<br>
•	g_name (Name der Gewinnerpartei - ) with_variable( 'maxVal', array_max( array( "SPD" , "CDU" , "Gruenen" , "AFD" , "Linke")), CASE WHEN "SPD" = @maxVal THEN 'SPD' WHEN "CDU" = @maxVal THEN 'CDU' WHEN "Gruenen" = @maxVal THEN 'Gruenen' WHEN "AFD" = @maxVal THEN 'AFD' WHEN "Linke" = @maxVal THEN 'Linke' END)<br>
•	g_proz_gueltig (Anteil an gültigen Stimmen) "G_value" / "gueltig" *100<br>
6. Symbolisierung<br>
Regelbasierte Darstellung für jede Partei erstellen:<br>
•	 z.B. Regel: „g_name“ = ‚SPD‘ und Beschriftung: ‚SPD‘<br>
Alpha-Regel hinzufügen, um die Transparenz je nach g_proz_gueltig zu steuern:<br>
•	set_color_part('black', 'alpha', scale_linear("g_proz_gueltig", 19, 47, 255, 0))<br>
7. Finalisieren<br>
•	 Darstellung überprüfen und Farben/Transparenz anpassen<br>
•	 Legende, Maßstab, Nordpfeil und Quellenangabe hinzufügen<br>

**Vorteile der Methode**<br>
<br>
Die Value-by-alpha Mapping-Methode bietet eine klare Möglichkeit, zwei verschiedene Datensätze auf einer Karte zu visualisieren. Durch die Kombination von Farbe und Transparenz (Alpha) lassen sich sowohl kategorielle Informationen (z. B. Parteien) als auch die Intensität dieser Kategorien (z. B. Stimmenanteile) gleichzeitig darstellen. Diese Methode ermöglicht es, starke Mehrheiten deutlich hervorzuheben, während schwächere Ergebnisse subtiler dargestellt werden, was zu einer besseren visuellen Wirkung führt. Besonders nützlich ist dies, wenn man Veränderungen oder Muster im Zeitverlauf, wie bei Wahlen, darstellen möchte. Wenn eine passende Legende verwendet wird, ist diese Darstellung für den Betrachter auch leicht verständlich, da sowohl Farbe als auch Transparenz schnell interpretiert werden können.<br>

**Nachteile der Methode**<br>

Trotz ihrer Vorteile bringt die Value-by-alpha Mapping-Methode einige Herausforderungen mit sich. Eine der größten Hürden ist, dass die Lesbarkeit der Karte bei vielen verschiedenen Farben und Transparenzgraden schnell leidet. Besonders bei einer hohen Anzahl von Parteien oder kleineren Differenzen in den Stimmenanteilen wird die Karte unübersichtlich und schwer interpretierbar. Darüber hinaus kann die Wahrnehmung der Transparenz subjektiv sein: Unterschiedliche Betrachter nehmen die Deckkraft von Farben unterschiedlich stark wahr, was zu einer fehlerhaften Interpretation führen kann. Ein weiteres Problem ist, dass sich Farben optisch mischen können, wenn sie zu transparent sind, was die Unterscheidung der Kategorien erschwert. Schließlich ist die Methode auch stark von der Hintergrundfarbe abhängig, bei ungünstigen Hintergrundfarben (z. B. dunkle Farben) kann die Transparenz verzerrt wirken, was die visuelle Klarheit beeinträchtigt.

## EP.05 Tilemaps

## EP.06 Flowmaps
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.06.png)<br>
<br>
**Arbeitsschritte**<br>
<br>
**Vorteile der Methode**<br>
<br>
**Nachteile der Methode**<br>
## EP.07 Mesh-Daten
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.07.gif)<br>
<br>
**Arbeitsschritte**<br>
<br>
**Vorteile der Methode**<br>
<br>
**Nachteile der Methode**<br>
## EP.08 Animationen in QGIS
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.08_Leffke_meteor%20shower.png)<br>
<br>
**Arbeitsschritte**<br>
<br>
**Vorteile der Methode**<br>
<br>
**Nachteile der Methode**<br>
## EP.09 3D-Gebäudemodelle
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.09_Leffke.png)<br>
<br>
**Arbeitsschritte**<br>
<br>
**Vorteile der Methode**<br>
<br>
**Nachteile der Methode**<br>
