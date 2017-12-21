# Sitzung 04. Datenabfragen. Konflikte in Git.

## Augaben für die Sitzung
1. Von der Lippe. Statistik. 1999
   Kapitel 3.

2. Arbeit mit den DataFrames:
   Sie bekommen einen ersten Datensatz und eine Reihe der Aufgaben,
   zu jeder Augabe gibt es eine Funktion, die Sie verwenden können.


2.1. Legen Sie einen DataFrame mit den folgenden Daten an:

    Wortart    TokenFrequenz	TypenFrequenz	Klasse
    ADJ	    421               271		offen
    ADV	    337      		    103		offen
    N	        1411              735		offen
    KONJ	    458               18 		geschlossen
    PRAEP	    455		        37		geschlossen

``` R
  Wortart <- c('ADJ', 'ADV', 'N', 'KONJ', 'PRAEP')
  TokenFrequenz <- c(421, 337, 1411, 458, 455)
  ...

  x <- data.frame(Wortart, TokenFrequenz, ...)

  str(x) # Was ist mit Faktoren passiert?

  x <- data.frame(Wortart, TokenFrequenz, ..., row.names=Wortart)

```

2.2. DF speichern:

``` R
  write.table(x, file=, sep='\t')
  # Siehe. `?write.table`

```
2.3. DF einlesen:

``` R
  # Standardparameter studieren: `?read.table`
  x <- read.table(file='', header=(TRUE|FALSE), row.names=1)

```
2.4. Elemente Ansprechen:

``` R
  x$TokenFrequenz
  x$Klasse

  attach(x)
  TokenFrequenz
  Klasse

  x[2,3]
  x[2,]
  x[,3]
  x[2]

  x[2:3, 3:4]
```

2.5. Konditionale Abfragen:

``` R
  x$Klasse == 'offen'
  x[x$Klasse == 'offen',]

  x[x[,4] == 'offen',]

  x[x$Klasse == 'offen',][x$TypenFrequenz > 150,]

   x[x$Klasse == 'offen',][x$TypenFrequenz < 500,]
  x[x$Klasse == 'geschlossen',][x$TypenFrequenz > 100,]

  x[,3][which(x[,2] > 450)]

```

2.6. subset

``` R
  subset(x, x$Klasse == 'geschlossen')

  # Wie wird das leere Ergebnis notiert?
  subset(x, x$Klasse == 'offen' & x$TypenFrequenz < 100)

  subset(x, x$Klasse == 'offen' & x$TypenFrequenz < 200)

  subset(x, x$Klasse == 'offen' | x$Wortart == 'KONJ')

  # unzulässig
  subset(x, x$Klasse == 'offen' | x$Wortart == ('KONJ' | 'PRAEP'))
  subset(x, x$Klasse == 'offen' | x$Wortart %in% c('KONJ', 'PRAEP'))
  subset(x, x$Wortart %in% c('N', 'ADJ'))
```

2.7. fix(): Eingebauter Editor

``` R
  fix(x) # не знаю, как оно под виндой будет
```

2.8. Sortieren

``` R
  vec <- c(1,5,2,3)
  sort(vec) # => [1] 1 2 3 5
  order(vec) # => [1] 1 3 4 2

  # `?order`
  x[order(x$TypenFrequenz),]
  x[order(-x$TypenFrequenz),]

```

2.9. Zufälligkeiten: sample()

``` R
  x[sample(length(x$Klasse)),] # попробовать несколько раз
```
