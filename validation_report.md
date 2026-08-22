# Rapport de validation — version 1.1.0

Statut : RÉUSSI

- Lignes : 10 000
- Colonnes : 7
- Identifiants uniques : 10 000
- Textes uniques : 10 000
- Textes vides : 0
- Familles de templates : 104
- Labels : 5 000 spam, 5 000 légitimes
- Domaines : 5 000 SMS, 5 000 emails
- Splits : entraînement 6335, validation 1834, test 1831
- Chevauchement des familles entre les splits : non
- Encodage : UTF-8

## Méthode

Les messages sont synthétiques et générés à partir de composants linguistiques diversifiés. Les identifiants de familles sont calculés avec SHA-256 après normalisation des composants de génération. Les familles sont séparées avant l'assignation des splits afin d'éviter que des variantes proches apparaissent dans plusieurs ensembles.

## Réserve d'interprétation

La validation confirme l'intégrité technique du fichier et la séparation des familles. Elle ne prouve pas la représentativité du corpus par rapport aux messages réels. Une évaluation externe sur des données naturelles reste nécessaire.

## Empreinte d'intégrité

SHA-256 de `data/messages.csv` :

`8d8f9130838a0bea10bc4f99dbe563b2ca903f90be38aa13a9a57c46e33aac4d`
