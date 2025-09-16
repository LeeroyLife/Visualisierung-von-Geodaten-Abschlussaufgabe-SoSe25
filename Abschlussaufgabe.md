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
<br>
**Vorteile der Methode**<br>
<br>
**Nachteile der Methode**<br>
## EP.04 Value-by-alpha Mapping
![image](https://github.com/LeeroyLife/Visualisierung-von-Geodaten-Abschlussaufgabe-SoSe25/blob/main/Fertig/EP.04_Leffke.jpg)<br>
<br>
**Arbeitsschritte**<br>
<br>
**Vorteile der Methode**<br>
<br>
**Nachteile der Methode**<br>
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
