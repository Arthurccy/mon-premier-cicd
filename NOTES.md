# Notes TP S4

## Experimentation 1 - fail-fast

Configuration principale :

- `fail-fast: false` dans la matrice Node.js.
- Si Node 20 echoue, le job Node 18 continue.
- Le job `report` demarre quand meme grace a `if: always()`.
- Le workflow final echoue si `lint` ou `test` n'est pas en succes.

Questions a valider dans GitHub Actions apres l'experience :

1. `test(18)` est-il annule quand `test(20)` echoue ? Non avec `fail-fast: false`.
2. Le job `report` demarre-t-il malgre l'echec ? Oui, grace a `if: always()`.
3. Que contient le Step Summary ? Le tableau de couverture disponible et le resultat global.
4. Quel est l'exit code final du workflow ? Echec, car `report` sort avec `exit 1`.

## Experimentation 2 - concurrency

La configuration suivante annule les runs obsoletes sur une meme branche :

```yaml
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true
```

Observation attendue : si trois pushes arrivent rapidement, les anciens runs sont annules et seul le plus recent va au bout.

## Experimentation 3 - artefacts

Artefacts attendus sur un run vert :

- `coverage-node-18`
- `coverage-node-20`

Les deux rapports doivent normalement afficher les memes pourcentages de couverture, car le code teste ne depend pas d'une API differente entre Node 18 et Node 20.

## Challenge 1 - path filters

Risque d'un filtre trop restrictif : un changement important peut ne pas declencher la CI, par exemple une modification de configuration, de documentation executable, de workflow ou de dependances oubliee dans les chemins surveilles.
