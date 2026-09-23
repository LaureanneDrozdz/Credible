# Périmètre du MVP

**Le MVP est atteint quand** je peux coller mon CV et une offre, et obtenir un rapport qui dit, preuve à l'appui, ce que je maîtrise, ce que j'ai seulement vu, ce qui me manque et ce que je ne pourrai pas défendre, avec une formulation honnête pour chaque écart.

## Dedans

| Story                        | Pourquoi c'est indispensable                                 |
| ---------------------------- | ------------------------------------------------------------ |
| US-01 Importer mon CV        | Point d'entrée du profil                                     |
| US-02 Valider mes preuves    | Garantit que l'analyse ne repose que sur des preuves réelles |
| US-04 Importer une offre     | Point d'entrée de l'offre                                    |
| US-05 Corriger les exigences | Une exigence mal extraite fausse directement le score        |
| US-06 Adéquation et score    | Première promesse du produit                                 |
| US-07 Alertes d'honnêteté    | Ce qui différencie Crédible des autres outils                |
| US-09 Formulations honnêtes  | La réponse concrète à chaque écart                           |

## Si le temps le permet (Should)

US-03, US-08 (cohérence CV / lettre), US-10, US-13 (démo), US-14 (enrichir le profil depuis une nouvelle version du CV).

## Dehors

- US-11 et US-12 : suivi et tableau des candidatures.
- Offre récupérée à partir d'une URL, CV importé en PDF.
- Authentification et plusieurs utilisateurs.

## Planning

| Jour | Contenu                                                                                         | Stories             |
| ---- | ----------------------------------------------------------------------------------------------- | ------------------- |
| J1   | Socle Docker, CI, modèle de données, seed du référentiel de compétences                         | —                   |
| J2   | Extraction de l'offre et du CV (LLM + Zod), **jeu d'évaluation v1**                             | US-01, US-04        |
| J3   | Relecture du profil et de l'offre, règles de classement et score, premier écran de bout en bout | US-02, US-05, US-06 |
| J4   | Alertes d'honnêteté et suggestions de formulation                                               | US-07, US-09        |
| J5   | Rapport côté front, cohérence CV / lettre si le temps le permet                                 | US-08               |
| J6   | Tests et mesures sur le jeu d'évaluation                                                        | —                   |
| J7   | README, déploiement, démo, vidéo                                                                | US-13               |

## Principaux risques

| Risque                                                           | Parade                                                                             |
| ---------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| Le LLM hallucine une compétence ou une preuve                    | Validation par l'utilisateur (US-02), verdicts rendus par des règles déterministes |
| Mauvaise correspondance des compétences (« Node » ≠ « Node.js ») | Référentiel `Skill` avec alias, rattachement fait par le LLM puis vérifié          |
| Le J4 déborde                                                    | US-08 (Should) est reportée, le front minimal existe déjà depuis le J3             |
| Coût de la démo publique                                         | Analyses calculées à l'avance, aucun appel au LLM en démo                          |
