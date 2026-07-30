# 05 — Contrôle validé, deux commits sur `main`, push rejeté : le distant a divergé

- **Date** : 30/07/2026
- **Numéro** : 05
- **Sujet** : le contrôle du fichier 04 est levé (l'écart 400 vs 358 venait du
  contrôle, pas du fichier). `main` a été avancé sur `b0eb487` puis les deux
  commits demandés ont été créés. **Le `git push` a été rejeté** : `origin/main`
  contient un PR mergé, inconnu en local, qui ajoute lui aussi `CLAUDE.md` avec
  un contenu différent. Arrêt demandé, arrêt effectué. Rien n'a été mergé,
  rebasé ni forcé.

## 1. État du repo au moment de l'écriture

- Branche courante : `main`, à `b21534f`.
- `origin/main` : à `7103c60`, **2 commits d'avance** inconnus en local.
- Base commune : `b0eb487`.
- Les deux branches ont donc **divergé**. Le distant n'a pas été modifié.

Ce fichier lève la décision A du fichier
[04](04_ecriture-prompt-recherche-secteur.md) (écart de lignes) et sa décision B
(les 5 lignes vides). Il lève aussi la décision C — le travail en attente est
committé — mais **pas poussé**.

## 2. La consigne reçue, reproduite intégralement

Deux messages successifs. Le premier était un simple renvoi du protocole,
recollé sans instruction ; il n'est pas reproduit ici (c'est le contenu de
`PROMPT_RECHERCHE_SECTEUR.md`, qui fait foi). Le second :

```
L'écart vient de mon contrôle, pas de ton fichier. Les 358 lignes
étaient mesurées avec wc -l sur la source ; le passage par la
conversation a ajouté des lignes vides. Les quatre marqueurs sont
présents, c'est le seul critère qui compte. Le fichier est bon.

Ne remets pas les 5 lignes vides, elles n'étaient pas
intentionnelles.

Nouveau contrôle de référence, à utiliser désormais :
grep -c "" PROMPT_RECHERCHE_SECTEUR.md  -> entre 350 et 420
et les quatre chaînes présentes.

Commit et push sur main : PROMPT_RECHERCHE_SECTEUR.md, plus le
travail en attente (CLAUDE.md, docs/passation). Deux commits séparés
avec des messages exacts.

Attention : tu es sur la branche docs/methode-api-naf-etape1. Bascule
sur main avant de committer. Rappel de la règle : une seule branche,
main, jamais de branche ni de PR. Si le push échoue, signale-le et
arrête-toi.
```

## 3. La réponse rendue, reproduite mot pour mot

> **Le push est rejeté. Je m'arrête.** Les deux commits existent en local, le
> distant est intact.
>
> **Ce qui a été fait**
>
> Contrôle de référence, nouvelle version — passé :
>
> | Contrôle | Attendu | Constaté |
> |---|---|---|
> | `grep -c ""` | 350–420 | **400** ✓ |
> | « /18 » | présent | 2 ✓ |
> | « 3 000 » | présent | 2 ✓ |
> | « Trustpilot » | présent | 5 ✓ |
> | « 48 h » | présent | 2 ✓ |
>
> J'ai aussi retranscrit votre second collage du protocole dans un fichier de
> travail séparé et l'ai comparé au fichier de la racine : `diff exit=0`, byte
> pour byte. Les 5 lignes vides ne sont pas remises.
>
> Bascule sur `main` : `main` était à `2f64a67`, ancêtre de `b0eb487`. Je l'ai
> avancé sur `b0eb487` en avance rapide, sans quoi committer sur `main` aurait
> fait disparaître le fichier 01 de l'arbre et cassé le renommage en index.
> Aucune perte.
>
> Deux commits, dans cet ordre :
>
> | Commit | Message | Contenu |
> |---|---|---|
> | `140f10f` | `protocole de recherche sectorielle` | `PROMPT_RECHERCHE_SECTEUR.md`, 400 insertions |
> | `b21534f` | `convention de passation et fichiers 00 à 04` | `CLAUDE.md`, `00_INDEX.md`, renommage du `01`, `02`, `03`, `04` — 6 fichiers, 723 insertions |
>
> Vous avez demandé des messages exacts sans les fournir. J'ai repris pour le
> premier le message de votre consigne d'origine (fichier 03), et formulé le
> second. Si les libellés ne sont pas ceux que vous voulez, ils sont encore
> réécrivables : rien n'est poussé.
>
> **Pourquoi le push échoue**
>
> ```
> $ git push origin main
> ! [rejected]        main -> main (fetch first)
> exit=1
> ```
>
> Ce n'est pas un problème d'authentification. **`origin/main` a deux commits
> que vous n'avez pas en local**, arrivés par un PR mergé :
>
> ```
> 7103c60 Merge pull request #1 from fabricegangitano800-lgtm/docs/methode-api-naf-etape1
> 9599bc4 Ajoute les règles de travail et le dimensionnement NAF des dix secteurs
> ```
>
> Ces commits ajoutent `CLAUDE.md`, `recherche/JOURNAL.md` et
> `recherche/PREFILTRE_NAF.md`.
>
> Trois choses à savoir avant de décider :
>
> 1. **Conflit certain sur `CLAUDE.md`.** Les deux côtés le créent, avec des
>    contenus différents : 199 lignes sur le distant, 51 en local. Un merge
>    s'arrêtera dessus. Il faudra trancher lequel des deux fait foi — la version
>    distante est presque quatre fois plus longue, elle contient probablement des
>    règles que ma version locale ignore.
> 2. **`recherche/PREFILTRE_NAF.md` existe** sur le distant, 329 lignes, et
>    `recherche/JOURNAL.md`, 173 lignes. Mon fichier 04 et l'index les donnaient
>    pour inexistants. C'était faux au moment où je l'ai écrit — corrigé par ce
>    fichier 05.
> 3. **Le PR #1 vient d'un autre compte GitHub** que celui de cette session :
>    `fabricegangitano800-lgtm`, mergé par `Novaships-dev`. C'est aussi un PR,
>    alors que la règle que vous venez de rappeler est « jamais de branche ni de
>    PR ». Il y a donc au moins une autre session, ou une autre machine, qui a
>    travaillé sur ce repo en parallèle et n'a pas suivi cette règle.
>
> **Je ne fais rien de plus.** Pas de `git pull`, pas de merge, pas de rebase,
> pas de `--force`. Un `--force` détruirait les 329 lignes de `PREFILTRE_NAF.md`
> et les 199 lignes du `CLAUDE.md` distant — c'est exactement ce qu'il ne faut
> pas faire à l'aveugle.
>
> Ce qu'il me faut de vous : quel `CLAUDE.md` fait foi, le distant (199 lignes)
> ou le local (51) ? Et voulez-vous que je vous montre le diff des deux avant de
> trancher ?

## 4. Preuves brutes

### 4.1 Contrôle de référence, nouvelle version

```
$ grep -c "" PROMPT_RECHERCHE_SECTEUR.md
400
$ grep -c -F -- '/18'        PROMPT_RECHERCHE_SECTEUR.md   → 2
$ grep -c -F -- '3 000'      PROMPT_RECHERCHE_SECTEUR.md   → 2
$ grep -c -F -- 'Trustpilot' PROMPT_RECHERCHE_SECTEUR.md   → 5
$ grep -c -F -- '48 h'       PROMPT_RECHERCHE_SECTEUR.md   → 2
```

400 est dans l'intervalle 350–420. Contrôle passé.

### 4.2 Seconde transcription indépendante

Le protocole recollé a été retranscrit dans un second fichier de travail, puis
comparé au fichier de la racine :

```
$ diff .../scratchpad/protocole2.md PROMPT_RECHERCHE_SECTEUR.md
diff exit=0
```

Aucune différence. Deux transcriptions faites séparément donnent le même
fichier, ce qui écarte une erreur de recopie de ma part.

### 4.3 Bascule sur `main`

```
$ git merge-base --is-ancestor main HEAD && echo ancetre
ancetre
```

```
$ git checkout -B main
Switched to and reset branch 'main'
D	NOTE_METHODE_API_ET_CODES_NAF.md
A	docs/passation/01_methode-api-codes-naf.md
Your branch is ahead of 'origin/main' by 1 commit.
exit=0
```

### 4.4 Les deux commits

```
$ git add PROMPT_RECHERCHE_SECTEUR.md
$ git commit PROMPT_RECHERCHE_SECTEUR.md -m 'protocole de recherche sectorielle'
[main 140f10f] protocole de recherche sectorielle
 1 file changed, 400 insertions(+)
 create mode 100644 PROMPT_RECHERCHE_SECTEUR.md
```

```
$ git add CLAUDE.md docs/
$ git commit -m 'convention de passation et fichiers 00 à 04'
[main b21534f] convention de passation et fichiers 00 à 04
 6 files changed, 723 insertions(+)
 create mode 100644 CLAUDE.md
 create mode 100644 docs/passation/00_INDEX.md
 rename NOTE_METHODE_API_ET_CODES_NAF.md => docs/passation/01_methode-api-codes-naf.md (100%)
 create mode 100644 docs/passation/02_convention-passation.md
 create mode 100644 docs/passation/03_commit-prompt-recherche-secteur-echec.md
 create mode 100644 docs/passation/04_ecriture-prompt-recherche-secteur.md
```

Le premier commit a été fait avec un pathspec (`git commit <chemin>`) afin que
le renommage déjà présent en index reste hors de ce commit et tombe dans le
second. Vérifié : `git log -1 --name-only` sur `140f10f` ne liste que
`PROMPT_RECHERCHE_SECTEUR.md`.

### 4.5 Le push, et sa cause

```
$ git push origin main
To https://github.com/Novaships-dev/Recherche-Business
 ! [rejected]        main -> main (fetch first)
error: failed to push some refs to 'https://github.com/Novaships-dev/Recherche-Business'
hint: Updates were rejected because the remote contains work that you do not
hint: have locally.
exit=1
```

```
$ git fetch origin
From https://github.com/Novaships-dev/Recherche-Business
   2f64a67..7103c60  main       -> origin/main
exit=0
```

```
$ git log --oneline -5 origin/main
7103c60 Merge pull request #1 from fabricegangitano800-lgtm/docs/methode-api-naf-etape1
9599bc4 Ajoute les règles de travail et le dimensionnement NAF des dix secteurs
b0eb487 Documente la méthode de dimensionnement NAF et les pièges de l'API
2f64a67 Initial commit
```

```
$ git log --oneline origin/main..main
b21534f convention de passation et fichiers 00 à 04
140f10f protocole de recherche sectorielle

$ git log --oneline main..origin/main
7103c60 Merge pull request #1 ...
9599bc4 Ajoute les règles de travail et le dimensionnement NAF des dix secteurs

$ git merge-base main origin/main | xargs git log --oneline -1
b0eb487 Documente la méthode de dimensionnement NAF et les pièges de l'API
```

Divergence confirmée : 2 commits de chaque côté depuis `b0eb487`.

```
$ git log --name-status --oneline main..origin/main
7103c60 Merge pull request #1 ...
9599bc4 Ajoute les règles de travail et le dimensionnement NAF des dix secteurs
A	CLAUDE.md
A	recherche/JOURNAL.md
A	recherche/PREFILTRE_NAF.md
```

### 4.6 Le conflit à venir sur `CLAUDE.md`

```
$ git show origin/main:CLAUDE.md > .../CLAUDE_remote.md
$ diff .../CLAUDE_remote.md CLAUDE.md >/dev/null && echo IDENTIQUES || echo DIFFERENTS
DIFFERENTS
$ git show origin/main:CLAUDE.md | wc -l   → 199
$ wc -l < CLAUDE.md                        → 51
```

```
$ git show origin/main:recherche/PREFILTRE_NAF.md | wc -l → 329
$ git show origin/main:recherche/JOURNAL.md       | wc -l → 173
```

```
$ git log -1 --format='%an <%ae> — %s' 7103c60
Novaships-dev <novaships.dev@outlook.com> — Merge pull request #1 from fabricegangitano800-lgtm/docs/methode-api-naf-etape1
$ git log -1 --format='%an <%ae> — %s' 9599bc4
fabricegangitano800-lgtm <fabrice.gangitano800@gmail.com> — Ajoute les règles de travail et le dimensionnement NAF des dix secteurs
```

**Commandes NON exécutées** : `git pull`, `git merge`, `git rebase`,
`git push --force`. Aucun chiffre de ce fichier ne s'y rapporte.

## 5. En attente de décision / bloqué

- **Bloqué** : le push. Il ne peut pas passer sans intégrer d'abord les deux
  commits distants, ce qui produira un conflit sur `CLAUDE.md`.
- **Décision A, prioritaire** : quel `CLAUDE.md` fait foi — le distant (199
  lignes, issu du PR #1) ou le local (51 lignes, celui qui régit la convention
  de passation) ? Les deux sont des règles de travail ; il faut soit choisir,
  soit fusionner à la main.
- **Décision B** : le PR #1 a été produit hors de cette session, depuis le
  compte `fabricegangitano800-lgtm`, et par un PR — contre la règle « une seule
  branche, main, jamais de branche ni de PR ». Faut-il considérer son contenu
  comme acquis, ou le rejouer ?
- **Décision C** : la branche `docs/methode-api-naf-etape1` existe encore, en
  local et sur le distant. La règle « une seule branche » implique sa
  suppression. Non fait : supprimer une branche distante n'était pas demandé.
- **Non levé** : les 4 arbitrages de périmètre du §6 du fichier
  [01](01_methode-api-codes-naf.md). Ils sont peut-être traités par
  `recherche/PREFILTRE_NAF.md` sur le distant — non vérifié, le fichier n'a pas
  été lu.

## 6. Réserves et pièges

- **Le fichier 04 contient deux affirmations désormais fausses**, non corrigées
  dans le fichier lui-même puisqu'il est committé tel quel : il donne
  `recherche/PREFILTRE_NAF.md` pour inexistant, et présente l'écart 400 vs 358
  comme non résolu. La correction est ici, au fichier 05. C'est le
  fonctionnement prévu de la convention : un fichier antérieur n'est pas
  réécrit, il est contredit par un numéro plus élevé.
- **Piège évité** : `git push --force`. Il aurait fait passer le push et
  détruit `recherche/PREFILTRE_NAF.md` (329 lignes), `recherche/JOURNAL.md`
  (173 lignes) et le `CLAUDE.md` distant (199 lignes). L'échec du push est ici
  une protection, pas une panne.
- **Piège évité** : `git checkout main` directement. L'index portait le
  renommage du fichier 01, dont la source n'existe pas sur `main` à `2f64a67` ;
  la bascule aurait échoué ou perdu le fichier. L'avance rapide de `main` sur
  `b0eb487` était nécessaire, et elle est sans perte parce que l'ancestralité a
  été vérifiée **avant**.
- **Il existe au moins un autre producteur de commits sur ce repo.** L'état du
  distant peut donc changer entre deux consignes. Tout `git status` de ces
  fichiers de passation est un instantané, non une vérité durable. Refaire
  `git fetch` avant toute opération d'écriture git.
- Les messages de commit ont été formulés par moi, la consigne demandant des
  « messages exacts » sans les donner. Ils sont encore modifiables tant que rien
  n'est poussé.
- Le contrôle de référence retenu (`grep -c ""` entre 350 et 420) est un
  intervalle large : il ne détecterait pas la perte de quelques dizaines de
  lignes. Les quatre chaînes sont le vrai garde-fou, et elles ne couvrent que
  quatre points du fichier.
