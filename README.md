# mon-premier-cicd

[![CI - Lint, Tests & Coverage](https://github.com/Arthurccy/mon-premier-cicd/actions/workflows/ci.yml/badge.svg)](https://github.com/Arthurccy/mon-premier-cicd/actions/workflows/ci.yml)

## Description

Projet Node.js utilise pour construire un pipeline CI/CD avance avec GitHub Actions, Jest et ESLint.

## Lancer les tests

```bash
npm ci
npm test
npm run test:ci
```

## Lancer le lint

```bash
npm run lint
```

## Pipeline CI/CD avance

Le workflow GitHub Actions se lance automatiquement sur les push vers `main` et `feature/**`, sur les pull requests vers `main`, et manuellement avec `workflow_dispatch`.

Architecture des jobs :

- `lint` : verification ESLint sur Node.js 18
- `test` : tests Jest en matrice sur Node.js 18 et 20
- `ci-success` : job final qui attend `lint` et `test` avec `needs`

Fonctionnalites du TP S2 :

- jobs paralleles pour reduire le temps d'execution
- cache npm via `actions/setup-node`
- `fail-fast: false` pour obtenir tous les resultats de la matrice
- artefacts `coverage-node-18` et `coverage-node-20`
- resume de couverture dans `$GITHUB_STEP_SUMMARY`
- seuil minimum de couverture Jest a 80%
