# GMAO / MAINTENANCE (prestataires)

Recherche effectuée le : 30/07/2026
Requêtes web effectuées : 15 WebSearch + 27 WebFetch = **42**

Étape 1 non refaite : reprise de `recherche/PREFILTRE_NAF.md` (requêtes du
30/07/2026). Étapes 2 à 6 conduites dans cette session.

## Verdict

**À CREUSER** — aucun des quatre éliminatoires ne se déclenche, et la fenêtre
réglementaire de septembre 2027 est réelle et exploitable ; mais la preuve
décisive du protocole — un corpus de défauts documentés — **n'existe pas
publiquement**, et le segment est en cours de consolidation active par un
groupe sous LBO.

**Critère décisif : l'absence de corpus d'avis.** 4 avis lisibles sur toutes
sources fortes confondues, contre 100 à 400 attendus. Le protocole interdit
d'en conclure « pas de problème » ; il impose de conclure « pas de données
publiques — vérification terrain requise ». Un GO reposerait donc sur une
hypothèse de douleur client non vérifiée, ce que la règle du NON par défaut
interdit.

**Ce qui empêche le NO-GO franc** : rien ne l'impose. Les quatre éliminatoires
sont passés, le plancher tarifaire est tenable, l'échéance réglementaire tombe
à 13 mois et la réutilisation du code BTP est forte. Le secteur mérite le test
à 48 h du § 9, pas l'abandon.

## 1. Dimensionnement

Codes NAF retenus : `33.11Z`, `33.12Z`, `33.13Z`, `33.14Z`, `33.19Z`,
`33.20A`, `33.20B`, `33.20C`, `33.20D` — **9 codes**.

**Code retiré du périmètre** : `71.20B` « Analyses, essais et inspections
techniques », 3 605 cibles. Arbitrage de l'utilisateur du 30/07/2026 : autre
métier, autre logiciel, et accréditation COFRAC en travers.

Entreprises totales : **10 348** (source : `recherche/PREFILTRE_NAF.md`,
requêtes du 30/07/2026 sur `https://recherche-entreprises.api.gouv.fr/search`).

Calcul : 13 953 (10 codes) − 3 605 (`71.20B`) = **10 348**. Soustraction sur
deux cellules exactes ; **aucune cellule plafonnée dans ce secteur**, la
précision reste « exacte ». Contrôle de cohérence effectué :
530+3 860+266+648+181+1 979+1 518+614+752 = 10 348.

| Code | Libellé NAF rév. 2 | Cible (actives, 1–499 sal.) |
|---|---|---|
| `33.12Z` | Réparation de machines et équipements mécaniques | 3 860 |
| `33.20A` | Installation de structures métalliques, chaudronnées et de tuyauterie | 1 979 |
| `33.20B` | Installation de machines et équipements mécaniques | 1 518 |
| `33.20D` | Installation d'équipements électriques, électroniques, optiques ou autres | 752 |
| `33.14Z` | Réparation d'équipements électriques | 648 |
| `33.20C` | Conception d'ensemble et assemblage sur site industriel d'équipements de contrôle | 614 |
| `33.11Z` | Réparation d'ouvrages en métaux | 530 |
| `33.13Z` | Réparation de matériels électroniques et optiques | 266 |
| `33.19Z` | Réparation d'autres équipements | 181 |
| | **TOTAL** | **10 348** |

La répartition par tranche d'effectif code par code figure au § 5 de
`recherche/PREFILTRE_NAF.md` et n'est pas recopiée ici.

Cible réaliste (segment adressable) : **INCONNU**. Aucune donnée n'a été
produite dans cette session sur la part de ces 10 348 entreprises déjà équipées
d'un logiciel, ni sur celles trop petites pour en acheter un. Le décompte NAF
est un majorant, pas un marché — règle 10 du § 1 de `CLAUDE.md`.

## 2. Éditeurs en place

**34 éditeurs identifiés** en 8 requêtes, bien au-delà des 8 à 15 visés. Le
constat le plus important de l'étape 2 est cette **fragmentation** : chaque
reformulation du vocabulaire métier fait remonter de nouveaux petits acteurs.
La seule requête sur le vocabulaire CVC en a révélé six inconnus des sept
requêtes précédentes.

### Famille A — gestion d'interventions (marché cible : prestataires itinérants)

Praxedo, Organilog, Synchroteam, Yuman, Bob! Desk, AntsRoute, InterFast,
Horneo, Planeo, SetInUp, Divalto, Nomadia, Kizeo Forms, Twimm, Lapala, Nexxio,
Technic-Soft, Mageltys, TooSmart, Sydev, CODIAL (Cibeo Consulting), Service 9000

### Famille B — GMAO industrielle (marché voisin, mesuré pour situer)

DIMO Maint, Mobility Work, CARL Source, Coswin (Siveco), Altair (DSD System),
Optimaint, Kimoce, allMAINT, RS GMAO, Alteva, DOMMS, B2O

### Instruits sur pièces

| Éditeur | Entité légale | SIREN | Créée | Cible réelle | CA (exercice) | Résultat net | Effectif 2023 | Prix d'entrée | Source |
|---|---|---|---|---|---|---|---|---|---|
| **Praxedo** | PRAXEDO, SARL, capital 1 M€ | 479788689 | 03/01/2005 | Prestataires itinérants, PME et ETI | `finances` = **null** — comptes confidentiels. Dernier accessible : **3 499 000 € (2014)**. *Rapporté par la presse, non vérifié sur pièces* : 28 286 999 € (2024), 16 439 150 € (2021), 7 003 000 € (2018) | 564 100 € (2014) | **100 à 199** | **35 €/util./mois, minimum 5 → 175 €/mois réels** | API RNE + societe.com + annuaire-startups.pro |
| **Organilog** | ADALGO, SARL, capital 100 k€ | 804963957 | 02/10/2014 | Prestataires itinérants | **INCONNU** — champ `ca` à 0, soit non renseigné, exercice 2025 | **216 363 €** (2025) | 20 à 49 | **0 € (Basique, archivage 72 h)** puis 19 € | API RNE + mentions légales |
| **Synchroteam** | SYNCHROTEAM | 430244749 | 01/02/2000 | Prestataires itinérants | **3 494 878 €** (2024) | 2 733 708 € (2024) | 6 à 9 | INCONNU — page tarifs en 404 | API RNE |
| **Nomadia Group** | NOMADIA GROUP, holding | 884911116 | 06/07/2020 | Groupe multi-produits | 4 705 941 € (2024) — **comptes sociaux de la holding uniquement** | **−1 387 996 €** (2024) | 10 à 19 | INCONNU | API RNE |
| **Bob! Desk** | BOB DEPANNAGE (mentions légales : « BOB&CO »), SAS, capital 10 525 € | 810972927 | 20/04/2015 | Prestataires **et** services internes | **INCONNU** — champ `ca` à 0, exercice 2024 | **−22 842 €** (2024) | 10 à 19 | **Non affiché, devis.** Essai 14 jours | API RNE + mentions légales |
| **Yuman** | Entité **belge**, Square de Meuûs 35, 1000 Bruxelles ; bureau 7 rue de Madrid, 75008 Paris | **INCONNU** | INCONNU | Mixte : industrie, patrimoine immobilier, prestataires, transport | **INCONNU** | INCONNU | INCONNU | INCONNU | site éditeur |
| **FreeMaint** | « Freemaint LLC ». App Store : développeur **Melek Mehrez**. Aucun SIREN, aucune adresse | — | Application v1.0 le **27/01/2026** | GMAO, services internes | **INCONNU** | INCONNU | INCONNU | **0 $ à vie**, puis 29/99/299 $ par mois **et par entreprise** | site éditeur + App Store |
| **openMAINT** | **PAT srl**, groupe **Zucchetti**, Italie, VAT IT 02378410266 | — | INCONNU | GMAO, services internes | INCONNU | INCONNU | INCONNU | Auto-hébergé libre ; **mobile et support payants**, prix non affichés | site éditeur |

**Non instruits, traités en bloc** : les 26 autres éditeurs listés au § 2. Ce
sont, pour la plupart apparente, de très petites structures ; **aucun compte n'a
été consulté pour eux** et leur CA est `INCONNU`. Arbitrage assumé de
l'utilisateur : un éditeur à un ou deux comptes publiés ne justifie pas une
requête chacun. Cette non-exhaustivité est une limite réelle du § 3.

Offre gratuite détectée : **OUI, mais aucune n'est complète.** Détail et
raisonnement au § 4.

Levées de fonds : **AUCUNE TROUVÉE.** Deux opérations capitalistiques
identifiées, qui n'en sont pas :

- **Praxedo / MBO+ (ex-MBO & Co)**, opération du **15/03/2022**, entrée d'un
  fonds **minoritaire**. Montant `INCONNU`. La fiche annuaire-startups.pro
  indique explicitement « Praxedo n'a réalisé aucune levée de fonds », total
  financements 0 €.
- **Nomadia Group / NEREUS TOPCO** (SIREN 953661816), président de la holding ;
  BSH (878114388) en directeur général délégué. Structure de LBO.

Conformément à l'arbitrage du 30/07/2026 inscrit au § 2 de `CLAUDE.md`, un
MBO/LBO est un **changement d'actionnariat**, pas une levée : l'argent va aux
actionnaires sortants et endette souvent la cible, au lieu de financer du
commercial et du marketing.

### Lecture du plafond de marché

Selon la grille de l'étape 3, le secteur correspond à la ligne **« Leader
5–30 M€, second < 3 M€ → cible idéale, marché prouvé mal desservi »** —
**mais seulement si l'on accepte le CA de presse de Praxedo**, et la condition
sur le second n'est pas remplie : Synchroteam publie 3 494 878 €, au-dessus des
3 M€.

Sur les seuls chiffres vérifiés sur pièces, le secteur relève plutôt de la ligne
**« Aucun compte publié, tous micro-entreprises → ambigu, creuser »** : le
leader dissimule ses comptes, deux éditeurs ne renseignent pas leur CA, et la
holding du consolidateur est en perte.

**Le fait structurel dominant n'est ni l'un ni l'autre : c'est la consolidation.**

### NOMADIA — le fait structurel du secteur

`NOMADIA GROUP` (884911116), holding créée le 06/07/2020, détenue par
`NEREUS TOPCO`. **Au moins dix filiales** identifiées dans l'Annuaire des
Entreprises : NOMADIA FIELD OPERATIONS (792037988), NOMADIA FIELD SALES
(341057024), NOMADIA SAAS SOLUTIONS (993230358), NOMADIA PROTECT (522997626),
NOMADIA DELIVERY (407566744), **SYNCHROTEAM** (430244749), WITH (382685436),
SMART SOURCE DEVELOPMENT (801819988), MOBILEDEV (823369509).

Chronologie des rachats (fusacq.com et cfnews.net, consultés le 30/07/2026) :

| Date | Opération |
|---|---|
| Printemps 2021 | Fusion de **Geoconcept**, **Danem** et **B&B Market** → naissance de Nomadia |
| 2023 | **Synchroteam** |
| 2024 | **Nomadvantage**, **Coredinate** (Allemagne, ouverture DACH) |
| Annoncé le 24/02/2025 | **7Opteam** (fondée 2013, 25 experts) et **Gazoleen** / Smart Source Development |

**Gazoleen est un acteur direct du segment cible** : gestion et optimisation des
interventions de maintenance en **chauffage et climatisation**, « plus de 1 000
entreprises clientes ». Rachetée il y a dix-sept mois.

**Deux des huit éditeurs de la famille A que vous vouliez instruire sont le même
groupe.** Un marché en consolidation active se lit autrement qu'un marché
fragmenté stable : la fragmentation observée à l'étape 2 est en train d'être
rachetée.

**Le CA consolidé du groupe est `INCONNU`.** Les 4 705 941 € sont les comptes
sociaux de la holding — des honoraires de gestion, pas l'activité du groupe. Ne
jamais présenter ce chiffre comme le chiffre d'affaires de Nomadia.

## 3. Défauts documentés

Corpus : **4 avis** lus intégralement — détail dans `GMAO_MAINTENANCE_avis.md`.

**Le corpus est inférieur à 30. C'est écrit explicitement, comme le protocole
l'exige, et la recherche primaire est devenue la source principale.**

Répartition : **0** Trustpilot / **4** stores (App Store uniquement) /
**0** Reddit-forums / **0** Capterra-G2 (volontairement non dépouillés).

| Catégorie | Occurrences (sources fortes) | Occurrences (sources faibles) | Éditeur(s) visé(s) |
|---|---|---|---|
| `mobile/terrain` | **1** | 0 | Praxedo |
| `bug/fiabilité` | **1** | 0 | Praxedo |
| `ergonomie` | **1** | 0 | Praxedo |
| `fonctionnalité manquante` | **1** | 0 | Praxedo |
| `prix caché` | **0 en avis** — mais constaté sur pièces chez Bob! Desk et Praxedo (§ 4) | 0 | Bob! Desk, Praxedo |
| toutes autres catégories | **0** | 0 | — |

Écart de notation détecté : **INCONNU**, et non « aucun ». La comparaison exige
des données des deux côtés ; il n'existe aucune source forte suffisante à
opposer aux 4,63/5 et 4,75/5 des comparateurs français. Ces notes ne sont pas
publiées comme information, leur poids étant nul.

Thèmes dominants : **aucun ne peut être établi.** Avec une occurrence par
catégorie, il n'y a pas de thème, il y a des anecdotes. Le seul reproche
techniquement intéressant — **le mode déconnecté qui ne couvre pas les zones
blanches** — apparaît **une seule fois** et ne fonde qu'une hypothèse à tester.

### Ce que l'absence de corpus signifie

Quatre sources fortes ont été épuisées :

- **Trustpilot** : aucune fiche n'existe pour aucun des éditeurs testés.
- **Google Play** : page rendue côté client, **illisible par fetch**, deux
  locales tentées.
- **App Store** : 918 avis annoncés chez Praxedo, **4 exposés**, aucune
  pagination.
- **Reddit et forums métier** : **aucun résultat**, aucune discussion de pairs.

Le logiciel métier B2B français a peu d'avis — le protocole l'annonce. Ici, il
n'en a **presque aucun**, et une part du volume existant est **annoncée mais
illisible**. Ce n'est pas un défaut de la recherche, c'est l'état du marché.

## 4. Contraintes réglementaires

| Obligation | Texte | Date d'entrée en vigueur | Qui est concerné |
|---|---|---|---|
| **Réception** de factures électroniques obligatoire | Réforme de la facturation électronique | **01/09/2026** | **Toutes les entreprises, quelle que soit leur taille** |
| **Émission** de factures électroniques | idem | **01/09/2026** | Grandes entreprises et ETI |
| **Émission** de factures électroniques | idem | **01/09/2027** | **PME et micro-entreprises** — soit la quasi-totalité des 10 348 cibles |

Source : `https://www.economie.gouv.fr/tout-savoir-sur-la-facturation-electronique-pour-les-entreprises`
et `https://www.impots.gouv.fr/facturation-electronique-qu-est-ce-que-ca-change-pour-moi`,
consultés le 30/07/2026.

**Le logiciel métier est-il certifié/agréé par l'État ? NON.**

Preuve : la réforme impose de passer par une **Plateforme de Dématérialisation
Partenaire**, et ce sont **les PDP** qui sont **immatriculées par la Direction
générale des Finances publiques** — plus de 70 le sont déjà. Un logiciel de
gestion métier n'est pas immatriculé : il **se connecte** à une PDP. La
contrainte est une contrainte d'intégration, pas une barrière d'agrément.

C'est précisément parce que ce point pouvait être éliminatoire qu'il a été
vérifié séparément, avec les termes `immatriculé` et `agréé`.

**Retrait de `71.20B` — conséquence réglementaire.** Le code sorti du périmètre
était le seul porteur d'une accréditation d'État (COFRAC) susceptible de
toucher l'outil. Son retrait éloigne le risque d'éliminatoire n° 3 ; il n'a pas
été instruit plus avant, puisque hors périmètre.

**Non instruit** : les obligations propres aux métiers du froid et de la
climatisation (attestation de capacité, manipulation des fluides frigorigènes)
et le décret BACS. Ils touchent une partie des cibles et **n'ont pas été
recherchés** — l'étape 6 était désignée comme la première à couper. Porté au
§ 11.

## 5. Ligne de score (à recopier telle quelle dans SYNTHESE.md)

| Champ | Valeur | Barème |
|---|---|---|
| Entreprises cibles | **10 348** → **1** | <3k = éliminé, 3-15k = 1, 15-50k = 2, >50k = 3 |
| CA du leader | **28,3 M€ (2024), rapporté par la presse, non vérifié sur pièces** → **3** | <2M = 1, 5-30M = 3, >30M ou levée >5M = éliminé |
| Prix plancher constaté | **19 €/util./mois** (Organilog Pro) → **1** | gratuit = éliminé, <30€ = 1, 30-100€ = 2, >100€ = 3 |
| Occurrences du reproche dominant (sources fortes) | **1** → **1** | 0-2 = 1, 3-9 = 2, >=10 = 3 |
| Échéance réglementaire exploitable | **01/09/2027, soit 13 mois** → **3** | aucune = 0, >36 mois = 1, 12-36 mois = 3, <12 mois = 1 |
| Réutilisation du code de l'app BTP | **forte, 3 briques sur 7** → **3** | aucune = 0, partielle = 2, forte = 3 |
| Certification d'État sur le logiciel | **NON** → **0** | OUI = éliminé, NON = 0 |

**Score total : 12/18**

**Réserve sur la ligne « CA du leader ».** Le 3 repose sur un chiffre de presse
porté par **une seule** des six sources secondaires consultées. Sur les seules
pièces, le CA du leader est `INCONNU` et la ligne vaudrait `INCONNU`, pas 3. Le
score est donc **12/18 avec ce chiffre, et non calculable sans lui**.

**Détail de la réutilisation du code BTP** — 3 briques transposent directement :

| Brique de l'app BTP | Transposable ? | Motif |
|---|---|---|
| **Application terrain mobile hors-ligne** | **OUI** | Cœur du métier de prestataire itinérant. Le seul reproche technique du corpus porte exactement là |
| **Génération de documents et signature** | **OUI** | Rapport d'intervention signé par le client sur site |
| **Factur-X / facturation électronique** | **OUI** | Obligation au 01/09/2027 pour les PME, soit la quasi-totalité de la cible |
| Devis, chantiers, situations de travaux | **Partiel** | Devis et interventions oui ; « situations de travaux » est propre au BTP |
| Suivi documentaire de sous-traitants, vigilance rang 2+ | **Non établi** | Les sites industriels imposent des plans de prévention, mais la chaîne de vigilance rang 2+ n'a pas été vérifiée sur ce secteur |
| Corps de métier structurés (carrelage, couverture…) | **NON** | Nomenclature BTP, sans rapport avec la maintenance industrielle |

Le score ne décide pas. **Les éliminatoires décident — et aucun ne se déclenche.**

### Les quatre éliminatoires, un par un

1. **Volume < 3 000** → **NON**, 10 348 cibles.
2. **Offre gratuite complète et crédible chez un acteur établi** → **NON**, mais
   c'est l'appel le plus serré du dossier. Voir ci-dessous.
3. **Certification d'État sur le logiciel** → **NON**, ce sont les PDP qui sont
   immatriculées, pas les logiciels métier.
4. **Trois acteurs > 20 M€, levée > 5 M€, ou leader > 30 M€** → **NON** sur les
   éléments établis. Un seul acteur approche les 20 M€, et encore par la presse.
   Les deux opérations financières sont des changements d'actionnariat.

### L'éliminatoire n° 2, en détail, parce qu'il s'est joué de près

| Produit | Gratuit permanent ? | Périmètre réel | Éditeur établi ? | Déclenche ? |
|---|---|---|---|---|
| **Organilog Basique** | **OUI, 0 €** | **Archivage 72 heures**, fonctionnalités limitées, **aucun support** | **OUI** — ADALGO, créée 2014, 20 à 49 salariés, 216 k€ de résultat net | **NON** : un prestataire ne peut pas perdre ses rapports d'intervention au bout de trois jours. L'offre n'est pas *complète* |
| **FreeMaint** | **OUI, « à vie »** | Utilisateurs, actifs et bons de travail **illimités**, app Android, préventif temporel | **NON** — développeur individuel, app de moins d'un an, **0 avis**, anglais seul, publiée aux É.-U. | **NON** : l'offre est complète, l'acteur n'est pas établi |
| **Fabrico** | OUI | **1 utilisateur, 10 machines, 10 tâches** | non instruit | **NON** : palier de démonstration |
| **Bob! Desk** | **NON** | Essai **14 jours**, prix sur devis | oui | **NON** : ce n'est pas une offre gratuite |
| **openMAINT** | Auto-hébergé | **Mobile, support et mises à jour payants** | OUI (PAT srl / Zucchetti) | **NON** : sans mobile, inutilisable par un itinérant |
| **GLPI** | Open source | **ITSM et parc informatique** | OUI (Teclib') | **Hors périmètre** |

Aucune combinaison ne réunit les trois conditions. **Mais le gratuit existe
partout sous forme dégradée** : c'est un marché où la gratuité est un argument
d'acquisition permanent, ce qui pèse sur le plancher tarifaire — et le plancher
constaté, 19 €/utilisateur, ne vaut qu'un point sur trois.

## 6. Périmètre du MVP, si GO

**Non renseigné — le verdict n'est pas GO.**

Remplir cette section supposerait de connaître les défauts des produits en
place. Ils ne sont pas documentés : une occurrence par catégorie sur quatre
avis. Écrire une liste de fonctions V1 ici reviendrait à inventer une douleur
client, exactement ce que le protocole interdit.

Cette section sera remplie **après** le test à 48 h du § 9, s'il valide
l'hypothèse.

## 7. Fenêtre de lancement

Calcul à rebours depuis l'échéance réglementaire la plus proche qui soit
exploitable — l'obligation d'**émission** pour les PME.

| Jalon | Date |
|---|---|
| Échéance réglementaire | **01/09/2027** |
| Pic d'achat estimé (échéance − 6 mois) | **01/03/2027** |
| Mise en ligne cible (échéance − 12 mois) | **01/09/2026** |
| Début du développement (mise en ligne − charge V1) | **INCONNU** — la charge V1 n'est pas estimable tant que le § 6 n'est pas rempli |

**La mise en ligne cible est dans un mois.** Elle est donc hors d'atteinte : le
périmètre V1 n'est pas défini, et il n'existe aucune ligne de code.

**Conséquence à écrire franchement : sur le cycle de l'obligation d'émission de
septembre 2027, ce secteur est déjà en retard.** Le pic d'achat de mars 2027
reste théoriquement atteignable, mais avec une mise en ligne postérieure à la
cible, donc face à des concurrents déjà installés sur le sujet.

L'échéance du **01/09/2026 — réception obligatoire pour toutes les entreprises**
est, elle, à un mois : totalement hors d'atteinte, et déjà couverte par le
marché.

## 8. Distribution

**Non renseigné — le verdict n'est pas GO.**

Aucun canal n'a été instruit dans cette session : l'étape 6 devait être coupée
en priorité et l'étape 5 a consommé le budget de recherche sans rien rendre.
Nommer ici des fédérations ou des salons sans les avoir vérifiés produirait
exactement le type de contenu que le protocole interdit.

Pistes **non vérifiées**, à instruire si le test à 48 h est concluant : les
organisations professionnelles de la maintenance industrielle et du génie
climatique, et les prescripteurs comptables — la contrainte Factur-X passe par
l'expert-comptable. **Aucune n'a été nommée ni contrôlée.**

Prix de lancement proposé : **non renseigné**, pour la même raison. Repère
constaté : plancher payant crédible à **19 €/utilisateur/mois**, prix d'entrée
réel du leader à **175 €/mois** pour 5 utilisateurs.

## 9. Le test à 48 h

Le corpus d'avis est vide. La seule chose qui manque pour décider n'est pas une
donnée de marché, c'est **une douleur client vérifiée**. Le test doit donc aller
la chercher directement, et non produire une analyse de plus.

**Test** : ouvrir les essais gratuits de **Praxedo**, **Organilog** et
**Bob! Desk** — les trois sont accessibles sans engagement, Bob! Desk sur
14 jours — et exécuter sur chacun le même parcours minimal, chronométré :
créer une intervention, la réaliser depuis le mobile **en mode avion**,
faire signer un rapport, puis générer la facture au format Factur-X.
Documenter chaque friction et chaque échec.

**Résultat qui invalide** : si les trois produits réalisent le parcours complet
sans échec bloquant, **et** produisent une facture conforme à la réforme
française, alors il n'y a pas d'espace. **Abandon.**

**Résultat qui confirmerait** : au moins deux des trois échouent sur le mode
avion ou sur Factur-X. Ce sont les deux briques les plus directement
réutilisables de l'application BTP, et le seul reproche technique du corpus
porte exactement sur la première.

Coût : deux jours, zéro euro, aucune ligne de code.

## 10. Sources consultées

| URL | Nature | Éditeur du site | Conflit d'intérêt |
|---|---|---|---|
| `https://recherche-entreprises.api.gouv.fr/search` | API décomptes et comptes annuels | DINUM / ministère de l'Économie | **Aucun — source d'État** |
| `https://annuaire-entreprises.data.gouv.fr` | Annuaire officiel, fiches et recherche | DINUM | **Aucun — source d'État** |
| `https://www.economie.gouv.fr/tout-savoir-sur-la-facturation-electronique-pour-les-entreprises` | Réglementaire | Ministère de l'Économie | **Aucun — source d'État** |
| `https://www.impots.gouv.fr/facturation-electronique-qu-est-ce-que-ca-change-pour-moi` | Réglementaire | DGFiP | **Aucun — source d'État** |
| `https://apps.apple.com/fr/app/praxedo-2026/id1534566584` | Avis et changelog | Apple | **Aucun — source forte** |
| `https://apps.apple.com/us/app/freemaint-cmms-software/id6757958686` | Avis et changelog | Apple | **Aucun — source forte** |
| `https://www.societe.com/societe/praxedo-479788689.html` | Comptes anciens | Societe.com | Faible — modèle freemium, données récentes payantes |
| `https://www.cfnews.net/...Praxedo-intervient-aupres-d-un-fonds-minoritaire-396466` | Presse M&A | CFNEWS | Modéré — **93 % de l'article derrière un paywall** |
| `https://www.fusacq.com/buzz/7opteam-et-gazoleen-rejoignent-le-groupe-nomadia-a251900_fr_` | Annonce d'opération | Fusacq | Modéré — reprise de communiqué d'opération |
| `https://www.maddyness.com/2023/05/29/que-font-les-fonds-mbo/` | Portrait de fonds | Maddyness | **Élevé — portrait du fonds MBO+ lui-même** |
| `https://www.annuaire-startups.pro/praxedo/` | Fiche entreprise | annuaire-startups.pro | Modéré — agrégateur, déclare s'appuyer sur RCS/INSEE/RNE, **non recoupé** |
| `https://www.itespresso.fr/press-release/praxedo-annonce-un-chiffre-daffaires-2017-de-6-millions-deuros` | Communiqué | ITespresso | **Élevé — communiqué de Praxedo lui-même**, via Business Wire |
| `https://www.praxedo.fr/tarifs/` | Page tarifs | **Praxedo** | **Éditeur — juge et partie** |
| `https://fr.organilog.com/offre/` et `/mentions-legales/` | Tarifs et identité | **Organilog / ADALGO** | **Éditeur** |
| `https://bob-desk.fr/offres/`, `/mentions-legales/`, `/bob-desk-maintenance-management-software/` | Tarifs et identité | **Bob! Desk / BOB DEPANNAGE** | **Éditeur** |
| `https://freemaint.com/fr` | Page produit | **Freemaint LLC** | **Éditeur** |
| `https://www.fabrico.io/fr/pricing` | Tarifs | **Fabrico** | **Éditeur** |
| `https://www.openmaint.org/en/home` | Page produit | **PAT srl / Zucchetti** | **Éditeur** |
| `https://glpi-project.org/fr/` | Page produit | **Teclib'** | **Éditeur** |
| `https://www.yuman.io/` | Page produit | **Yuman** | **Éditeur** |

**Comparatifs volontairement écartés**, tous publiés par des éditeurs ou des
affiliés, et donc sans valeur sur leurs concurrents : Organilog, Bob! Desk,
Praxedo, InterFast, Divalto, Vertuoza, B2O, DOMMS, Alteva, appvizer,
lebonlogiciel, logiciels.pro, comparatif-logiciels.fr, lafabriquedunet,
100jourspourentreprendre, codeur.com, gmao.org, clientelec.

**Sources inaccessibles, à consigner** : `pappers.fr`, `verif.com`,
`infogreffe.fr` et `usinenouvelle.com` renvoient **HTTP 403** au robot.
`lesechos.fr` **bloque explicitement le crawler**. `play.google.com` est rendu
côté client et **illisible par fetch**.

## 11. Zones d'ombre

Par ordre décroissant d'impact sur la décision.

1. **Le CA réel de Praxedo.** Comptes confidentiels (`finances: null`), dernier
   chiffre sur pièces datant de 2014. Les 28,3 M€ de 2024 ne sont portés que par
   **une** source secondaire. C'est le chiffre dont dépend la ligne de score la
   plus lourde. **À vérifier** : commande d'un extrait de comptes annuels auprès
   du greffe, ou consultation manuelle de pappers depuis un navigateur.
2. **Le CA consolidé du groupe Nomadia.** `INCONNU`. Si le groupe dépasse 20 M€,
   la lecture concurrentielle change : deux acteurs significatifs au lieu d'un.
   **À vérifier** : comptes consolidés déposés par NEREUS TOPCO ou NOMADIA GROUP.
3. **La douleur client.** Aucune donnée publique. Le seul reproche technique
   apparaît une fois. **À vérifier** : le test à 48 h du § 9, puis des entretiens
   directs avec des responsables d'exploitation de sociétés de 10 à 50
   salariés en `33.12Z` et `33.20B`.
4. **Le taux d'équipement des 10 348 cibles.** Aucune donnée. Une entreprise de
   6 salariés en réparation de machines a-t-elle un logiciel, un tableur, ou
   rien ? La cible adressable réelle en dépend entièrement.
5. **Les obligations propres au froid et à la climatisation** (attestation de
   capacité, fluides frigorigènes) et le **décret BACS**. Non recherchés,
   l'étape 6 ayant été désignée comme coupable en priorité. Ils peuvent ouvrir
   une seconde fenêtre réglementaire, ou la fermer.
6. **La chaîne de vigilance rang 2+ de l'app BTP** est-elle transposable aux
   plans de prévention des sites industriels ? Si oui, la réutilisation passe de
   3 à 4 briques et l'angle d'entrée change.
7. **Les 26 éditeurs non instruits.** Aucun compte consulté. L'un d'eux peut
   être plus gros qu'il n'y paraît, ou déjà racheté par Nomadia.
8. **Les 918 avis App Store de Praxedo.** Ils existent et sont illisibles par
   cette voie. Un accès depuis un appareil iOS, ou via une API de store,
   donnerait le corpus qui manque à toute cette étude.
