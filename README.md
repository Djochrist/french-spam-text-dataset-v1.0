# Dataset français de détection des spams

<p align="center">
  <img src="https://img.shields.io/badge/🚀_VERSION-1.1.0-7c3aed?style=for-the-badge&labelColor=111827" alt="Version 1.1.0">
  <img src="https://img.shields.io/badge/📦_MESSAGES-10_000-0ea5e9?style=for-the-badge&labelColor=111827" alt="10 000 messages">
  <img src="https://img.shields.io/badge/🇫🇷_LANGUE-Français-f97316?style=for-the-badge&labelColor=111827" alt="Français">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/🧪_NATURE-Synthétique_diversifié-e11d48?style=for-the-badge&labelColor=111827" alt="Corpus synthétique diversifié">
  <img src="https://img.shields.io/badge/🛡️_SÉPARATION-Splits_par_templates-16a34a?style=for-the-badge&labelColor=111827" alt="Séparation par familles de templates">
  <img src="https://img.shields.io/badge/⚖️_LICENCE-CC_BY_4.0-f59e0b?style=for-the-badge&labelColor=111827" alt="Licence CC BY 4.0">
</p>

> Données synthétiques françaises destinées à l’entraînement et à l’évaluation de modèles d’intelligence artificielle dédiés à la détection des spams.

## Présentation

Ce dataset contient des SMS et des emails en français, répartis entre messages indésirables et messages légitimes. Les textes sont conçus pour entraîner, tester et comparer des modèles de classification automatique.

Le corpus comprend différentes formulations, longueurs, situations et catégories de spam afin de fournir une base de travail diversifiée pour les projets de traitement automatique du langage.

## Chiffres clés

| Propriété | Valeur |
|---|---:|
| Nombre total de messages | 10 000 |
| Messages spam | 5 000 |
| Messages légitimes | 5 000 |
| SMS | 5 000 |
| Emails | 5 000 |
| Familles de templates | 104 |
| Textes uniques | 10 000 |
| Textes vides | 0 |
| Encodage | UTF-8 |

## Répartition des données

| Ensemble | Nombre de messages |
|---|---:|
| Entraînement | 6 335 |
| Validation | 1 834 |
| Test | 1 831 |

Les familles de templates sont séparées entre les différents ensembles afin d’éviter qu’une même structure de message apparaisse à la fois dans l’entraînement et dans le test.

## Catégories de spam

Les messages indésirables sont répartis dans plusieurs catégories :

- Hameçonnage ;
- Arnaque ;
- Publicité non sollicitée ;
- Abonnement ou service surtaxé ;
- Sextorsion ou chantage ;
- Logiciel malveillant ou lien dangereux ;
- Autres types de spam.

Les messages légitimes utilisent la catégorie `unknown`.

## Structure du fichier

Le fichier principal est disponible à l’emplacement suivant :

```text
data/messages.csv
```

Il contient les colonnes suivantes :

| Colonne | Description |
|---|---|
| `id` | Identifiant unique du message |
| `text` | Contenu textuel du SMS ou de l’email |
| `label` | Étiquette : `spam` ou `legitimate` |
| `domain` | Type de message : `sms` ou `email` |
| `spam_category` | Catégorie du spam |
| `split` | Ensemble : `train`, `validation` ou `test` |
| `template_group` | Identifiant de la famille de template |

## Utilisation recommandée

Pour entraîner un modèle de classification :

- utilisez `text` comme donnée d’entrée ;
- utilisez `label` comme variable cible ;
- conservez les ensembles `train`, `validation` et `test` ;
- excluez `id` et `template_group` des variables utilisées par le modèle ;
- utilisez `domain` et `spam_category` uniquement comme informations auxiliaires.

Exemple de lecture avec Python :

```python
import pandas as pd

dataset = pd.read_csv("data/messages.csv")

train = dataset[dataset["split"] == "train"]
validation = dataset[dataset["split"] == "validation"]
test = dataset[dataset["split"] == "test"]

X_train = train["text"]
y_train = train["label"]
```

## Limites

Ce dataset est entièrement synthétique. Les messages sont uniques et diversifiés, mais ils ne proviennent pas de conversations réelles.

Il ne représente donc pas nécessairement :

- la fréquence réelle des spams ;
- toutes les habitudes d’écriture des utilisateurs ;
- les fautes et abréviations réellement utilisées ;
- les nouvelles techniques de fraude ;
- toutes les variétés de la langue française ;
- la diversité des messages reçus dans un environnement professionnel ou personnel.

Avant toute utilisation en production, il est recommandé de tester le modèle sur un corpus réel, légalement obtenu, anonymisé et annoté par des experts humains.

## Intégrité du fichier

L’empreinte SHA-256 du fichier `data/messages.csv` est :

```text
8d8f9130838a0bea10bc4f99dbe563b2ca903f90be38aa13a9a57c46e33aac4d
```

Cette empreinte permet de vérifier que le fichier utilisé correspond exactement à la version publiée.

## Licence

Le dataset est distribué sous licence **Creative Commons Attribution 4.0 International — CC BY 4.0**.

Cette licence autorise l’utilisation, la modification et la redistribution du dataset, y compris dans des projets commerciaux, à condition de créditer la source.

Attribution recommandée :

> Dataset français de détection des spams, version 1.1.0, corpus synthétique diversifié, 2026.

Consultez le fichier `LICENSE.md` pour plus d’informations.

## Citation

```text
Dataset français de détection des spams,
version 1.1.0,
corpus synthétique diversifié,
2026.
```
