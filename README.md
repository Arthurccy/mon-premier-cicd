# mon-premier-cicd

[![CI Pipeline](https://github.com/VOTRE_USERNAME/mon-premier-cicd/actions/workflows/ci.yml/badge.svg)](https://github.com/VOTRE_USERNAME/mon-premier-cicd/actions/workflows/ci.yml)

## Description

Premier pipeline CI/CD avec GitHub Actions, Node.js, Jest et ESLint.

## Lancer les tests

```bash
npm ci
npm test
```

## Lancer le lint

```bash
npm run lint
```

## Pipeline CI/CD

Le workflow GitHub Actions se lance automatiquement sur les push et pull requests vers `main`.

Etapes principales :

- checkout du code
- installation de Node.js
- installation stricte avec `npm ci`
- verification ESLint
- tests Jest avec couverture
- archivage du rapport de couverture

Bonus inclus :

- jobs paralleles `lint` et `test`
- matrice de tests sur Node.js 18 et 20
- seuil minimum de couverture Jest a 80%
