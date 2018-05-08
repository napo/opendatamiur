# Tutorial per imparare python/pandas investigando i dati del MIUR

Il tutorial è stato sviluppato all'interno dell'evento ["Laboratorio sulle competenze Open Data all’Opificio Golinelli"](http://www.ervet.it/?p=13032)
![](https://raw.githubusercontent.com/napo/opendatamiur/master/images/header.png)

## Setup
il tutorial si sviluppa utilizando [jupyter notebook](http://jupyter.org/) per python.

Per iniziare si consiglia di installare l'ambiente [anaconda](https://anaconda.org/) ed eseguire così jupyter notebook. Anacoda è disponibile per i sistemi operativi Linux, Windows e Apple.

## HOWTO
Il tutorial viene veicolato aprendo il file [MIUR OpenData](https://github.com/napo/opendatamiur/blob/master/MIUR_OpenData.ipynb) e da lì seguire i comandi presentati passo-passo.<br/>
I singoli comandi si trovano nelle celle grigie e sono introdotti dal testo del tutorial.<br/>
Lo studente può aprire il proprio jupyter notebook sul proprio computer e copiare e incollare i comandi presentati per testarli e capirli.

Il tutorial guida lo studente a conoscere come interrogare le varie tabelle messe a disposizione dal MIUR attraverso [pandas](http://pandas.pydata.org) (una libreria python molto potente per l'analisi dati).<br/>
L'analisi dei dati aiuta anche a capire come è strutturata la scuola in Italia.

Lo studente sarà così in grado di interrogare i dati, effettuare qualche calcolo e manipolazione e creare grafici

Il tutorial è strutturao in modo che poi, il docente, possa delegare gli studenti a lavorare in gruppo in modo da ripetere quanto acquisito.

Oltre a pandas vengono introdotti, in maniera molto semplice, le librerie [geocoder](http://geocoder.readthedocs.io/) e [folium](http://folium.readthedocs.io) con cui poter geocodificare dati e creare mappe.

## Riassunto python
ecco un piccolo riassunto di cosa viene veicolato dal tutorial riguardo python pandas (ed altro)

### importare moduli 
vanno caricati (*import*) e in alcuni [casi installati](#potenziarepython)

questi i moduli usati
```python
     import requests
     import io
     import pandas as panda
     import geocode
     import folium
```
### metodi per interrogare un DataFrame (tabella) pandas
(nell'esempio *nometabella*)

#### conoscere le prime 3 righe (ma il valore possiamo cambiarlo
```python
   nometabella.head(3)
```
#### la forma della tabella (numero di righe e numero di colonne)
```python
   nometabella.shape
```
#####  e da lì il numero di righe
```python
   nometabella.shape[0]
```
##### e il numero di colonne
```python
   nometabella.shape[1]
```
##### i nomi delle colonne
```python
   nometabella.columns
```
##### e contare quante sono
```python
   nometabella.columns.size
```
#####  avere una descrizione su come è fatta una colonna di un dataframe partendo dal suo nome 
(es. *nomecolonna*))
```python
   nometabella.nomecolonna.describe()
```

### unire più DataFrame 
```python
   panda.concat([tabella1, tabella2])
```
### confrontare colonne fra tabelle diverse 
(es. *tabella1* e *tabella2*)
```python
   tabella1.columns.equals(tabella2.columns)
```
###  vedere cosa cambia fra le colonne delle due tabelle
```python
   tabella1.columns.difference(tabella2.columns)
```

### individuare i valori univoci all'interno di una colonna
```python
   nometabella.nomecolonna.unique()
```
### contare il numero di volte in cui compare ogni valore della colonna
```python
   nometabella.groupby(nometabella.nomecolonna).size()
```
### ordinare una tabella per i valori di una colonna
```python
   nometabella.sort_values("nomecolonna")
```
### filtrare una tabella per un valore di una colonna
```python
   nometabella[nometabella.nomeoclonna == 'valore da cercare']
```
### trasformare tutti i valori di una tabella con un altro
Esempio: trasformare tutti i "SI" in "1"
```python
    nometabella.eq('SI').mul(1)
```

### ribaltare righe con colonne (pivot)
#### scegliendo quale colonna usare come indice
```python
   nometabella.pivot_table(index='colonnacomeindice')
```
##### e se necessario assegnare il valore zero dove i valori mancano
```python
   nometabella.pivot_table(index='colonnasceltacomeindice').fillna(0)
```
##### ed anche più complesse dove sommare i valori  presenti in una colonna
```python
   nometabella.pivot_table(index='colonnasceltacomeindice', columns='colonnescelte', values='colonnaconivalori',
                aggfunc='sum', fill_value=0)
```


### rappresentare i valori di un dataframe in grafico a barre verticali
e con dimensioni 10x10 in DPI [punti per pollice](https://it.wikipedia.org/wiki/Punti_per_pollice) e assegnare un titolo
```python
   nometabella.plot.bar(title='titolo',figsize[10,10])
```
#### e a barre orizzontali
```python
   nometabella.plot.barh(title='titolo',figsize[10,10])
```
#### e a barre orizzontali a segmenti
```python
    nometabella.plot.bar(stacked=True,figsize=(10,10))
```
#### e a barre verticali a segmenti scegliendo i colori
*colormap* è una variabile che può essere in ogni grafico.

l'elenco dei colori si trova qui https://matplotlib.org/examples/color/colormaps_reference.html
```python
    nometabella.plot.hbar(stacked=True,figsize=[10,10],colormap='Pastel2')
```

### usare un geocoder
con komoot

```python
geocoder.komoot("Via Paolo Nanni Costa, 14, Bologna, Italia")
```
con google

```python
geocoder.google("Opificio Golinelli")
```
#### ed estrarre latitudine e longitudine
```python
   opificio_gollinelli = geocoder.komoot("Opificio Gollinelli")
   latitudine = opificio_gollinelli.latlng[0]
   longitudine = opificio_gollinelli.latlng[1]
```


### rappresentare un punto su una mappa
es.
latitudine = 44.5082397
longitudine = 11.3066287

```python
    mappa = folium.Map(location=[44.5082397, 11.3066287])
    folium.Marker([44.5082397, 11.3066287]).add_to(mappa)
```
