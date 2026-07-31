# Agriculture / Viticulture

Recherche effectuée le : 31/07/2026
Requêtes web effectuées : 30 (+ 5 requêtes `recherche-entreprises.api.gouv.fr`)

Ordre d'exécution appliqué : **étape 6 d'abord, puis étape 3** (`CLAUDE.md` § 0
point 3). Les étapes 2, 4 et 5 n'ont pas été menées — le secteur a été fermé
avant. Les éliminatoires qu'elles instruisent sont marqués `INCONNU`, **pas
« franchis »**.

## Verdict

**NO-GO** — ISAGRI SAS réalise **144 887 287 €** de chiffre d'affaires en 2024,
soit 4,8 fois le seuil de 30 M€ qui élimine sur le critère n° 4.

Critère décisif : **éliminatoire n° 4 — leader à plus de 30 M€.** Le seuil est
dépassé au niveau de l'entité éditrice comme au niveau du groupe
(GROUPE ISA : **340 980 000 €** en 2024). Source d'État, champ `finances` de
`recherche-entreprises.api.gouv.fr`, alimenté par les comptes annuels INPI.

**Second motif indépendant, à ne pas confondre avec le premier :** la seule
échéance réglementaire du secteur tombe le **01/01/2027**, dans 5 mois, et
l'État met à cette date un **outil gratuit** à disposition de tous les
agriculteurs pour s'y conformer. La fenêtre de lancement est fermée et la porte
d'entrée réglementaire est occupée par la gratuité publique.

## 1. Dimensionnement

Codes NAF retenus : 01.11Z, 01.13Z, 01.19Z, 01.21Z, 01.24Z, 01.25Z, 01.41Z,
01.43Z, 01.45Z, 01.46Z, 01.47Z, 01.50Z, 01.61Z, 01.62Z, 01.63Z, 01.64Z, 11.02A,
11.02B (18 codes).

Entreprises cibles : **≥ 72 866** — actives (`etat_administratif=A`), tranches
d'effectif 01 à 32 (1 à 499 salariés). Décompte non refait dans cette session :
il provient de l'étape 1, détail par code et par tranche dans
`recherche/PREFILTRE_NAF.md` § 4 (source : `recherche-entreprises.api.gouv.fr`,
30/07/2026).

**Le total est un minorant.** La cellule `01.11Z` / tranche 01 est plafonnée à
`>10000 (PLAFOND)` et n'a pas été levée. Conformément à la règle 4 du § 1 de
`CLAUDE.md`, 10000 n'est pas un nombre.

| Tranche d'effectif | Nombre |
|---|---|
| 01 à 32 (cible) | **≥ 72 866** |
| Détail par tranche | `recherche/PREFILTRE_NAF.md` § 4 |

Éliminatoire n° 1 (< 3 000) : **FRANCHI**, et de très loin. Barème : > 50 000
= 3 points.

### Registre officiel du métier (règle 10 du § 1 de `CLAUDE.md`)

La profession dispose d'un décompte d'État distinct du NAF, il faut donc publier
les deux chiffres et l'écart.

| Source | Chiffre | Date |
|---|---|---|
| Recensement agricole, France entière | **416 054 exploitations en activité** | 2020 |
| Recensement agricole, France métropolitaine | ~389 000 exploitations | 2020 |
| NAF, cible 01–32 (au moins 1 salarié) | **≥ 72 866** | 30/07/2026 |

**Écart : facteur ≈ 5,7. Le NAF sous-compte**, et la cause est identifiée : la
cible retenue exclut les tranches `00` (0 salarié) et `NN` (non renseigné), or
la très grande majorité des exploitations françaises sont individuelles et sans
salarié. Les 72 866 ne sont donc pas « les exploitations agricoles » mais **les
exploitations employeuses**.

Ce n'est pas une erreur de comptage : une exploitation sans salarié est une
cible commerciale plus faible. Mais l'écart doit être connu et ne pas être lu
comme une marge de sécurité — il n'ajoute pas 340 000 clients solvables.

### Ce que le volume ne prédit pas

**72 866 cibles est le plus gros volume rencontré depuis le début de l'étude, et
cela ne vaut aucun point d'avance.** Sur les quatre secteurs précédents, aucun
n'est tombé par manque de marché : l'éliminatoire n° 1 a été franchi quatre fois
sur quatre, et les quatre secteurs sont NO-GO pour d'autres raisons. **Le volume
n'a encore jamais rien prédit.**

Sur ce secteur, il joue même à l'envers : un marché de 72 866 exploitations
employeuses nourrit un éditeur de 1 000 à 1 999 salariés. C'est précisément ce
qui déclenche l'éliminatoire n° 4.

## 2. Éditeurs en place

**Étape 2 non menée.** Conformément au § 0 point 3 de `CLAUDE.md`, elle ne sert
plus qu'à alimenter l'étape 3, et l'étape 3 a conclu sur le premier éditeur
instruit. Le tableau ci-dessous ne recense donc que les entités effectivement
instruites, pas le paysage concurrentiel du secteur, qui reste `INCONNU`.

| Éditeur | Créé en | Cible | CA (exercice) | Effectif | Prix d'entrée | Source |
|---|---|---|---|---|---|---|
| ISAGRI SAS (327733432) | 1983 | Agriculteurs, viticulteurs, éleveurs | **144 887 287 € (2024)** | 1 000 à 1 999 | `INCONNU` | API, 31/07/2026 |
| GROUPE ISA (379163546) | — | Holding de tête d'ISAGRI | **340 980 000 € (2024)** | 6 à 9 | — | API, 31/07/2026 |
| SMAG (430406918) | — | Agriculteurs, coopératives | 10 810 333 € (2022) | 100 à 199 | `INCONNU` | API, 31/07/2026 |

Offre gratuite détectée : **`INCONNU` — mais un signal fort est documenté**, voir
§ 4. Étape 4 non menée, aucun prix d'entrée relevé.

Levées de fonds : **`INCONNU`** — non recherchées, l'éliminatoire ayant été
déclenché par le CA seul.

Lecture du plafond de marché (grille de l'étape 3) : ligne **« Trois acteurs
> 20 M€, ou levées > 5 M€ → éliminatoire »**, atteinte par le seul CA du leader,
qui relève de la ligne « > 30 M€ ».

### Ce que le champ `dirigeants` a rendu, avant d'aller chercher les CA

Méthode du § 5 de `CLAUDE.md` : `dirigeants` avant `finances`, sur la même
requête, sans coût supplémentaire.

| Entité | SIREN | Président | Lecture |
|---|---|---|---|
| ISAGRI SAS | 327733432 | **GROUPE ISA** (379163546), personne morale | Filiale d'une holding |
| SMAG | 430406918 | **INVIVO AG** (801076274), personne morale | Filiale d'une union de coopératives |

**Deux consolidations sur deux éditeurs instruits.** Le croisement a rendu
immédiatement ce que la lecture des marques aurait masqué :

1. **ISAGRI n'est pas un éditeur, c'est un portefeuille.** Le champ
   `nom_complet` de l'API le dit seul :
   `ISAGRI (ISAGRI, AGIRIS, TERRE-NET, SO'NEO, PROMIZE, C2J INFO, I-CONE)`.
   Les mentions légales d'`isagri.fr` ajoutent la liste des logiciels :
   **Geofolia** et Geofolia OAD (parcellaire), **ISAVIGNE** et **ISACUVE**
   (viticulture), **Troup'O**, **Pig'UP**, **ISAOVIN**, **ISACHEVRE** (élevage),
   ISALIM, ISACOMPTA, ISAFACT, ISAPAYE.
2. **SMAG appartient à InVivo**, première union de coopératives agricoles
   françaises. C'est un point à retenir pour l'éliminatoire n° 2 : l'outil d'un
   éditeur détenu par une coopérative peut être distribué à l'adhérent dans des
   conditions qui ne sont pas un prix de marché. **Non vérifié** — étape 4 non
   menée.

**SMAG perd de l'argent** : résultat net 2022 = **− 2 560 468 €** pour
10 810 333 € de CA, et aucun exercice plus récent n'est publié. Le second acteur
instruit du secteur est déficitaire à 10,8 M€ pendant que le premier fait 144,9 M€.

### Éliminatoire n° 4 — déclenché

Seuil du § 2 de `CLAUDE.md` : « un leader à plus de 30 M€ → éliminé ».

| Niveau | Entité | CA 2024 | Rapport au seuil de 30 M€ |
|---|---|---|---|
| Entité éditrice | ISAGRI SAS | **144 887 287 €** | **× 4,8** |
| Groupe | GROUPE ISA | **340 980 000 €** | **× 11,4** |

Résultat net 2024 d'ISAGRI SAS : 11 375 410 €. L'éditeur n'est pas seulement
gros, il est **très rentable** — ce qui exclut la lecture « leader fragile ».

**Réserve à porter, elle ne change pas le verdict.** Le CA de 144 887 287 € est
celui de l'entité ISAGRI SAS **toutes activités confondues**, et cette entité
porte aussi AGIRIS (logiciel de cabinets comptables) et TERRE-NET (média
agricole). **La part réalisée sur le seul logiciel d'exploitation agricole et
viticole est `INCONNU`** : elle n'est pas publiée et je ne l'estimerai pas
(règle 2 du § 1).

Ce qui est en revanche établi, et suffit :

- L'entité est classée en **NAF 58.29C** — édition de logiciels applicatifs.
- Sa gamme couvre **la totalité des sous-segments du secteur** : productions
  végétales, viticulture, productions animales. Ce point est décisif pour la
  règle de rétrécissement, voir ci-dessous.
- Elle emploie **1 000 à 1 999 salariés**. Un développeur solo n'affronte pas un
  service commercial de cette taille sur le produit.

### Le rétrécissement a été cherché, il n'existe pas

Règle de l'utilisateur : un éliminatoire qui ne frappe qu'un sous-segment ne
ferme pas le secteur, il le rétrécit — il faut alors nommer le sous-segment,
retirer ses codes NAF, recalculer le résidu et continuer.

**Ce contrôle a été fait et il échoue : l'éliminatoire n° 4 frappe les 18 codes.**

| Sous-segment | Codes NAF | Produit ISAGRI correspondant |
|---|---|---|
| Grandes cultures, maraîchage, arboriculture | 01.11Z, 01.13Z, 01.19Z, 01.24Z, 01.25Z, 01.61Z | Geofolia, Geofolia OAD |
| Viticulture et vinification | 01.21Z, 11.02A, 11.02B | ISAVIGNE, ISACUVE Web |
| Élevage | 01.41Z, 01.43Z, 01.45Z, 01.46Z, 01.47Z, 01.62Z | Troup'O, Pig'UP, ISAOVIN, ISACHEVRE |
| Polyculture-élevage | 01.50Z | gamme complète |
| Traitement récoltes / semences | 01.63Z, 01.64Z | ISALIM |

Aucun code ne sort. **Résidu après retrait : 0.** Le secteur est fermé en
entier, pas rétréci.

## 3. Défauts documentés

**Corpus : 0 avis. Étape 5 non menée.**

Le secteur a été fermé par l'éliminatoire n° 4 avant l'étape 5. Aucun avis n'a
été lu, sur aucune plateforme. Le fichier `AGRICULTURE_VITICULTURE_avis.md`
existe et documente cette absence.

| Catégorie | Occurrences (sources fortes) | Occurrences (sources faibles) | Éditeur(s) visé(s) |
|---|---|---|---|
| — | `INCONNU` | `INCONNU` | — |

Écart de notation détecté : `INCONNU` — non recherché.

Thèmes dominants : `INCONNU`.

**À ne pas reporter comme « 0 reproche » dans `SYNTHESE.md`.** La valeur est
`INCONNU`. Un corpus non constitué n'est pas un corpus vide, et un corpus vide
n'autoriserait de toute façon que la conclusion « pas de données publiques »
(protocole, étape 5).

## 4. Contraintes réglementaires

C'est l'étape qui a été menée en premier. Elle n'a pas fermé le secteur, mais
elle a produit le second motif du verdict.

| Obligation | Texte | Date d'entrée en vigueur | Qui est concerné |
|---|---|---|---|
| Tenue du registre d'utilisation des produits phytopharmaceutiques, contenu enrichi | Arrêté du 24/12/2025, art. 7 | **01/01/2026** (en vigueur) | Tout établissement identifié par un SIRET utilisant des produits phyto |
| Registre au **format électronique lisible par machine** ; conversion annuelle au plus tard le 31 janvier de l'année n+1 | Arrêté du 24/12/2025, art. 4 et annexe II | **01/01/2027** | idem |
| Conversion au format électronique sous **30 jours** après application | Arrêté du 24/12/2025 | **01/01/2030** | idem |
| Déclarations viticoles obligatoirement en ligne (VENDANGES, STOCK, OENO, PARCEL) — le papier n'est plus admis | Portail douane.gouv.fr | En vigueur | Récoltants, caves, négociants |
| EUDR — déclaration de diligence raisonnée, traçabilité géolocalisée | Règlement (UE) 2023/1115 | **30/12/2026** (grandes et moyennes entreprises) / **30/12/2027** (micro et petits opérateurs primaires) | Filières bétail, soja, bois, cacao, café, palme, caoutchouc |

Fondement européen du registre phyto : règlement (CE) n° 1107/2009 art. 67,
règlements d'exécution (UE) **2023/564** et **2025/2203**.

### Le logiciel métier est-il certifié/agréé par l'État ?

**Réponse en deux parties. Il fallait les séparer.**

**a) Sur le registre phytosanitaire — NON.** C'est établi sur le texte lui-même.
L'arrêté du 24/12/2025 impose un **format** (« format électronique, lisible par
machine, au sens de l'article 2, point 13, de la directive (UE) 2019/1024 » ;
annexe II : « format de fichier structuré de telle manière que des applications
logicielles peuvent facilement identifier, reconnaître et extraire des données
spécifiques »). Il **n'impose aucun agrément, aucune homologation, aucune
certification et aucun référencement du logiciel** qui tient le registre. Les
tableurs Excel sont explicitement acceptés.

C'est une différence de nature avec le cas TRANSPORT : là-bas le règlement eFTI
certifiait la plateforme ; ici le texte contraint le fichier, pas l'éditeur.

**b) Sur la notification d'identification animale — un agrément existe, et son
accès n'a pas été établi.**

La notification informatisée des mouvements bovins (naissances, achats, ventes,
mortalité) impose un logiciel agréé. Formulation relevée :

> « Dans le cas d'une édition par un logiciel, il faut utiliser une application
> agréée par l'Institut de l'Elevage. »
> — FRGDS Auvergne-Rhône-Alpes, consulté le 31/07/2026

Une seconde source décrit un **numéro de référence attribué par l'Institut de
l'Élevage** à l'application. À l'inverse, la page du ministère
(`agriculture.gouv.fr/identification-et-tracabilite-des-animaux-de-rente`)
n'emploie « agréés » que pour les **repères d'identification** — boucles
auriculaires et transpondeurs — et **ne mentionne aucun agrément de logiciel**.

**Ce que je conclus, et ce que je ne conclus pas :**

- **Établi** : un agrément portant sur l'application existe, il est délivré par
  l'Institut de l'Élevage, et il conditionne la notification informatisée.
- **`INCONNU`** : son fondement réglementaire exact, ses conditions d'accès,
  son coût, et si un développeur solo peut l'obtenir. La liste publique des
  logiciels agréés n'a pas pu être ouverte — `idele.fr` renvoie une page de
  protection anti-robot.
- **Ce n'est donc pas un éliminatoire n° 3 constaté**, c'est une **restriction
  fonctionnelle établie de portée non mesurée**. Elle ne porte que sur la
  fonction de notification, pas sur le logiciel d'élevage entier.

**Éliminatoire n° 3 : NON sur le registre phyto (établi sur le texte),
`INCONNU` sur la notification animale.** Ne pas le reporter comme franchi
en bloc.

### L'État met un outil gratuit sur la seule échéance exploitable du secteur

C'est le fait le plus lourd de l'étape 6, et il ne vient pas d'un éditeur.

> « Le ministère de l'agriculture développe en partenariat avec chambre
> d'agriculture France un outil numérique accessible à tous et qui sera mis à
> disposition courant 2026 gratuitement. »
> — DRAAF Centre-Val de Loire, consulté le 31/07/2026

> « L'outil gratuit qui sera mis à disposition par le ministère de
> l'Agriculture, de l'Agro-alimentaire et de la Souveraineté alimentaire »
> — Chambres d'agriculture France, consulté le 31/07/2026, qui le dit
> **« opérationnel en janvier 2027 »**

La combinaison est mauvaise sur les deux tableaux à la fois :

- **La seule échéance réglementaire sectorielle** — le registre phyto numérique
  au 01/01/2027 — est **exactement l'objet de l'outil gratuit**, disponible à la
  même date.
- L'angle d'entrée « module réglementaire que les gros ne maintiennent pas »,
  qui est l'un des trois seuls angles autorisés par le protocole (§ 6 du fichier
  de sortie), est donc **fermé par la gratuité publique**, pas par un
  concurrent.

**Ce n'est pas l'éliminatoire n° 2 tel que le protocole le définit** — celui-ci
vise « une offre gratuite complète et crédible chez un **acteur établi** », donc
un éditeur. L'État n'est pas un éditeur, et le périmètre fonctionnel de l'outil
n'est pas publié : registre seul, ou gestion parcellaire complète ? **`INCONNU`.**

Mais l'effet sur un développeur solo est le même, et il est même pire : on ne
descend pas sous zéro, et on ne concurrence pas un outil gratuit **prescrit par
le ministère qui écrit l'obligation**.

**Éliminatoire n° 2 : `INCONNU`, avec un signal fort documenté.** Il n'a pas été
instruit — l'étape 4 n'a pas été menée, les tarifs de MesParcelles ne sont pas
publiés en ligne (les Chambres renvoient à un conseiller), et le périmètre de
l'outil ministériel n'est pas connu. **Ne pas le reporter comme franchi.**

Note sur MesParcelles, pour éviter une confusion rencontrée en cours de
recherche : **MesParcelles est l'outil payant des Chambres d'agriculture, il est
distinct de l'outil gratuit du ministère.** Les Chambres le présentent
elles-mêmes comme une alternative — « ou un logiciel de gestion parcellaire
comme MesParcelles ». Un moteur de recherche a conflué les deux ; la confusion a
été écartée sur la page des Chambres d'agriculture France. Le prix de
MesParcelles reste **`INCONNU`** : aucune des cinq pages de Chambres consultées
n'affiche de tarif.

### Les déclarations douanières viticoles ne barrent pas le logiciel

Hypothèse de départ : la piste la plus susceptible de fermer le secteur. **Elle
ne ferme pas.**

Les cinq téléprocédures (VENDANGES, STOCK, OENO, PARCEL, fiche de compte) sont
obligatoirement en ligne et le papier n'est plus admis, mais le dépôt se fait
**directement sur le portail douane.gouv.fr après création de compte**. La page
officielle de la douane n'emploie **aucun** des termes `agréé`, `certifié`,
`homologué`, `référencé` à propos d'un intermédiaire.

Un canal EDI existe et suppose, lui, un prestataire certifié par la douane — un
éditeur mentionne « @GP pour ISAVIGNE ». Mais **l'EDI est une commodité, pas une
obligation** : le portail reste ouvert et gratuit. Un éditeur non certifié EDI
perd une automatisation, il n'est pas exclu du marché.

Conséquence pour le rétrécissement : **aucun sous-segment viticole n'est barré
par une certification.** Ce qui ferme la viticulture, c'est ISAVIGNE — « logiciel
viticole de gestion commerciale n° 1 », plus de 7 000 utilisateurs, chez ISAGRI.

### HVE et cahiers des charges AOC/IGP

**Aucune obligation portant sur le logiciel.** La certification HVE est une
démarche **volontaire** portant sur l'exploitation, contrôlée par des organismes
certificateurs dont la liste est publique. Les logiciels de gestion facilitent
la préparation de l'audit, ils ne sont pas requis. Pas de zone barrée, mais pas
d'échéance exploitable non plus.

## 5. Ligne de score (à recopier telle quelle dans SYNTHESE.md)

| Champ | Valeur | Barème |
|---|---|---|
| Entreprises cibles | **≥ 72 866** (minorant) | > 50k = **3** |
| CA du leader | **144 887 287 €** (ISAGRI SAS, 2024) | > 30M = **ÉLIMINÉ** |
| Prix plancher constaté | `INCONNU` — étape 4 non menée | — |
| Occurrences du reproche dominant (sources fortes) | `INCONNU` — étape 5 non menée | — |
| Échéance réglementaire exploitable | 01/01/2027, soit **5 mois** | < 12 mois = **1** |
| Réutilisation du code de l'app BTP | **3** — voir détail ci-dessous | forte = 3 |
| Certification d'État sur le logiciel | **NON** sur le registre phyto ; `INCONNU` sur la notification animale | NON = **0** |

**Score total : NON TOTALISÉ — secteur éliminé.**

Cinq champs sur sept sont renseignés et pèsent 7 points. Deux sont `INCONNU`.
**Le total sur 18 ne doit être ni publié ni comparé** : il serait faux par
construction, et le score ne décide de rien face à un éliminatoire.

### Réutilisation du code de l'app BTP — détail brique par brique

Barème du § 6 de `CLAUDE.md` : 3 si au moins trois briques transposent, 2 si une
ou deux, 0 si aucune. **Contrôle obligatoire à chaque ligne : vers quoi la
brique atterrit-elle, et cette cible est-elle en zone barrée ?**

| # | Brique BTP | Transpose ? | Cible d'arrivée en agriculture | Zone barrée ? |
|---|---|---|---|---|
| 1 | **Factur-X / facturation électronique** | **OUI** | Facturation des ventes : céréales à la coopérative, vin au négoce, animaux. Les exploitations sont des entreprises soumises à la réforme au même titre que les autres | **OUI — éliminatoire n° 4.** ISAGRI édite ISAFACT, et ISAVIGNE est présenté comme le n° 1 de la gestion commerciale viticole avec plus de 7 000 utilisateurs |
| 2 | **Suivi documentaire de sous-traitants, relances, contrôle de validité en cascade** | **OUI, et c'est la mieux ajustée** | Validité des **Certiphyto** (certificat individuel à renouveler), agrément d'entreprise pour l'application de produits phyto, documents des saisonniers (contrat, MSA, titre de séjour), suivi des prestataires ETA | **NON.** Le Certiphyto certifie la **personne**, pas le logiciel. Aucune certification ne pèse sur l'outil qui en suit l'échéance |
| 3 | **Devis, chantiers, situations de travaux** | **PARTIELLEMENT** | « Chantier » → parcelle et intervention culturale ; « devis » → prestations d'ETA. **« Situations de travaux » ne transpose pas** : il n'y a pas de facturation à l'avancement en agriculture | **OUI pour le parcellaire** — Geofolia, ISAGRI |
| 4 | **App terrain mobile hors-ligne** | **OUI, pleinement** | Saisie de l'intervention **à la parcelle**, sans réseau. La parcelle est au réseau ce que le chantier est au BTP, et l'arrêté impose l'enregistrement sans délai après utilisation | **OUI — et c'est le piège.** Elle atterrit exactement sur le registre phyto, c'est-à-dire sur l'objet de **l'outil gratuit du ministère** opérationnel en janvier 2027 |
| 5 | **Génération de documents et signature** | **PARTIELLEMENT** | Bons de livraison, contrats d'apport, documents réglementaires | **OUI en grande partie.** Les déclarations viticoles ne s'impriment pas, elles se déposent sur le portail douane ; la notification d'identification animale passe par une application agréée Institut de l'Élevage. Un document généré n'y sert à rien |
| 6 | **Corps de métier structurés** (carrelage, couverture, électricité, maçonnerie, menuiserie, isolation, façade, chauffage/climatisation) | **NON** | L'équivalent agricole serait le référentiel cultures / espèces / itinéraires techniques, adossé à la base des AMM. Référentiel entièrement différent, à maintenir à jour réglementairement | Sans objet |

**Score : 3.** Trois briques transposent pleinement (n° 1, 2, 4), deux
partiellement (n° 3, 5), une pas du tout (n° 6).

**Et pour la cinquième fois consécutive, ce score ne décide rien.** Il tombe même
au plus mauvais endroit possible : les deux briques les mieux ajustées atterrissent
l'une chez ISAGRI (facturation), l'autre sur l'outil gratuit de l'État (saisie au
champ). Le contrôle du § 6 de `CLAUDE.md` — vérifier vers **quoi** une brique
transpose, pas seulement **si** elle transpose — est ce qui a rendu ce constat
visible. Seule la brique n° 2 atterrit en zone libre.

## 6. Périmètre du MVP, si GO

**Sans objet — le secteur est NO-GO.** Aucun périmètre MVP n'est proposé : le
protocole le réserve au cas GO, et proposer un MVP sur un secteur éliminé
reviendrait à contourner l'éliminatoire par le produit.

## 7. Fenêtre de lancement

Calcul à rebours depuis l'échéance réglementaire la plus proche du secteur.

| Jalon | Date | État au 31/07/2026 |
|---|---|---|
| Échéance réglementaire (registre phyto numérique) | **01/01/2027** | dans 5 mois |
| Pic d'achat estimé (échéance − 6 mois) | 01/07/2026 | **DÉPASSÉ** |
| Mise en ligne cible (échéance − 12 mois) | 01/01/2026 | **DÉPASSÉ** |
| Début du développement (mise en ligne − charge V1) | antérieur au 01/01/2026 | **DÉPASSÉ** |

**La fenêtre est fermée sur ce cycle réglementaire.** Les trois jalons sont
derrière nous. C'est un motif d'élimination indépendant de l'éliminatoire n° 4,
et il resterait vrai même si ISAGRI n'existait pas.

L'échéance suivante — conversion sous 30 jours au **01/01/2030**, dans 41 mois —
est hors de la fenêtre utile du barème (> 36 mois = 1 point) et porte sur la
même obligation, déjà couverte par l'outil gratuit du ministère.

## 8. Distribution

**Non instruite** — sans objet sur un secteur éliminé. `INCONNU`.

Un seul élément a été relevé en passant, et il mérite d'être noté pour un autre
secteur : le réseau des **Chambres d'agriculture** est à la fois prescripteur
réglementaire, co-développeur de l'outil gratuit du ministère et éditeur de son
propre outil payant (MesParcelles). Un canal de distribution qui est aussi un
concurrent et un prescripteur d'État n'est pas un canal.

Prix de lancement proposé : sans objet.

## 9. Le test à 48 h

Sans objet — le test à 48 h sert à invalider une hypothèse avant de développer.
L'hypothèse est déjà invalidée, sur pièces, par une source d'État.

**Si le secteur devait être rouvert** — il ne devrait pas — la question la moins
chère à trancher en premier serait : *quel est le périmètre fonctionnel exact de
l'outil gratuit du ministère opérationnel en janvier 2027 ?* Une question, un
destinataire : Chambres d'agriculture France, qui le co-développe.

## 10. Sources consultées

| URL | Nature | Éditeur du site | Conflit d'intérêt |
|---|---|---|---|
| `https://recherche-entreprises.api.gouv.fr/search` | API de décompte et de comptes annuels | DINUM / État | Aucun — source opposable |
| `https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000053228465` | Arrêté du 24/12/2025, texte intégral | État | Aucun |
| `https://draaf.centre-val-de-loire.agriculture.gouv.fr/evolution-du-registre-phytopharmaceutique-a-partir-du-1er-janvier-2026-a1972.html` | Note réglementaire | DRAAF, service déconcentré de l'État | Aucun |
| `https://agriculture.gouv.fr/identification-et-tracabilite-des-animaux-de-rente` | Page réglementaire | Ministère de l'Agriculture | Aucun |
| `https://www.douane.gouv.fr/fiche/les-declarations-viticoles-en-ligne-obligatoires` | Page réglementaire | DGDDI | Aucun |
| `https://chambres-agriculture.fr/sinformer/reglementation/environnement/detail-de-lactualite/registre-phytosanitaire-numerique-au-1er-janvier-2027` | Note réglementaire | Chambres d'agriculture France | **OUI** — co-développe l'outil gratuit du ministère et édite MesParcelles, outil payant concurrent |
| `https://ain.chambres-agriculture.fr/...`, `https://hautegaronne.chambres-agriculture.fr/...` | Notes réglementaires | Chambres départementales | **OUI** — même conflit |
| `https://mesparcelles.fr/nos-formules-dabonnement` | Page produit | Chambres d'agriculture | **OUI** — éditeur, page de vente. Aucun tarif affiché |
| `https://www.frgdsaura.fr/notifier-les-mouvements-et-les-naissances-2.html` | Note pratique | FRGDS Auvergne-Rhône-Alpes, organisme sanitaire | Faible — pas éditeur de logiciel |
| `https://www.isagri.fr/mentions-legales` | Mentions légales | ISAGRI SAS | **OUI** — éditeur. Utilisé **uniquement** pour l'identité légale et la liste des marques, jamais pour juger le marché |
| `https://www.terre-net.fr/produits-phytos/article/892753/...` | Article de presse | **Terre-net, propriété d'ISAGRI** (marque listée dans `nom_complet` de l'entité 327733432) | **OUI, majeur** — média détenu par l'éditeur leader du secteur. Utilisé uniquement pour le calendrier réglementaire, recoupé sur Légifrance et DRAAF |
| `https://www.reussir.fr/grandes-cultures/...` | Article de presse | Réussir | Faible |
| `https://agreste.agriculture.gouv.fr/` (via recherche) | Recensement agricole 2020 | Ministère de l'Agriculture | Aucun |

**Deux sources perdues, à consigner comme telles :**

- `https://bretagne.chambres-agriculture.fr/detail-actu/le-registre-phyto-numerique-devient-obligatoire-en-2026` → **HTTP 404**.
- `http://idele.fr/domaines-techniques/tracabilite-et-certification/...` → page de
  **protection anti-robot** (« connection verification », « haphash »). C'est ce
  qui empêche d'établir les conditions de l'agrément des logiciels d'élevage.
- `https://alsace.edeidentification.fr/conventionsEDE/Convention_57.pdf` → PDF
  récupéré mais **non extractible en texte**.

Rappel du § 5 de `CLAUDE.md`, vérifié une fois de plus : `pappers.fr` et
`societe.com` apparaissent dans les résultats de recherche mais n'ont pas été
interrogés — le champ `finances` de l'API a suffi, et c'est une source d'État.

## 11. Zones d'ombre

Par ordre décroissant d'impact sur la décision. Aucune ne remet en cause le
verdict — l'éliminatoire n° 4 est établi sur source d'État — mais toutes
resteraient à lever si le secteur était rouvert.

1. **Périmètre fonctionnel de l'outil gratuit du ministère** (janvier 2027).
   Registre phyto seul, ou gestion parcellaire complète ? C'est la différence
   entre « un angle d'entrée est fermé » et « le secteur est gratuit ».
   À qui poser la question : Chambres d'agriculture France, co-développeur.
2. **Part du CA d'ISAGRI SAS réalisée sur le logiciel d'exploitation agricole**,
   hors AGIRIS et Terre-net. Non publiée. Ne change pas le verdict au niveau
   groupe, mais chiffrerait la domination réelle sur le secteur.
3. **Conditions d'accès à l'agrément des logiciels d'élevage** délivré par
   l'Institut de l'Élevage : fondement réglementaire, cahier des charges, coût,
   délai, et si un éditeur solo peut y prétendre. Bloqué par l'anti-robot
   d'`idele.fr`. À demander directement à l'Institut de l'Élevage ou à un EDE.
4. **Tarifs de MesParcelles**, et surtout : l'abonnement est-il inclus dans la
   cotisation aux Chambres d'agriculture, ou facturé en sus ? Aucune des cinq
   pages consultées ne l'indique ; toutes renvoient à un conseiller. C'est la
   question qui trancherait l'éliminatoire n° 2 sous sa forme « outil déjà payé
   par la cotisation ».
5. **Conditions de distribution de SMAG aux adhérents d'InVivo.** Un éditeur
   détenu par une union de coopératives peut servir l'adhérent à un prix qui
   n'est pas un prix de marché. Non vérifié.
6. **Paysage concurrentiel complet.** L'étape 2 n'a pas été menée. MyEasyFarm,
   Agriconomie, Ekylibre et les filiales logicielles des coopératives n'ont pas
   été instruits — la seule requête lancée sur `MYEASYFARM` ne rend qu'un
   véhicule d'investissement (`MYEASYFARM WISEED PARTICIPATIONS`, 944868298,
   NAF 66.30Z, `finances: null`), pas l'éditeur.
7. **Éliminatoires n° 2 et le volet animal du n° 3 : `INCONNU`.** Voir § 4. Ne
   pas les reporter comme franchis dans `SYNTHESE.md`.
