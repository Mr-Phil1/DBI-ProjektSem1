---
title: Bericht für das 1. Semester Projekt
author: Mr. Phil
rights: Nah
language: de-AT
keywords: DBI; MySQL; Database
---
## Einleitung


## Verwendete Technologien
Technologien-Name | Verwendete Version
------------ | -------------
Ubuntu |Ubuntu 20.04 LTS
Oracle SQL Datamodeler  | 20.2.0.167.1538


## Durchführung




## Bilder des Entwurs

### Logisch
![Logisches Design](https://raw.githubusercontent.com/Mr-Phil1/DBI-ProjektSem1/main/Bilder/Logical.svg?token=AIXSKYDKYFMAB22KJB6NN53AAQ5E4)
### Relational
![Relationales Design](https://raw.githubusercontent.com/Mr-Phil1/DBI-ProjektSem1/main/Bilder/Relational_1.svg?token=AIXSKYAB5HLUW5A3TPI25F3AAQ5HY)

## Erstellung des PDF
Für die PDF Erstellung wurde auf den Parser Pandoc zurückgegriffen. Zu diesem Zeitpunkt wird nicht weiter auf die Funktionsweise von Pandoc eingehen. Mit folgendem Befehl wurde das ganze Dokument zu einem PDF umgewandelt:

* `pandoc -V papersize=a4pape -V geometry:margin=1.5cm -V fontsize=12p -s -V lang=de-DE --toc -o ./Arbeitsbericht.pdf ./Arbeitsbericht.md`


## Literatur

* Mit Hilfe der [Ubuntuusers-Wikiseiten:](https://wiki.ubuntuusers.de)
  * [tar](https://wiki.ubuntuusers.de/tar/)
  * [rsync](https://wiki.ubuntuusers.de/rsync/)
  * [scp](https://wiki.ubuntuusers.de/SSH/#scp)
  * [pandoc](https://wiki.ubuntuusers.de/Pandoc/)
* Verwendete Scripte:
  * [BackupScript](https://gitlab.com/Mr-Phil1/schule/-/blob/master/Linux-Script/2020-12-15/backupScript.bash)

---

Copyright (c) 2021 Copyright mr-phil1 All Rights Reserved.
