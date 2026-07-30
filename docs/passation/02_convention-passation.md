# 02 — Mise en place de la convention de passation

- **Numéro** : 02
- **Date** : 29/07/2026
- **Sujet en une ligne** : création de la convention de passation dans `CLAUDE.md`, de l'index `00_INDEX.md`, et déplacement du fichier 01 vers son emplacement normalisé.

## État du repo au moment de l'écriture

**Ce qui existe :**

| Chemin | Nature |
|---|---|
| `README.md` | Une ligne, titre du repo. Aucun contenu |
| `CLAUDE.md` | **Créé par cette passation.** Instructions permanentes, section « Passation » |
| `docs/passation/00_INDEX.md` | **Créé par cette passation.** Index des passations |
| `docs/passation/01_methode-api-codes-naf.md` | **Déplacé par cette passation** depuis `NOTE_METHODE_API_ET_CODES_NAF.md` (racine). Contenu inchangé |
| `docs/passation/02_convention-passation.md` | Ce fichier |

**Ce qui a été lancé :** rien de neuf. Cette passation est purement
organisationnelle : aucune requête API, aucune recherche web, aucune collecte
de données.

**Ce qui n'a pas été lancé :** l'étape 1 du protocole (comptage NAF) reste
bloquée sur les 4 arbitrages du §6 du fichier 01. Les étapes 2 à 6 n'ont pas
été abordées. `recherche/` est un dossier vide, non tracké par git (git ne
suit pas les dossiers vides) ; aucun fichier de résultat n'existe.

**Branche git** : `docs/methode-api-naf-etape1`. `main` ne contient que le
commit initial et son `README.md` — le fichier 01 n'est pas sur `main`.

---

## 1. Consigne reçue, reproduite intégralement

> Convention permanente à ajouter à CLAUDE.md, section « Passation ».
>
> À chaque fois que je te donne une consigne et que tu me réponds, tu
> écris ta réponse dans un fichier du repo, en plus de l'afficher.
>
> Emplacement et nommage :
> docs/passation/NN_sujet-court.md
> NN = numéro d'ordre à deux chiffres, incrémenté à chaque fois.
> Le fichier 01 existe déjà (méthode API et codes NAF).
>
> Chaque fichier doit être autonome : lisible par quelqu'un qui n'a
> aucun accès à notre conversation. Il contient :
>
> 1. En-tête : date, numéro, sujet en une ligne, et l'état du repo au
>    moment de l'écriture (ce qui existe, ce qui a été lancé, ce qui ne
>    l'a pas été).
> 2. La consigne que je t'ai donnée, reproduite intégralement.
> 3. Ta réponse reproduite mot pour mot, sans coupe ni reformulation.
> 4. Les preuves brutes : chaque commande exécutée avec sa sortie
>    réelle, de sorte que tout chiffre soit reproductible. Aucun chiffre
>    sans sa commande.
> 5. Ce qui reste en attente de ma décision, et ce qui est bloqué.
> 6. Les réserves et pièges découverts, même mineurs.
>
> Règles :
> - Ne répète pas ce qui est déjà écrit dans un fichier de passation
>   antérieur. Renvoie à son numéro.
> - Ne résume pas et ne « nettoie » pas ta réponse : je la transmets
>   telle quelle à un tiers qui doit pouvoir la contredire.
> - Si tu t'es trompé ou si tu as corrigé une hypothèse en cours de
>   route, écris-le. L'erreur corrigée est une information utile.
> - Mets à jour docs/passation/00_INDEX.md à chaque fois : une ligne par
>   fichier avec numéro, date, sujet, et statut (validé / en attente /
>   périmé).
>
> Crée docs/passation/00_INDEX.md maintenant et référence le fichier 01
> existant.

---

## 2. Réponse rendue, reproduite mot pour mot

Ce qui suit est le texte intégral de la réponse affichée, sans coupe ni
reformulation.

---

Convention en place. Quatre fichiers touchés.

| Fichier | Action |
|---|---|
| `CLAUDE.md` | Créé — n'existait pas. Section « Passation » avec l'emplacement, les 6 rubriques obligatoires, les règles et les statuts d'index |
| `docs/passation/00_INDEX.md` | Créé. Référence les fichiers 01 et 02, plus un état d'avancement du projet |
| `docs/passation/01_methode-api-codes-naf.md` | **Déplacé** depuis `NOTE_METHODE_API_ET_CODES_NAF.md` |
| `docs/passation/02_convention-passation.md` | Créé — cette réponse-ci relève déjà de la convention |

**Un point sur lequel j'ai pris une initiative, à valider.** Tu m'as dit « le fichier 01 existe déjà », mais il était à la racine sous le nom `NOTE_METHODE_API_ET_CODES_NAF.md` — pas au chemin `docs/passation/NN_sujet-court.md` que la convention impose. Un index qui pointe vers un fichier hors convention serait faux dès la première ligne, donc je l'ai renommé en `docs/passation/01_methode-api-codes-naf.md`.

Fait avec `git mv`, et vérifié : `1 file changed, 0 insertions(+), 0 deletions(-)`. Pur renommage, contenu intact, 442 lignes. L'historique git suit le fichier. Si tu voulais qu'il reste à la racine, dis-le et je le remets.

**Statut du 01 dans l'index : « en attente »**, pas « validé ». Il l'est parce que ses 4 arbitrages de périmètre bloquent le comptage — pas parce que son contenu serait douteux. La méthode et les preuves qu'il contient tiennent.

Deux réserves que je consigne dans le 02 :

1. La convention crée une **dépendance circulaire bénigne** : le fichier 02 contient ma réponse mot pour mot, et cette réponse décrit la création du fichier 02. J'ai écrit le fichier avant d'afficher le texte, les deux sont identiques. Pour les prochaines passations, l'ordre sera le même — fichier d'abord, affichage ensuite — afin que le « mot pour mot » soit vrai et non approximatif.

2. La rubrique 4 (« aucun chiffre sans sa commande ») est peu applicable à une passation d'organisation comme celle-ci : les seules commandes sont des opérations git. Je ne vais pas fabriquer du volume de preuve là où il n'y a rien à prouver — j'ai consigné les sorties réelles des 4 commandes exécutées, et c'est tout ce qu'il y a.

Rien n'est commité pour l'instant. Le déplacement du 01 est en zone d'index (`R` dans `git status`), les trois autres fichiers sont non trackés. Dis-moi si je commit et push, et je le fais sur la branche courante `docs/methode-api-naf-etape1`.

---

*Fin de la réponse reproduite mot pour mot.*

---

## 3. Preuves brutes

Chaque commande exécutée le 29/07/2026, avec sa sortie réelle.
Cette passation étant organisationnelle, elle ne produit aucun chiffre de
recherche : les seules commandes sont des inspections et des opérations git.

### 3.1 État du repo avant modification

```console
$ ls -la CLAUDE.md
ls: cannot access 'CLAUDE.md': No such file or directory

$ ls -la docs/
ls: cannot access 'docs/': No such file or directory

$ git ls-files
NOTE_METHODE_API_ET_CODES_NAF.md
README.md

$ git branch --show-current
docs/methode-api-naf-etape1
```

Constat : ni `CLAUDE.md` ni `docs/` n'existaient. La convention est donc créée
de zéro, elle ne modifie aucune instruction antérieure. Le fichier 01 était
tracké à la racine, hors convention.

### 3.2 Déplacement du fichier 01

```console
$ mkdir -p docs/passation
$ git mv NOTE_METHODE_API_ET_CODES_NAF.md docs/passation/01_methode-api-codes-naf.md

$ git status --short
R  NOTE_METHODE_API_ET_CODES_NAF.md -> docs/passation/01_methode-api-codes-naf.md

$ wc -l docs/passation/01_methode-api-codes-naf.md
442 docs/passation/01_methode-api-codes-naf.md

$ git diff --cached --stat
 .../passation/01_methode-api-codes-naf.md                                 | 0
 1 file changed, 0 insertions(+), 0 deletions(-)
```

**Preuve d'intégrité :** `0 insertions(+), 0 deletions(-)` et le statut `R`
(rename) établissent que le contenu du fichier 01 n'a pas été altéré — 442
lignes, identiques. Le déplacement est un pur renommage suivi par git.

### 3.3 Correction effectuée en cours de route

Première rédaction de `CLAUDE.md` : une faute d'accord, « Un chiffre sans
source **se** écrit `INCONNU` ». Corrigée en « **s'**écrit » par une édition
immédiate. Sans incidence sur le fond, consignée par application de la règle
« l'erreur corrigée est une information utile ».

### 3.4 Ce qui n'a pas été exécuté

Aucune requête vers `recherche-entreprises.api.gouv.fr`, aucune requête web,
aucun commit, aucun push. Les chiffres de dimensionnement déjà acquis figurent
au §3 du fichier 01 et ne sont pas recopiés ici (règle de non-répétition).

---

## 4. En attente de décision

| Sujet | Décision attendue | Effet si refusée |
|---|---|---|
| **Déplacement du fichier 01** | Confirmer que `docs/passation/01_methode-api-codes-naf.md` est le bon emplacement | Retour à `NOTE_METHODE_API_ET_CODES_NAF.md` à la racine, et correction du lien dans l'index |
| **Commit et push** | Rien n'est commité. Autoriser le commit sur la branche `docs/methode-api-naf-etape1` | Les 3 nouveaux fichiers et le renommage restent dans l'arbre de travail, non versionnés |
| **Fusion vers `main`** | La branche `docs/methode-api-naf-etape1` n'est pas fusionnée. `main` ne contient que le `README.md` initial | `CLAUDE.md` n'est pas sur `main` : une session travaillant depuis `main` **ne verra pas la convention de passation** |

**Bloqué :** l'étape 1 du protocole (comptage NAF) attend les 4 arbitrages de
périmètre détaillés au §6 du fichier 01. Cette passation ne les débloque pas.

---

## 5. Réserves et pièges

1. **Dépendance circulaire bénigne du dispositif.** Ce fichier contient la
   réponse mot pour mot, et cette réponse décrit la création de ce fichier.
   Résolution adoptée : le fichier est écrit **avant** l'affichage du texte,
   de sorte que la reproduction « mot pour mot » soit exacte et non
   approximative. Ordre à conserver pour les passations suivantes.

2. **La rubrique 4 est peu applicable aux passations d'organisation.**
   « Aucun chiffre sans sa commande » suppose des chiffres. Ici il n'y en a
   pas : les seules commandes sont des opérations git, dont les sorties réelles
   sont au §3. Aucun volume de preuve n'a été fabriqué pour donner l'apparence
   du contraire.

3. **`CLAUDE.md` n'est pas sur `main`.** Tant que la branche n'est pas
   fusionnée, une session Claude Code démarrée sur `main` ne chargera pas la
   convention et ne produira pas de fichier de passation. C'est le risque
   pratique le plus élevé de cette passation.

4. **Le numéro `NN` n'a pas de garde-fou automatique.** Rien n'empêche
   mécaniquement de réutiliser un numéro ou d'en sauter un. La convention
   impose de lister `docs/passation/` avant d'écrire ; c'est une discipline,
   pas un contrôle. Deux sessions travaillant en parallèle produiraient un
   conflit de numéro.

5. **`recherche/` est un dossier vide et invisible pour git.** Il avait été
   créé en prévision des fichiers de résultat. Git ne versionnant pas les
   dossiers vides, il n'apparaît ni dans `git ls-files` ni dans `git status`,
   et disparaîtra sur un clone frais. Sans conséquence : il sera recréé au
   premier fichier de résultat.

6. **Statut « en attente » du fichier 01 : à ne pas mal lire.** Ce statut porte
   sur les arbitrages de périmètre qui bloquent le comptage, pas sur la
   fiabilité du contenu. La méthode, les preuves du plafond de l'API et les 71
   libellés NAF du fichier 01 sont établis et sourcés.
