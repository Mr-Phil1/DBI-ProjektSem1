# *Projektbericht Entity-Relationship-Modell für eine persönliche Filmsammlung*   

</br>

## Inhaltsverzeichnis
* [Einleitung](#einleitung)
* [Verwendete Technologien](#verwendete-technologien)
* [Durchführung](#durchführung)
* [Darstellung](#darstellung)
    * [Filme](#darstellung)
        * [Logisch](#logisch)
        * [Relational](#relational)
    * [Serien](#darstellung)
        * [Logisch](#logisch)
        * [Relational](#relational)
* [Literatur](#literatur)
---

## Einleitung
Das Entity-Relationship-Modell – ER-Modell oder ERM, dient der Darstellung von Dingen, Gegenständen, Objekten und der Beziehungen bzw. Zusammenhänge zwischen diesen. Dieses Modell dient dazu, im Rahmen der semantischen Datenmodellierung den in einem gegebenen Kontext (z. B. einem Projekt zur Erstellung eines Informationssystems) relevanten Ausschnitt der realen Welt zu bestimmen und darzustellen. Das ER-Modell besteht im Wesentlichen aus einer Grafik (ER-Diagramm) sowie einer Beschreibung der darin verwendeten Elemente. Ein ER-Modell dient sowohl in der konzeptionellen Phase der Anwendungsentwicklung der Verständigung zwischen Anwendern und Entwicklern (dabei wird nur das Was behandelt, d. h. fachlich-sachliche Gegebenheiten, nicht das Wie, z. B. die Technik) als auch in der Implementierungsphase als Grundlage für das Design der – meist relationalen – Datenbank.

</br>

## Verwendete Technologien
Technologien-Name | Verwendete Version
------------ | -------------
Oracle SQL Datamodeler  | 20.2.0.167.1538

</br>

## Durchführung

Das ER-Modell dient vor allem der logischen Darstellung und sollte so übersichtlich wie möglich gestaltet werden.
Aus diesem Grund, beginnen die Bezeichnungen der Attribute mit Großbuchstaben.
Das dargestellte ER-Modell dient der Veranschaulichung, wie die Speicherung einer persönlichen Filmsammlung im logischen Modell umgesetzt werden kann.
Es enthält zahlreiche Entitäten mit ihren Eigenschaften und Relationships untereinander.
Das Modell stellt alle gespeicherten Filme der Sammlung dar.  
Es besteht die Möglichkeit, einen Film, je nach verwendeteten Medium ( z.B.: DVD, VHS, Blu Ray, etc.) zu speichern.  
Desweiteren können die Filme nach Länge, Sprache, Erscheinungsjahr oder Genre unterteilt werden.  
Eine Besonderheit stellt die Entität IMDB dar. Dies ermöglicht den Nutzer, Filme nach Bewertung zu speichern bzw. auszuwählen.  
Unter anderem werden Supertyps bzw. Subtypes in der Entität Filmstar verwendet. Dies hat folgenden Hintergrund.
Eine Person kann gleichzeit Schauspieler, Regisseur und Produzent sein (z.B.: Denzel Washington).  
Da es sich in diesem Projekt um eine persönliche Filmsammlung handelt, haben wir zudem eine Entität Verleihhistorie und eine Entität Person eingebaut.
Diese beiden stehen zusammen mit der Entität Film Titel in einer Beziehung. Dies ermöglicht den Nutzer auf einen Blick zu sehen, wer wann welchen Film ausgeliehen hat.  
Mit Hilfe der Barred Relationship sichern wir zusätzlich ab, dass ein Film nur einmal pro bestimmten Datum ausgeliehen werden kann.  
Der Grund dafür ist, dass es sich um eine persönliche Filmsammlung handelt und ein Film nur einmal vorhanden ist.

</br>

## Darstellung
### Filme
#### Logisch
![Logisches Design](https://raw.githubusercontent.com/Mr-Phil1/DBI-ProjektSem1/main/Bilder/Filme/Logisches-Modell.jpg)

</br>

#### Relational
![Relationales Design](https://raw.githubusercontent.com/Mr-Phil1/DBI-ProjektSem1/main/Bilder/Filme/Relationales-Modell.jpg)

### Serien
#### Logisch
![Logisches Design](https://raw.githubusercontent.com/Mr-Phil1/DBI-ProjektSem1/main/Bilder/Serien/Logisches-Modell.jpg)

</br>

#### Relational
![Relationales Design](https://raw.githubusercontent.com/Mr-Phil1/DBI-ProjektSem1/main/Bilder/Serien/Relationales-Modell.jpg)

## Diskusion

## Literatur

* Mit Hilfe der [Deutschen Wikipedia](https://de.wikipedia.org)
  * [Entity-Relationship-Modell](https://de.wikipedia.org/wiki/Entity-Relationship-Modell)
  * [Normalisierung (Datenbank)](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank))  
* Die Projek-Dateien:
  * [Filme](https://github.com/Mr-Phil1/DBI-ProjektSem1/blob/main/zip/Filme.zip)
  * [Serien](https://github.com/Mr-Phil1/DBI-ProjektSem1/blob/main/zip/Serie.zip)
---
Copyright (c) 2021 Copyright [mr-phil1](https://github.com/Mr-Phil1) + [Vercetti90](https://gist.github.com/Vercetti90) All Rights Reserved.
