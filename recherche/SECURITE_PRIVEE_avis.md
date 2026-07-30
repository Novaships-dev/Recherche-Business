# Sécurité privée — corpus d'avis (données brutes)

Date : 30/07/2026
Fichier de sortie de l'**étape 5** du protocole `PROMPT_RECHERCHE_SECTEUR.md`.

## Corpus : 0 avis

**L'étape 5 n'a pas été menée.** Ce n'est pas un corpus vide, c'est une étape non
exécutée — la distinction est essentielle et ne doit pas être perdue en
agrégeant les secteurs.

| # | Éditeur | Plateforme | Note | Date | Reproche en une phrase | Catégorie | URL |
|---|---|---|---|---|---|---|---|
| — | — | — | — | — | — | — | — |

## Pourquoi elle n'a pas été menée

Le secteur a été fermé à l'**étape 3** par l'éliminatoire n° 4 : SENEF SOFT
(SIREN 529974511), éditeur du logiciel de sécurité privée Seenet, a levé
**6,5 M€ d'argent frais** auprès d'Isatis Capital le 02/05/2023, en série A.
Détail et preuves dans `SECURITE_PRIVEE.md` § 2.

Le § 0 point 3 de `CLAUDE.md` prescrit de ne pas payer le protocole entier après
une fermeture. L'étape 5 est la plus coûteuse du protocole et n'a plus aucune
valeur de décision une fois un éliminatoire déclenché : le score ne décide pas,
les éliminatoires décident.

## Ce que cela interdit de conclure

Conformément au § 3 de `CLAUDE.md` et à l'étape 5 du protocole :

- **Interdit** : « aucun défaut détecté chez les éditeurs en place ».
- **Interdit** : reporter une quelconque valeur dans la colonne « reproche
  dominant » de `SYNTHESE.md`. Elle vaut `INCONNU`, pas 0.
- **Autorisé** : « les défauts des logiciels de sécurité privée n'ont pas été
  instruits ».

## Ce qu'il faudrait faire si le secteur était rouvert

Le secteur ne peut être rouvert que par l'invalidation de l'éliminatoire n° 4
(test à 48 h, § 9 du fichier principal). Dans ce cas seulement, l'étape 5
partirait de la liste d'éditeurs déjà établie.

### Cibles d'avis identifiées, non parcourues

| Éditeur | Dénomination légale | Piste de corpus |
|---|---|---|
| Seenet | SENEF SOFT | Revendique « +2 000 entreprises accompagnées » (groupe, tous produits) |
| Comète | AEXAE | Revendique ~650 entreprises clientes et 7 000 utilisateurs quotidiens dans une dizaine de pays. **Application `Comète Link` sur Google Play — source forte, à dépouiller en priorité** |
| Trackforce Valiant / GuardTek | ALPHA SYSTEM | Acteur international (San Diego), a absorbé TrackTik en juin 2022. Corpus anglophone probablement plus fourni que le français |
| SEKUR | LE WEB FRANCAIS | — |
| MC Tracker | MC TRACKER | Société créée le 12/02/2026 — corpus quasi certainement inexistant |
| Hector Solution | VIGIFORMATION | Société créée le 03/09/2025 — idem |
| BanetteOne | INCONNU | — |
| Kelio (ex-Bodet Software) | KELIO | Corpus GTA généraliste, à filtrer sur les clients du secteur |
| Horoquartz | HOROQUARTZ | idem |

### Ordre de dépouillement à respecter (hiérarchie du § 3 de `CLAUDE.md`)

1. **Google Play / App Store** — sources fortes, aucune sollicitation par
   l'éditeur. `Comète Link` est la porte d'entrée identifiée. Les applications
   agent de terrain de chaque éditeur sont à chercher systématiquement : c'est le
   seul endroit où l'utilisateur final — l'agent, pas l'acheteur — s'exprime.
2. **Trustpilot** — source forte.
3. **Reddit, forums métier, groupes Facebook** — sources fortes. Le secteur a une
   vie syndicale et professionnelle dense (SNES, GES, USP), et des groupes
   Facebook d'agents très actifs.
4. **Capterra / G2 / GetApp** — source faible, à ne lire que pour mesurer l'écart
   avec les sources fortes.
5. **Comparateurs français** — poids **nul**. Sur ce secteur, `lebonlogiciel`,
   `logiciels.pro` et `appvizer` sont apparus dans les résultats ; s'y ajoute une
   couche locale plus trompeuse encore : les « comparatifs » publiés par
   **BanetteOne**, **SEKUR** et **Hector Solution**, qui sont des éditeurs et se
   classent premiers. Ne jamais les compter comme corpus.

### Avertissement particulier à ce secteur

La recherche d'étape 6 a montré que la documentation en ligne sur la sécurité
privée est écrite en majorité par les éditeurs eux-mêmes, y compris sur des
sujets réglementaires, et que deux d'entre eux y affirment une obligation légale
inexistante. Un corpus d'avis constitué sur ce secteur devra donc être filtré
avec une sévérité inhabituelle : la frontière entre avis d'utilisateur et
contenu d'éditeur y est particulièrement poreuse.
