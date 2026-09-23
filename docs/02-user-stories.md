# User stories

Priorités **MoSCoW** : **M**ust, **S**hould, **C**ould, **W**on't.

## E1 · Profil

### US-01 · Importer mon CV — **M**

> En tant que candidat·e, je veux coller le texte de mon CV **afin que** mes expériences et mes compétences soient extraites sans ressaisie.

- Le texte collé est enregistré comme un `Document` de type CV.
- Le système propose des expériences (type, poste, structure, dates) et, pour chacune, les compétences utilisées.
- Le système relève aussi les compétences que le CV **affiche**, avec le niveau et le nombre d'années quand ils sont indiqués. Ce sont elles que l'analyse d'honnêteté confronte aux preuves.
- Tout ce qui est proposé reste **non validé** tant que je ne l'ai pas relu.
- Si l'extraction échoue, un message clair s'affiche et le texte collé n'est pas perdu.

### US-02 · Valider mes preuves — **M**

> En tant que candidat·e, je veux relire, corriger et valider chaque expérience et chaque compétence **afin que** l'analyse repose uniquement sur ce que je peux prouver.

- Je peux modifier le type d'une expérience (pro, formation, perso), ses dates et les compétences associées.
- Je peux supprimer une proposition erronée.
- Seuls les éléments **validés** sont utilisés dans l'analyse.

### US-03 · Ajouter une preuve à la main — **S**

> En tant que candidat·e, je veux ajouter une expérience ou une compétence oubliée par l'extraction.

### US-14 · Enrichir mon profil depuis une nouvelle version du CV — **S**

> En tant que candidat·e, je veux que les expériences ajoutées dans une nouvelle version de mon CV me soient proposées **afin de** ne pas avoir à les ressaisir dans mon profil.

- À chaque nouvelle version du CV, les expériences extraites sont comparées à celles du profil.
- Une expérience est considérée comme **déjà connue** si la structure est la même (après normalisation) et si les périodes se chevauchent. Cette comparaison est faite par le code, pas par le LLM.
- Seules les expériences nouvelles me sont proposées, non validées, avec leurs compétences. Je les relis comme en US-02.
- Les expériences déjà connues ne sont jamais modifiées automatiquement.

## E2 · Offre

### US-04 · Importer une offre — **M**

> En tant que candidat·e, je veux coller le texte d'une offre **afin d'**obtenir la liste de ses exigences.

- Chaque exigence indique : la compétence correspondante (ou « aucune correspondance »), obligatoire ou souhaitée, et le nombre d'années demandé s'il est précisé.
- Le texte d'origine de chaque exigence est conservé.

### US-05 · Corriger les exigences — **M**

> En tant que candidat·e, je veux corriger les exigences mal extraites de l'offre **afin que** l'analyse ne me pénalise pas à cause d'une erreur du LLM.

- Je peux passer une exigence d'obligatoire à souhaitée, et inversement. Exemple : « Docker serait un plus » extrait à tort comme obligatoire.
- Je peux rattacher une exigence à une compétence du référentiel quand l'extraction l'a laissée sans correspondance ou s'est trompée. Exemple : « framework JS côté serveur » → NestJS.
- Je peux supprimer une exigence qui n'en est pas une, comme une phrase sur les avantages de l'entreprise.

## E3 · Analyse

### US-06 · Voir mon adéquation — **M**

> En tant que candidat·e, je veux voir, pour chaque exigence, si je la maîtrise, si je l'ai vue en formation ou si elle me manque, **afin de** savoir où j'en suis vraiment.

- Classement : preuve professionnelle → _maîtrisé_ ; preuve en formation ou en projet perso → _vu en formation_ ; aucune preuve → _manquant_.
- Chaque classement affiche la preuve qui le justifie.
- Score sur 100 : exigence obligatoire ×2, souhaitée ×1 ; maîtrisé = 1, vu en formation = 0,5, manquant = 0.

### US-07 · Repérer ce que je ne peux pas défendre — **M**

> En tant que candidat·e, je veux être alerté·e quand mon CV affiche une compétence qu'aucune preuve ne justifie **afin de** ne pas être pris·e au dépourvu en entretien.

- Compétence affichée sans aucune preuve validée → alerte **forte**.
- Niveau affiché « avancé » ou « expert » avec seulement une preuve en formation → alerte **moyenne**.
- Nombre d'années affiché supérieur à la durée cumulée des preuves → alerte **moyenne**.

### US-08 · Vérifier la cohérence CV / lettre — **S**

> En tant que candidat·e, je veux savoir si ma lettre contredit mon CV.

- Une compétence citée dans la lettre mais absente du CV est signalée.
- Un niveau ou un nombre d'années différent entre les deux documents est signalé.

### US-09 · Présenter honnêtement un écart — **M**

> En tant que candidat·e, je veux, pour chaque écart important, une proposition de formulation honnête **afin de** le présenter au lieu de le cacher.

- Exemple : « Microservices : pas d'expérience en production, découverts en formation sur [projet]. »
- La suggestion ne doit jamais inventer une expérience qui n'existe pas : elle cite les preuves validées sur lesquelles elle s'appuie, et le code écarte toute suggestion qui cite une preuve inexistante.
- Rien n'est modifié automatiquement : l'utilisateur reprend ce qu'il veut dans une nouvelle version de son document.

### US-10 · Historique des analyses — **S**

> En tant que candidat·e, je veux comparer une analyse avec la précédente après avoir modifié mon CV.

## E4 · Suivi

### US-11 · Statut de candidature — **C**

> En tant que candidat·e, je veux indiquer si une candidature est en brouillon, envoyée, en entretien, acceptée ou refusée.

- Ajoutera une table `Application` dédiée au suivi : l'offre, le statut, la date d'envoi et l'analyse retenue.

### US-12 · Tableau de suivi — **W**

> En tant que candidat·e, je veux une vue d'ensemble de toutes mes candidatures.

## E5 · Démo

### US-13 · Démo en lecture seule — **S**

> En tant que visiteur·se, je veux parcourir une analyse d'exemple sans configurer quoi que ce soit.

- Données fictives, aucun appel au LLM, aucune écriture en base.
