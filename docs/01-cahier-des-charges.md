# Cahier des charges

## Contexte

Les outils d'aide à la candidature optimisent surtout le CV pour les filtres automatiques (ATS). Ils poussent à ajouter des mots-clés, parfois sans lien avec l'expérience réelle. Or un CV gonflé finit par se voir en entretien.

**Crédible** prend le contre-pied : il aide à présenter son profil de façon **juste et défendable**.

## Objectifs

| #   | Objectif                                          | Indicateur de réussite                                                                                    |
| --- | ------------------------------------------------- | --------------------------------------------------------------------------------------------------------- |
| O1  | Montrer l'écart réel entre un profil et une offre | Chaque exigence est classée « maîtrisé / vu en formation / manquant », avec la preuve correspondante      |
| O2  | Repérer ce qui ne se défend pas en entretien      | Les compétences affichées sans preuve sont signalées, avec peu de fausses alertes sur le jeu d'évaluation |
| O3  | Vérifier la cohérence CV / lettre                 | Les contradictions sur les technos, les niveaux ou les durées sont détectées                              |
| O4  | Aider à présenter honnêtement un écart            | Chaque écart important reçoit une proposition de formulation                                              |

## Utilisateurs

- **Candidat·e** (utilisateur principal) : développeur·se junior ou en reconversion qui postule à plusieurs offres et veut des candidatures solides.
- **Visiteur·se de la démo** (recruteur, curieux) : parcourt une démo en lecture seule, sur des données fictives.

## Périmètre fonctionnel

1. **Profil** : saisie du CV en texte, extraction automatique des expériences et des compétences, puis relecture et validation par l'utilisateur.
2. **Offre** : saisie de l'offre en texte, puis extraction structurée des exigences (obligatoires ou souhaitées, nombre d'années).
3. **Analyse** : comparaison entre le profil et l'offre, score, alertes d'honnêteté, cohérence CV / lettre, suggestions de formulation.
4. **Historique** : chaque analyse est conservée, avec l'offre et les versions exactes du CV et de la lettre analysées. Le suivi des candidatures (statut, envoi) viendra après le MVP.

## Exigences non fonctionnelles

| Domaine              | Exigence                                                                                                                             |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------ |
| Fiabilité            | Toute sortie du LLM est validée par un schéma Zod. En cas d'échec, une seule nouvelle tentative, puis une erreur explicite.          |
| Explicabilité        | Les verdicts (classement, score, alertes) viennent de **règles déterministes**. Le LLM extrait et rédige, il ne juge pas.            |
| Reproductibilité     | Chaque analyse enregistre le modèle et la version du prompt utilisés, et n'est jamais modifiée après coup.                           |
| Qualité              | Les règles sont testées avec Vitest. Un jeu d'évaluation construit à partir de vraies candidatures anonymisées mesure les résultats. |
| Performance          | Une analyse complète prend moins de 30 s.                                                                                            |
| Données personnelles | Le CV est une donnée personnelle : il n'est jamais envoyé ailleurs qu'au LLM, et la démo n'utilise que des données fictives.         |
| Déploiement          | Docker Compose, avec une CI GitHub Actions (lint, typecheck, tests, build).                                                          |

## Contraintes

- **Délai** : 7 jours.
- **Stack imposée** : NestJS, Next.js, PostgreSQL, Prisma, Zod, Vitest, Docker, et l'API Claude d'Anthropic.
- **Un seul profil, sans authentification**, pour le MVP.

## Hors périmètre (pour l'instant)

- Récupération automatique d'une offre à partir d'une URL : chaque site a sa propre structure.
- Import d'un CV en PDF.
- Plusieurs utilisateurs et authentification.
- Génération automatique d'un CV ou d'une lettre.
