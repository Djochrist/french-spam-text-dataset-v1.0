# Fiche descriptive du dataset

## Nature du corpus

Cette version contient 10 000 messages synthétiques uniques en français : SMS et emails, répartis équitablement entre spams et messages légitimes. Les textes sont générés par combinaison contrôlée de formulations, contextes, références et styles variés. Aucun message utilisateur réel n'est inclus.

## Utilisation prévue

- Prototypage et comparaison de modèles de classification de spams.
- Tests de pipelines de données et d'évaluation.
- Création de premiers benchmarks en français.

## Limites

Même lorsqu'ils sont naturels et uniques, les messages synthétiques ne constituent pas des observations réelles. Ils peuvent contenir des régularités de génération et ne représentent pas la prévalence, la diversité ou l'évolution des spams dans la population. Les résultats doivent être confirmés sur un corpus réel indépendant avant toute production.

## Contrôle de séparation

Les variantes issues d'une même famille de templates sont conservées dans un seul split. La colonne `template_group` sert à auditer cette séparation et ne doit pas être fournie au modèle.

## Confidentialité et droit d'utilisation

Le corpus ne contient intentionnellement aucune donnée personnelle réelle. Il est distribué sous licence CC BY 4.0 ; voir `LICENSE.md`. La responsabilité de vérifier les droits de publication et les usages dérivés incombe à l'utilisateur.
