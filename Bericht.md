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
ssh  | OpenSSH_8.2p1 Ubuntu-4ubuntu0.1, OpenSSL 1.1.1f  31 Mar 2020
tar | tar (GNU tar) 1.30
rsync | version 3.1.3  protocol version 31
pandoc | pandoc 2.2.1,  pandoc-types 1.17.5.1, texmath 0.11.1, skylighting 0.7.5 


## Durchführung
Für dieses Script ist eine Mitgabe von Argumenten zwingend erforderlich. Diese Tabelle veranschaulicht, welches Argument wann und für was benötigt wird.

Namen der Variablen | Speicherort für: | Arg. Nr | Beispiel Eingaben
------------  | ------------- | ------------- | -------------
**folderToBackup**| *Das Verzeichnis für den Backup-Ordner* | **1** | *Background/Hoch*
**backupFolder** | *Das Verzeichnis für den Speicherort der Backup-Datei* | **2** | *Backup*
**backupFileName** | *Den Namen der fertigen .tar.gz Datei* | **3** | *Bilder-HochFormat*
backupDate | *Das aktuelle Datum mit Uhrzeit* | k. E. erf. | *2020-12-15_12-05-30*

Das BackupScript kann folgendermaßen aufgerufen werden:

* `bash backupScript.bash Background/Hoch Backup Bilder-HochFormat`


### Quellcode
```bash
#!/bin/bash
# Copyright Mr-Phil
######put the Arg in to my variables######
folderToBackup="$1"
backupFolder="$2"
backupFileName="$3"
backupDate=`date +%Y-%m-%d_%H-%M-%S`
##########################################


clear
echo "--------------------------------------------------------------------------"
echo "                  Welcome to the Mr. Phil1 Backup-Script"
echo "--------------------------------------------------------------------------"
if [[ "$3" == '' ]] ; then
  echo "  Sie haben zu wenigen Argumente mitgegeben!"
  echo "  Sie müssen folderToBackup, backupFolder und backupFileName angegeben"
  echo "--------------------------------------------------------------------------"
  exit 1
fi

if [ $# -eq 4 ] ; then
  echo "  Sie haben zu viele Argumente mitgegeben!"
  echo "  Sie müssen folderToBackup, backupFolder und backupFileName angegeben"
  echo "--------------------------------------------------------------------------"
  exit 1
fi
echo "  folderToBackup: ${folderToBackup}"
echo "  backupFolder:   ${backupFolder}"
echo "  backupFileName: `date +%Y-%m-%d_%H-%M-%S`_${backupFileName}.tar.gz"
echo "--------------------------------------------------------------------------"
if [ ! -d $folderToBackup ]; then
  echo "  Nicht vorhandener Sicherungs-Ordner"
  echo "  !! Der Ordner "${folderToBackup}" existiert nicht !!"
  echo "--------------------------------------------------------------------------"
  exit 1
fi

if [ ! -d ${backupFolder} ]; then
  echo "  Nicht vorhandener Backup-Ordner"
  echo "  Der Ordner "${backupFolder}" existiert nicht und wird erstellt!"
  mkdir ${backupFolder}/
  echo "--------------------------------------------------------------------------"
fi

echo "  Backup wird nun gestartet!"
echo "  Je nach Größe des folderToBackup kann dieser Prozess eine Weile dauern."
tar -czf ${backupFolder}/${backupDate}_${backupFileName}.tar.gz ${folderToBackup};
2>> ${backupFolder}/error-msg.txt; echo "" >>${backupFolder}/error-msg.txt
echo "  Das Backup von "${folderToBackup}" ist nun fertig gestellt."
echo "  Vielen Herzlichen Dank für Ihr Vertrauen."
echo "--------------------------------------------------------------------------"
if [ -s ${backupFolder}/${backupDate}_${backupFileName}.tar.gz ]; then
  rsync --numeric-ids -avz  ${backupFolder}/${backupDate}_${backupFileName}.tar.gz username@ip-address:
else
  echo "  Nicht vorhandener *.tar.gz Datei"
  echo "  !! Die *.tar.gz Datei existiert nicht oder ist kleiner 0 Byte!!"
  echo "--------------------------------------------------------------------------"
  exit 1
fi
# Copyright Mr-Phil
```
### Erklärung des Quellcodes

#### Erster IF-Verweigung:
In diesem Bereich wird überprüft, ob man dem Script weniger als drei Argumente mitgegeben hat. Wenn dieser Fall zutrifft, gibt das Programm eine Fehlermeldung aus und beendet dieses.
```bash
if [[ "$3" == '' ]] ; then
  echo "  Sie haben zu wenigen Argumente mitgegeben!"
  echo "  Sie müssen folderToBackup, backupFolder und backupFileName angegeben"
  echo "--------------------------------------------------------------------------"
  exit 1
fi
```

#### Zweiter IF-Verweigung:
In diesem Bereich wird überprüft, ob man dem Script mehr als drei Argumente mitgegeben hat. Wenn dieser Fall zutrifft, gibt das Programm eine Fehlermeldung aus und beendet dieses.
```bash
if [ $# -eq 4 ] ; then
  echo "  Sie haben zu viele Argumente mitgegeben!"
  echo "  Sie müssen folderToBackup, backupFolder und backupFileName angegeben"
  echo "--------------------------------------------------------------------------"
  exit 1
fi
```

#### Dritter IF-Verweigung:
In diesem Bereich wird überprüft, ob der zu Sichernde Ordner nicht vorhanden ist. Wenn dieser Fall zutrifft, gibt das Programm eine Fehlermeldung aus und beendet dieses.
```bash
if [ ! -d $folderToBackup ]; then
  echo "  Nicht vorhandener Sicherungs-Ordner"
  echo "  !! Der Ordner "${folderToBackup}" existiert nicht !!"
  echo "--------------------------------------------------------------------------"
  exit 1
fi
```

#### Vierter IF-Verweigung:
In diesem Bereich wird überprüft, ob der Backup-Ordner nicht vorhanden ist. Wenn dieser Fall zutrifft, wird ein Ordner mit diesem Namen erstellt.
```bash
if [ ! -d ${backupFolder} ]; then
  echo "  Nicht vorhandener Backup-Ordner"
  echo "  Der Ordner "${backupFolder}" existiert nicht und wird erstellt!"
  mkdir ${backupFolder}/
  echo "--------------------------------------------------------------------------"
fi
```


#### Erstellung der tar.gz Datei:
Mit der nun folgenden Codezeile wird mit Hilfe von tar eine Sicherung mit dem Inhalt von **{folderToBackup}**, in den Ordner **{backupFolder}** mit dem **aktuellen Datum, der aktuellen Uhrzeit** und dem **{backupFileName}** erstellt. Sollte während diesem Vorgang eine Fehlermeldung auftauchen, wird diese im **{backupFolder}**  in einer txt-Datei mit dem Namen error-msg zwischengespeichert.

```bash
tar -czf ${backupFolder}/${backupDate}_${backupFileName}.tar.gz ${folderToBackup};
2>> ${backupFolder}/error-msg.txt; echo "" >>${backupFolder}/error-msg.txt
```


#### Übermittelung der tar.gz Datei auf einen remote Server:
* Vor der Erstanwendung sollte  **username@ip-address** mit einem gültigen **username** und einer gültigen **ip-address** ersetzt werden.

Zunächst wird mit einer IF-Verzweigung überprüft, ob die zu erstellende Datei .tar.gz größer als 0 Bytes ist. Wenn das nicht zutrifft, wird das Programm an dieser Stelle beendet, ansonsten wird die Datei mit Hilfe von rsync auf den zuvor eingestellten Server hochgeladen.

```bash
if [ -s ${backupFolder}/${backupDate}_${backupFileName}.tar.gz ]; then
  rsync --numeric-ids -avz ${backupFolder}/${backupDate}_${backupFileName}.tar.gz username@ip-address:
else
  echo "  Nicht vorhandener *.tar.gz Datei"
  echo "  !! Die *.tar.gz Datei existiert nicht oder ist kleiner 0 Byte!!"
  echo "--------------------------------------------------------------------------"
exit 1
fi
```
## Automatisierung durch die Crontab

* `crontab -e`
* nano auswählen (meistens die Ziffer 1)
* beispielsweise folgende Zeilen einfügen:
* ` */1 * * * * /usr/bin/bash /home/mr-phil/backupScript.bash /home/mr-phil/Dokumente
/home/mr-phil/backup backupFileName`
* mit strg +x speichern
* und dem Zauber einfach seinem Lauf lassen.

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
