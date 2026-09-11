# Predikcija koncentracije PM2.5 primenom mašinskog učenja

Projekat se bavi primenom i poređenjem različitih metoda mašinskog učenja za predviđanje koncentracije PM2.5 na osnovu vremenskih i meteoroloških podataka.

##  Pregled projekta

U projektu su implementirani i upoređeni sledeći regresioni modeli:

- Linearna regresija i ElasticNet
- SVM
- KNN
- Random Forest
- Potpuno povezana neuronska mreža

Pored formiranja modela, izvršeni su analiza i priprema skupa podataka, podešavanje hiperparametara i poređenje performansi dobijenih modela.

### Rezultati

Na test skupu dobijeni su sledeći rezultati:

- Linearna regresija: R² = 0.268, MAE = 57.60, RMSE = 79.90
- ElasticNet: R² = 0.268, MAE = 57.51, RMSE = 79.90
- RBF SVM: R² = 0.652, MAE = 32.52, RMSE = 55.06
- KNN: R² = 0.619, MAE = 33.10, RMSE = 57.62
- Random Forest: R² = 0.799, MAE = 25.66, RMSE = 41.90
- Neuronska mreža: R² = 0.697, MAE = 33.49, RMSE = 51.44

Najbolje performanse ostvario je Random Forest model, sa najvećom R² vrednošću i najmanjim vrednostima MAE i RMSE.

##  Metodologija

### Skup podataka

U projektu je korišćen skup podataka `PRSA_data_2010.1.1-2014.12.31.csv`, koji sadrži podatke o koncentraciji PM2.5 i meteorološkim uslovima u Pekingu u periodu od 2010. do 2014. godine.

Skup sadrži 43.824 zapisa i 13 atributa. Ciljna promenljiva je `pm2.5`, dok ostali relevantni atributi predstavljaju vremenske i meteorološke podatke, kao što su temperatura, atmosferski pritisak, temperatura tačke rose, pravac i brzina vetra, kiša i sneg.

### Priprema podataka

Pre treniranja modela izvršeni su:

- uklanjanje atributa `No`, koji predstavlja redni broj zapisa
- uklanjanje redova sa nedostajućom vrednošću ciljne promenljive `pm2.5`
- one-hot kodiranje kategorijskog atributa `cbwd`
- izdvajanje ulaznih atributa i ciljne promenljive
- podela podataka na trening, validacioni i test skup
- standardizacija ulaznih atributa kod modela kod kojih je potrebna

Trening skup korišćen je za obučavanje modela, validacioni skup za izbor hiperparametara i najboljih varijanti modela, dok je test skup korišćen za konačnu evaluaciju.

##  Implementirani modeli

### 1. Linearna regresija i ElasticNet

Linearna regresija primenjena je kao osnovni regresioni model.

Pored nje primenjen je ElasticNet, koji kombinuje L1 i L2 regularizaciju. Podešavanjem hiperparametara kao najbolje vrednosti izabrane su:

- `alpha = 0.01`
- `l1_ratio = 0.5`

Linearna regresija i ElasticNet ostvarili su veoma slične rezultate, sa R² vrednošću od približno 0.27 na test skupu.

Rezultati ukazuju da linearni modeli imaju ograničenu sposobnost da opišu složenije odnose između ulaznih atributa i koncentracije PM2.5.

### 2. SVM

Ispitani su linearni SVM i SVM sa RBF kernelom.

RBF kernel omogućava modelovanje nelinearnih odnosa i ostvario je značajno bolje rezultate od linearnog SVM modela.

Kao najbolji hiperparametri izabrani su:

- `C = 100`
- `gamma = 1`

RBF SVM na test skupu ostvario je R² vrednost od približno 0.65.

### 3. KNN

Kod KNN regresionog modela ispitane su različite vrednosti broja najbližih suseda.

Najbolji rezultat na validacionom skupu ostvaren je za:

- `k = 2`

Konačni KNN model na test skupu ostvario je R² vrednost od približno 0.62.

### 4. Random Forest

Kod Random Forest modela ispitane su različite vrednosti broja stabala i maksimalne dubine stabala.

Kao najbolji hiperparametri izabrani su:

- `n_estimators = 200`
- `max_depth = None`

Random Forest na test skupu ostvario je R² vrednost od približno 0.80 i pokazao se kao najbolji od svih ispitanih modela.

U okviru analize Random Forest modela dodatno je analizirana važnost ulaznih atributa za formiranje predviđanja.

### 5. Potpuno povezana neuronska mreža

Ispitane su tri različite arhitekture potpuno povezane neuronske mreže:

- prva arhitektura - dva skrivena sloja sa 32 i 16 neurona
- druga arhitektura - dva skrivena sloja sa 64 i 32 neurona
- treća arhitektura - tri skrivena sloja sa 128, 64 i 32 neurona

Sve arhitekture imaju jedan neuron u izlaznom sloju, jer se rešava regresioni problem.

U skrivenim slojevima korišćena je ReLU aktivaciona funkcija, dok je za optimizaciju korišćen Adam optimizator.

Poređenjem rezultata na validacionom skupu kao najbolja izabrana je treća arhitektura, sa tri skrivena sloja od 128, 64 i 32 neurona.

Ova arhitektura na test skupu ostvarila je R² vrednost od približno 0.70.
## Zaključak

Rezultati projekta pokazuju da nelinearni modeli ostvaruju značajno bolje performanse od linearnih modela pri predviđanju koncentracije PM2.5.

Linearna regresija i ElasticNet ostvarili su najslabije rezultate, dok su KNN, SVM sa RBF kernelom i neuronska mreža ostvarili značajno veće R² vrednosti.

Od svih ispitanih pristupa najbolje performanse ostvario je Random Forest model, sa R² vrednošću od približno 0.80 na test skupu.

Dobijeni rezultati ukazuju da su nelinearni modeli pogodniji za modelovanje složenih odnosa između vremenskih i meteoroloških atributa i koncentracije PM2.5.
