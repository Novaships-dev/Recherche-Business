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
| [04](04_ecriture-prompt-recherche-secteur.md) | 30/07/2026 | Écriture du protocole tel quel dans `PROMPT_RECHERCHE_SECTEUR.md` : les 4 chaînes de contrôle sont présentes, mais le fichier fait 400 lignes et non 358 | `périmé` — écart tranché par le fichier 05 (le contrôle était faux, pas le fichier) ; contient aussi une affirmation fausse sur `recherche/PREFILTRE_NAF.md` |
| [05](05_commits-main-push-rejete.md) | 30/07/2026 | Contrôle validé, `main` avancé sur `b0eb487`, deux commits créés (`140f10f`, `b21534f`), **push rejeté** : `origin/main` avait divergé | validé sur les faits git ; **deux affirmations corrigées par le fichier 06** — le PR #1 était un rapatriement de fork après un 403, pas une session parallèle, et la règle « main uniquement » lui est postérieure |
| [06](06_merge-distant-claude-md-push-ok.md) | 30/07/2026 | Merge du distant, `CLAUDE.md` distant (199 l.) retenu et complété sur trois points, push réussi (`dccbd7a`). `PREFILTRE_NAF.md` 329 l. et `JOURNAL.md` 173 l. vérifiés, non touchés | **en attente** — le merge a retiré la convention de passation de `CLAUDE.md` ; décision A du fichier 06 requise |

## État d'avancement du projet

Protocole de recherche sectorielle : voir la consigne d'origine reproduite au
§0 du fichier 01.

- **Étape 1 (dimensionnement NAF)** : `recherche/PREFILTRE_NAF.md` existe (329
  lignes) et le `CLAUDE.md` en vigueur donne les dix secteurs comme « Comptés ».
  **Non vérifié dans cette session** : le fichier n'a pas été lu, consigne de ne
  pas y toucher. Les 4 arbitrages du §6 du fichier 01 sont donc peut-être clos —
  à confirmer en le lisant.
- **Étapes 2 à 6** : non lancées. Aucun éditeur, aucun avis, aucune contrainte
  réglementaire n'a été recherché.
- **Fichiers de résultat** : `recherche/PREFILTRE_NAF.md` (329 l.) et
  `recherche/JOURNAL.md` (173 l.), arrivés par le merge du fichier 06. Aucun
  fichier secteur n'a été créé.
- **`PROMPT_RECHERCHE_SECTEUR.md`** : existe à la racine, 400 lignes, contenu
  fourni par l'utilisateur et écrit tel quel. **Validé** (cf. fichier 05) :
  l'écart 400 vs 358 venait du contrôle, pas du fichier. Contrôle de référence
  désormais `grep -c "" PROMPT_RECHERCHE_SECTEUR.md` entre 350 et 420, plus les
  quatre chaînes « /18 », « 3 000 », « Trustpilot », « 48 h ».
- **Branche** : `main` uniquement, règle inscrite au §7 du `CLAUDE.md` en
  vigueur. Jamais de branche de travail, jamais de PR ; si un push échoue, le
  signaler et s'arrêter. La branche `docs/methode-api-naf-etape1` subsiste
  néanmoins, en local et sur `origin` — suppression non demandée.
- **Commits** : `main` poussé jusqu'à `dccbd7a`, aligné avec `origin/main`.
  Détail des commits aux fichiers 05 et 06.
- **`CLAUDE.md` en vigueur** : la version distante de 199 lignes, complétée à
  265 lignes (fichier 06). **Elle ne contient plus la convention de passation** —
  décision A du fichier 06, en attente.
