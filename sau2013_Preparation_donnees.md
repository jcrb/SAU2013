SAU 2013 - Preparation des donnés
========================================================

L'étude porte du 1/1/2013 au 31/12/2013 avec un compatatif sur la même période en 2012.
Les données sont extraite de SAGEC HUS et copiées/collées dans un tableur libre office. La dernière colonne (supprimer) est supprimées. La feuille est enregistrée sous *sau2013.csv*

Le présent document décrit la manière de procéder pour produire un fichier binaire *sau2013.Rda* qui sera exploité.


```r
file <- "~/Documents/Resural/Stat Resural/SAU2013"
setwd(file)
timestamp()
```

```
## ##------ Sun Nov 17 11:18:08 2013 ------##
```

```r
d <- read.csv("sau2013.csv", header = TRUE)
```

Préparation des données
------------------------
Transformation de la colonne *date* du format jj/mm/aaaa au format yyyy-mm-dd

```r
d$date <- as.Date(d$date, "%d/%m/%Y")
```

Renommage de la colonne *organisme* par la création d'une nouvelle colonne *hop*
NB: on ignore le CMCO. Trois structures sont absentes de la base: Haguenau, Ste Anne et Diaconnat-Fonderie. Les urgences mains du CCOM gardent le même nom pour les différecier des urgences adulte.

```r
d$hop[d$Organisme == "CCOM"] <- "CCOM"
d$hop[d$Organisme == "CH Altkirch"] <- "ALK"
d$hop[d$Organisme == "CH de Colmar (CMC Le Parc)"] <- "COL"
d$hop[d$Organisme == "CH de Colmar (Louis Pasteur)"] <- "COL"
d$hop[d$Organisme == "CH de Guebwiller"] <- "GEB"
d$hop[d$Organisme == "CH de Mulhouse ( Hasenrain)"] <- "MUL"
d$hop[d$Organisme == "CH de Mulhouse (Emile Muller-Moenschberg"] <- "MUL"
d$hop[d$Organisme == "CH de Saverne"] <- "SAV"
d$hop[d$Organisme == "CH de Sélestat"] <- "SEL"
d$hop[d$Organisme == "CH de Thann"] <- "TAN"
d$hop[d$Organisme == "CH de Wissembourg"] <- "WIS"
d$hop[d$Organisme == "CHU de Strasbourg (Hôp. Civil)"] <- "HUS"
d$hop[d$Organisme == "CHU de Strasbourg(Hautepierre)"] <- "HUS"
d$hop[d$Organisme == "Clinique des Diaconesses"] <- "DIA"
d$hop[d$Organisme == "Clinique Ste Odile (Strasbourg"] <- "ODI"
d$hop[d$Organisme == "Clinique des 3 Frontières"] <- "CTF"
```

Renommage de la colonne *service* par la création d'une nouvelle colonne *ser2*

```r
d$ser2[d$service == "CCOM Chirurgie"] <- "CCOM"
d$ser2[d$service == "Upatou"] <- "sALK"
d$ser2[d$service == "SAU Le Parc"] <- "pCOL"
d$ser2[d$service == "SAU Pasteur"] <- "aCOL"
d$ser2[d$service == "UHTCD"] <- "sGEB"
d$ser2[d$service == "PEDIATRIE NEONATOLOGIE"] <- "pMUL"
d$ser2[d$service == "URGENCES"] <- "aMUL"
d$ser2[d$service == "S.A.U. (ADULTES)"] <- "aSAV"
d$ser2[d$service == "PEDIATRIE"] <- "pSAV"
d$ser2[d$service == "Acceuil des urgences"] <- "sSEL"
d$ser2[d$Organisme == "CH de Thann" & d$service == "Urgences"] <- "sTAN"
d$ser2[d$Organisme == "CH de Wissembourg" & d$service == "Urgences"] <- "sWIS"
d$ser2[d$service == "Urgences Médico-Chirurgicales NHC"] <- "NHC"
d$ser2[d$service == "Urgences chirurgicales pédiatriques"] <- "pHTP"
d$ser2[d$service == "Urgences Adulte HTP"] <- "aHTP"
d$ser2[d$service == "Gynéco-Obstétrique (HTP)"] <- "gHTP"
d$ser2[d$service == "SOS Main"] <- "sDIA"
d$ser2[d$Organisme == "Clinique Ste Odile (Strasbourg" & d$service == "UPATOU"] <- "sODI"
d$ser2[d$service == "UPATOU (Structure des urgences)"] <- "sCTF"
d$ser2[d$Organisme == "CH de Wissembourg" & d$service == "Urgences "] <- "sWIS"
```

Sauvegarde:

```r
save(d, file = "sau2013.Rda")
```

