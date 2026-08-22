# Dataset français de détection des spams

<p align="center"><img src="https://img.shields.io/badge/🚀_VERSION-1.1.0-7c3aed?style=for-the-badge&labelColor=111827"><img src="https://img.shields.io/badge/📦_MESSAGES-10_000-0ea5e9?style=for-the-badge&labelColor=111827"><img src="https://img.shields.io/badge/🇫🇷_LANGUE-Français-f97316?style=for-the-badge&labelColor=111827"></p>
<p align="center"><img src="https://img.shields.io/badge/🧪_NATURE-Synthétique_diversifié-e11d48?style=for-the-badge&labelColor=111827"><img src="https://img.shields.io/badge/🛡️_SÉPARATION-Splits_par_templates-16a34a?style=for-the-badge&labelColor=111827"><img src="https://img.shields.io/badge/⚖️_LICENCE-CC_BY_4.0-f59e0b?style=for-the-badge&labelColor=111827"></p>

> Corpus synthétique diversifié de textes français pour entraîner et évaluer des modèles de classification `spam` / `legitimate` sur SMS et emails.

## Présentation

Cette version remplace les formulations trop répétitives de la version précédente par des messages synthétiques plus variés : styles conversationnels, formulations professionnelles, longueurs différentes, références contextuelles et variations de vocabulaire. Ils restent synthétiques et ne doivent pas être présentés comme des messages réellement collectés.

## Chiffres clés

| Propriété | Valeur |
|---|---:|
| Messages | 10 000 |
| Spam / légitime | 5 000 / 5 000 |
| SMS / emails | 5 000 / 5 000 |
| Familles de templates | 104 |
| Entraînement / validation / test | 6335 / 1834 / 1831 |
| Textes uniques | 10 000 |
| Encodage | UTF-8 |

## Fichiers

- `data/messages.csv` — dataset prêt pour la modélisation.
- `DATASET_CARD.md` — provenance, usages, risques et limites.
- `validation_report.md` — contrôles d'intégrité et de séparation.
- `LICENSE.md` — licence CC BY 4.0 et attribution.

## Schéma

`id`, `text`, `label`, `domain`, `spam_category`, `split`, `template_group`.

Utilisez `text` comme entrée et `label` comme cible. N'utilisez pas `id` ni `template_group` comme variables de modèle. `spam_category` est une information de supervision secondaire et doit être exclue d'un classifieur binaire standard.

## Limites

Ce corpus est synthétique. Sa diversité est supérieure à la version précédente, mais il ne reproduit pas parfaitement les fautes, les habitudes, les langues mélangées, les campagnes émergentes et la distribution réelle des spams. Une validation finale sur des données réelles obtenues légalement reste indispensable.

## Intégrité

SHA-256 de `data/messages.csv` :

```text
8d8f9130838a0bea10bc4f99dbe563b2ca903f90be38aa13a9a57c46e33aac4d
```

## Citation

> Dataset français de détection des spams, version 1.0, corpus synthétique diversifié, 2026.
