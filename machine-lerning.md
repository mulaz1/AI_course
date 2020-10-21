# Machine Learning 
[Slide](https://elly2020.dia.unipr.it/pluginfile.php/29265/mod_resource/content/1/03_introduzione_ML_iris2D.pdf)

## Five Step to Start
* > Porre una domanda interessante (che tempo fara' domani cose cosí)
* > Ottenere i dati
* > Esplorare i dati
* > Creare un modello per i dati
* > Comunicare e presentare i risultati

***

## Librerie di Python
* > Scikit-learn *contiene algoritmi di ML per python*
* > Pandas *Gestione matrici* 
* > Numpy *Gestione matrici* 
* > Matplotlib  *plotting dei dati*
* > Jupyter Notebook *visualizzazione web spezzettato per vedere cosa sta facendo* 

***

## "HELLO WORLD!" example (IRIS-2D)

> Problema di classificazione degli Iris 
 
![](https://www.giardinaggio.net/giardino/bulbi/iris_NG1.jpg)

Libraries:
```python
from sklnear.datasets import load_iris
import pandas as pd
import Matplotlib.pyplot as plotting
import numpty as np 
iris = load_iris()
iris.keys()
```

### formalismo standard 

> *__x__ sono le feature ( insieme di classificazioni dei valori delle colonne delle features*

> *__y__ minuscolo classi del dataset ( colonna delle classi)*

__Il programma una volta inseriti i dati tirera' fuori una distribuzione di questo tipo:__ [guarda slide](https://elly2020.dia.unipr.it/pluginfile.php/29265/mod_resource/content/1/03_introduzione_ML_iris2D.pdf)
![](http://www.r-project.it/_book/53-classification-CTREE_files/figure-html/bq-1.png)
  
###Codice Python

```python

# importo il modulo tree da sklearn (scikit-learn) libreria per ML
from sklearn import tree
# fra gli alberi scelgo un albero di decisione
clf = tree.DecisionTreeClassifier()
# l'operazione di fit addestra il classificatore coi dati presenti in X e y clf = clf.fit(X, y)

```


Esistono diversi tipologie di sistemi decisionali

* __DecisionTreeClassifier__ ( *Albero decisionale* )
  ![](https://scikit-learn.org/stable/_images/iris.png)

### Abbiamo addestrato il nostro modello --> Ora dobbiamo testarlo

Per testarlo gli diamo due nuovi fiori uno blu e uno rosso

Possiamo chiamare la classe Predict:


```python 
    clf.predict([[4, 1.5]])     #Essendo vicino al gruppo Virginica   riuscira' ad azzeccarlo con facilita' 
    array([1])
```

```python
clf.predict([[5, 1.6]])            
clf.predict_proba([[5, 1.6]])

```

 __Piu' si e' lontani dalla linea creata dal logaritmo piu' la probabilita' di azzeccarci diminuisce__
