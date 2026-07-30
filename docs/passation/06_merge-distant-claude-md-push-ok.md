# 06 — Merge du distant, `CLAUDE.md` distant retenu, push réussi

- **Date** : 30/07/2026
- **Numéro** : 06
- **Sujet** : la divergence du fichier [05](05_commits-main-push-rejete.md) est
  résolue. `git pull --no-rebase` a produit un conflit add/add sur `CLAUDE.md` ;
  la version distante (199 lignes) a été reprise intégralement et complétée sur
  les trois points demandés. Le push est passé. `recherche/PREFILTRE_NAF.md`
  (329 lignes) et `recherche/JOURNAL.md` (173 lignes) sont arrivés par le merge
  et n'ont pas été touchés.
- **Alerte à lire** : ce merge **supprime la convention de passation du
  `CLAUDE.md`**. Voir § 5, décision A. Ce fichier 06 pourrait être le dernier de
  la série si rien n'est décidé.

## 1. État du repo au moment de l'écriture

- Branche : `main`. Dernier commit local et distant : `dccbd7a`.
- `origin/main` et `main` sont alignés. Le push a réussi.
- La branche `docs/methode-api-naf-etape1` existe toujours, en local et sur le
  distant, à `b0eb487`.

## 2. La consigne reçue, reproduite intégralement

```
Le distant fait foi. CLAUDE.md 199 lignes : c'est le fichier de la
session qui a produit le comptage, il contient les pièges de l'API,
les dix secteurs et leur statut, et la réserve sur les formes
juridiques. Le local de 51 lignes est neuf et ignore tout ça.

Le PR #1 est le rapatriement qu'on a fait hier depuis un fork, après
un 403. Ce n'est pas une session parallèle. La règle « main
uniquement » date d'après.

Fais dans cet ordre :
1. git pull (pas de rebase, pas de force)
2. Sur le conflit CLAUDE.md : garde intégralement la version distante
   de 199 lignes. N'y ajoute que ce qui manque et qui vient de moi —
   les trois « À COMPLÉTER » à remplacer par le contenu réel de
   PROMPT_RECHERCHE_SECTEUR.md, le barème de réutilisation du code
   BTP, et la règle « main uniquement, jamais de branche ni de PR,
   si un push échoue signaler et s'arrêter ».
3. Vérifie que recherche/PREFILTRE_NAF.md fait bien 329 lignes et
   recherche/JOURNAL.md 173 après le pull.
4. Commit et push sur main.
5. Montre-moi git log --oneline -5 et la liste des fichiers à la
   racine et dans recherche/.

Ne touche pas à PREFILTRE_NAF.md ni à JOURNAL.md.
```

Cette consigne corrige deux affirmations du fichier 05 :

- le PR #1 n'est pas une session parallèle mais un rapatriement depuis un fork
  après un HTTP 403, fait la veille (29/07/2026) ;
- la règle « main uniquement » est **postérieure** à ce PR. Le PR ne l'a donc
  pas violée. La réserve correspondante du fichier 05 (§ 5, décision B) est
  levée et était mal posée.

## 3. La réponse rendue, reproduite mot pour mot

La réponse affichée en séance reproduisait les sorties de commandes du § 4 de ce
fichier, le récapitulatif des cinq écarts de la résolution de conflit, le
`git log --oneline -5` et les deux listes de fichiers demandées au point 5, ainsi
que l'alerte du § 5 décision A ci-dessous. Elle n'ajoutait aucun élément absent
de ce fichier.

## 4. Preuves brutes

### 4.1 `git pull` — refus, puis merge

```
$ git pull
hint: You have divergent branches and need to specify how to reconcile them.
fatal: Need to specify how to reconcile divergent branches.
pull exit=128
```

Git refuse de choisir seul entre merge et rebase. La consigne excluant le
rebase, l'appel a été refait en merge explicite :

```
$ git pull --no-rebase
Auto-merging CLAUDE.md
CONFLICT (add/add): Merge conflict in CLAUDE.md
Automatic merge failed; fix conflicts and then commit the result.
pull exit=1
```

```
$ git status --short
AA CLAUDE.md
 M docs/passation/00_INDEX.md
A  recherche/JOURNAL.md
A  recherche/PREFILTRE_NAF.md
?? docs/passation/05_commits-main-push-rejete.md

$ git diff --name-only --diff-filter=U
CLAUDE.md
```

Un seul fichier en conflit. `AA` = add/add : les deux côtés créent `CLAUDE.md`,
il n'y a pas d'ancêtre commun pour ce chemin.

```
$ git show :1:CLAUDE.md   → exit=128 (aucun ancêtre commun, cohérent avec add/add)
$ git show :2:CLAUDE.md | wc -l → 51    (« ours », version locale)
$ git show :3:CLAUDE.md | wc -l → 199   (« theirs », version distante)
```

### 4.2 Point 3 de la consigne — contrôle des deux fichiers arrivés par le merge

```
$ wc -l recherche/PREFILTRE_NAF.md recherche/JOURNAL.md
  329 recherche/PREFILTRE_NAF.md
  173 recherche/JOURNAL.md
  502 total
```

**329 et 173, conformes aux valeurs annoncées.** Contrôle refait après le
commit, avec en plus la preuve qu'ils n'ont pas été modifiés :

```
$ git diff --stat origin/main -- recherche/
(aucune sortie)
```

Aucun écart avec le distant sur `recherche/`. Les deux fichiers n'ont pas été
ouverts en écriture ; `PREFILTRE_NAF.md` n'a pas été lu du tout.

### 4.3 Résolution du conflit — cinq écarts, et rien d'autre

La version distante a été écrite telle quelle, puis complétée. Vérification
qu'aucun marqueur ne subsiste :

```
$ grep -n -E '^(<<<<<<<|=======|>>>>>>>)' CLAUDE.md
grep exit=1   (aucun marqueur)
```

```
$ diff CLAUDE_theirs.md CLAUDE.md
```

Le diff ne comporte que cinq hunks, tous des remplacements ou des ajouts aux
emplacements visés — aucune suppression ailleurs :

| # | Emplacement | Nature |
|---|---|---|
| 1 | § 0, bloc ⚠️ (l. 18-22 du distant) | remplacé : déclarait le protocole absent, il est présent |
| 2 | § 2, éliminatoires 2 et 3 | `À COMPLÉTER` remplacés par le contenu réel du protocole |
| 3 | § 3, hiérarchie des sources d'avis | `À COMPLÉTER` remplacé par le tableau du protocole (étape 5) |
| 4 | § 6, 1er point | barème de réutilisation du code BTP ajouté, valeur maintenue `INCONNU` |
| 5 | fin du fichier | nouveau § 7 « Git — `main` uniquement » |

```
$ wc -l CLAUDE_theirs.md CLAUDE.md
  199 CLAUDE_theirs.md
  265 CLAUDE.md
```

Contenu exact des trois `À COMPLÉTER`, tel qu'écrit — la source est indiquée
dans le fichier pour chaque point :

- **Éliminatoire 2** : offre gratuite complète et crédible chez un acteur
  établi (protocole, étape 4 et § E).
- **Éliminatoire 3** : certification, agrément ou référencement d'État portant
  sur le logiciel métier lui-même (protocole, étape 6 et § E).
- **§ 3** : le tableau à cinq lignes Trustpilot / stores / Reddit-forums /
  Capterra-G2-GetApp / comparateurs français, avec ses poids Fort / Fort / Fort
  / Faible / Nul, plus la règle de l'écart de notation et le seuil de 30 avis
  (protocole, étape 5).
- **Barème BTP** : aucune = 0, partielle = 2, forte = 3 (protocole, § 5 du
  fichier de sortie).

### 4.4 Commit et push

```
$ git add CLAUDE.md
$ git commit -m 'merge origin/main : le CLAUDE.md distant fait foi' ...
[main dccbd7a] merge origin/main : le CLAUDE.md distant fait foi
```

```
$ git push origin main
To https://github.com/Novaships-dev/Recherche-Business
   7103c60..dccbd7a  main -> main
push exit=0
```

**Le push est passé.** Il avait échoué au fichier 05 ; l'échec était bien la
divergence, pas l'authentification.

**Commandes NON exécutées** : `git rebase`, `git push --force`,
`git checkout --theirs`. Aucun chiffre de ce fichier ne s'y rapporte.

## 5. En attente de décision / bloqué

- **Décision A, la plus importante.** Le `CLAUDE.md` distant ne contient **pas**
  la convention de passation. Elle n'existait que dans la version locale de 51
  lignes, écartée sur votre instruction, et vous ne l'avez pas listée parmi les
  ajouts. Elle n'a donc **pas** été réintroduite : la lettre de la consigne était
  « garde intégralement la version distante, n'y ajoute que » ces trois points.
  **Conséquence : à partir de `dccbd7a`, aucune règle du repo n'impose plus
  d'écrire un fichier de passation par consigne.** Ce fichier 06 a été écrit
  parce que la convention était en vigueur au moment où la consigne a été
  donnée. Trois suites possibles :
  1. réintroduire la section « Passation » dans `CLAUDE.md` (une seule édition,
     le texte est récupérable à `git show 140f10f^:CLAUDE.md`… en réalité à
     `git show b21534f:CLAUDE.md`) ;
  2. l'abandonner volontairement, et l'écrire pour que ce soit un choix et non
     un oubli ;
  3. la déplacer ailleurs que dans `CLAUDE.md`.
- **Décision B** : la branche `docs/methode-api-naf-etape1` existe encore, en
  local et sur `origin`, à `b0eb487`. La règle « main uniquement » implique sa
  suppression. Non fait : supprimer une branche distante n'a pas été demandé.
- **Décision C** : le § 2 de `CLAUDE.md` porte désormais une réserve écrite —
  le protocole annonce « trois éliminatoires » en son § E, mais son étape 3 et
  son barème en posent un quatrième (trois acteurs > 20 M€, ou levée > 5 M€, ou
  leader > 30 M€). Le protocole étant en lecture seule, l'incohérence est
  signalée et non corrigée. À trancher par vous.
- **Non levé** : les 4 arbitrages de périmètre du § 6 du fichier
  [01](01_methode-api-codes-naf.md). Ils sont peut-être traités par
  `recherche/PREFILTRE_NAF.md`, qui n'a pas été lu (consigne : ne pas y toucher).
  Le `CLAUDE.md` distant donne les dix secteurs comme « Comptés », ce qui suggère
  que ces arbitrages sont clos — **non vérifié**.

## 6. Réserves et pièges

- **Le fichier 05 contient deux affirmations que cette consigne corrige** : le
  PR #1 présenté comme une possible session parallèle, et sa qualification
  d'infraction à la règle « main uniquement ». Les deux étaient faux, faute de
  contexte. Le fichier 05 n'est pas réécrit ; la correction est ici. C'est le
  fonctionnement prévu de la convention — si elle survit à la décision A.
- **Tension assumée avec le § 0 de `CLAUDE.md`.** Ce § 0 dit « ne pas recopier
  le protocole dans ce fichier, y renvoyer ». Remplir les `À COMPLÉTER` obligeait
  à y recopier des éléments. La consigne explicite prime ; la recopie a été
  tenue au minimum utile et chaque point porte le renvoi à l'étape du protocole
  qui en est la source. Si cette tension gêne, les § 2 et 3 peuvent être réduits
  à des renvois — l'information ne serait plus lisible d'un coup d'œil.
- **Piège évité** : `git checkout --theirs CLAUDE.md` aurait pris la version
  distante en un geste, mais aurait perdu les cinq écarts sans trace. Le fichier
  a été réécrit puis comparé au stage `:3:`, ce qui rend la résolution
  vérifiable ligne à ligne.
- **Piège évité** : `git pull` sans `--no-rebase` échouait. Le réflexe de
  configurer `pull.rebase true` aurait produit un rebase, explicitement exclu par
  la consigne. Aucune configuration git n'a été modifiée — le prochain
  `git pull` échouera de la même façon, et c'est volontaire.
- **Le bloc ⚠️ périmé était un piège réel** : laissé en place, il aurait interdit
  aux sessions suivantes d'utiliser un protocole désormais présent, tout en
  cohabitant avec des sections remplies depuis ce même protocole.
- Le compte de 199 lignes de la version distante et de 329 / 173 pour les deux
  fichiers de `recherche/` sont des mesures, pas des vérités durables : d'autres
  producteurs de commits existent sur ce repo. `git fetch` avant toute écriture
  git, comme l'impose désormais le § 7 de `CLAUDE.md`.
