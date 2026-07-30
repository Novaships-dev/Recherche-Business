# 04 — Écriture de `PROMPT_RECHERCHE_SECTEUR.md` : contenu conforme, compte de lignes non conforme

- **Date** : 30/07/2026
- **Numéro** : 04
- **Sujet** : le texte intégral du protocole de recherche sectorielle a été
  fourni et écrit tel quel dans `PROMPT_RECHERCHE_SECTEUR.md` à la racine. La
  vérification demandée échoue sur un seul point : le fichier fait **400
  lignes** et non 358. Les quatre chaînes demandées sont toutes présentes.
  Conformément à la consigne, **rien n'a été enchaîné** après le constat.

## 1. État du repo au moment de l'écriture

Branche : `docs/methode-api-naf-etape1`. Dernier commit : `b0eb487`.

Cette consigne répond à la **décision 1 du fichier [03](03_commit-prompt-recherche-secteur-echec.md)**
(origine du contenu de `PROMPT_RECHERCHE_SECTEUR.md`) : l'option retenue est la
2 — l'utilisateur fournit le texte, il est écrit tel quel. Le fichier 03 est
donc partiellement levé ; sa décision 2 (sort du travail déjà en attente de
commit) reste ouverte.

```
$ git status --short
R  NOTE_METHODE_API_ET_CODES_NAF.md -> docs/passation/01_methode-api-codes-naf.md
?? CLAUDE.md
?? PROMPT_RECHERCHE_SECTEUR.md
?? docs/passation/00_INDEX.md
?? docs/passation/02_convention-passation.md
?? docs/passation/03_commit-prompt-recherche-secteur-echec.md
```

Aucun `git add`, `git commit` ni `git push` n'a été exécuté dans cette
passation. L'état du distant est inchangé.

## 2. La consigne reçue, reproduite intégralement

```
Voici le protocole complet. Écris-le TEL QUEL dans
PROMPT_RECHERCHE_SECTEUR.md à la racine, sans reformuler, sans
résumer, sans réorganiser, sans corriger la mise en forme. Copie
intégrale.

Puis vérifie : le fichier doit faire 358 lignes et contenir « /18 »,
« 3 000 », « Trustpilot », « 48 h ». Si le compte ne correspond pas,
dis-le et n'enchaîne pas.

[le protocole intégral ici]
```

Le texte du protocole suivait immédiatement ce bloc, du titre
`# Prompt de recherche sectorielle — logiciel métier France` jusqu'à la ligne
finale `vrai.`. Il n'est pas recopié ici : il constitue désormais le contenu de
`PROMPT_RECHERCHE_SECTEUR.md`, qui fait foi.

## 3. La réponse rendue, reproduite mot pour mot

> **Le compte ne correspond pas : 400 lignes, pas 358.** Je n'enchaîne pas.
>
> Le fichier est écrit à la racine, copie intégrale, sans reformulation ni
> correction de mise en forme.
>
> **Vérification**
>
> | Contrôle | Attendu | Constaté |
> |---|---|---|
> | Nombre de lignes | 358 | **400** ✗ |
> | « /18 » | présent | 2 occurrences (l. 272, 274) ✓ |
> | « 3 000 » | présent | 2 occurrences (l. 74, 395) ✓ |
> | « Trustpilot » | présent | 5 occurrences (l. 133, 141, 168, 240, 245) ✓ |
> | « 48 h » | présent | 2 occurrences (l. 327, 384) ✓ |
>
> Les quatre chaînes sont toutes là. Seul le compte de lignes diverge, de 42
> lignes.
>
> **Sur l'écart.** Le texte que vous m'avez donné fait 400 lignes tel quel,
> fin de fichier comprise. Je ne peux pas le ramener à 358 sans supprimer du
> contenu ou refermer des paragraphes, ce que la consigne interdit
> explicitement. Deux lectures possibles, je ne tranche pas :
>
> - le compte 358 vient d'une version antérieure du protocole, plus courte que
>   celle collée ;
> - ou il compte autre chose que les lignes physiques. Repères mesurés sur le
>   fichier : 279 lignes non vides, 121 lignes vides, 15 517 octets.
>
> Aucun de ces chiffres ne fait 358, donc je n'ai pas de règle de comptage à
> vous proposer qui réconcilierait les deux.
>
> **Un point à signaler.** `PROMPT_RECHERCHE_SECTEUR.md` existait déjà quand
> j'ai commencé — il n'existait pas au moment du fichier de passation 03. Son
> contenu était le même protocole, mais précédé de 5 lignes vides et sans
> retour à la ligne final. Je l'ai remplacé par la copie propre. Si ces 5
> lignes vides étaient intentionnelles, dites-le, je les remets.
>
> Rien d'autre n'a été fait : pas de `git add`, pas de commit, pas de push.

## 4. Preuves brutes

### 4.1 Comparaison avant écrasement

Le protocole a d'abord été transcrit dans un fichier de travail hors du repo,
puis comparé au fichier déjà présent à la racine.

```
$ diff /tmp/.../scratchpad/protocole.md PROMPT_RECHERCHE_SECTEUR.md
0a1,5
>
>
>
>
>
diff exit=1
```

```
$ md5sum /tmp/.../scratchpad/protocole.md PROMPT_RECHERCHE_SECTEUR.md
70be6d6db36373f1588f9a1b1a43a2fa  /tmp/.../scratchpad/protocole.md
7b572bc7ee5f98d093d54b128cd410eb  PROMPT_RECHERCHE_SECTEUR.md
```

Seule différence : 5 lignes vides en tête du fichier préexistant. Le corps du
protocole était identique.

### 4.2 Écriture et vérification

```
$ cp /tmp/.../scratchpad/protocole.md PROMPT_RECHERCHE_SECTEUR.md
$ md5sum /tmp/.../scratchpad/protocole.md PROMPT_RECHERCHE_SECTEUR.md
70be6d6db36373f1588f9a1b1a43a2fa  /tmp/.../scratchpad/protocole.md
70be6d6db36373f1588f9a1b1a43a2fa  PROMPT_RECHERCHE_SECTEUR.md
```

Les deux empreintes sont identiques : le fichier de la racine est octet pour
octet la transcription du texte fourni.

```
$ wc -l -c PROMPT_RECHERCHE_SECTEUR.md
  400 15517 PROMPT_RECHERCHE_SECTEUR.md
```

```
$ grep -c -F -- '/18'        PROMPT_RECHERCHE_SECTEUR.md   → 2
$ grep -c -F -- '3 000'      PROMPT_RECHERCHE_SECTEUR.md   → 2
$ grep -c -F -- 'Trustpilot' PROMPT_RECHERCHE_SECTEUR.md   → 5
$ grep -c -F -- '48 h'       PROMPT_RECHERCHE_SECTEUR.md   → 2
```

```
$ grep -n -F -e '/18' -e '3 000' -e 'Trustpilot' -e '48 h' PROMPT_RECHERCHE_SECTEUR.md
74:**Seuil d'arrêt : moins de 3 000 entreprises dans la cible → arrêter la
133:| Trustpilot | Rare, avis spontanés | **Fort** |
141:des avis Trustpilot négatifs est, lui, une information de premier ordre — le
168:répété trois fois sur Trustpilot pèse plus que quinze avis 5 étoiles sur
240:Répartition : [n] Trustpilot / [n] stores / [n] Reddit-forums / [n] Capterra-G2
245:Écart de notation détecté : [note Capterra/G2 vs contenu Trustpilot/stores —
272:**Score total : /18**
274:Le score ne décide pas. Les éliminatoires décident. Un secteur à 17/18 avec un
327:## 9. Le test à 48 h
384:Y inclure les tests à 48 h (section 9) des deux premiers secteurs du
395:plus de 3 000 entreprises cibles, aucune offre gratuite crédible d'un acteur
```

### 4.3 Comptages alternatifs, pour documenter l'écart de 42 lignes

```
$ wc -l < PROMPT_RECHERCHE_SECTEUR.md              → 400
$ grep -c '[^[:space:]]' PROMPT_RECHERCHE_SECTEUR.md → 279   (lignes non vides)
$ wc -c < PROMPT_RECHERCHE_SECTEUR.md              → 15517  (octets)
```

Lignes vides : 400 − 279 = 121. **Aucun de ces comptages ne donne 358.** Le
chiffre 358 n'est donc rattaché à aucune commande dans ce repo ; son origine
est `INCONNU`.

```
$ tail -c1 PROMPT_RECHERCHE_SECTEUR.md | od -c | head -1
0000000  \n
```

Le fichier se termine bien par un retour à la ligne.

## 5. En attente de décision / bloqué

- **Bloqué, et volontairement** : toute suite (commit, push, lancement d'un
  secteur) est suspendue. La consigne dit « si le compte ne correspond pas,
  dis-le et n'enchaîne pas ». Le compte ne correspond pas.
- **Décision A** : que faire de l'écart 400 vs 358 — le protocole collé est-il
  bien la version voulue, ou une version plus courte existe-t-elle ailleurs ?
  Tant que ce point n'est pas tranché, le fichier de la racine ne peut pas être
  déclaré conforme.
- **Décision B** : les 5 lignes vides en tête du fichier préexistant ont été
  supprimées. À confirmer ou à annuler.
- **Décision C** (héritée du fichier [03](03_commit-prompt-recherche-secteur-echec.md),
  toujours ouverte) : faut-il committer le travail en attente — `CLAUDE.md`,
  `00_INDEX.md`, `02`, `03`, le renommage du `01` — et sous quel message ?
- Rappel : les 4 arbitrages de périmètre du §6 du fichier
  [01](01_methode-api-codes-naf.md) restent ouverts. L'étape 1 du protocole ne
  peut pas démarrer avant.

## 6. Réserves et pièges

- **`PROMPT_RECHERCHE_SECTEUR.md` existait déjà** au début de cette passation,
  alors qu'il n'existait pas au moment du fichier 03 (preuves au §4 du 03 :
  `git add` en 128, `grep -rli` sans résultat). Il a donc été créé entre les
  deux, hors de la trace des passations. Son contenu correspondait au
  protocole, à 5 lignes vides près. **Aucune passation ne documente sa
  création** — c'est un trou dans la chaîne.
- **Piège évité** : écraser le fichier sans le comparer d'abord aurait détruit
  une éventuelle divergence sans que personne ne le sache. La comparaison a été
  faite avant le `cp`, et c'est elle qui a révélé les 5 lignes vides.
- **Piège évité** : « ajuster » le fichier pour atteindre 358 lignes. Cela
  aurait exigé de supprimer 42 lignes d'un texte que la consigne impose de
  recopier intégralement. Un fichier qui passe le contrôle mais a perdu du
  contenu est pire qu'un contrôle en échec.
- Le fichier reste **non suivi par git**. Il n'est protégé par rien : une
  suppression accidentelle du répertoire de travail le perd. Le committer dès
  que le contenu est validé est la première chose à faire.
- Le nom et l'emplacement (`PROMPT_RECHERCHE_SECTEUR.md` à la racine) sont ceux
  demandés. La réserve du fichier 03 sur l'emplacement cible — racine, `docs/`,
  ou `recherche/` — est tranchée de fait par cette consigne : racine.
