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

1.	Datenbeschaffung<br> 
•	Flüchtlingszahlen vom UNHCR sowie Landesgrenzen von Natural Earth herunterladen<br>
2.	Datenaufbereitung<br>
•	Die Flüchtlingszahlen in einer Pivot-Tabelle aggregieren (nach Zielland und Jahr) und als CSV exportieren<br>
3.	 Import in QGIS<br>
•	CSV-Datei und Länder Geometrien in QGIS laden und CSV als textbasierter Layer ohne Geometrie einbinden<br>
4.	 Zentroid-Berechnung<br>
•	Mittelpunkte aller Länder erzeugen, bei Bedarf manuell korrigieren<br>
5.	Koordinaten-Felder<br>
•	Für die Zielorte sowie den StartpunktX-/Y-Koordinaten in der Attributtabelle anlegen<br>
6.	Linienerzeugung<br>
•	Mit dem Tool "XY to Line" Linien vom Startpunkt zu den Zielzentroiden erzeugen<br>
7.	Projektion<br>
•	Eigene orthografische Projektion definieren:<br>
•	+proj=ortho +lat_0=50.3 +lon_0=30.3 +x_0=0 +y_0=0 +a=6371000 +b=6371000 +units=m +no_defs<br>
8.	 Symbolisierung<br>
•	Linienbreite nach Flüchtlingszahl gestaffelt (5 Klassen)<br>
•	Ukraine als auffälliger, roter Startpunkt dargestellt<br>
•	Hintergrund als Globus mit dunklem Ozean und leuchtendem Rand<br>
•	Legende, Maßstab, Nordpfeil und Quellenangabe hinzugefügt<br>

**Vorteile der Methode**<br>

Die Flow Map-Methode bietet eine sehr anschauliche Möglichkeit, Bewegungen – wie in diesem Fall die ukrainische Flüchtlingsbewegung von 2022 bis 2024 – geografisch darzustellen. Besonders hilfreich ist die visuelle Verknüpfung zwischen Ausgangs- und Zielregionen, wodurch die Bewegungsrichtungen sofort erkennbar werden. Die Nutzung unterschiedlich dicker Linien zur Darstellung der Flüchtlingszahlen ermöglicht zudem eine schnelle Einschätzung des Umfangs der Bewegung. Dadurch lassen sich verschiedene Zielländer direkt miteinander vergleichen. Der räumliche Kontext wird klar vermittelt, da die Daten auf einer realen Weltkarte eingebettet sind. Diese Form der Darstellung ist außerdem visuell ansprechend und eignet sich gut für Präsentationen, Berichte oder zur Informationsvermittlung an ein breiteres Publikum.<br>

**Nachteile der Methode**<br>

Trotz ihrer Vorteile bringt die Flow Map-Methode auch einige Einschränkungen mit sich. Bei einer großen Anzahl von Zielregionen kann es schnell zu einer Überlagerung der Linien kommen, was die Lesbarkeit und Übersichtlichkeit der Karte deutlich beeinträchtigt – besonders in dicht besiedelten Regionen wie Europa. Außerdem dominieren sehr große Flüchtlingsströme (wie in diesem Fall nach Russland) das Bild stark, wodurch kleinere, aber dennoch relevante Bewegungen visuell in den Hintergrund treten. Die Methode bietet zudem keine Informationen über Ursachen, Zeitverläufe oder Dynamiken der Fluchtbewegungen – sie zeigt lediglich die Richtung und die Menge. Ein weiterer Nachteil besteht in der gewählten Kartenprojektion, die zu Verzerrungen in der Größen- und Entfernungswahrnehmung führen kann. Gerade kleine Länder oder weniger prominente Regionen sind auf solchen Karten häufig schwer zu erkennen, was zur Unschärfe in der Interpretation führen kann.<br>

## EP.07 Mesh-Daten
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.07.gif)<br>
<br>
**Arbeitsschritte**<br>

1.	Datenbeschaffung<br>
•	Download der GRIB-Daten für Wind (10 m u- & v-Komponenten) vom 19. Januar 2007 über Copernicus<br>
•	Zusätzlich werden Verwaltungsgrenzen Europas von Natural Earth geladen<br>
2.	Import in QGIS<br>
•	Die GRIB-Datei per Drag & Drop in QGIS laden<br>
•	Die Mesh-Daten erscheinen automatisch mit Zeitstempel<br>
3.	Symbolisierung<br>
•	Windgeschwindigkeit als Farbflächen (z. B. violett → orange) darstellen<br>
•	Windrichtung über Pfeile (Vektoren) visualisieren<br>
•	Farbschema und Pfeilstil anpassen<br>
4.	Zeitsteuerung aktivieren und anzeigen<br>
•	In den Layer-Eigenschaften den Mesh-Layer als „zeitlich“ markieren<br>
•	Zeitsteuerungs-Panel aktivieren, um die zeitbasierte Animation zu ermöglichen<br>
•	Einen transparenten Punkt-Layer anlegen, der die Zeitangabe als Beschriftung enthält. Ausdruck:<br>
format_date(@map_start_time, 'd. MMMM yyyy') || '\n' || format_date(@map_start_time, 'HH:mm')<br>
5.	Kartenlayout vorbereiten<br>
•	In Ansicht → Dekorationen <br>
•	Titel, Maßstab, Legende, Farbskala für Windgeschwindigkeit hinzufügen<br> 
6.	Export der Animation und GIF-Erstellung<br>
•	Die Zeitsteuerung im QGIS aktivieren und die Animation abspielen lassen. Mit dem Uhr-Werkzeug einzelne Frames als PNG exportieren<br>
•	Die PNG-Bildserie mit GIMP zu einer animierten GIF-Datei zusammenfügen<br>

**Vorteile der Methode**<br>

Die Visualisierung von Mesh-Daten bietet eine anschauliche Möglichkeit, Wetterphänomene wie Sturm Kyrill dynamisch darzustellen. Durch die Animation wird der zeitliche Verlauf von Windrichtung und -geschwindigkeit gut nachvollziehbar. Farbverläufe und Richtungspfeile sorgen für eine intuitive Lesbarkeit, auch ohne tieferes Fachwissen. Die Einblendung von Datum und Uhrzeit unterstützt zusätzlich das Verständnis der Abläufe. Insgesamt entsteht eine visuell ansprechende Darstellung, die sich gut für Präsentationen und die Vermittlung komplexer Informationen eignet.<br>

**Nachteile der Methode**<br>

Allerdings bringt die Methode auch einige Einschränkungen mit sich. Exakte Zahlenwerte sind in der Animation meist nicht direkt ablesbar, und eine gut lesbare Legende lässt sich nur schwer integrieren. Da GIFs weder pausiert noch zurückgespult werden können, ist eine gezielte Analyse erschwert. Zudem erfolgt die Erstellung der Animation außerhalb von QGIS mit externen Tools, was den Aufwand erhöht. Die resultierenden Dateien können durch hohe Auflösung und viele Frames sehr groß werden, was ihre Nutzung auf Onlineplattformen einschränken kann.<br>

## EP.08 Animationen in QGIS
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.08_Leffke_meteor%20shower.png)<br>
<br>
**Arbeitsschritte**<br>

1.	Datenbeschaffung<br>
•	Meteordaten als CSV-Datei von einer öffentlichen Quelle (z. B. Meteor-Map) herunterladen<br>
2.	Datenaufbereitung<br>
•	Die Zeitstempel in den Daten müssen im richtigen Format für QGIS konvertiert werden, um später die zeitliche Animation korrekt anzuzeigen<br>
•	Für eine statische Darstellung können die Daten als CSV in QGIS geladen werden<br>
3.	Geometrieerzeugung<br>
•	Mit dem „Geometrie nach Ausdruck“-Werkzeug eine Linie für jede Meteorspur erzeugen (indem die Start- und Endkoordinaten der Meteoriten miteinander verbunden werden)<br> 
•	Ausdruck:<br> 
make_line($geometry, make_point("LonEnd", "LatEnd"))<br>
4.	Hintergrund<br>
•	Einen passenden Hintergrund auswählen, z. B. eine ESRI-Background-Map (um die Visualisierung auf einer realistischen Karte darzustellen)<br>
5.	Symbolisierung<br>
•	Die Meteoriten als „Meteoritenschweife“ visualisieren (interpolierte Linie mit einem Farbverlauf)<br>
6.	Kartenlayout<br>
•	Titel, Maßstab, Quellenangabe hinzufügen<br>
•	Das finale Layout im gewünschten Maßstab exportieren, z. B. als PNG mit einer Auflösung von 1080x1080px<br>

**Vorteile der Methode**<br>

Die Visualisierung der Meteorschauer in QGIS ist intuitiv und ermöglicht es, die Bewegungen der Meteoriten schnell zu verstehen. Das Verfahren ist einfach, erfordert keine komplexen Tools und liefert dennoch ein ansprechendes Ergebnis. Der Farbverlauf und die Linienbewegung werden leicht mit einer dynamischen Bewegung assoziiert, auch ohne dass eine echte Animation nötig ist.<br>

**Nachteile der Methode**<br>

Ein Nachteil dieser Methode ist, dass der zeitliche Verlauf des Ereignisses durch die Animation verloren gehen kann, was die Detailanalyse erschwert. Bei vielen Meteoriten auf einmal kann die Karte schnell unübersichtlich werden. Außerdem können unregelmäßig verteilte Datenpunkte zu Clustern führen, die die Karte überfrachten. Zudem haben die Daten keinen hohen Informationswert, da sie auf zufälligen Beobachtungen basieren, was die Methode eher ästhetisch als analytisch macht.<br>

## EP.09 3D-Gebäudemodelle
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.09_Leffke.png)<br>
<br>
**Arbeitsschritte**<br>

1.	Datenquelle<br>
•	3D-Gebäudedaten von der Webseite www.geodaten.sachsen.de herunterladen und in QGIS importieren<br>
2.	Symbolisierung aktivieren<br>
•	In den Layereigenschaften den Stil 2.5D auswählen<br> 
•	Für das Höhenattribut einen passenden Wert aus dem Datensatz (z. B. Gebäudehöhe) einstellen<br> 
•	Dächer und Wände werden dabei mit verschiedenen Füllungen dargestellt<br>
3.	Farbgestaltung<br>
•	Unter „Einzelsymbol“ die Füllungen anpassen<br> 
•	Farbverläufe oder unterschiedliche Farben können für verschiedene Gebäudetypen vergeben werden<br>
•	So entsteht eine klare visuelle Differenzierung<br>
4.	3D-Ansicht vorbereiten<br>
•	Im Reiter 3D Ansicht zusätzliche Parameter einstellen (z. B. Offset für korrekte Höhenwerte)<br> 
5.	Interaktive Erkundung<br>
•	Über Ansicht → 3D-Kartenansicht:<br> 
•	Perspektive frei ändern (Zoom, Neigung, Drehung), sodass die Gebäudestruktur besser erfasst werden kann<br>
•	Die Ansicht kann hier auch gespeichert werden<br>

**Vorteile der Methode**<br>

Das 2.5D-Gebäudemodell von Dresden hat einige Vorteile. Es zeigt die Gebäudehöhen auf anschauliche Weise und macht so die Stadtstruktur leicht verständlich. Dadurch kann man schnell Unterschiede zwischen niedrigen und hohen Gebäuden erkennen. Die Methode ist außerdem einfacher zu erstellen als ein richtiges 3D-Modell und bleibt übersichtlicher. Besonders für Stadtplanung oder um Bebauungsdichten darzustellen ist sie gut geeignet.<br>

**Nachteile der Methode**<br>

Es gibt aber auch Nachteile. Die Gebäude sind nur grob dargestellt, Dachformen oder Fassadendetails fehlen. Da es sich nicht um echtes 3D handelt, ist der Blickwinkel festgelegt und man kann nicht durch die Stadt „navigieren“. Teilweise wirken Gebäude auch verzerrt oder verdecken sich gegenseitig. Zudem hängt die Qualität stark von den zugrunde liegenden Daten ab.
