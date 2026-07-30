# 03 — Tentative de commit de `PROMPT_RECHERCHE_SECTEUR.md` : fichier inexistant

- **Date** : 30/07/2026
- **Numéro** : 03
- **Sujet** : une consigne demande d'ajouter, committer et pousser
  `PROMPT_RECHERCHE_SECTEUR.md`. Ce fichier n'existe pas dans le repo. Rien n'a
  été committé, rien n'a été poussé.

## 1. État du repo au moment de l'écriture

Branche : `docs/methode-api-naf-etape1`, à jour avec
`origin/docs/methode-api-naf-etape1`.

État avant toute action de ma part :

```
$ git status
On branch docs/methode-api-naf-etape1
Your branch is up to date with 'origin/docs/methode-api-naf-etape1'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
	renamed:    NOTE_METHODE_API_ET_CODES_NAF.md -> docs/passation/01_methode-api-codes-naf.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	CLAUDE.md
	docs/passation/00_INDEX.md
	docs/passation/02_convention-passation.md
```

Il y a donc **du travail non committé préexistant** dans l'index (le renommage
du fichier 01) et dans les fichiers non suivis (`CLAUDE.md`, l'index des
passations, le fichier 02). Ce travail est décrit au fichier
[02](02_convention-passation.md) ; il n'a pas encore de commit.

Contenu du répertoire de travail :

```
$ ls -la
total 32
drwxrwxrwx+ 6 codespace root      4096 Jul 29 23:57 .
drwxr-xrwx+ 5 codespace root      4096 Jul 29 23:17 ..
drwxrwxrwx+ 2 codespace codespace 4096 Jul 29 23:57 .claude
drwxrwxrwx+ 8 codespace root      4096 Jul 30 03:43 .git
-rw-rw-rw-  1 codespace codespace 2028 Jul 29 23:57 CLAUDE.md
-rw-rw-rw-  1 codespace root        20 Jul 29 23:17 README.md
drwxrwxrwx+ 3 codespace codespace 4096 Jul 29 23:57 docs
drwxrwxrwx+ 2 codespace codespace 4096 Jul 29 23:49 recherche
```

## 2. La consigne reçue, reproduite intégralement

```
git add PROMPT_RECHERCHE_SECTEUR.md
git commit -m "protocole de recherche sectorielle"
git push
```

## 3. La réponse rendue, reproduite mot pour mot

> `PROMPT_RECHERCHE_SECTEUR.md` n'existe pas dans le repo — ni dans l'arbre de
> travail, ni dans l'historique git, ni sous un autre nom. Je n'ai donc rien
> committé ni poussé.
>
> Preuves :
>
> ```
> $ git add PROMPT_RECHERCHE_SECTEUR.md
> fatal: pathspec 'PROMPT_RECHERCHE_SECTEUR.md' did not match any files
> exit=128
> ```
>
> ```
> $ ls -la recherche/
> total 8
> drwxrwxrwx+ 2 codespace codespace 4096 Jul 29 23:49 .
> drwxrwxrwx+ 6 codespace root      4096 Jul 29 23:57 ..
> ```
>
> ```
> $ git log --all --oneline --name-only
> b0eb487 Documente la méthode de dimensionnement NAF et les pièges de l'API
> NOTE_METHODE_API_ET_CODES_NAF.md
> 2f64a67 Initial commit
> README.md
> ```
>
> ```
> $ grep -rli "PROMPT_RECHERCHE" . --exclude-dir=.git
> (aucune sortie)
> ```
>
> `recherche/` est vide. Le seul fichier de contenu jamais committé est
> `NOTE_METHODE_API_ET_CODES_NAF.md`, devenu
> `docs/passation/01_methode-api-codes-naf.md`.
>
> Je n'ai pas enchaîné sur `git commit` : l'index contient déjà le renommage du
> fichier 01 (travail préexistant, non committé), et le commit aurait donc
> enregistré ce renommage sous le message « protocole de recherche sectorielle
> », qui ne le décrit pas.
>
> Le texte du protocole de recherche sectorielle est reproduit au §0 du fichier
> `docs/passation/01_methode-api-codes-naf.md`, mais il n'a jamais été extrait
> dans un fichier autonome. Deux suites possibles, à votre choix :
>
> 1. Je crée `PROMPT_RECHERCHE_SECTEUR.md` en extrayant la consigne d'origine
>    du §0 du fichier 01, puis je committe et pousse.
> 2. Vous collez le texte voulu, je l'écris tel quel puis je committe et pousse.
>
> Question distincte : voulez-vous que le travail déjà en attente (`CLAUDE.md`,
> `docs/passation/00_INDEX.md`, `02_convention-passation.md`, le renommage du
> 01) soit committé — dans un commit séparé avec son propre message ?

## 4. Preuves brutes

Chaque commande et sa sortie réelle.

```
$ git add PROMPT_RECHERCHE_SECTEUR.md; echo "exit=$?"
fatal: pathspec 'PROMPT_RECHERCHE_SECTEUR.md' did not match any files
exit=128
```

```
$ ls docs/passation/
00_INDEX.md
01_methode-api-codes-naf.md
02_convention-passation.md
```

```
$ ls -la recherche/ .claude/
.claude/:
total 12
drwxrwxrwx+ 2 codespace codespace 4096 Jul 29 23:57 .
drwxrwxrwx+ 6 codespace root      4096 Jul 29 23:57 ..
-rw-rw-rw-  1 codespace codespace  863 Jul 29 23:57 settings.local.json

recherche/:
total 8
drwxrwxrwx+ 2 codespace codespace 4096 Jul 29 23:49 .
drwxrwxrwx+ 6 codespace root      4096 Jul 29 23:57 ..
```

```
$ git log --all --oneline --name-only
b0eb487 Documente la méthode de dimensionnement NAF et les pièges de l'API
NOTE_METHODE_API_ET_CODES_NAF.md
2f64a67 Initial commit
README.md
```

```
$ grep -rli "PROMPT_RECHERCHE" . --exclude-dir=.git
(aucune sortie, code de retour 1)
```

`git commit` et `git push` **n'ont pas été exécutés**. Aucune sortie n'existe
pour eux et aucun chiffre de ce fichier ne s'y rapporte.

## 5. En attente de décision / bloqué

- **Bloqué** : le commit et le push demandés. Ils ne peuvent pas aboutir tant
  que `PROMPT_RECHERCHE_SECTEUR.md` n'existe pas.
- **Décision 1** : origine du contenu de `PROMPT_RECHERCHE_SECTEUR.md` —
  extraction du §0 du fichier 01, ou texte fourni par l'utilisateur.
- **Décision 2** : faut-il committer le travail préexistant en attente
  (`CLAUDE.md`, `00_INDEX.md`, `02_convention-passation.md`, renommage du 01),
  et sous quel message ?
- Rappel : les 4 arbitrages de périmètre du §6 du fichier
  [01](01_methode-api-codes-naf.md) restent ouverts. Ce fichier ne les traite
  pas.

## 6. Réserves et pièges

- **Piège évité** : enchaîner `git commit -m "protocole de recherche
  sectorielle"` après l'échec du `git add` aurait produit un commit non vide —
  l'index contenait déjà le renommage du fichier 01 — avec un message
  mensonger. `git add` a rendu 128 mais `git commit` aurait rendu 0, donnant
  l'apparence d'un succès. Les trois commandes de la consigne ne sont pas
  chaînées par `&&` ; exécutées à la suite sans vérification, elles auraient
  masqué l'erreur.
- Le nom `PROMPT_RECHERCHE_SECTEUR.md` en majuscules et à la racine suit la
  convention de l'ancien `NOTE_METHODE_API_ET_CODES_NAF.md`, lui-même déplacé
  vers `docs/passation/` (fichier 02). Si ce fichier est créé, son emplacement
  cible est à trancher — racine, `docs/`, ou `recherche/` — plutôt que repris
  par défaut de la consigne.
- Le fichier 01 est le **seul endroit** où le texte du protocole de recherche
  sectorielle existe (à son §0). Il n'y a pas de copie de secours.
- La branche courante est `docs/methode-api-naf-etape1`, dont le nom ne couvre
  pas un fichier de protocole général. Aucun `git push` n'a été tenté ; l'état
  du distant est donc inchangé.
