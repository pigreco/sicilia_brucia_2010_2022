# Aree percorse dal fuoco Sicilia 2010-2022

--------- IN COSTRUZIONE ---------

Analisi delle aree percorse dal fuoco in Sicilia tra gli anni 2010 e 2022 - dati SIF

QGIS:
![](imgs/img02bis.png)

QGIS pagina atlante:
![](imgs/img03.png)

## tabella

![](imgs/tabella.png)

- `Commissariato 2023`: indica se il comune corrente è stato commissariato nel 2023
- `Area bruciate`: indica il numero di aree bruciate dal 2010 al 2022;
- `TOT area [ha]`: indica la somma delle supoerfici bruciate dal 2010 al 2022
- `anni`: indica il numero di anni in cui il comune corrente è stato percorso da incendi;
- `area comunale [%]`: indica la percentuale di superficie comunale (tolta l'area dei centri abitati) rispetto alla superficie delle aree bruciate nello stesso comune;
- `overlap aree [%]`: indica la percentuale di aree bruciate sovrapposte negli anni

## Quota

![](imgs/quota.png)

sono quote sul livello del mare e indicano la quota massima dell'area percorsa dagli incendi del comune corrente, la minima e la quota media della singola area bruciata. (NB: i punti sono stati tracciati come point on surface per ogni aree bruciata e il calcolo della quota è stata derivata dal DTM Tinitaly)

## Istogramma

![](imgs/istogramma.png)

rappesenta la superficie percorsa dal fuoco - per ogni comune - negli anni dal 2010 al 2022; in ascisse gli anni, in ordinata la somma deglle aree percorse dagli indendi per ogni anno.

## Mappa

![](imgs/mappa.png)

nella mappa è rappresentato, oltre al nome del comune e provincia:
- come sfondo OpenStreetMap;
- i limiti amministrativi del comune corrente;
- le aree percorse dal fuoco dal 2010 al 2022;
- l'area dei centri abitati;
- punti:
  - in rosso il punto con quota massima dell'incendio;
  - in verde il punto con quota minima dell'incendio.


## DATI

- [CONFINI DELLE UNITÀ AMMINISTRATIVE A FINI STATISTICI AL 1° GENNAIO 2023](https://www.istat.it/it/archivio/222527)
-  [Ufficio stampa della Regione Siciliana - commissari](https://www.regione.sicilia.it/la-regione-informa/incendi-nominati-commissari-catasto-aree-bruciate-nei-comuni-inadempienti)
-  [Banca dati della Regione Siciliana costituita da una serie di banche dati del settore forestale SIF (Sistema Informativo Forestale)](https://sifweb.regione.sicilia.it/arcgis/rest/services)


## RIFERIMENTI

- QGIS: <https://www.qgis.org/it/site/>


## Espressioni usate nel filtro Atlante

### trova la pagina dell'Atlante con il comune con max numero di incendi
```
maximum(relation_aggregate('rel', 'count', @id))
= 
relation_aggregate('rel', 'count', @id) 
```

![](imgs/comuni_max_nro_incendi/Monreale.png)

### trova la pagina dell'Atlante con il comune con max numero di incendi tra quelli commissariati

```
maximum(relation_aggregate('rel','count',"commissario"='Sì'))
= 
relation_aggregate('rel','count',"commissario"='Sì')
```
![](imgs/comuni_max_nro_incendi/Randazzo.png)

### trova i comuni con numero max di anni percorsi da incendi e commissariati nel 2023

```
maximum(relation_aggregate('rel','count_distinct',"anno"))
=
relation_aggregate('rel','count_distinct',"anno")
AND 
"commissario" IS NOT NULL
```
