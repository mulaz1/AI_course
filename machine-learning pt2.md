## Machine Learning Part 2

usiamo sklearn

> clf.predict(item)  return classe di appartenenza

>clf.predict_proba(item) return la probabilita' della classe di appartenenza

Esempio con item [2,2]

INPUT
```python
clf.predict([2,2])
clf.predit_prova([2,2]])
```
OUTPUT
```python 

array(2)
array([[0, 0.33, 0,66]]) # 33% classe 2 o 66% classe 3 

```
### SVM

```python
    # cambiamo classificatore
    # Support Vector Machine
    from sklearn.svm import SVC
    clf = SVC(gamma='auto', probability=True)
    clf.fit(X, y)
    print(clf.predict([[4, 1.5]]))
    print(clf.predict_proba([[4, 1.5]]))
```

OUTPUT 

```python 
array([1])
array([[ 0.00839442, 0.97857937, 0.01302621]])
```

La __confidence__ è spalmata sulle tre classi

confidence: livello di affidabilità della predizione

## Valutazione del classificatore

* Dataset Split
* Cross Validation

## Dataset Split

dividere il data set in due parti : 
    * Una parte di training ( solitamente 66%)
    * Una parte di test ( solitamente 33%)

Límportante e' che non siano tutti i dati per i test 

### classi bilanciate

> Ossia tenere un numero di esempi uguale per tutte le classi di addestramento
Altrimenti in caso di incertezza il nostro sistema riportara la classe che conosce meglio

#### Esempio

> Dividiamo il dataset (X,y) in [(X_train, y_train) e (X_test, y_test)]

INPUT
```python
from sklearn.model_selection import train_test_split
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.33, random_state=42)
print(len(X_train), len(y_train))
print(len(X_test), len(y_test))

```

OUTPUT 

```python
100 100
50 50
```

> Addestriamo sul solo training set

```python

clf.fit(X_train, y_train) 

```

__Testiamo il classificatore addestrato sul solo training set__
Sia sullo stesso __training set__ che sul __test set__

INPUT 
```python 

print("TRAIN SET", clf.score(X_train, y_train))
print("TEST SET", clf.score(X_test, y_test))
```


OUTPUT

```Python

TRAIN SET 0.99 # errore di 1%
TEST SET 0.98 # errore di 2%

```

Probabilemte sbagliera gli elementi piu' esterni del albero decisionale

concetto di __accuracy__ - accuratezza della classificazione
> Quali sono gli errori ??

```python
print("Errori in training set")
predictions = clf.predict(X_train)
for elem, prediction, label in zip(X_train, predictions, y_train):
if prediction != label:
print(elem, 'has been classified as ', prediction, 'and should be ', label)
# similmente per test set...

```
OUTPUT

```python 

Errori in training set
[ 4.8 1.8] has been classified as 2 and should be 1
Errori in test set
[ 5.1 1.5] has been classified as 1 and should be 2

```

#### Matrice di confusione

* quanti elementi di una certa classe sono associati alle altre classi

```python

from sklearn.metrics import confusion_matrix
cm = confusion_matrix(y_train, clf.predict(X_train))
print("CM per Train set\n", cm)
# similmente per test set...

```

OUTPUT 

```python

CM per Train set
[[31 0 0]
[ 0 34 1]
[ 0 0 34]]

CM per Test set
[[19 0 0]
[ 0 15 0]
[ 0 1 15]]   # sbagliato un elemento di classe 2

```

* Se trovo tanti errori su una riga significa che quella classe e' confusa e si fatica a predirla significa che i dati del training set di quella classe non vanno bene ( esempi poco legati a quella classe )

* Altrimenti va molto bene e abbiamo il 100% di  accuratenzza ( matrice diagonale )

#### Valutazione del classificatore

## Cross Validation

* Se abbiamo pochi dati e non possiamo permetterci di splittare fra train e test set ( e non posso permettermi di dividerli )
* parametri
  * folds (numero di blocchi in cui suddivido il mio dataset)

![](/images/image6.png)
> cross_val_score ( classificatore, elementi e il numero di cross validation)
```python 

from sklearn.model_selection import cross_val_score
print(cross_val_score(clf, X, y, cv=4))

```
OUTPUT 

Restituisce l'accuracy di tutte le cross validation e poi faccio la media di tutti i risultati

```python 

[ 0.97435897 0.94871795 0.91666667 0.97222222] 

#accuracy 0.95
```