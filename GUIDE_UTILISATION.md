# Guide d'utilisation

## Objectif

Ce guide explique comment utiliser `data/messages.csv` pour entraîner,
valider et tester un modèle de détection des spams en français.

Le dataset contient des messages synthétiques. Il est adapté à
l'apprentissage initial, aux expériences, aux benchmarks et au
prototypage. Une évaluation sur des messages réels reste nécessaire
avant toute utilisation en production.

## 1. Installation

Installez Python 3.9 ou une version plus récente, puis les bibliothèques
nécessaires :

```bash
pip install pandas scikit-learn
```

## 2. Chargement du dataset

```python
import pandas as pd

dataset = pd.read_csv("data/messages.csv")

print(dataset.head())
print(dataset.shape)
print(dataset["label"].value_counts())
```

Les colonnes principales sont :

- `text` : texte à analyser ;
- `label` : classe cible, `spam` ou `legitimate` ;
- `domain` : type de message, `sms` ou `email` ;
- `split` : ensemble d'utilisation ;
- `spam_category` : catégorie du spam ;
- `template_group` : identifiant d'audit à ne pas utiliser comme entrée du modèle.

## 3. Séparation des ensembles

Les ensembles sont déjà fournis dans le fichier. Il est recommandé de
les conserver tels quels :

```python
train = dataset[dataset["split"] == "train"]
validation = dataset[dataset["split"] == "validation"]
test = dataset[dataset["split"] == "test"]
```

N'utilisez pas les données de test pendant l'entraînement ou le réglage
des hyperparamètres.

## 4. Préparation des données

Pour un classifieur binaire standard, utilisez :

```python
X_train = train["text"]
y_train = train["label"]

X_validation = validation["text"]
y_validation = validation["label"]

X_test = test["text"]
y_test = test["label"]
```

Les colonnes `id` et `template_group` doivent être exclues des entrées
du modèle. La colonne `spam_category` doit également être exclue si
l'objectif est uniquement de prédire `spam` ou `legitimate`.

## 5. Exemple complet avec TF-IDF et régression logistique

```python
import pandas as pd

from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import Pipeline
from sklearn.metrics import classification_report, confusion_matrix

dataset = pd.read_csv("data/messages.csv")

train = dataset[dataset["split"] == "train"]
validation = dataset[dataset["split"] == "validation"]
test = dataset[dataset["split"] == "test"]

modele = Pipeline([
    ("tfidf", TfidfVectorizer(
        lowercase=True,
        ngram_range=(1, 2),
        min_df=2,
        sublinear_tf=True
    )),
    ("classification", LogisticRegression(
        max_iter=1000,
        class_weight="balanced"
    ))
])

modele.fit(train["text"], train["label"])

prediction_validation = modele.predict(validation["text"])
print("Résultats sur la validation :")
print(classification_report(
    validation["label"],
    prediction_validation,
    digits=4
))

prediction_test = modele.predict(test["text"])
print("Résultats sur le test :")
print(classification_report(
    test["label"],
    prediction_test,
    digits=4
))

print("Matrice de confusion :")
print(confusion_matrix(test["label"], prediction_test))
```

## 6. Mesures à rapporter

Ne vous limitez pas à l'accuracy. Rapportez au minimum :

- la précision ;
- le rappel ;
- le score F1 ;
- la matrice de confusion ;
- les résultats séparés pour les SMS et les emails ;
- les résultats par catégorie de spam lorsque cela est pertinent.

Dans un système anti-spam, le rappel des spams et le taux de faux
positifs sont particulièrement importants. Un faux positif correspond à
un message légitime classé à tort comme spam.

## 7. Évaluation par domaine

Pour analyser les performances séparément sur les SMS et les emails :

```python
from sklearn.metrics import classification_report

for domaine in ["sms", "email"]:
    sous_ensemble = test[test["domain"] == domaine]
    predictions = modele.predict(sous_ensemble["text"])

    print(f"\nRésultats pour le domaine : {domaine}")
    print(classification_report(
        sous_ensemble["label"],
        predictions,
        digits=4
    ))
```

## 8. Prédire un nouveau message

```python
nouveau_message = [
    "Votre compte doit être vérifié immédiatement. Cliquez sur le lien."
]

prediction = modele.predict(nouveau_message)
probabilite = modele.predict_proba(nouveau_message)

print("Classe prédite :", prediction[0])
print("Probabilités :", probabilite[0])
```

## 9. Bonnes pratiques

- Conservez le jeu de test séparé jusqu'à l'évaluation finale.
- N'utilisez pas `template_group` comme variable d'entrée.
- Vérifiez les performances sur les SMS et les emails séparément.
- Testez le modèle avec des formulations jamais rencontrées.
- Analysez manuellement les faux positifs et les faux négatifs.
- Évaluez le modèle sur des données réelles indépendantes avant un
  déploiement.
- Prévoyez un seuil de décision adapté au coût des faux positifs.

## 10. Limites à prendre en compte

Les messages de ce dataset sont synthétiques. Une bonne performance
peut refléter l'apprentissage de régularités propres à la génération
des textes plutôt qu'une compréhension générale des spams français.

Ce dataset ne doit donc pas être utilisé seul pour prendre des décisions
automatiques dans un environnement réel. Il constitue une base pour
l'apprentissage, l'expérimentation et le prototypage.