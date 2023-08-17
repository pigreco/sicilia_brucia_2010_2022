# Aree percorse dal fuoco Sicilia 2010-2022

--------- IN COSTRUZIONE ---------

<!-- TOC -->

- [Aree percorse dal fuoco Sicilia 2010-2022](#aree-percorse-dal-fuoco-sicilia-2010-2022)
  - [Tabella](#tabella)
  - [Quota](#quota)
  - [Istogramma](#istogramma)
  - [Mappa](#mappa)
  - [DATI](#dati)
  - [RIFERIMENTI](#riferimenti)
- [Espressioni usate nel filtro Atlante](#espressioni-usate-nel-filtro-atlante)
    - [trova la pagina dell'Atlante con il comune con max numero di incendi](#trova-la-pagina-dellatlante-con-il-comune-con-max-numero-di-incendi)
    - [trova la pagina dell'Atlante con il comune con max numero di incendi tra quelli commissariati](#trova-la-pagina-dellatlante-con-il-comune-con-max-numero-di-incendi-tra-quelli-commissariati)
    - [trova i comuni, con numero max di anni, percorsi da incendi e commissariati nel 2023](#trova-i-comuni-con-numero-max-di-anni-percorsi-da-incendi-e-commissariati-nel-2023)
    - [trova i comuni che non hanno mai subito incendi](#trova-i-comuni-che-non-hanno-mai-subito-incendi)
    - [trova i comuni inadempienti o commissariati](#trova-i-comuni-inadempienti-o-commissariati)

<!-- /TOC -->

Analisi delle aree percorse dal fuoco in Sicilia tra gli anni 2010 e 2022 - dati SIF

QGIS:
![](imgs/img02bis.png)

QGIS pagina atlante:
![](imgs/img03.png)

## Tabella

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

- **QGIS**: <https://www.qgis.org/it/site/>


# Espressioni usate nel filtro Atlante

![](imgs/filtro.png)

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

### trova i comuni, con numero max di anni, percorsi da incendi e commissariati nel 2023

```
maximum(relation_aggregate('rel','count_distinct',"anno"))
=
relation_aggregate('rel','count_distinct',"anno")
AND 
"commissario" IS NOT NULL
```

risultato:<br>
Burgio, Carlentini, Catania, Licata, Niscemi, Randazzo, Caccamo,   Castelmola, Cefalù, Mongiuffi Melia, Ragalna, Sciacca

### trova i comuni che non hanno mai subito incendi

```
relation_aggregate( 'rel', 'sum', "sup_bruciate") = 0
```
risultato:<br>
Aci Bonaccorsi, Canicattì, Castrofilippo, Favignana, Ficarazzi, Joppolo Giancaxio, Mazzarrone, Merì, Milazzo, Misiliscemi, Misterbianco, Montedoro, Pace del Mela, Petrosino, Pozzallo, Raddusa, 
Ramacca, Riposto, San Pietro Clarenza, Sant'Agata li Battiati, Scordia, Ustica, Valverde.

esempio:

![](imgs/comuni_mai_percorsi_da_incendi/Aci%20Bonaccorsi.png)

### trova i comuni inadempienti o commissariati

```
"commissario" is not null
```

risultato:<br>
Aci Castello, Acireale, Adrano, Agira, Alcara li Fusi, Alì, Antillo, Aragona, Assoro, Augusta, Barcellona Pozzo di Gotto, Belpasso, Brolo, Burgio, Butera, Caccamo, Calamonaci, Caltavuturo, Cammarata, Campofelice di Fitalia, Camporeale, Capizzi, Capo d'Orlando, Capri Leone, Carlentini, Casalvecchio Siculo, Castel di Iudica, Casteldaccia, Castelmola, Casteltermini, Castronovo di Sicilia, Catania, Cefalù, Centuripe, Cesarò, Comitini, Condrò, Contessa Entellina, Falcone, Favara, Ficarra, Floridia, Fondachelli-Fantina, Forza d'Agrò, Francavilla di Sicilia, Francofonte, Furci Siculo, Furnari, Gaggi, Gagliano Castelferrato, Gallodoro, Gela, Giarre, Gioiosa Marea, Giuliana, Grammichele, Graniti, Grotte, Gualtieri Sicaminò, Itala, Leni, Letojanni, Licata, Licodia Eubea, Lipari, Lucca Sicula, Maletto, Malvagna, Mandanici, Maniace, Mascali, Menfi, Milena, Militello in Val di Catania, Milo, Mineo, Mirabella Imbaccari, Monforte San Giorgio, Mongiuffi Melia, Montalbano Elicona, Montallegro, Motta Camastra, Motta Sant'Anastasia, Naro, Naso, Nicosia, Niscemi, Nissoria, Nizza di Sicilia, Novara di Sicilia, Palma di Montechiaro, Partanna, Paternò, Patti, Pettineo, Pietraperzia, Piraino, Ragalna, Randazzo, Ravanusa, Reitano, Riesi, Roccafiorita, Roccalumera, Roccapalumba, Rodì Milici, Rosolini, San Cono, San Fratello, San Giovanni Gemini, San Gregorio di Catania, San Mauro Castelverde, San Michele di Ganzaria, San Teodoro, San Vito Lo Capo, Sant'Agata di Militello, Sant'Alessio Siculo, Sant'Angelo di Brolo, Santa Cristina Gela, Santa Flavia, Santa Margherita di Belice, Santa Marina Salina, Santo Stefano di Camastra, Savoca, Scaletta Zanclea, Sciacca, Siracusa, Sperlinga, Taormina, Terme Vigliatore, Terrasini, Torregrotta, Torrenova, Torretta, Trapani, Tremestieri Etneo, Troina, Valderice, Valdina, Venetico, Viagrande, Vicari, Villafranca Sicula, Villafranca Tirrena, Vita, Vizzini, Zafferana Etnea.

![](imgs/comuni_inadempienti/Alì.png)
