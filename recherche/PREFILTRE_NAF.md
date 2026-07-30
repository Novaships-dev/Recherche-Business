# PRÉFILTRE NAF — dimensionnement des secteurs (étape 1)

- **Date de toutes les requêtes : 30/07/2026.**
- Source unique des décomptes : `https://recherche-entreprises.api.gouv.fr/search`
- Source des libellés NAF : `https://www.insee.fr/fr/metadonnees/nafr2/sousClasse/[code]`
- Source des libellés de tranche : `https://raw.githubusercontent.com/annuaire-entreprises-data-gouv-fr/search-api/main/app/labels/tranches-effectifs.json` (fichier de libellés de l'API, référencé par sa spec OpenAPI)
- Source des libellés de forme juridique : `https://xml.insee.fr/schema/cj-enum.html` (attribut `dc:title`)
- Nomenclature : **NAF rév. 2 (2008)**, seule acceptée par `activite_principale`.

## Définition de la cible

> Entreprise **active** (`etat_administratif=A`) dont la `tranche_effectif_salarie` est comprise entre **01 et 32**, soit **1 à 499 salariés**.

Définition fixée par l'utilisateur le 30/07/2026. Elle remplace la procédure de comptage de la section 5 de `NOTE_METHODE_API_ET_CODES_NAF.md`.

Sont donc exclus de la cible : `NN` (unité non employeuse), `00` (0 salarié au 31/12),
et `41` à `53` (500 salariés et plus).

## Comment chaque chiffre a été obtenu

**Cible d'un code NAF = somme de 9 requêtes**, une par tranche :

```
https://recherche-entreprises.api.gouv.fr/search?activite_principale=[code]&etat_administratif=A&tranche_effectif_salarie=[01|02|03|11|12|21|22|31|32]
```

**Cible d'un secteur = somme des cibles de ses codes.** Légitime : `activite_principale`
filtre sur le code de l'unité légale elle-même, vérifié sur 300 résultats (300/300 exacts),
et les codes NAF sont mutuellement exclusifs. Aucun double-compte.

> ⚠️ **La requête à liste (`tranche_effectif_salarie=01,02,…,32`) n'a pas été utilisée
> pour publier un chiffre.** Elle est documentée par l'API et fonctionne comme un OU
> logique, mais son `total_results` est faux — de l'ordre de 0,5 %, dans les deux sens.
> Établi par énumération exhaustive de 80.10Z : `total_results` annonce 3461, alors que
> l'énumération des 139 pages rend 3445 SIREN distincts, sans doublon, aucun hors 01–32,
> et la somme des 9 requêtes par tranche unique donne exactement 3445. Détail dans
> `recherche/JOURNAL.md`.

`>10000 (PLAFOND)` : l'API plafonne `total_results` à 10000. Une cellule à cette valeur
signifie « ≥ 10000, valeur inconnue ». Le total du code devient alors un **minorant**, noté `≥`.

## Synthèse — les dix secteurs

| # | Secteur | Codes | Cible (actives, 1–499 sal.) | Précision | Éliminé (< 3 000 cibles) |
|---|---|---|---|---|---|
| 1 | SYNDICS / GESTION LOCATIVE | 2 | **4 743** | exacte | NON |
| 2 | TRANSPORT DERNIER KM | 4 | **22 323** | exacte | NON |
| 3A | SÉCURITÉ PRIVÉE | 3 | **4 775** | exacte | NON |
| 3B | PROPRETÉ | 5 | **≥ 26 353** | **minorant** — 1 code dont une cellule plafonne | NON |
| 3C | INTÉRIM / PLACEMENT | 3 | **10 002** | exacte | NON |
| 4 | AGRICULTURE / VITICULTURE | 18 | **≥ 72 866** | **minorant** — 1 code dont une cellule plafonne | NON |
| 5 | GMAO / MAINTENANCE (prestataires) | 10 | **13 953** | exacte | NON |
| 6A | ASSOCIATIONS | 12 | **≥ 81 615** | **minorant** — 2 codes dont une cellule plafonne | NON |
| 6B | COLLECTIVITÉS | 3 | **≥ 41 383** | **minorant** — 1 code dont une cellule plafonne | NON |
| 7 | CABINETS COMPTA / JURIDIQUE | 2 | **31 896** | exacte | NON |
| 8 | RSE / VSME / QUESTIONNAIRES FOURNISSEURS | — | **INCONNU** | — | **INDÉTERMINÉ** |

**Aucun des dix secteurs comptés n'est éliminé par le seuil de 3 000.** Le plus petit,
SYNDICS / GESTION LOCATIVE, est à 4 743 cibles, soit 1,6× le seuil.

Un total marqué `≥` est un **minorant** : au moins une cellule de tranche a atteint le
plafond de l'API et n'a pas pu être résolue. Cela ne change aucune décision
d'élimination — les secteurs concernés dépassent tous largement le seuil — mais ces
chiffres ne doivent pas être comparés entre eux comme s'ils étaient exacts.

**Le total d'actives toutes tranches confondues n'est volontairement pas agrégé au
niveau secteur** : il est plafonné sur la majorité des codes, et en additionner des
plafonds produit un nombre dénué de sens — sur 6B il donnerait même un « total » 
inférieur à la cible. Il figure code par code dans le détail, avec sa mention de plafond.

## Détail par secteur

### 1 — SYNDICS / GESTION LOCATIVE

**Cible du secteur : 4 743.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `68.32A` | Administration d'immeubles et autres biens immobiliers | 2 077 | 840 | 465 | 558 | 338 | 83 | 52 | 10 | 10 | **4 433** | >10000 (PLAFOND) |
| `68.32B` | Supports juridiques de gestion de patrimoine immobilier | 224 | 51 | 12 | 13 | 5 | 2 | 2 | 1 | 0 | **310** | >10000 (PLAFOND) |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **4 743** | |

### 2 — TRANSPORT DERNIER KM

**Cible du secteur : 22 323.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `49.41A` | Transports routiers de fret interurbains | 2 699 | 1 930 | 1 425 | 1 576 | 1 467 | 493 | 251 | 43 | 77 | **9 961** | >10000 (PLAFOND) |
| `49.41B` | Transports routiers de fret de proximité | 3 478 | 2 456 | 1 794 | 1 843 | 1 302 | 344 | 143 | 25 | 29 | **11 414** | >10000 (PLAFOND) |
| `49.41C` | Location de camions avec chauffeur | 81 | 77 | 60 | 103 | 158 | 51 | 40 | 9 | 6 | **585** | 1 091 |
| `52.29A` | Messagerie, fret express | 47 | 36 | 45 | 49 | 86 | 43 | 28 | 9 | 20 | **363** | 1 124 |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **22 323** | |

### 3A — SÉCURITÉ PRIVÉE

**Cible du secteur : 4 775.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `80.10Z` | Activités de sécurité privée | 585 | 525 | 513 | 633 | 697 | 277 | 139 | 34 | 42 | **3 445** | >10000 (PLAFOND) |
| `80.20Z` | Activités liées aux systèmes de sécurité | 450 | 311 | 177 | 162 | 114 | 39 | 10 | 5 | 3 | **1 271** | 5 060 |
| `80.30Z` | Activités d'enquête | 38 | 10 | 2 | 3 | 3 | 1 | 1 | 1 | 0 | **59** | 1 153 |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **4 775** | |

### 3B — PROPRETÉ

**Cible du secteur : ≥ 26 353.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `81.10Z` | Activités combinées de soutien lié aux bâtiments | **>10000** | 784 | 106 | 75 | 33 | 5 | 8 | 0 | 2 | **≥ 11 013** | >10000 (PLAFOND) |
| `81.21Z` | Nettoyage courant des bâtiments | 3 198 | 2 094 | 1 502 | 1 580 | 1 399 | 605 | 303 | 61 | 148 | **10 890** | >10000 (PLAFOND) |
| `81.22Z` | Autres activités de nettoyage des bâtiments et nettoyage industriel | 993 | 601 | 443 | 427 | 366 | 142 | 44 | 11 | 14 | **3 041** | >10000 (PLAFOND) |
| `81.29A` | Désinfection, désinsectisation, dératisation | 379 | 183 | 109 | 79 | 54 | 6 | 1 | 1 | 2 | **814** | 5 696 |
| `81.29B` | Autres activités de nettoyage n.c.a. | 290 | 125 | 64 | 64 | 38 | 5 | 3 | 2 | 4 | **595** | 6 052 |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **≥ 26 353** | |

Cellules plafonnées, reprises par sous-partition en 260 formes juridiques :
- `81.10Z` tranche 01 : **`>10000 (PLAFOND)`, non résolue.** La levée demande 260 requêtes pour cette seule cellule (cf. § Cellules plafonnées).

### 3C — INTÉRIM / PLACEMENT

**Cible du secteur : 10 002.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `78.10Z` | Activités des agences de placement de main-d'œuvre | 306 | 127 | 59 | 52 | 54 | 17 | 11 | 6 | 3 | **635** | 3 331 |
| `78.20Z` | Activités des agences de travail temporaire | 1 132 | 1 568 | 681 | 360 | 120 | 29 | 10 | 1 | 5 | **3 906** | 6 860 |
| `78.30Z` | Autre mise à disposition de ressources humaines | 1 925 | 1 032 | 635 | 678 | 675 | 327 | 144 | 22 | 23 | **5 461** | >10000 (PLAFOND) |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **10 002** | |

### 4 — AGRICULTURE / VITICULTURE

**Cible du secteur : ≥ 72 866.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `01.21Z` | Culture de la vigne | 9 423 | 4 661 | 1 639 | 738 | 233 | 26 | 8 | 0 | 0 | **16 728** | >10000 (PLAFOND) |
| `11.02A` | Fabrication de vins effervescents | 51 | 47 | 41 | 31 | 28 | 12 | 12 | 2 | 2 | **226** | 410 |
| `11.02B` | Vinification | 158 | 134 | 130 | 115 | 80 | 13 | 11 | 2 | 1 | **644** | 1 311 |
| `01.11Z` | Culture de céréales (à l'exception du riz), de légumineuses et de graines oléagineuses | **>10000** | 1 611 | 243 | 94 | 30 | 5 | 4 | 0 | 2 | **≥ 11 989** | >10000 (PLAFOND) |
| `01.13Z` | Culture de légumes, de melons, de racines et de tubercules | 2 191 | 978 | 410 | 284 | 140 | 28 | 9 | 4 | 4 | **4 048** | >10000 (PLAFOND) |
| `01.19Z` | Autres cultures non permanentes | 354 | 181 | 80 | 70 | 31 | 4 | 2 | 1 | 1 | **724** | 9 264 |
| `01.24Z` | Culture de fruits à pépins et à noyau | 1 216 | 619 | 247 | 156 | 74 | 9 | 1 | 1 | 0 | **2 323** | >10000 (PLAFOND) |
| `01.25Z` | Culture d'autres fruits d'arbres ou d'arbustes et de fruits à coque | 228 | 70 | 23 | 15 | 3 | 1 | 0 | 0 | 0 | **340** | 4 500 |
| `01.41Z` | Élevage de vaches laitières | 8 636 | 989 | 126 | 37 | 4 | 1 | 0 | 0 | 0 | **9 793** | >10000 (PLAFOND) |
| `01.43Z` | Élevage de chevaux et d'autres équidés | 1 502 | 429 | 122 | 55 | 18 | 1 | 0 | 0 | 0 | **2 127** | >10000 (PLAFOND) |
| `01.45Z` | Élevage d'ovins et de caprins | 2 095 | 239 | 51 | 17 | 4 | 0 | 0 | 0 | 0 | **2 406** | >10000 (PLAFOND) |
| `01.46Z` | Élevage de porcins | 1 290 | 522 | 116 | 46 | 7 | 3 | 0 | 0 | 0 | **1 984** | 6 815 |
| `01.47Z` | Élevage de volailles | 1 786 | 297 | 90 | 80 | 54 | 11 | 6 | 0 | 3 | **2 327** | >10000 (PLAFOND) |
| `01.50Z` | Culture et élevage associés | 8 843 | 1 310 | 221 | 54 | 19 | 4 | 1 | 0 | 0 | **10 452** | >10000 (PLAFOND) |
| `01.61Z` | Activités de soutien aux cultures | 3 347 | 1 250 | 563 | 379 | 134 | 19 | 5 | 1 | 1 | **5 699** | >10000 (PLAFOND) |
| `01.62Z` | Activités de soutien à la production animale | 615 | 197 | 72 | 61 | 44 | 15 | 10 | 0 | 2 | **1 016** | 7 475 |
| `01.63Z` | Traitement primaire des récoltes | 12 | 9 | 3 | 1 | 1 | 0 | 0 | 0 | 0 | **26** | 98 |
| `01.64Z` | Traitement des semences | 6 | 2 | 3 | 0 | 3 | 0 | 0 | 0 | 0 | **14** | 52 |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **≥ 72 866** | |

Cellules plafonnées, reprises par sous-partition en 260 formes juridiques :
- `01.11Z` tranche 01 : **`>10000 (PLAFOND)`, non résolue.** La levée demande 260 requêtes pour cette seule cellule (cf. § Cellules plafonnées).

### 5 — GMAO / MAINTENANCE (prestataires)

**Cible du secteur : 13 953.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `33.11Z` | Réparation d'ouvrages en métaux | 129 | 104 | 86 | 98 | 76 | 20 | 6 | 4 | 7 | **530** | 1 749 |
| `33.12Z` | Réparation de machines et équipements mécaniques | 1 657 | 1 026 | 499 | 374 | 216 | 47 | 23 | 6 | 12 | **3 860** | >10000 (PLAFOND) |
| `33.13Z` | Réparation de matériels électroniques et optiques | 75 | 61 | 34 | 34 | 34 | 15 | 9 | 2 | 2 | **266** | 742 |
| `33.14Z` | Réparation d'équipements électriques | 201 | 159 | 103 | 103 | 54 | 16 | 10 | 1 | 1 | **648** | 1 643 |
| `33.19Z` | Réparation d'autres équipements | 81 | 39 | 23 | 15 | 13 | 7 | 3 | 0 | 0 | **181** | 921 |
| `33.20A` | Installation de structures métalliques, chaudronnées et de tuyauterie | 669 | 493 | 310 | 284 | 183 | 29 | 10 | 1 | 0 | **1 979** | 7 760 |
| `33.20B` | Installation de machines et équipements mécaniques | 498 | 309 | 236 | 254 | 163 | 42 | 13 | 1 | 2 | **1 518** | 3 449 |
| `33.20C` | Conception d'ensemble et assemblage sur site industriel d'équipements de contrôle des processus industriels | 133 | 139 | 90 | 120 | 74 | 36 | 16 | 3 | 3 | **614** | 1 266 |
| `33.20D` | Installation d'équipements électriques, de matériels électroniques et optiques ou d'autres matériels | 266 | 169 | 121 | 98 | 66 | 22 | 7 | 0 | 3 | **752** | 2 725 |
| `71.20B` | Analyses, essais et inspections techniques | 1 795 | 725 | 362 | 324 | 230 | 86 | 45 | 15 | 23 | **3 605** | >10000 (PLAFOND) |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **13 953** | |

### 6A — ASSOCIATIONS

**Cible du secteur : ≥ 81 615.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `94.99Z` | Autres organisations fonctionnant par adhésion volontaire | **>10000** | 5 564 | 2 945 | 2 516 | 1 341 | 296 | 106 | 13 | 26 | **≥ 22 807** | >10000 (PLAFOND) |
| `94.12Z` | Activités des organisations professionnelles | 1 195 | 455 | 249 | 199 | 102 | 24 | 13 | 3 | 4 | **2 244** | >10000 (PLAFOND) |
| `94.20Z` | Activités des syndicats de salariés | 1 434 | 313 | 102 | 54 | 48 | 22 | 8 | 0 | 2 | **1 983** | >10000 (PLAFOND) |
| `94.11Z` | Activités des organisations patronales et consulaires | 1 039 | 579 | 300 | 241 | 94 | 95 | 38 | 5 | 10 | **2 401** | 9 669 |
| `94.91Z` | Activités des organisations religieuses | 3 029 | 741 | 335 | 265 | 152 | 47 | 17 | 0 | 2 | **4 588** | >10000 (PLAFOND) |
| `94.92Z` | Activités des organisations politiques | 120 | 17 | 8 | 6 | 5 | 2 | 0 | 0 | 0 | **158** | 3 462 |
| `93.12Z` | Activités de clubs de sports | **>10000** | 6 535 | 2 273 | 1 291 | 654 | 144 | 56 | 10 | 10 | **≥ 20 973** | >10000 (PLAFOND) |
| `93.19Z` | Autres activités liées au sport | 1 722 | 608 | 250 | 176 | 99 | 27 | 6 | 2 | 3 | **2 893** | >10000 (PLAFOND) |
| `88.99A` | Autre accueil ou accompagnement sans hébergement d'enfants et d'adolescents | 50 | 46 | 53 | 62 | 42 | 25 | 14 | 5 | 9 | **306** | 3 152 |
| `88.99B` | Action sociale sans hébergement n.c.a. | 2 432 | 1 499 | 1 050 | 1 487 | 1 765 | 1 053 | 435 | 81 | 161 | **9 963** | >10000 (PLAFOND) |
| `88.91A` | Accueil de jeunes enfants | 311 | 1 903 | 1 613 | 1 510 | 722 | 223 | 59 | 14 | 12 | **6 367** | >10000 (PLAFOND) |
| `88.10A` | Aide à domicile | 555 | 523 | 589 | 1 660 | 2 519 | 735 | 244 | 26 | 81 | **6 932** | >10000 (PLAFOND) |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **≥ 81 615** | |

Cellules plafonnées, reprises par sous-partition en 260 formes juridiques :
- `94.99Z` tranche 01 : **`>10000 (PLAFOND)`, non résolue.** La levée demande 260 requêtes pour cette seule cellule (cf. § Cellules plafonnées).
- `93.12Z` tranche 01 : **`>10000 (PLAFOND)`, non résolue.** La levée demande 260 requêtes pour cette seule cellule (cf. § Cellules plafonnées).

### 6B — COLLECTIVITÉS

**Cible du secteur : ≥ 41 383.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `84.11Z` | Administration publique générale | 5 191 | **>10000** | 5 660 | 6 042 | 5 376 | 2 332 | 1 583 | 341 | 799 | **≥ 37 324** | >10000 (PLAFOND) |
| `84.12Z` | Administration publique (tutelle) de la santé, de la formation, de la culture et des services sociaux, autre que sécurité sociale | 481 | 566 | 528 | 367 | 172 | 141 | 81 | 13 | 40 | **2 389** | 3 398 |
| `84.13Z` | Administration publique (tutelle) des activités économiques | 240 | 229 | 203 | 295 | 394 | 110 | 122 | 21 | 56 | **1 670** | 2 352 |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **≥ 41 383** | |

Cellules plafonnées, reprises par sous-partition en 260 formes juridiques :
- `84.11Z` tranche 02 : **`>10000 (PLAFOND)`, non résolue.** La levée demande 260 requêtes pour cette seule cellule (cf. § Cellules plafonnées).

### 7 — CABINETS COMPTA / JURIDIQUE

**Cible du secteur : 31 896.** Éliminé (< 3 000) : **NON**

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `69.10Z` | Activités juridiques | 8 644 | 4 068 | 2 446 | 2 087 | 882 | 122 | 38 | 3 | 9 | **18 299** | >10000 (PLAFOND) |
| `69.20Z` | Activités comptables | 4 005 | 3 165 | 2 425 | 2 359 | 1 224 | 263 | 101 | 20 | 35 | **13 597** | >10000 (PLAFOND) |
| | **TOTAL SECTEUR** |  |  |  |  |  |  |  |  |  | **31 896** | |

## Libellés des tranches d'effectif

| Code | Libellé officiel | Dans la cible |
|---|---|---|
| `NN` | Unité non employeuse (pas de salarié au cours de l'année de référence et pas d'effectif au 31/12) | non |
| `00` | 0 salarié (n'ayant pas d'effectif au 31/12 mais ayant employé des salariés au cours de l'année de référence) | non |
| `01` | 1 ou 2 salariés | **oui** |
| `02` | 3 à 5 salariés | **oui** |
| `03` | 6 à 9 salariés | **oui** |
| `11` | 10 à 19 salariés | **oui** |
| `12` | 20 à 49 salariés | **oui** |
| `21` | 50 à 99 salariés | **oui** |
| `22` | 100 à 199 salariés | **oui** |
| `31` | 200 à 249 salariés | **oui** |
| `32` | 250 à 499 salariés | **oui** |
| `41` | 500 à 999 salariés | non |
| `42` | 1 000 à 1 999 salariés | non |
| `51` | 2 000 à 4 999 salariés | non |
| `52` | 5 000 à 9 999 salariés | non |
| `53` | 10 000 salariés et plus | non |

## Secteur 8 — RSE / VSME / questionnaires fournisseurs

**Dimensionnement : `INCONNU`.**

Ce n'est pas un secteur NAF. La cible — les fournisseurs soumis au questionnaire VSME —
est transverse à toutes les activités : aucun code d'activité ne la délimite.

Conformément à l'arbitrage du 30/07/2026, **aucun proxy comparable n'a été construit**.
La méthode de substitution envisagée en session 1 (dimensionnement par tranche
d'effectif toutes activités confondues) a été écartée : elle aurait produit un nombre
d'apparence comparable aux dix autres secteurs sans l'être.

Mesures existantes, insuffisantes pour dimensionner et rappelées seulement pour mémoire :
`categorie_entreprise=PME`, `categorie_entreprise=ETI` et `tranche_effectif_salarie=22`
renvoient toutes trois 10000, c'est-à-dire le plafond, donc aucune information.

Ce secteur ne peut pas être comparé aux dix autres, ni noté sur le même barème, tant
qu'une définition opérationnelle de sa cible n'a pas été fournie.

## Réserves sur l'interprétation de ces chiffres

1. **Un décompte NAF est un majorant, pas un marché.** Le code décrit une activité
   déclarée, pas un besoin logiciel ni une capacité d'achat.
2. **Le filtre d'effectif corrige le biais du § 2.5, et c'est mesuré.** La note de
   session 1 établissait que 68.32A était noyé de sociétés civiles immobilières
   (`nature_juridique=6540`, plafonnée à ≥10000 dans la seule tranche `NN`). Dans la
   cible 01–32, ces SCI ne pèsent plus que **89 unités sur 4 433, soit 2,0 %** :
   une SCI n'a, par construction, pas de salarié. La restriction aux tranches 01–32
   évacue donc mécaniquement ce biais précis.

   ```
   https://recherche-entreprises.api.gouv.fr/search?activite_principale=68.32A&etat_administratif=A&nature_juridique=6540
       &tranche_effectif_salarie=[01…32]   -> 74+11+2+2+0+0+0+0+0 = 89
   ```

   Ce n'est vrai que de ce biais-là. Le filtre ne dit rien de la solvabilité ni de
   l'appétence logicielle, et il ne purge pas les associations dormantes employeuses.
3. **84.11Z (administration publique générale) reste à traiter avec prudence** : la
   population est très majoritairement composée de petites communes, dont beaucoup sans
   budget logiciel. Le décompte est juste, la cible commerciale est probablement bien plus
   étroite.
4. **Aucune donnée d'étape 2 à 6.** Aucun éditeur, aucun avis, aucune contrainte
   réglementaire n'a été recherché. Ce fichier ne dit rien de la concurrence.
5. **Le champ « réutilisation du code de l'app BTP » du barème reste `INCONNU`** :
   aucune information n'a jamais été fournie sur cette application.

## Cellules plafonnées

Cinq cellules de tranche atteignent le plafond de 10000 :
`81.10Z`/01, `01.11Z`/01, `94.99Z`/01, `93.12Z`/01, `84.11Z`/02.
Ce sont elles, et elles seules, qui affectent la précision des totaux de 3B, 4, 6A et 6B.

Méthode de levée, validée : sous-partition de la cellule par les 260 valeurs de
`nature_juridique`, seul axe à la fois exclusif et exhaustif que l'API expose. Coût :
**1 300 requêtes**. Les axes géographiques (`region`, `code_postal`, `code_commune`,
`epci`) ne peuvent pas servir : comme `departement`, ils filtrent sur les
**établissements** et double-comptent les unités multi-établissements.

**État : 5 des 5 cellules restent non résolues** (`81.10Z`/01, `01.11Z`/01, `94.99Z`/01, `93.12Z`/01, `84.11Z`/02). Les totaux de secteur
correspondants sont donc des **minorants**, marqués `≥`.

**Aucune décision d'élimination ne dépend de ces cellules** : les quatre secteurs
concernés dépassent le seuil de 3 000 d'un ordre de grandeur.

> Note de méthode sur l'API : la latence est très irrégulière — 12 requêtes
> séquentielles identiques mesurées le 30/07/2026 donnent 12/12 réussies, médiane 0,22 s,
> **maximum 40,3 s**. Aucun blocage, aucun HTTP 429. En revanche l'API renvoie des
> réponses non-JSON quand plusieurs campagnes tournent en parallèle. Le § 2.6 de la note
> (« aucune limitation rencontrée en séquentiel ») est à nuancer sur ce point.

## Journal d'audit

Une ligne par requête publiée (URL complète, `total_results`, date) a été tenue pendant
le comptage : **682 requêtes** pour les 62 codes des dix secteurs, hors requêtes de
diagnostic et de sous-partition. Le détail par code et par tranche est reproduit dans les
tableaux ci-dessus ; l'URL de chaque cellule se reconstruit exactement par le patron
donné plus haut, par exemple :

```
https://recherche-entreprises.api.gouv.fr/search?activite_principale=68.32A&etat_administratif=A&tranche_effectif_salarie=12
```
