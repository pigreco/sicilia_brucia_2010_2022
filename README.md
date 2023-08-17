# Aree percorse dal fuoco Sicilia 2010-2022

--------- IN COSTRUZIONE ---------

Analisi delle aree percorse dal fuoco in Sicilia tra gli anni 2010 e 2022 - dati SIF

QGIS:
![](imgs/img02bis.png)

QGIS pagina atlante:
![](imgs/img03.png)

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
