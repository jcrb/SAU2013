SAU2013 - libreOffice2R
========================================================
Tansforme les données saisies dans un tableur Libre Office en un fichier R.


```r
file <- "~/Documents/Resural/Stat Resural/SAU2013"
setwd(file)
d2 <- read.csv("sau2013.csv", header = TRUE, sep = ",")
```

Préparation des données
------------------------
Transformation de la colonne *date* du format jj/mm/aaaa au format yyyy-mm-dd

```r
d2$date <- as.Date(d2$date, "%d/%m/%Y")
```

date du fichier:

```r
min(d2$date)
```

```
## [1] "2013-01-01"
```

```r
max(d2$date)
```

```
## [1] "2013-03-19"
```


Renommage de la colonne *organisme* par la création d'une nouvelle colonne *hop*
NB: on ignore le CMCO. Deux structures sont absentes de la base: Sta anne et Diaconnat-Fonderie

```r
d2$hop[d2$Organisme == "CCOM"] <- "HUS"
d2$hop[d2$Organisme == "CH Altkirch"] <- "ALK"
d2$hop[d2$Organisme == "CH de Colmar (CMC Le Parc)"] <- "COL"
d2$hop[d2$Organisme == "CH de Colmar (Louis Pasteur)"] <- "COL"
d2$hop[d2$Organisme == "CH de Guebwiller"] <- "GEB"
d2$hop[d2$Organisme == "CH de Mulhouse ( Hasenrain)"] <- "MUL"
d2$hop[d2$Organisme == "CH de Mulhouse (Emile Muller-Moenschberg"] <- "MUL"
d2$hop[d2$Organisme == "CH de Saverne"] <- "SAV"
d2$hop[d2$Organisme == "CH de Sélestat"] <- "SEL"
d2$hop[d2$Organisme == "CH de Thann"] <- "TAN"
d2$hop[d2$Organisme == "CH de Wissembourg"] <- "WIS"
d2$hop[d2$Organisme == "CHU de Strasbourg (Hôp. Civil)"] <- "HUS"
d2$hop[d2$Organisme == "CHU de Strasbourg(Hautepierre)"] <- "HUS"
d2$hop[d2$Organisme == "Clinique des Diaconesses"] <- "DIA"
d2$hop[d2$Organisme == "Clinique Ste Odile (Strasbourg"] <- "ODI"
d2$hop[d2$Organisme == "Clinique des 3 Frontières"] <- "CTF"
```

Renommage de la colonne *service* par la création d'une nouvelle colonne *ser2*

```r
d2$ser2[d2$service == "CCOM Chirurgie"] <- "CCOM"
d2$ser2[d2$service == "Upatou"] <- "sALK"
d2$ser2[d2$service == "SAU Le Parc"] <- "pCOL"
d2$ser2[d2$service == "SAU Pasteur"] <- "aCOL"
d2$ser2[d2$service == "UHTCD"] <- "sGEB"
d2$ser2[d2$service == "PEDIATRIE NEONATOLOGIE"] <- "pMUL"
d2$ser2[d2$service == "URGENCES"] <- "aMUL"
d2$ser2[d2$service == "S.A.U. (ADULTES)"] <- "aSAV"
d2$ser2[d2$service == "PEDIATRIE"] <- "pSAV"
d2$ser2[d2$service == "Acceuil des urgences"] <- "sSEL"
d2$ser2[d2$Organisme == "CH de Thann" & d2$service == "Urgences"] <- "sTAN"
d2$ser2[d2$Organisme == "CH de Wissembourg" & d2$service == "Urgences"] <- "sWIS"
d2$ser2[d2$service == "Urgences Médico-Chirurgicales NHC"] <- "NHC"
d2$ser2[d2$service == "Urgences chirurgicales pédiatriques"] <- "pHTP"
d2$ser2[d2$service == "Urgences Adulte HTP"] <- "aHTP"
d2$ser2[d2$service == "Gynéco-Obstétrique (HTP)"] <- "gHTP"
d2$ser2[d2$service == "SOS Main"] <- "sDIA"
d2$ser2[d2$Organisme == "Clinique Ste Odile (Strasbourg" & d2$service == "UPATOU"] <- "sODI"
d2$ser2[d2$service == "UPATOU (Structure des urgences)"] <- "sCTF"
d2$ser2[d2$Organisme == "CH de Wissembourg" & d2$service == "Urgences "] <- "sWIS"
```

Sauvegarde
----------

```r
d <- d2
save(d, file = "sau2013.Rda")
```


