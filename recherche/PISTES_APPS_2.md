# PISTES_APPS_2 — deuxième passe : artisans de service, commerce de bouche, réparation, professions réglementées

Session du **06/08/2026**. Recherche **par irritant**, pas par code NAF. Même
méthode que `recherche/PISTES_APPS.md` (session du 31/07/2026), sur **30 métiers
nouveaux**, aucun de ceux déjà traités.

Le protocole sectoriel (`PROMPT_RECHERCHE_SECTEUR.md`) reste **suspendu** pour
cette phase. Les règles de données du § 1 de `CLAUDE.md` s'appliquent
intégralement : aucun chiffre sans URL et sans date, `INCONNU` autorisé et
préférable à un proxy, 10000 n'est jamais un nombre.

---

## 0. Méthode, périmètre et limites — à lire avant les fiches

### Critères appliqués (identiques à la première passe)

**Restent éliminatoires :**
1. un logiciel **certifié, agréé, qualifié ou référencé par l'État** sur ce
   besoin précis ;
2. un **outil gratuit** fourni par l'État, une chambre consulaire ou un
   organisme financé par cotisation obligatoire, **sur ce besoin précis** ;
3. un **concurrent gratuit crédible et pérenne** d'un acteur établi.

**Ne sont pas éliminatoires :** la présence d'un gros éditeur (question
reformulée : *couvre-t-il CE besoin, ou seulement le métier en général ?*), et
un marché sous 3 000 entreprises.

**Seuil retenu :** 500 clients à 50 €/mois, soit **300 k€/an**. Chaque fiche
donne la **pénétration requise** = 500 ÷ population.

**Consigne du 06/08/2026 :** privilégier les irritants **transverses**. Le
fichier est en deux parties — transverses d'abord, mono-métier ensuite.

### Ce que cette passe a trouvé de nouveau, et qui change la lecture

**L'irritant le mieux prouvé de tout le corpus est le même dans cinq familles de
métiers : le document réglementaire à remettre au client avant la prestation.**
Quatre enquêtes indépendantes de la DGCCRF, sur quatre secteurs sans rapport
entre eux, mesurent le même échec :

| Secteur contrôlé | Année | Contrôlés | En anomalie | Taux |
|---|---|---:|---:|---:|
| Dépannage à domicile (plomberie, serrurerie, chauffage) | 2023 | 548 | 350 | **64 %** |
| Entretien et réparation automobile | 2024 | ~1 600 | ~640 | **~40 %** |
| Optique et audioprothèse (100 % santé) | 2023-2024 | 700+ | 514 | **72 %** |
| Prestations funéraires | 2017-2018 | `INCONNU` | `INCONNU` | **66 %** *(non vérifié, cf. § limites)* |

Sources et détail dans les fiches A1 et A2. **C'est une mesure d'État de la
non-conformité, pas une impression d'éditeur** — c'est la première fois dans ce
corpus qu'un irritant est établi par une source forte et chiffrée. La première
passe n'avait que des blogs d'éditeurs sur ses trois meilleures pistes.

**Ce que cela ne prouve pas, et qu'il faut écrire :** un taux d'anomalie mesure
que le professionnel *ne respecte pas* l'obligation. Il ne prouve pas qu'il en
*souffre*, ni qu'il paierait pour s'y conformer. Une partie des anomalies est
délibérée (la DGCCRF relève des prestations facturées non réalisées, du
dénigrement de l'offre 100 % santé). **Un fraudeur n'achète pas un outil de
conformité.** La part de non-conformité subie plutôt que choisie est `INCONNU`
et c'est la question à trancher en terrain.

### Quatre limites de cette session

1. **Reddit reste inaccessible à l'agent.** Vérifié le 06/08/2026 :
   `API Error: 400 The following domains are not accessible to our user agent:
   ['reddit.com']`. La source forte n° 3 du § 3 de `CLAUDE.md` est **absente de
   ce corpus**, comme dans la première passe. Les groupes Facebook ne sont pas
   récupérables sans authentification.
2. **Les forums métier testés sont fermés ou vides.** `apiculture-france.com`
   et `ruches-apiculture.com` ne rendent que leur page de connexion à l'agent
   (testé le 06/08/2026 sur deux fils précis). Aucun fil de forum métier n'a pu
   être lu intégralement dans cette session.
3. **`economie.gouv.fr` est inaccessible à l'agent.** Toutes les pages DGCCRF
   renvoient **HTTP 403** (protection Cloudflare : « Just a moment… Enable
   JavaScript and cookies to continue »), à la fois par l'outil de récupération
   de page et par `curl` avec en-tête de navigateur. **Conséquence directe :
   chaque fois qu'un chiffre DGCCRF n'a pas pu être vérifié sur un relais
   accessible, il est marqué `NON VÉRIFIÉ` et ne doit pas être publié ailleurs
   sans reprise.** C'est le cas du taux funéraire de 66 %. Les taux dépannage,
   automobile et 100 % santé ont, eux, été vérifiés sur des pages effectivement
   lues (DREETS, UFC-Que Choisir, éditeur identifié).
4. **La tranche `NN` est cette fois exploitable sur la majorité des codes.**
   Contrairement à la première passe, où `NN` plafonnait presque partout, elle
   rend ici une valeur réelle sur 27 des 40 codes testés (par exemple 75.00Z
   `NN` = 9 361, 47.22Z `NN` = 9 430, 96.01B `NN` = 8 459). Les populations de
   ces métiers sont donc connues **indépendants compris**, ce qui n'était pas le
   cas au 31/07/2026.

### Socle de population — décomptes NAF du 06/08/2026

API `recherche-entreprises.api.gouv.fr`, `etat_administratif=A`, **somme des
tranches `01`+`02`+`03`+`11`+`12` prises une par une** (jamais en liste — piège
documenté au § 5 de `CLAUDE.md`), plus la tranche `NN` relevée séparément.
Forme de la requête :
`https://recherche-entreprises.api.gouv.fr/search?activite_principale=[CODE]&etat_administratif=A&tranche_effectif_salarie=[T]&per_page=1`

| Code | Libellé court | Somme 01→12 (≥ 1 salarié) | Tranche `NN` |
|---|---|---:|---|
| 43.22A | Installation d'eau et de gaz | 14 913 | >10000 (PLAFOND) |
| 43.22B | Installation d'équipements thermiques et de clim. | 12 045 | >10000 (PLAFOND) |
| 43.32B | Menuiserie métallique et serrurerie | 7 306 | >10000 (PLAFOND) |
| 43.21A | Travaux d'installation électrique (bâtiments) | 21 237 *(minorant, tranche 01 plafonnée)* | >10000 (PLAFOND) |
| 43.29B | Autres travaux d'installation n.c.a. | 1 693 | 4 824 |
| 45.20A | Entretien et réparation de véhicules légers | 27 124 *(minorant, tranches 01 et 02 plafonnées)* | >10000 (PLAFOND) |
| 45.20B | Entretien et réparation d'autres véhicules | 1 303 | 1 913 |
| 45.40Z | Commerce et réparation de motocycles | 2 756 | 5 848 |
| 45.19Z | Commerce d'autres véhicules automobiles | 648 | 1 306 |
| 45.32Z | Commerce de détail d'équipements automobiles | 3 111 | 7 739 |
| 71.20A | Contrôle technique automobile | 4 132 | 2 290 |
| 71.20B | Analyses, essais et inspections techniques | 3 433 | >10000 (PLAFOND) |
| 66.21Z | Évaluation des risques et dommages | 483 | 1 718 |
| 47.78A | Commerce de détail d'optique | 9 160 | 5 625 |
| 47.74Z | Commerce de détail d'articles médicaux et orthopédiques | 3 081 | 3 400 |
| 96.02A | Coiffure | 23 301 *(minorant, tranches 01 et 02 plafonnées)* | >10000 (PLAFOND) |
| 75.00Z | Activités vétérinaires | 3 515 | 9 361 |
| 01.49Z | Élevage d'autres animaux (dont apiculture) | 834 | >10000 (PLAFOND) |
| 03.21Z | Aquaculture en mer | 1 335 | 2 444 |
| 03.22Z | Aquaculture en eau douce | 257 | 1 114 |
| 47.76Z | Commerce de détail de fleurs et plantes | 6 415 | >10000 (PLAFOND) |
| 10.71C | Boulangerie et boulangerie-pâtisserie | 21 322 | >10000 (PLAFOND) |
| 10.71D | Pâtisserie | 2 228 | 6 771 |
| 47.24Z | Commerce de détail de pain, pâtisserie, confiserie | 1 630 | 3 322 |
| 10.13A | Préparation industrielle de produits à base de viandes | 406 | 413 |
| 10.13B | Charcuterie | 1 441 | 1 517 |
| 47.22Z | Commerce de détail de viandes | 8 185 | 9 430 |
| 47.23Z | Commerce de détail de poissons et crustacés | 1 078 | 1 656 |
| 47.25Z | Commerce de détail de boissons | 3 156 | 5 875 |
| 47.29Z | Autres commerces de détail alimentaires spécialisés | 5 605 | 9 638 |
| 10.83Z | Transformation du thé et du café | 423 | 820 |
| 96.01B | Blanchisserie-teinturerie de détail | 2 335 | 8 459 |
| 95.23Z | Réparation de chaussures et articles en cuir | 682 | 2 397 |
| 47.77Z | Commerce de détail d'horlogerie et bijouterie | 2 424 | 3 552 |
| 95.25Z | Réparation d'articles d'horlogerie et bijouterie | 173 | 733 |
| 47.78C | Autres commerces de détail spécialisés divers | 8 718 | >10000 (PLAFOND) |
| 96.03Z | Services funéraires | 2 401 | 3 552 |
| 79.11Z | Activités des agences de voyage | 2 097 | 5 368 |
| 79.12Z | Activités des voyagistes | 589 | 1 982 |
| 49.42Z | Services de déménagement | 1 080 | 2 316 |

**Repris de la première passe** (requêtes du 31/07/2026, même méthode,
`recherche/PISTES_APPS.md` socle B) : 96.02B soins de beauté **9 966** ·
86.90E rééducation et podologues **5 569** · 01.62Z soutien à la production
animale **987** (`NN` = 6 319) · 47.79Z biens d'occasion **1 884** ·
85.53Z enseignement de la conduite **5 499** · 74.10Z design **3 794** ·
95.29Z réparation d'autres biens personnels **1 260**.

> **Rappel de la règle 10 du § 1 de `CLAUDE.md`** : ces décomptes sont une
> approximation de sens inconnu, pas un marché. Deux cas mesurés ici :
> **47.78C** (« autres commerces de détail spécialisés divers », 8 718) est
> trop hétérogène pour dimensionner les encadreurs et n'est utilisé nulle part
> comme population ; **45.20A** mélange mécanique générale et carrosserie sans
> permettre de les séparer.

### Registres officiels relevés (règle 10 : publier registre ET NAF)

- **Experts en automobile : « plus de 3 400 » inscrits sur la liste nationale**
  établie par le ministre chargé des transports —
  `https://tuning-auto.com/consulter-la-liste-nationale-des-experts-automobile-agrees-en-france/`,
  consulté le 06/08/2026. *Source secondaire, à reprendre sur la liste
  ministérielle elle-même.* Aucun code NAF ne les isole : 71.20B (3 433) et
  66.21Z (483) les contiennent mêlés à d'autres activités. **Écart NAF/registre :
  non mesurable en l'état.**
- **Maréchaux-ferrants : « environ 1 700 en activité, dont 1 500 chefs
  d'entreprise et 200 salariés »** —
  `https://www.lemondedesartisans.fr/actualites/marechal-ferrant-ce-metier-quel-pied`,
  consulté le 06/08/2026. NAF 01.62Z rend 987 (≥ 1 salarié) et 6 319 en `NN`,
  mais ce code contient aussi les autres activités de soutien à la production
  animale. **Le registre fait foi : ~1 700.**
- **Vétérinaires, opticiens, audioprothésistes, pédicures-podologues, auto-écoles,
  agences de voyage, opérateurs funéraires** disposent tous d'un registre, d'un
  ordre, d'une habilitation préfectorale ou d'une immatriculation. **Aucun n'a
  été dénombré dans cette session** — c'est un trou à combler, listé au § final.

### Deux gratuités établies, qui ferment des pistes d'un coup

- **Beekube — application d'apiculture « entièrement gratuite, pour un nombre
  illimité de ruches, toutes fonctionnalités professionnelles incluses »**,
  générant automatiquement le **registre d'élevage réglementaire** —
  `https://www.beekube.com/apiculture/guide-apiculture/outils-logiciels-apiculteurs/gerer-rucher-gratuitement-mobile/`
  et `https://www.beekube.com/a-propos-de-beekube.html`, consultés le 06/08/2026.
  → **Toute piste « registre d'élevage apicole » est morte** (éliminatoire n° 3).
- **Mobilio — « suite d'outils en ligne gratuite » pour déménageurs** : devis,
  **lettre de voiture**, factures d'acompte et de solde, calcul de volume,
  **déclaration de valeur**, en PDF avec les mentions légales —
  `https://www.mobilio.mobi/`, consulté le 06/08/2026 *(la page d'accueil ne rend
  que son titre à l'agent ; le périmètre ci-dessus vient de la description
  indexée, **non vérifiée par essai**)*.
  → **La piste « documents obligatoires du déménagement » est fermée**
  (éliminatoire n° 3), sous réserve de constater le périmètre réel.

---

# PARTIE A — PISTES TRANSVERSES

---

## A1. Le devis conforme de l'intervention technique : dépannage à domicile et réparation automobile

- **Métiers visés** — plombier-chauffagiste · serrurier · garagiste indépendant ·
  carrossier · mécanicien deux-roues. **Élargissement issu des recherches** :
  électricien, vitrier, couvreur-dépanneur (mêmes obligations, même enquête
  DGCCRF), centre de contrôle technique. Point commun : **un document normé doit
  être remis au client AVANT l'intervention, il engage le prix, et la même
  administration contrôle les cinq métiers avec la même grille.**

- **Population** — décomptes NAF du 06/08/2026 (socle ci-dessus), **minorants
  ≥ 1 salarié** :
  · Dépannage bâtiment : 43.22A **14 913** + 43.22B **12 045** + 43.32B **7 306**
  + 43.21A **21 237** *(minorant)* + 43.29B **1 693** = **57 194**.
  · Automobile : 45.20A **27 124** *(minorant)* + 45.20B **1 303** + 45.40Z
  **2 756** = **31 183**.
  · **Total minorant : 88 377.** Les tranches `NN` de six de ces huit codes sont
  **>10000 (PLAFOND)** : la population réelle est `INCONNU` et nettement
  supérieure.
  **Pénétration requise ≤ 0,57 %.** C'est la plus basse de tout le corpus, les
  deux passes confondues.

- **L'irritant** — *l'obligation existe, elle est précise, et la majorité des
  professionnels contrôlés ne la tient pas.*
  · **Dépannage à domicile, enquête DGCCRF 2023** : « Sur les 548 professionnels
  contrôlés par les enquêteurs CCRF, 350 ne respectaient pas la réglementation en
  vigueur, soit un **taux d'anomalie de 64 %** ». Manquements relevés :
  « l'information sur les prix et les conditions particulières de vente, avec des
  écarts importants entre les tarifs affichés et ceux réellement facturés », « le
  non-respect des obligations relatives à la vente hors établissement notamment
  le **non-respect du délai de rétractation** », « l'absence d'informations
  précontractuelles obligatoires ». Suites : « 163 avertissements, 231
  injonctions, 72 procès-verbaux administratifs […] ainsi qu'à 65 procès-verbaux
  pénaux ». —
  `https://pays-de-la-loire.dreets.gouv.fr/Depannage-a-domicile-gare-aux-arnaques`,
  consulté le 06/08/2026. **Page effectivement lue.**
  · Fondement : **arrêté du 24 janvier 2017** relatif à la publicité des prix des
  prestations de dépannage, réparation et entretien dans le secteur du bâtiment
  et de l'équipement de la maison, en vigueur au 1er avril 2017 —
  `https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000033935513`, consulté le
  06/08/2026.
  · **Réparation automobile, enquête DGCCRF 2024** : « près de 1 600
  établissements contrôlés », « près de 40 % […] ont fait l'objet de suites
  correctives ou répressives », « plus de 580 avertissements », « près de 500
  injonctions », « plus de 220 procès-verbaux ». Taux d'anomalie par thème :
  **information sur les pièces issues de l'économie circulaire 56 %**, prix et
  conditions particulières de vente 54 %, obligation générale d'information
  précontractuelle 53 %, garantie légale 48 %. L'enquête 2022 donnait « 30 % de
  suites correctives sur 1 400 établissements » — **+10 points en deux ans**. —
  `https://movalib.com/blog/enquete-dgccrf-reparation-automobile-points-vigilance-garagistes`,
  consulté le 06/08/2026.
  · Fondement : **loi du 8 octobre 2018** — obligation d'informer le
  consommateur, sur le devis remis avant travaux, de l'existence de pièces
  issues de l'économie circulaire, et de **consigner le refus du client dans le
  dossier de réparation** —
  `https://www.inc-conso.fr/content/1er-janvier-2017-entree-en-vigueur-du-decret-sur-les-pieces-de-reemploi-en-automobile`
  et `https://www.euro-conformite.com/point-legislatif-les-garagistes-ont-l-obligation-de-proposer-des-pieces-d-occasion-lors-d-une`,
  consultés le 06/08/2026.

- **Poids de la preuve** — **FORT sur le dépannage, MOYEN-FORT sur l'automobile.**
  Le chiffre du dépannage vient d'une **DREETS**, service déconcentré de l'État,
  page lue directement. Le chiffre automobile est relayé par **Movalib, éditeur
  d'un logiciel de gestion pour garages** (mentions légales vérifiées le
  06/08/2026 : « 17bis Rue du Haut de la Cruppe BAT 3, 59650 Villeneuve-d'Ascq ») —
  **conflit d'intérêt : il décrit le manque que son produit comble.** La source
  primaire `economie.gouv.fr` est inaccessible à l'agent (HTTP 403). Les taux
  détaillés par thème **doivent être repris sur la page DGCCRF** avant tout
  engagement.
  ⚠️ **Réserve de fond, valable pour toute la fiche** : un taux d'anomalie mesure
  la non-conformité, pas la douleur. La DGCCRF relève dans le même mouvement des
  fraudes délibérées — « des garagistes facturaient aux consommateurs des
  prestations de retrait et de remplacement de pièces détachées, alors qu'aucune
  manipulation de cette sorte n'avait été réalisée ». **La part subie de la
  non-conformité est `INCONNU`.**

- **Ce qu'ils utilisent aujourd'hui** — carnet à souches, devis Word, et pour la
  partie automobile des logiciels de facturation généralistes. Rien dans ces
  outils ne connaît l'arrêté de 2017 ni l'obligation « pièces de réemploi ».

- **Outils existants, et ce qui leur manque** — la brique *devis-facture* est
  saturée et partiellement gratuite (voir éliminatoires). Ce qu'aucun ne fait :
  le **bloc de conformité** — barème horaire et frais de déplacement affichés et
  horodatés, devis remis avant intervention y compris en urgence, **formulaire de
  rétractation et renonciation expresse en cas d'urgence** (vente hors
  établissement), **devis en deux versions pièce neuve / pièce de réemploi** avec
  **trace du refus du client**, archivage opposable pour le contrôle.

- **Prix et revenu** — 35 à 60 €/mois. **500 × 50 € = 300 k€/an** ; à 40 €/mois
  il faut **625 clients**, soit **0,71 %** de la base minorée.

- **Éliminatoires** —
  · **n° 1 NON déclenché.** Vérifié : l'**habilitation au SIV** est « une
  autorisation d'accès au SIV accordée par le préfet » portant sur le
  **professionnel** (un an d'activité minimum, casier vierge), pas sur le
  logiciel —
  `https://www.nord.gouv.fr/Demarches/Immatriculation-carte-grise/Habilitation-et-agrement-au-Systeme-d-Immatriculation-des-Vehicules-SIV`,
  consulté le 06/08/2026. Aucun agrément d'État sur le logiciel de devis.
  · **n° 2 DÉCLENCHÉ — contrôle exécuté le 06/08/2026, résultat défavorable.**
  Le balayage des 17 CMA de région annoncé comme réserve a été mené
  (`recherche/TEST_TERRAIN_P2A1.md` § 5 bis). **CMA France a retenu Abby à
  l'issue d'un marché public** pour distribuer, sous marque CMA, un outil de
  gestion dont l'offre **« Basique » est à 0 €/mois, sans engagement, sans carte
  bancaire, avec « devis et factures illimités »** et « facturation électronique
  conforme » — `https://www.cma-gestion.fr/` et
  `https://www.cma-martinique.com/facturation-electronique-martinique/`,
  consultés le 06/08/2026. La CMA affiche elle-même « Un conseiller CMA pour vous
  accompagner ». Une chambre consulaire est financée par la taxe pour frais de
  chambres de métiers : **c'est la deuxième forme de l'éliminatoire n° 2.**
  → **La brique « produire un devis et une facture » sort du périmètre d'A1**,
  exactement comme le registre RGPD en était sorti en première passe. Abby étant
  en outre une **plateforme agréée par l'État**, la brique « facturation
  électronique » est barrée une seconde fois par l'éliminatoire n° 1.
  **Ce qui reste : la seule couche de conformité** (barème affiché, devis avant
  intervention en urgence, rétractation et renonciation expresse, double devis
  pièce neuve / pièce de réemploi, traçabilité du refus, archivage opposable) —
  **`INCONNU` tant que les gratuits n'ont pas été essayés.**
  · **n° 3 NON déclenché sur le besoin précis, mais la brique adjacente est
  gratuite.** Sur le devis-facture nu, au moins trois offres gratuites existent :
  **Free Devis Factures** annonce un « module garagiste gratuit » incluant
  « véhicules, interventions, devis, factures et **ordres de réparation** »
  (`https://www.free-devis-factures.com/logiciel-de-devis-et-facturation-pour-garagiste-gerez-aussi-vos-vehicules-et-interventions-mecaniques/`),
  **Henrri** un logiciel de facturation gratuit pour garage
  (`https://www.henrri.com/facture-garagiste/`), **Synobat** une formule de
  départ gratuite limitée à « 3 devis de plomberie et 3 factures par mois »
  (`https://synobat.fr/logiciel-devis-facture-plombier`) — consultés le
  06/08/2026, **aucun essayé**. **Aucun ne traite la conformité réglementaire.**
  → Conséquence commerciale, à écrire noir sur blanc : **ce produit ne peut pas
  être vendu comme un outil de devis.** Il ne se vend que comme un outil de
  *conformité* — sinon il affronte trois gratuits.

- **Charge de développement, dev seul** — **10 à 14 semaines.** **Réutilisation
  de l'app BTP : forte (3/3).** Trois briques transposent directement — devis et
  situations, application terrain mobile hors-ligne, génération de documents et
  signature. Une quatrième, les corps de métier structurés
  (chauffage/climatisation, plomberie, électricité), est **déjà écrite pour ces
  métiers-là**. Piège vérifié sur TRANSPORT : contrôler vers **quoi** chaque
  brique transpose — ici, aucune n'atterrit dans une zone certifiée.

- **Verdict — À CREUSER, AMPUTÉE.** *(Verdict initial du 06/08/2026 : « À
  CREUSER, premier du fichier ». Révisé le même jour après exécution du contrôle
  CMA.)* La pénétration requise reste la meilleure du corpus (0,57 %) et
  l'irritant est mesuré par l'État sur deux familles indépendantes. Mais
  **l'éliminatoire n° 2 a emporté la brique devis-facture**, et il ne reste
  qu'une **couche de conformité posée sur un socle gratuit que la CMA pousse
  activement à tous les artisans de France**. **Trois réserves, dont une
  bloquante** : (1) l'essai réel des offres gratuites — deux heures, il décide
  seul de ce qu'il reste ; (2) la question de savoir si un artisan en anomalie
  *veut* se mettre en conformité ; (3) le contrôle DGCCRF non exécuté (403).
  **Ne pas engager les entretiens terrain avant la réserve (1).**

---

## A2. Le formulaire imposé par arrêté : le produire, le versionner, le prouver

- **Métiers visés** — opticien indépendant · audioprothésiste · pompes funèbres ·
  agence de voyage indépendante. Point commun : **le contenu et la présentation
  du document remis au client sont fixés par un arrêté ministériel, l'arrêté
  change, le document doit être archivé, et l'administration contrôle sa forme
  autant que son fond.** Ce n'est pas un devis : c'est un formulaire d'État à
  remplir.

- **Population** — décomptes NAF du 06/08/2026, **≥ 1 salarié** : 47.78A optique
  **9 160** (`NN` = 5 625) · 47.74Z articles médicaux et orthopédiques **3 081**
  (`NN` = 3 400) · 96.03Z services funéraires **2 401** (`NN` = 3 552) · 79.11Z
  agences de voyage **2 097** (`NN` = 5 368) · 79.12Z voyagistes **589**
  (`NN` = 1 982). **Total ≥ 1 salarié : 17 328** ; total tranches connues
  incluant `NN` : **37 255**.
  ⚠️ **47.74Z n'est pas le code des audioprothésistes** : il couvre l'ensemble du
  commerce d'articles médicaux et orthopédiques. Le nombre d'audioprothésistes
  est `INCONNU` — le registre ADELI n'a pas été interrogé.
  **Pénétration requise ≤ 2,89 %** sur la base ≥ 1 salarié, **≤ 1,34 %** sur la
  base incluant les `NN`.

- **L'irritant** — *quatre arrêtés, quatre formulaires, et des taux d'anomalie
  de 64 à 72 % sur la forme du document.*
  · **Optique et audioprothèse.** Devis normalisé obligatoire, **arrêté du
  28 avril 2017 modifié**, modèles définitifs par **arrêté du 29 août 2019**,
  en vigueur au **1er janvier 2020** — et l'obligation s'applique « que les aides
  auditives et produits d'optique correctrice soient remboursables ou non par la
  Sécurité sociale »
  (`https://www.audioinfos365.fr/6512-telechargez-le-devis-normalise-100-sante/`
  et `https://www.acuite.fr/actualite/legislation/166520/devis-normalise-en-optique-larrete-definitif-publie-au-journal-officiel`,
  consultés le 06/08/2026). Enquête DGCCRF : « Un peu plus de **700 magasins ont
  été visités** », « **514** d'entre eux présentaient au moins une anomalie, soit
  un taux d'établissements en non-conformité de **72 %** ». Manquements :
  « modifications ou mauvaise rédaction des devis normalisés », offre 100 %
  santé absente. Suites : « 384 avertissements, 123 injonctions de conformité,
  17 procès-verbaux administratifs, et 15 suites pénales » —
  `https://www.quechoisir.org/actualite-100-sante-opticiens-et-audioprothesistes-epingles-n102140/`,
  consulté le 06/08/2026. **Page effectivement lue.**
  ⚠️ Un autre chiffrage circule — « plus de 1 300 opticiens, audioprothésistes et
  chirurgiens-dentistes contrôlés, taux d'anomalie de 75 %, dont 79 % des
  opticiens et 70 % des audioprothésistes » — attribué à une page
  `economie.gouv.fr` **inaccessible à l'agent (HTTP 403)**. **NON VÉRIFIÉ. Ne pas
  l'utiliser.** Le périmètre diffère (dentistes inclus), ce qui explique peut-être
  l'écart, mais rien ne le prouve.
  · **Funéraire.** Modèle de devis fixé par **arrêté du 23 août 2010**, **modifié
  par l'arrêté du 11 février 2025, applicable au 1er juillet 2025**
  (`https://cremation-ffc.fr/modele-de-devis-larrete-du-11-fevrier-2025/`,
  consulté le 06/08/2026). L'obligation de dépôt est fixée par l'**article
  L. 2223-21-1 du CGCT** : dépôt « auprès des communes où elles sont implantées,
  ainsi qu'auprès des communes de plus de 5 000 habitants » du département du
  siège ou de l'établissement secondaire. **La phrase qui décrit l'irritant, telle
  qu'écrite par la presse professionnelle du secteur : « chaque modification
  tarifaire oblige à faire le tour de toutes les mairies pour renouveler le
  document ».** Sanction : article L. 2223-25, 1° du CGCT — le préfet peut
  prononcer « la suspension de l'habilitation pour une durée maximale d'un an, ou
  son retrait » —
  `https://www.resonance-funeraire.com/magazine/reglementation/5577-nouveau-point-sur-l-obligation-faite-aux-pompes-funebres-de-deposer-leurs-devis-types-en-mairie`,
  consulté le 06/08/2026. **Page effectivement lue.**
  Taux d'anomalie DGCCRF de **66 %** (enquête 2017-2018) et **> 68 %** :
  **NON VÉRIFIÉS**, attribués à deux pages `economie.gouv.fr` inaccessibles.
  **Le nombre de communes de plus de 5 000 habitants en France est `INCONNU`** —
  la donnée existe dans le répertoire statistique de la DGCL mais n'a pas été
  obtenue.
  · **Agences de voyage.** Information précontractuelle formalisée, transposition
  de la directive (UE) 2015/2302, en vigueur au 1er juillet 2018. Enquête DGCCRF
  2019 : « 364 établissements visités », « 201 établissements avaient des
  anomalies » — soit **55 %**. *Chiffre issu d'une page `economie.gouv.fr`
  inaccessible, **NON VÉRIFIÉ**.* Élément vérifiable : « l'information
  précontractuelle communiquée au consommateur fait partie intégrante du contrat
  et ne peut être modifiée sauf accord exprès des parties par écrit » —
  `https://www.inc-conso.fr/content/voyage-forfait-prestation-de-voyage-liee-quels-sont-vos-droits-et-recours`,
  consulté le 06/08/2026.

- **Poids de la preuve** — **FORT sur l'optique-audio** (UFC-Que Choisir,
  association de consommateurs indépendante des éditeurs, page lue). **MOYEN sur
  le funéraire** : l'obligation et la sanction sont établies sur une page lue, le
  taux d'anomalie ne l'est pas. **FAIBLE sur les agences de voyage** : aucun
  chiffre vérifié.

- **Ce qu'ils utilisent aujourd'hui** — le logiciel métier quand il existe
  (Carbone14 et Qontum côté funéraire), sinon un PDF rempli à la main et
  photocopié. Le dépôt en mairie se fait par courrier ou par déplacement.

- **Outils existants, et ce qui leur manque** — **Carbone14** (éditeur de Mâcon,
  SaaS, « prix sur demande ») automatise le dossier du défunt et l'envoi de la
  demande d'inhumation à la mairie du cimetière
  (`https://www.logiciels-carbone14.fr/`, consulté le 06/08/2026) — mais **rien
  n'indique qu'il gère le dépôt et le versionnage des devis-types dans toutes
  les communes de plus de 5 000 habitants du département**. Côté optique-audio,
  les logiciels métier sont d'abord des outils de **facturation SESAM-Vitale**
  (voir éliminatoire n° 1). Ce qui manque partout : **le suivi de version du
  formulaire quand l'arrêté change**, la preuve d'avoir remis le bon modèle à la
  bonne date, et la traçabilité du dépôt.

- **Prix et revenu** — 40 à 70 €/mois (l'enjeu est une habilitation
  préfectorale ou une sanction pénale). **500 × 50 € = 300 k€/an** ; à 60 €/mois
  il faut **417 clients**, soit **2,4 %** de la base ≥ 1 salarié.

- **Éliminatoires** —
  · **n° 1 : DÉCLENCHÉ sur la facturation optique-audio, PAS sur le devis
  normalisé.** Distinction établie et à ne pas confondre. Le **CNDA** agrée tout
  logiciel « dès lors que des données de facturation sont échangées entre 2
  logiciels », et l'éditeur « doit signer un protocole d'agrément avec le CNDA » —
  `https://www.areasante.fr/fr/faq-sesam-vitale/id-27-agrement-sesam-vitale`,
  consulté le 06/08/2026. Depuis le **1er janvier 2025**, le tiers payant sur la
  part AMO est réservé aux facturations sécurisées SESAM-Vitale
  (`https://www.areasante.fr/fr/normes-reglementation/sesam-vitale`, consulté le
  06/08/2026). **Conséquence : un produit qui facture est barré. Un produit qui
  ne fait que le devis normalisé ne l'est pas** — le devis s'impose y compris hors
  remboursement. C'est une lame étroite, et c'est la seule qui passe.
  · **n° 2 : PARTIELLEMENT DÉCLENCHÉ.** Les **modèles vierges sont fournis
  gratuitement par l'administration** (annexes des arrêtés, modèle funéraire
  relayé par l'AMF —
  `https://www.amf.asso.fr/documents-modele-devis-and8211-prestations-funeraires/11250`,
  consulté le 06/08/2026). **Le précédent CNIL de la première passe s'applique
  directement** : quand l'État distribue le formulaire, « produire le formulaire »
  sort du périmètre. **Ce qui reste vendable** : le remplissage assisté et
  contrôlé, le versionnage à chaque arrêté, l'archivage opposable, et le suivi des
  dépôts en mairie. **Ce qui ne l'est plus** : « nous vous fournissons le modèle ».
  · **n° 3 : NON déclenché.** Aucune offre gratuite crédible trouvée sur ce besoin
  chez un acteur établi, dans aucun des quatre métiers.

- **Charge de développement, dev seul** — **12 à 16 semaines.** **Réutilisation
  de l'app BTP : partielle (2/3)** — génération de documents et signature,
  archivage. Ni chantiers, ni corps de métier, ni Factur-X ne transposent.

- **Verdict — À CREUSER SOUS RÉSERVE.** L'obligation est indiscutable, la
  sanction est lourde (retrait d'habilitation dans le funéraire), et
  l'éliminatoire n° 1 laisse passer le devis normalisé. Mais **la moitié du
  besoin est déjà servie gratuitement par l'État sous forme de modèle**, et la
  population par métier est petite : le produit n'existe que s'il couvre les
  quatre métiers, ce qui est une promesse difficile à tenir avec un formulaire
  différent par arrêté.

---

## A3. Le bien confié au professionnel : preuve d'état, réserves, abandon

- **Métiers visés** — pressing · cordonnier · horloger-bijoutier · encadreur ·
  garagiste et carrossier · réparateur deux-roues. **Élargissement** : réparateur
  d'électroménager, gardiennage de véhicules. Point commun : **le professionnel
  est dépositaire du bien d'autrui, il est présumé responsable de sa perte ou de
  sa dégradation, et c'est à lui de prouver qu'il n'a pas fauté.**

- **Population** — décomptes NAF du 06/08/2026, **≥ 1 salarié** (`NN` entre
  parenthèses) : 96.01B pressing **2 335** (8 459) · 95.23Z cordonnerie **682**
  (2 397) · 47.77Z horlogerie-bijouterie **2 424** (3 552) · 95.25Z réparation
  d'horlogerie **173** (733) · 45.20A **27 124** *(minorant)* · 45.40Z **2 756**
  (5 848). **Total ≥ 1 salarié : 35 494** *(minorant)*.
  **Les encadreurs ne sont pas dimensionnables** : 47.78C (8 718) est un code
  fourre-tout — population **`INCONNU`**, non incluse dans le total.
  **Pénétration requise ≤ 1,41 %.**

- **L'irritant** — *l'obligation de preuve pèse entièrement sur le professionnel,
  et elle est tenue sur un ticket papier.* Établi sur la fiche de l'**Institut
  national de la consommation** (source publique), consultée le 06/08/2026 —
  `https://www.inc-conso.fr/content/les-teinturiers-et-pressings` :
  · Le ticket de dépôt doit porter, au titre de l'**arrêté du 27 mars 1987** :
  raison sociale, date de remise, nombre et nature des objets, qualité du service,
  prix de chaque prestation, **réserves éventuelles émises par le prestataire**,
  **valeur d'achat des articles confiés**, existence du constat amiable.
  · Le professionnel doit « conserver les objets qui ont été laissés chez lui
  **pendant un an** à compter du dépôt, **nonobstant toute clause contraire** »
  (loi du 31 décembre 1903, modifiée par la loi n° 2016-816 du 20 juin 2016) ;
  au-delà, vente aux enchères, produit consigné à la Caisse des dépôts.
  · « La perte d'un vêtement est **supposée** lorsque l'article n'a pas été rendu
  dans le délai de **deux mois** à compter de la remise. »
  · Le professionnel est « **présumé responsable** » de la perte, sauf à prouver
  « qu'il n'a commis aucune faute et que cette perte est due à une cause
  étrangère qu'il ne pouvait prévoir ».
  · Côté automobile, le même mécanisme se retrouve : « les rayures, bosses,
  kilométrage, niveau de carburant et équipements non documentés à l'entrée
  deviennent des litiges à la sortie » —
  `https://iziscar.com/atelier-pro-checklists-etats-des-lieux-vehicule/`,
  consulté le 06/08/2026 *(source éditeur)*.

- **Poids de la preuve** — **MOYEN, et c'est la faiblesse de la fiche.**
  L'obligation juridique est établie par une source publique de premier ordre
  (INC) et par des textes datés. **Mais aucune source ne mesure ce que ces
  litiges coûtent aux professionnels** — pas de statistique de contentieux, pas
  de témoignage de pro en source forte, aucun forum métier lisible. Les autres
  sources disponibles sont des sites d'aide au consommateur en litige
  (`litige.fr`, `defendstesdroits.fr`) : **ils décrivent le droit du client, pas
  la souffrance du professionnel.** C'est exactement la faiblesse qu'avait A3
  dans la première passe.

- **Ce qu'ils utilisent aujourd'hui** — carnet à souches, étiquette agrafée,
  photo prise au téléphone et jamais rattachée au dossier.

- **Outils existants, et ce qui leur manque** — le marché est **vertical et
  cloisonné**, ce qui est précisément l'ouverture :
  · Pressing : **Xinaya**, **WOSH**, **EasyPressing**, **Gesticlean**,
  **Askpressing** — tarifs « à partir d'environ 59 €/mois »
  (`https://www.guidecaisseenregistreuse.com/logiciel-de-caisse-pressing/`,
  consulté le 06/08/2026 — *comparateur, poids nul au sens du § 3 de
  `CLAUDE.md`*). Ce sont d'abord des **logiciels de caisse**.
  · Automobile et location : **WeProov**, **Myrentpad**, **Sarool**
  (« preuve opposable pour vos véhicules », `https://sarool.app/`), **Auto
  Proof 24** — états des lieux photo horodatés et signés, consultés le
  06/08/2026.
  · Cordonnerie, horlogerie, encadrement : **rien de spécifique n'a été trouvé.**
  · **Ce qui manque : un outil du dépôt lui-même**, indépendant du métier — ticket
  conforme à l'arrêté de 1987, photos horodatées à l'entrée, réserves écrites,
  valeur déclarée, **compteur des deux mois et de l'an**, relance automatique de
  l'abandon, dossier de preuve exportable. Aucun des outils ci-dessus ne suit les
  **délais légaux d'abandon**.

- **Prix et revenu** — 25 à 40 €/mois (ticket faible, métiers à petite marge).
  **500 × 50 € = 300 k€/an** ; à 30 €/mois il faut **833 clients**, soit **2,3 %**
  de la base minorée. **C'est le point faible économique de la fiche.**

- **Éliminatoires** — n° 1 **NON** · n° 2 **NON** · **n° 3 DÉCLENCHÉ sur la
  branche déménagement uniquement** (Mobilio, voir § 0), qui sort donc du
  périmètre. Sur les branches retenues, aucune gratuité trouvée.

- **Charge de développement, dev seul** — **8 à 12 semaines.** **Réutilisation de
  l'app BTP : partielle (2/3)** — application terrain mobile hors-ligne, photos,
  génération de documents et signature.

- **Verdict — À CREUSER SOUS RÉSERVE EXPRESSE.** La mécanique juridique est
  réellement commune à six métiers que personne ne sert ensemble, les délais
  légaux (2 mois, 1 an) sont un ressort produit que personne n'exploite, et les
  trois éliminatoires sont francs. **Mais l'irritant n'est pas prouvé côté
  professionnel, et le prix soutenable est bas.** À confirmer par entretiens
  avant tout engagement — comme A3 de la première passe, et pour la même raison.

---

## A4. L'entretien périodique obligatoire et son attestation

- **Métiers visés** — plombier-chauffagiste · frigoriste et installateur de
  climatisation ou de pompe à chaleur · ramoneur. Point commun : **une
  intervention légalement périodique, une attestation à remettre au client dans
  un délai, et une déclaration annuelle agrégée à une administration.**

- **Population** — 43.22B installation d'équipements thermiques et de
  climatisation **12 045** (`NN` >10000 PLAFOND) + 43.29B autres travaux
  d'installation **1 693** (`NN` = 4 824), décomptes du 06/08/2026.
  **Total minorant : 13 738.** Le nombre d'opérateurs titulaires de
  l'**attestation de capacité fluides frigorigènes** est publié en open data par
  l'ADEME — jeu « REP-GF – Liste des opérateurs attestés »,
  `https://data.ademe.fr/datasets/operateur-atteste-gf` — **mais il n'a pas été
  dénombré dans cette session : `INCONNU`.**
  **Pénétration requise ≤ 3,64 %** sur la base minorante.

- **L'irritant** — *chaque intervention sur un fluide frigorigène produit un
  document CERFA, et l'ensemble doit être agrégé une fois par an pour une
  déclaration.* « À chaque intervention, le technicien doit remplir une fiche
  d'intervention détaillée dans laquelle est spécifié la quantité de fluide
  neufs, récupérés, réintroduits », au format **CERFA 15497*04** ; une
  **déclaration annuelle** regroupe « tous les mouvements de fluides » et
  s'effectue « directement auprès de l'ADEME dans le portail internet
  **SYDEREP** » — `https://globaletech.fr/attestation-de-capacite-fluides-frigorigenes/`,
  consulté le 06/08/2026. L'attestation de capacité est elle-même encadrée par
  l'**arrêté du 21 novembre 2025** relatif à la délivrance des attestations de
  capacité aux opérateurs (article R. 543-99 du code de l'environnement) —
  `https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000052993429`, consulté le
  06/08/2026.

- **Poids de la preuve** — **FAIBLE.** L'obligation est établie (Légifrance,
  organismes certificateurs), mais **la source qui décrit la charge est un
  organisme de formation à l'attestation de capacité** — il vend ce qu'il décrit.
  **Aucune source ne montre qu'un frigoriste souffre de tenir ses fiches.** Deux
  points restent `INCONNU` et sont décisifs : le périmètre exact de l'obligation
  déclarative annuelle pour un **opérateur** (la source consultée l'attribue aux
  « distributeurs et producteurs »), et le nombre d'opérateurs attestés.

- **Ce qu'ils utilisent aujourd'hui** — le CERFA papier en trois exemplaires, et
  un tableur en fin d'année.

- **Outils existants, et ce qui leur manque** — non instruits. **`INCONNU`.**

- **Prix et revenu** — non instruit.

- **Éliminatoires** — n° 1 : `INCONNU`, non instruit. **n° 2 : à instruire en
  priorité** — le portail **SYDEREP** est un outil d'État sur la déclaration
  annuelle ; s'il couvre aussi la fiche d'intervention, l'éliminatoire tombe.
  n° 3 : `INCONNU`.

- **Verdict — NON INSTRUIT, à reprendre.** La piste a la forme d'une bonne piste
  (obligation datée, document normé, déclaration périodique) mais **aucun de ses
  trois éliminatoires n'a été vérifié et l'irritant n'est pas prouvé**. Elle est
  publiée ici pour ne pas être perdue, pas pour être engagée. Conformément au
  § 0.3 de `CLAUDE.md`, ses éliminatoires sont **`INCONNU`, pas franchis**.

---

## A5. Le suivi de l'appareillage et du dossier de santé — **ÉCARTÉ**

- **Métiers visés** — audioprothésiste, opticien, pédicure-podologue.

- **L'irritant supposé** — le suivi de l'appareillage est une obligation
  professionnelle continue : « au moins 3 séances de contrôle la première année
  et 2 par an durant toute la vie de l'appareil », plus l'envoi du questionnaire
  « Évaluation R – partie 3 » à l'issue de la seconde année —
  `https://mon-centre-auditif.com/blog/rendez-vous-suivi-audioprothesiste` et
  `https://www.surdi.info/professionnels-sante-soins/l-audioprothesiste/la-prestation-de-suivi-de-l-audioprothesiste/`,
  consultés le 06/08/2026. Côté podologue, la fabrication d'un dispositif médical
  sur mesure impose une **déclaration à l'ANSM** avant première mise sur le
  marché et une traçabilité documentée (décret du 30 mai 2018, article 11) —
  `https://fnp-podologues.fr/reglementation-podologie/`, consulté le 06/08/2026.

- **Éliminatoires** — **n° 1 DÉCLENCHÉ.** Le logiciel métier de ces professions
  est indissociable de la facturation SESAM-Vitale, laquelle impose l'agrément
  **CNDA** (voir A2), et le tiers payant AMO y est réservé depuis le
  **1er janvier 2025**. Un outil de suivi qui ne facture pas ne remplace pas le
  logiciel métier : il s'y ajoute, et devient un second abonnement pour un
  praticien qui en paie déjà un.

- **Verdict — ÉCARTÉ.** Le besoin est réel mais il est structurellement
  **adjacent à un logiciel agréé** dont il ne peut pas prendre la place.
  **Le devis normalisé reste, lui, exploitable — il est traité en A2.**

---

## A6. Les registres réglementaires d'élevage et d'apiculture — **ÉCARTÉ**

- **Métiers visés** — apiculteur, pisciculteur, éleveur.

- **L'irritant** — réel : le registre d'élevage apicole est obligatoire « pour
  tous les apiculteurs qui vendent leur production », au titre de l'**arrêté du
  5 juin 2000**, doit contenir données sanitaires, zootechniques et médicales, et
  se conserve **5 ans** —
  `https://mouchamiel.fr/2025/08/01/registre-elevage-apiculture-obligation-2000/`
  et `https://www.snapiculture.com/registre-delevage/`, consultés le 06/08/2026.

- **Éliminatoires** — **n° 2 ET n° 3 DÉCLENCHÉS, tous les deux.**
  · n° 2 : la déclaration annuelle de ruches se fait sur **MesDémarches**,
  téléprocédure d'État, « strictement gratuite », avec récépissé immédiat —
  `https://mesdemarches.agriculture.gouv.fr/demarches/particulier/effectuer-une-declaration-55/article/declarer-des-ruches`,
  consulté le 06/08/2026.
  · n° 3 : **Beekube** est « entièrement gratuit pour un nombre illimité de
  ruches », génère automatiquement le registre d'élevage réglementaire, et
  annonce un support français gratuit (voir § 0).

- **Verdict — ÉCARTÉ.** L'État tient la déclaration, un acteur privé tient le
  registre, les deux gratuitement. **Populations de toute façon insuffisantes** :
  01.49Z **834** à ≥ 1 salarié, 03.21Z **1 335**, 03.22Z **257**.

---

## A7. La prise de rendez-vous et l'encaissement des métiers de la beauté — **ÉCARTÉ**

- **Métiers visés** — barbier, prothésiste ongulaire, coiffeur.

- **Population** — 96.02A coiffure **23 301** *(minorant, deux tranches
  plafonnées)* et 96.02B soins de beauté **9 966** (première passe). Base large.

- **Éliminatoires** — **n° 3 DÉCLENCHÉ par la première passe**, et confirmé ici
  par l'occupation du terrain. **Zen Agenda** annonçait une application « 100 %
  gratuite » incluant agenda, clients, facturation conforme et rappels SMS
  (`recherche/PISTES_APPS.md` § A4, 31/07/2026). Le segment payant est par
  ailleurs tenu par **Planity**, qui n'a « pas de formule gratuite durable pour
  un usage professionnel » et se situe autour de **94 à 114 €/mois HT** pour un
  salon solo — `https://www.lacaisseideale.fr/articles/planity-avis/`, consulté
  le 06/08/2026 *(éditeur d'un concurrent — conflit d'intérêt)*.
  Aucun irritant réglementaire distinct n'a été trouvé : la profession de
  prothésiste ongulaire « ne nécessite pas de diplôme spécifique » et son
  obligation se limite à la déclaration d'activité au guichet unique —
  `https://propulsebyca.fr/idees-business/prothesiste-ongulaire/reglementation-prothesiste-ongulaire`,
  consulté le 06/08/2026.

- **Verdict — ÉCARTÉ** : gratuité installée sur le besoin, et aucune obligation
  réglementaire spécifique sur laquelle bâtir autre chose.

---

# PARTIE B — PISTES MONO-MÉTIER

---

## B1. L'auto-école : le livret numérique et le calcul des places d'examen

- **Métier et population** — 85.53Z enseignement de la conduite, **5 499**
  entreprises actives à ≥ 1 salarié (première passe, 31/07/2026), tranche `NN`
  **>10000 (PLAFOND)**. **Pénétration requise ≤ 9,1 %** sur la base ≥ 1 salarié —
  élevé.

- **L'irritant** — *le livret d'apprentissage numérique est obligatoire, l'État
  ne fournit pas la solution, et les données saisies décident du nombre de places
  d'examen attribuées.* « Le livret numérique sera obligatoire à compter du
  **1er janvier 2024** » ; « les éditeurs de livret numérique auront l'obligation
  de transmettre certaines informations administratives et pédagogiques du livret
  à l'État » ; le livret « permettra la mise à jour automatique du seuil de
  formation des auto-écoles dans **RdvPermis** en fonction des heures de formation
  déclarées ». Conséquence chiffrée par la presse professionnelle : une école non
  labellisée réalisant 300 examens par an pourrait perdre « l'équivalent de 6 à
  10 places d'examen » face à une concurrente labellisée —
  `https://www.permismag.com/livret-numerique-les-auto-ecoles-non-labellisees-seront-penalisees/`,
  consulté le 06/08/2026. **Page effectivement lue.**

- **Poids de la preuve** — **MOYEN.** `permismag.com` est une publication
  professionnelle du secteur, pas un éditeur de logiciel : elle critique
  ouvertement la mesure (« sortie de nulle part »). Mais c'est une source unique,
  et **aucun témoignage direct d'exploitant n'a pu être lu**.

- **Ce qu'ils utilisent** — le logiciel de gestion d'auto-école, qui intègre
  désormais le livret.

- **Outils existants, et ce qui leur manque** — le marché est **déjà constitué et
  dense** : **Klaxo** (à partir de « 39 €/mois », livret numérique inclus sans
  surcoût, `https://klaxo.fr/prix-logiciel-auto-ecole/`), **AGX Informatique**,
  **Mounki**, **Drivup**, **Parcours Conduite**, **ENPC-Ediser**, **MyECF** pour
  le réseau ECF — consultés le 06/08/2026. **Il n'y a pas de trou.**

- **Prix et revenu** — 39 à 60 €/mois constatés chez le concurrent principal.

- **Éliminatoires** — n° 1 **NON déclenché en l'état, mais `INCONNU` sur le
  fond** : l'obligation faite aux éditeurs de transmettre des données à l'État
  suppose une convention ou une qualification technique dont **aucune liste
  publique n'a été trouvée** ; c'est le point à vérifier en premier, et il peut
  fermer la piste seul. n° 2 **NON déclenché** : « l'État ne proposera pas de
  solution de livret numérique »
  (`https://klaxo.fr/blog/le-livret-numerique-obligatoire-ce-qui-change-pour-les-auto-ecoles/`,
  consulté le 06/08/2026 — *source éditeur*). n° 3 **NON déclenché**.

- **Verdict — ÉCARTÉ.** Non pas sur un éliminatoire, mais sur l'arithmétique :
  **5 499 entreprises, 9,1 % de pénétration requise, et au moins sept éditeurs
  déjà installés dont un à 39 €/mois livret inclus.** L'obligation est arrivée en
  2024 : la fenêtre s'est refermée avant cette recherche.

---

## B2. L'architecte d'intérieur : la coordination des lots et le suivi de chantier

- **Métier et population** — 74.10Z activités spécialisées de design, **3 794**
  entreprises à ≥ 1 salarié (première passe), tranche `NN` **>10000 (PLAFOND)**.
  Le code couvre l'ensemble du design, pas seulement l'architecture d'intérieur :
  **population du métier `INCONNU`**. **Pénétration requise ≤ 13,2 %** sur la
  base ≥ 1 salarié — élevé, mais la base est fausse par construction.

- **L'irritant** — *le métier est en réalité un métier de chef de projet, et la
  gestion administrative en est le point aveugle.* « Le quotidien de l'architecte
  d'intérieur indépendant ressemble davantage à celui d'un chef de projet qu'à
  celui d'un créatif isolé, avec la gestion des clients, le suivi de chantier,
  les arbitrages budgétaires et la coordination des artisans » ; « la gestion
  administrative est un enjeu souvent **sous-estimé** par les architectes
  d'intérieur indépendants » —
  `https://www.devenirarchitecte.fr/actu-conseils/realite-du-metier-d-architecte-d-interieur-au-quotidien`,
  consulté le 06/08/2026. Honoraires de 8 à 15 % du montant des travaux : le
  suivi du budget travaux est directement le suivi de sa propre rémunération.

- **Poids de la preuve** — **FAIBLE.** `devenirarchitecte.fr` est un site
  d'orientation et de formation — il décrit le métier pour vendre une formation,
  pas pour rapporter une souffrance mesurée. **Aucune source forte.**

- **Ce qu'ils utilisent** — SketchUp, tableur, WhatsApp avec les artisans.

- **Outils existants, et ce qui leur manque** — **Batichiffrage** (chiffrage),
  **ArchiReport** (comptes rendus de chantier annotés, coordination des
  artisans), SketchUp Viewer / BIMx / Twinmotion côté maquette — consultés le
  06/08/2026 via la même source. **Le suivi de chantier est déjà outillé.**

- **Prix et revenu** — 40 à 60 €/mois plausible ; non instruit.

- **Éliminatoires** — n° 1 **NON** (l'architecte d'intérieur n'est pas une
  profession réglementée, contrairement à l'architecte). n° 2 et n° 3 :
  **`INCONNU`, non instruits.**

- **Verdict — ÉCARTÉ, à réexaminer.** Pas de preuve d'irritant sourcée en source
  acceptable, conformément à la consigne. **À réexaminer en priorité si la piste
  A1 est engagée** : c'est le même client final que le BTP, la même mécanique de
  lots et de situations de travaux, et donc la **réutilisation de code la plus
  directe de tout le corpus** — mais il faut d'abord prouver la douleur.

---

## B3. Le boucher-charcutier et le boulanger : traçabilité, origine et DLC — **ÉCARTÉ**

- **Métiers et population** — 47.22Z commerce de détail de viandes **8 185**
  (`NN` = 9 430) · 10.13B charcuterie **1 441** (1 517) · 10.71C boulangerie et
  boulangerie-pâtisserie **21 322** (`NN` >10000 PLAFOND) · 10.71D pâtisserie
  **2 228** (6 771) · 47.24Z détail pain et pâtisserie **1 630** (3 322).
  **Total ≥ 1 salarié : 34 806.** C'est **la plus grosse population du fichier**
  après A1.

- **L'irritant** — réel et daté : l'affichage de l'origine des viandes est
  obligatoire (règlement européen sur l'étiquetage de la viande bovine, en
  application depuis le **1er janvier 2002**), la traçabilité doit être documentée
  et les **documents conservés au minimum 5 ans**, sous peine de sanctions
  « de 1 500 € à 3 000 € par infraction, avec fermeture administrative possible
  en cas de récidive » —
  `https://bpifrance-creation.fr/activites-reglementees/boucher` et
  `https://www.economie.gouv.fr/dgccrf/tracabilite-de-la-viande-bovine`
  *(page DGCCRF non lue — 403)*, consultés le 06/08/2026.

- **Éliminatoires** — **n° 3 DÉCLENCHÉ, hérité de la première passe et non levé.**
  Le cœur du besoin (relevés de températures, PMS, DLC, plan HACCP) est occupé
  par **au moins trois applications gratuites** : HACCP Facile, Hygie HACCP et
  `app-haccp-gratuite.fr` (`recherche/PISTES_APPS.md` § A5, 31/07/2026).
  Sur la partie affichage d'origine, des **modèles PDF gratuits** circulent
  (`https://octopus-haccp.com/affichage-origine-des-viandes-pdf-gratuit/`,
  consulté le 06/08/2026) et **INTERBEV**, interprofession financée par
  cotisation volontaire étendue, référence gratuitement les professionnels dans
  ses outils (`https://www.interbev.fr/cahiers-des-charges/cahiers-des-charges-interprofessionnels/`,
  consulté le 06/08/2026) — **signal d'éliminatoire n° 2 à instruire.**
  Côté production, **Hello Harel** couvre recettes, lots et coût de revient à
  « 49 € à 199 €/mois » (`https://www.helloharel.com/agroalimentaire/boulanger/`,
  consulté le 06/08/2026) : **payant, donc pas un éliminatoire — mais le terrain
  est pris.**

- **Verdict — ÉCARTÉ** : gratuité installée sur l'hygiène et la traçabilité, la
  plus grosse population du fichier étant précisément celle où le besoin est déjà
  couvert à zéro euro. **C'est le contre-exemple à retenir : la taille du marché
  ne compense jamais un éliminatoire.**

---

## B4. Le fleuriste et les plateformes de transmission florale — **ÉCARTÉ**

- **Métier et population** — 47.76Z, **6 415** entreprises à ≥ 1 salarié
  (06/08/2026), tranche `NN` **>10000 (PLAFOND)**.

- **L'irritant supposé** — la commission prélevée par les réseaux de transmission
  florale (Interflora, Florajet) sur des commandes que le fleuriste exécute.
  Indice trouvé, formulé **par des clients et non par des fleuristes** : « les
  fleuristes peuvent faire un plus beau bouquet lorsqu'ils ne paient pas de
  commission à Interflora » —
  `https://ma-reclamation.fr/interflora/`, consulté le 06/08/2026.

- **Poids de la preuve** — **NUL.** Aucune source ne rapporte le point de vue du
  fleuriste. Le taux de commission est **`INCONNU`**. Les avis Trustpilot de
  Florajet (83 597 avis) sont des **avis de consommateurs sur la livraison**, pas
  de professionnels sur leur outil.

- **Verdict — ÉCARTÉ** : pas de preuve d'irritant sourcée, conformément à la
  consigne. Le sujet « désintermédiation d'un réseau à commission » est réel dans
  d'autres métiers et mérite d'être reposé, mais pas sur cette base.

---

## B5. L'horloger-bijoutier et le livre de police des métaux précieux — **ÉCARTÉ**

- **Métier et population** — 47.77Z **2 424** (`NN` = 3 552) · 95.25Z **173**
  (`NN` = 733), au 06/08/2026. **Total ≥ 1 salarié : 2 597.**

- **L'irritant** — obligation de déclaration d'existence auprès des douanes,
  poinçon de responsabilité, et **tenue d'un livre de police** assurant la
  traçabilité des métaux, « sous peine de sanction de 30 000 € d'amende » —
  `https://www.livre-de-police.com/activite/livre-de-police-bijouterie.html` et
  `https://registeo.fr/guide/bijoutier`, consultés le 06/08/2026.
  ⚠️ **Ces deux sources vendent le registre qu'elles décrivent.**

- **Éliminatoires** — n° 1 **NON** · n° 2 **NON** · n° 3 **NON**.

- **Verdict — ÉCARTÉ** pour la même raison que le brocanteur en première passe
  (`PISTES_APPS.md` § B7) : **marché trop étroit (2 597 à ≥ 1 salarié) et déjà
  servi par des spécialistes du livre de police** (Registeo,
  livre-de-police.com, registre.fr). L'obligation est réelle, la place est prise.

---

## B6. Les métiers écartés sur le seul dimensionnement

Instruits au décompte, arrêtés avant l'étape irritant faute de base suffisante
pour 500 clients. **Leurs éliminatoires sont `INCONNU`, pas franchis.**

| Métier | Code(s) | ≥ 1 salarié | `NN` | Pénétration requise | Motif |
|---|---|---:|---:|---:|---|
| Maréchal-ferrant | 01.62Z | 987 | 6 319 | **29 %** *(sur le registre : ~1 700)* | Registre professionnel à ~1 700 actifs — 500 clients = 29 % du métier |
| Pisciculteur | 03.21Z + 03.22Z | 1 592 | 3 558 | 31 % | Base insuffisante |
| Torréfacteur | 10.83Z | 423 | 820 | 118 % | Base insuffisante |
| Cordonnier | 95.23Z | 682 | 2 397 | 73 % | Base insuffisante seul ; rejoint A3 |
| Encadreur | 47.78C *(inexploitable)* | `INCONNU` | `INCONNU` | `INCONNU` | Non dimensionnable ; rejoint A3 |
| Expert automobile | 71.20B / 66.21Z *(non isolants)* | `INCONNU` | `INCONNU` | **14,7 %** *(sur le registre : ~3 400)* | Liste nationale à ~3 400 inscrits |
| Caviste | 47.25Z | 3 156 | 5 875 | 15,8 % | Base étroite **et** faux irritant : la DRM ne concerne pas les cavistes (voir ci-dessous) |
| Antiquaire | 47.79Z | 1 884 *(31/07/2026)* | — | 26,5 % | Déjà écarté en première passe (§ B7) |

> **Un faux irritant corrigé avant publication.** La déclaration récapitulative
> mensuelle (DRM) aux douanes, envisagée comme irritant du caviste, **ne le
> concerne pas** : « c'est le statut douanier du vin (droits suspendus) qui
> déclenche l'obligation, pas le métier. Les cavistes, grossistes et
> distributeurs qui achètent en droits acquittés ne sont pas concernés » —
> `https://www.wineriz.com/drm-vin-guide-complet-declaration-recapitulative-mensuelle/`,
> consulté le 06/08/2026. Et pour ceux qui y sont soumis, le dépôt se fait
> obligatoirement via **CIEL**, téléprocédure de la douane
> (`https://www.douane.gouv.fr/demarche/deposer-une-declaration-recapitulative-mensuelle-drm`,
> consulté le 06/08/2026) — **éliminatoire n° 2**.

---

## B7. Le vétérinaire libéral — **ÉCARTÉ, doublement**

- **Métier et population** — 75.00Z, **3 515** à ≥ 1 salarié et **9 361** en
  `NN` (06/08/2026), soit **12 876** unités connues. Base suffisante,
  pénétration requise **3,9 %**.

- **Éliminatoires** — **n° 1 ET n° 2 DÉCLENCHÉS.**
  · **n° 1 : qualification obligatoire du logiciel métier.** « Tous les éditeurs
  de logiciels de gestion des établissements vétérinaires doivent faire
  **qualifier** leur logiciel pour que les transmissions automatiques des données
  concernées démarrent dès le 14 mars 2023. » La liste des logiciels qualifiés
  est **publiée par le Conseil national de l'Ordre des vétérinaires** et compte
  au moins dix-sept produits (Argos, AssistoVet, Bourgelat, dr.veto, Epivet,
  GmVET, iVET, JVET, Koudou, Simax, Starvet, Tracivet, Vetdom, Veto-Win,
  Zoodiag…) — `https://www.epivet.com/calypso-faisons-le-point/`, consulté le
  06/08/2026. **C'est exactement l'éliminatoire n° 3 du protocole : un
  référencement d'État portant sur le logiciel métier lui-même.**
  · **n° 2 : outil gratuit d'un organisme à cotisation obligatoire.**
  **CalypsoVet** est « une application en ligne permettant les échanges de
  données entre vétérinaires, l'administration et les autres acteurs sanitaires »,
  mise en place par le **Conseil national de l'Ordre des vétérinaires**, soutenue
  par le **ministère de l'Agriculture** et le **Fonds pour la transformation de
  l'action publique**, accessible depuis le 14 mars 2023 —
  `https://www.veterinaire.fr/la-profession-veterinaire/calypso-la-plateforme-au-service-du-quotidien-des-veterinaires`,
  consulté le 06/08/2026. L'inscription à l'Ordre est obligatoire pour exercer :
  **c'est une cotisation obligatoire au sens du § 2 de `CLAUDE.md`.**

- **Verdict — ÉCARTÉ.** Le seul métier du fichier fermé **deux fois**, et par le
  contrôle le moins cher : deux requêtes ont suffi. Illustration directe du
  § 0.3 de `CLAUDE.md` — chercher d'abord là où ça ferme.

---

# CLASSEMENT PAR ATTRACTIVITÉ

## Retenues — À CREUSER

| Rang | Piste | Type | Population défendable | Pénétration pour 500 clients | Éliminatoires | Ce qui la porte / ce qui la fragilise |
|---|---|---|---|---|---|---|
| **1** | **A1 — Devis conforme de l'intervention technique** *(AMPUTÉE le 06/08/2026)* | Transverse (5 métiers demandés + 3 élargis) | **≥ 88 377** *(minorant)* | **≤ 0,57 %** | **n° 2 DÉCLENCHÉ sur la brique devis-facture** · n° 1 franchi · **n° 3 `INCONNU`** | Meilleure pénétration requise des deux passes · irritant **mesuré par l'État** sur deux familles indépendantes (64 % et ~40 % d'anomalie) · **réutilisation BTP forte (3/3)** · mais **CMA France distribue Abby gratuitement sous sa marque, choisi par marché public** : il ne reste qu'une couche de conformité sur un socle gratuit. **Son rang ne tient que si l'essai des gratuits confirme que la conformité n'y est pas** — deux heures de travail, non faites |
| **2** | **A2 — Le formulaire imposé par arrêté** | Transverse (4 métiers) | **17 328** *(≥ 1 salarié)* · 37 255 avec `NN` | **≤ 2,89 %** | **2 franchis**, n° 1 **contourné par la seule lame du devis normalisé**, n° 2 **partiellement déclenché** | Obligation opposable, sanction lourde (retrait d'habilitation funéraire), 72 % d'anomalie mesuré en optique-audio · mais l'État fournit le formulaire vierge, et le produit n'existe que s'il couvre quatre métiers aux arrêtés différents |
| **3** | **A3 — Le bien confié au professionnel** | Transverse (6 métiers) | **≥ 35 494** *(minorant)* | **≤ 1,41 %** | **3 franchis** | Mécanique juridique réellement commune (arrêté 1987, loi 1903, présomption de responsabilité), délais légaux 2 mois / 1 an qu'aucun outil ne suit, marché vertical et cloisonné · mais **irritant non prouvé côté professionnel** et prix soutenable bas (25-40 €/mois) |

## Non instruite

| Piste | État |
|---|---|
| **A4 — Entretien périodique et attestation (fluides frigorigènes)** | Forme prometteuse, **aucun éliminatoire vérifié**, irritant non prouvé. `INCONNU` sur les trois. À reprendre en commençant par SYDEREP (éliminatoire n° 2) |

## Écartées, et pourquoi

| Piste | Motif d'écartement |
|---|---|
| **B7 — Vétérinaire libéral** | Éliminatoires n° 1 **et** n° 2 : qualification obligatoire des logiciels par l'Ordre, et CalypsoVet gratuit financé par l'Ordre et le ministère |
| **A5 — Suivi d'appareillage santé (opticien, audio, podologue)** | Éliminatoire n° 1 : agrément CNDA sur la facturation SESAM-Vitale, tiers payant AMO réservé depuis le 01/01/2025. Le devis normalisé échappe seul, et part en A2 |
| **A6 — Registres d'élevage et apiculture** | Éliminatoires n° 2 **et** n° 3 : téléprocédure d'État gratuite pour la déclaration de ruches, Beekube gratuit et illimité pour le registre |
| **A7 — RDV et encaissement beauté (barbier, onglerie)** | Éliminatoire n° 3 hérité de la première passe (Zen Agenda), aucune obligation réglementaire distincte |
| **B3 — Boucher, charcutier, boulanger** | Éliminatoire n° 3 : trois applications HACCP gratuites ; signal d'éliminatoire n° 2 côté INTERBEV. **La plus grosse population du fichier, et le besoin y est gratuit** |
| **B1 — Auto-école** | Pas d'éliminatoire, mais 5 499 entreprises, 9,1 % de pénétration requise et sept éditeurs installés dont un à 39 €/mois livret inclus. Fenêtre refermée depuis 2024 |
| **B2 — Architecte d'intérieur** | Pas de preuve d'irritant sourcée. **À réexaminer en priorité si A1 est engagée** — réutilisation de code la plus directe du corpus |
| **B4 — Fleuriste** | Aucune source ne rapporte le point de vue du fleuriste ; taux de commission `INCONNU` |
| **B5 — Horloger-bijoutier** | Marché trop étroit (2 597 à ≥ 1 salarié) et livre de police déjà servi par trois spécialistes |
| **Déménageur** | Éliminatoire n° 3 : Mobilio annonce devis, lettre de voiture, factures, calcul de volume et déclaration de valeur **gratuits** |
| **B6 — Maréchal-ferrant, pisciculteur, torréfacteur, cordonnier, encadreur, expert automobile, caviste, antiquaire** | Dimensionnement insuffisant ou non établi. Le caviste porte en plus un **faux irritant corrigé** : la DRM ne le concerne pas |

## Les 30 métiers demandés — où chacun est traité

| Métier | Traité en | Sort |
|---|---|---|
| Plombier-chauffagiste | A1, A4 | **Retenu** (A1) |
| Serrurier | A1 | **Retenu** |
| Garagiste indépendant | A1, A3 | **Retenu** |
| Carrossier | A1, A3 | **Retenu** |
| Mécanicien deux-roues | A1, A3 | **Retenu** |
| Opticien indépendant | A2, A5 | **Retenu sur le devis normalisé** ; écarté sur le suivi |
| Audioprothésiste | A2, A5 | **Retenu sur le devis normalisé** ; écarté sur le suivi |
| Prothésiste ongulaire | A7 | Écarté |
| Barbier | A7 | Écarté |
| Pédicure-podologue | A5 | Écarté |
| Vétérinaire libéral | B7 | Écarté ×2 |
| Maréchal-ferrant | B6 | Écarté (dimensionnement) |
| Apiculteur | A6 | Écarté ×2 |
| Pisciculteur | A6, B6 | Écarté |
| Fleuriste | B4 | Écarté (preuve) |
| Boulanger-pâtissier | B3 | Écarté (gratuité) |
| Boucher-charcutier | B3 | Écarté (gratuité) |
| Caviste | B6 | Écarté (faux irritant + dimensionnement) |
| Torréfacteur | B6 | Écarté (dimensionnement) |
| Pressing | A3 | **Retenu** |
| Cordonnier | A3, B6 | **Retenu dans A3** ; écarté seul |
| Horloger-bijoutier | A3, B5 | **Retenu dans A3** ; écarté seul |
| Encadreur | A3, B6 | **Retenu dans A3** ; non dimensionnable seul |
| Antiquaire | B6 | Écarté (déjà traité en première passe) |
| Pompes funèbres | A2 | **Retenu** |
| Auto-école | B1 | Écarté (marché pris) |
| Agence de voyage indépendante | A2 | **Retenu** |
| Déménageur | A3, § 0 | Écarté (gratuité Mobilio) |
| Architecte d'intérieur | B2 | Écarté (preuve), à réexaminer |
| Expert automobile | B6 | Écarté (dimensionnement) |

**Élargissements retenus, apparus en cours de recherche** : électricien, vitrier
et couvreur-dépanneur (A1, mêmes obligations et même enquête DGCCRF) ; centre de
contrôle technique (A1) ; frigoriste et ramoneur (A4) ; réparateur
d'électroménager et gardiennage de véhicules (A3).

---

## Ce qui reste à faire avant d'engager quoi que ce soit

> **Les points 1, 2, 4 et 5 sont opérationnalisés dans
> `recherche/TEST_TERRAIN_P2A1.md`** — protocole de vérification primaire d'A1 en
> deux jours, avec ses seuils chiffrés fixés à l'avance. La question qu'il
> tranche est celle que ce fichier ne peut pas trancher : **parmi les artisans en
> anomalie, quelle part subit la non-conformité et quelle part la choisit ?**

1. ~~**Balayer les CMA régionales et départementales — pour A1 cette fois.**~~
   **FAIT le 06/08/2026, résultat défavorable** (`recherche/TEST_TERRAIN_P2A1.md`
   § 5 bis). 17 CMA de région sur 18 instruites — Mayotte et `artisanat.fr`
   restent `INCONNU`. **CMA France distribue Abby gratuitement sous marque CMA,
   après marché public** : éliminatoire n° 2 déclenché sur la brique
   devis-facture, retirée du périmètre d'A1.
   **Remplacé par la tâche qui décide maintenant : essayer réellement les quatre
   offres gratuites** (Abby, Free Devis Factures, Henrri, Synobat) et vérifier si
   l'une couvre la rétractation à 14 jours ou le double devis pièce neuve /
   pièce de réemploi. Deux heures, quatre comptes, aucune dépense. **Si oui, A1
   est morte. Ne pas lancer les entretiens terrain avant ce résultat.**
   *À noter pour toute piste future* : le réseau des CMA est désormais établi
   comme un **distributeur actif d'outils gratuits**, pas comme un émetteur de
   brochures. Toute piste dont le cœur est un document commercial d'artisan doit
   être testée contre CMA × Abby **en premier**.
2. **Reprendre les taux DGCCRF sur leurs pages primaires.** `economie.gouv.fr`
   est inaccessible à l'agent (HTTP 403, Cloudflare). Trois chiffres du fichier
   sont **NON VÉRIFIÉS** et ne doivent pas ressortir ailleurs en l'état : le
   66 % funéraire, le 55 % agences de voyage, et le chiffrage alternatif
   « 1 300 contrôlés / 75 % » du 100 % santé. Un navigateur humain suffit.
3. **Vérifier si les éditeurs de livret numérique auto-école sont conventionnés
   ou qualifiés par la DSR.** Cela ne change rien au verdict de B1 (écarté sur le
   marché), mais c'est le même mécanisme que la qualification Calypso : s'il
   existe, il faut le connaître avant de croiser une obligation d'État ailleurs.
4. **Constater par essai les gratuités déclarées.** Mobilio, Beekube, Free Devis
   Factures et Henrri ferment ou fragilisent quatre pistes sur la foi de leurs
   pages de présentation. Le § 2 de `CLAUDE.md` interdit explicitement de tenir
   une gratuité pour acquise sans en constater le périmètre réel.
5. **Prouver l'irritant en primaire sur A1 et A3.** Un taux d'anomalie n'est pas
   une intention d'achat. Cinq à dix entretiens par famille de métier
   trancheraient la question que ce fichier ne peut pas trancher : **la
   non-conformité est-elle subie ou choisie ?** Reddit et les groupes Facebook
   étant inaccessibles à l'agent, et les forums métier testés fermés, aucune
   requête supplémentaire n'y répondra.
6. **Dénombrer les registres professionnels laissés `INCONNU`** : opticiens et
   audioprothésistes (ADELI/RPPS), opérateurs funéraires habilités, agences de
   voyage immatriculées Atout France, opérateurs attestés fluides frigorigènes
   (jeu ADEME déjà identifié), et le nombre de communes de plus de 5 000
   habitants (répertoire statistique DGCL). Chacun remplace un décompte NAF
   approximatif par une cible commerciale exacte.
