# Diagramme d'activité · Préparer une candidature

Parcours principal du MVP, du CV collé jusqu'au rapport.

![Diagramme d'activité](diagrams/activite.svg)

<sub>Source : [diagrams/activite.puml](diagrams/activite.puml)</sub>

## Points clés

### Le LLM ne fait que deux choses

**1. Extraire** du texte en données structurées : le CV, l'offre, la lettre et chaque nouvelle version d'un document.

- Les **preuves** (issues du CV) et les **exigences** (issues de l'offre) sont relues et corrigées par l'utilisateur avant de servir à l'analyse (US-02, US-05).
- Les **compétences affichées** (issues du CV ou de la lettre) ne sont pas relues une par une. Le rapport montre chacune avec sa formulation d'origine : une extraction erronée se voit tout de suite.

**2. Rédiger des formulations honnêtes** pour chaque écart important (US-09) :

- **Pour quels écarts** : exigence obligatoire manquante, compétence vue seulement en formation, et chaque alerte d'honnêteté.
- **Ce que le LLM reçoit** : l'écart détecté par les règles et les preuves validées qui s'y rapportent. Rien d'autre.
- **Ce qu'il propose** : une formulation pour le CV ou la lettre qui présente l'écart sans le cacher. Exemple : « Microservices : découverts en formation sur [projet], pas encore en production. »
- **Garde-fou contre l'invention** : chaque suggestion doit citer les preuves sur lesquelles elle s'appuie. Le code vérifie que ces preuves existent et sont validées. Une suggestion qui cite une preuve inexistante est écartée.
- **Ce ne sont que des propositions** : rien n'est modifié automatiquement. L'utilisateur reprend ce qu'il veut dans une nouvelle version de son document, puis relance l'analyse.

Classement, score et alertes, eux, restent des **règles déterministes** : le LLM ne rend aucun verdict.

### Documents

- **Le CV joue deux rôles.** Il sert à construire le profil : les expériences et les preuves, relues par l'utilisateur. Il est aussi le document analysé : les compétences qu'il affiche.
- **Une nouvelle version du CV** met à jour les compétences affichées, qui sont extraites de nouveau. Les expériences qu'elle ajoute sont détectées par comparaison avec le profil et proposées à la relecture (US-14). Les expériences déjà connues ne sont jamais modifiées automatiquement.
- **La lettre est facultative** et se colle au moment de l'analyse.
- **Modifier un document ne réécrit jamais l'ancien** : on crée une nouvelle version, puis une nouvelle analyse, ce qui permet de les comparer (US-10).
