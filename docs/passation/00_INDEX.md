# Index des passations

Un fichier par consigne reçue et réponse rendue. Convention définie dans
`CLAUDE.md`, section « Passation ».

Chaque fichier est autonome : il se lit sans accès à la conversation d'origine.
Ils ne se répètent pas entre eux — un fichier renvoie au numéro d'un autre
plutôt que de recopier son contenu.

Statuts : `validé` (la décision est prise, le contenu fait foi) /
`en attente` (une décision est requise pour avancer) /
`périmé` (contredit ou remplacé par un fichier ultérieur).

| N° | Date | Sujet | Statut |
|---|---|---|---|
| [01](01_methode-api-codes-naf.md) | 29/07/2026 | Méthode de dimensionnement NAF, pièges de l'API recherche-entreprises, et 71 codes NAF candidats pour les 8 secteurs | **en attente** — 4 arbitrages de périmètre requis avant tout comptage (cf. §6 du fichier) |
| [02](02_convention-passation.md) | 29/07/2026 | Mise en place de la convention de passation : `CLAUDE.md`, cet index, et déplacement du fichier 01 à son emplacement normalisé | validé |
| [03](03_commit-prompt-recherche-secteur-echec.md) | 30/07/2026 | Tentative de commit de `PROMPT_RECHERCHE_SECTEUR.md` : le fichier n'existe pas dans le repo. Rien n'a été committé ni poussé | **en attente** — décision 1 (origine du contenu) levée par le fichier 04 ; décision 2 (sort du travail en attente de commit) toujours ouverte |
| [04](04_ecriture-prompt-recherche-secteur.md) | 30/07/2026 | Écriture du protocole tel quel dans `PROMPT_RECHERCHE_SECTEUR.md` : les 4 chaînes de contrôle sont présentes, mais le fichier fait 400 lignes et non 358 | **en attente** — vérification en échec sur le compte de lignes, aucune suite enchaînée |

## État d'avancement du projet

Protocole de recherche sectorielle : voir la consigne d'origine reproduite au
§0 du fichier 01.

- **Étape 1 (dimensionnement NAF)** : méthode établie et vérifiée, comptage
  **non démarré** — bloqué sur les 4 arbitrages du §6 du fichier 01.
- **Étapes 2 à 6** : non lancées. Aucun éditeur, aucun avis, aucune contrainte
  réglementaire n'a été recherché.
- **Fichiers de résultat** : aucun. `recherche/PREFILTRE_NAF.md` n'existe pas
  encore. Aucun fichier secteur n'a été créé.
- **`PROMPT_RECHERCHE_SECTEUR.md`** : existe à la racine, 400 lignes, contenu
  fourni par l'utilisateur et écrit tel quel. **Validé** (cf. fichier 05) :
  l'écart 400 vs 358 venait du contrôle, pas du fichier. Contrôle de référence
  désormais `grep -c "" PROMPT_RECHERCHE_SECTEUR.md` entre 350 et 420, plus les
  quatre chaînes « /18 », « 3 000 », « Trustpilot », « 48 h ».
- **Branche** : `main` uniquement. Jamais de branche de travail, jamais de PR.
- **Commits** : `main` a été avancé sur `b0eb487` (avance rapide), puis deux
  commits ont été ajoutés — `protocole de recherche sectorielle`, puis
  `convention de passation et fichiers 00 à 04`. Détail au fichier 05.
