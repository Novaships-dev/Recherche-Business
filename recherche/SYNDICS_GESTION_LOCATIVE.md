# SYNDICS / GESTION LOCATIVE

Recherche effectuée le : 30/07/2026
Requêtes effectuées : **47 requêtes web** (19 recherches + 28 récupérations de page),
**8 requêtes curl directes** (contournement de blocages, tests d'accessibilité),
**15 requêtes** à `recherche-entreprises.api.gouv.fr`.

## Verdict

**NO-GO** — le marché est refermé par deux consolidateurs sous LBO, dont le leader
dépasse 100 M€ de revenus ; un développeur solo n'y trouve pas de place.

Critère décisif : **éliminatoire n° 4 (concentration)**, mesuré à l'étape 3. Orisha
Real Estate a dépassé **100 M€ de revenus** au T1 2025 après absorption de Seiitra, et
**trois entités distinctes du secteur publient plus de 20 M€** de chiffre d'affaires.
Le seuil du protocole — « un leader à plus de 30 M€ » — est franchi d'un facteur
supérieur à trois.

Les trois autres éliminatoires sont **franchis** : le volume de cibles est largement
suffisant, aucune offre gratuite crédible ne vise le professionnel, et aucune
certification d'État ne pèse sur le logiciel. C'est bien la concentration, et elle
seule, qui ferme le secteur.

## 1. Dimensionnement

Codes NAF retenus : **68.32A, 68.32B**
Entreprises cibles (tranches 01–32, `etat_administratif=A`) : **4 743**
(source : `recherche-entreprises.api.gouv.fr`, relevé du 30/07/2026, repris de
`recherche/PREFILTRE_NAF.md` — non recompté dans cette session)

| Code | Libellé officiel NAF rév. 2 | Cible 01–32 | Actives, toutes tranches |
|---|---|---|---|
| 68.32A | Administration d'immeubles et autres biens immobiliers | 4 433 | >10000 (PLAFOND) |
| 68.32B | Supports juridiques de gestion de patrimoine immobilier | 310 | >10000 (PLAFOND) |
| | **TOTAL** | **4 743** | |

### Cible commerciale : la carte professionnelle, pas le NAF

Arbitrage de l'utilisateur du 30/07/2026 : **la carte professionnelle est la cible
commerciale, et l'éliminatoire n° 1 se rejoue sur elle.** Chiffres CCI France, qui
tient le fichier national des professionnels de l'immobilier depuis le 01/07/2015
(décret n° 2015-703 du 19 juin 2015) :

| Mention d'activité | 1.1.2024 | 1.1.2025 | 1.1.2026 |
|---|---|---|---|
| **Carte G — gestion immobilière** | 15 613 | 15 437 | **15 430** |
| **Carte S — syndic** | 5 229 | 5 088 | **5 061** |
| dont mention unique « S » | 473 | 462 | INCONNU |
| Carte T — transaction | 43 832 | 42 221 | 41 471 |
| **Total cartes en circulation** | INCONNU | INCONNU | **43 886** |

Sources, deux relevés indépendants qui concordent :
- 1.1.2024 et 1.1.2025 : tableau UNIS « Cartes professionnelles délivrées par les CCI »,
  données CCI France, republié le 30/01/2025 par CNACIM —
  `https://www.cnacim.immo/blog/statistiques-2025-cartes-professionnelles-immobilier-cci-france/`
  (le tableau est une image ; chiffres lus directement dans le fichier
  `https://www.cnacim.immo/wp-content/uploads/2025/01/cartes-cci-immobilier.jpg`),
  consulté le 30/07/2026.
- 1.1.2026 : Journal de l'Agence, « 5 chiffres clés sur le paysage des professionnels
  de l'immobilier en 2026 », source citée « Fichier national des professionnels de
  l'immobilier — CCI » —
  `https://www.journaldelagence.com/1410307-5-chiffres-cles-sur-les-professionnels-de-limmobilier-en-2026`,
  consulté le 30/07/2026.

Contrôle de cohérence : 15 437 (1.1.2025) → 15 430 (1.1.2026) et 5 088 → 5 061. Deux
sources, deux dates, même trajectoire de lent déclin. Cohérent.

**Éliminatoire n° 1 : franchi.** 15 430 titulaires d'une mention G, très au-dessus du
seuil de 3 000. Même la mention S seule (5 061) le franchit.

### L'écart NAF / carte G — l'inverse de ce qui était attendu

| Mesure | Valeur | Rapport au NAF |
|---|---|---|
| Cible NAF 68.32A + 68.32B, tranches 01–32 | 4 743 | référence |
| Mentions « gestion immobilière » (carte G) | 15 430 | **× 3,25** |
| Mentions « syndic » (carte S) | 5 061 | × 1,07 |

**Le NAF sous-compte la population carte G d'un facteur 3,25.** L'hypothèse de travail
annoncée avant la recherche — un NAF majorant, gonflé par des inscriptions sans besoin
logiciel — est **fausse sur ce métier**. Le NAF est ici un **minorant**.

Deux causes structurelles, toutes deux vérifiables :
1. **`68.31Z` (agences immobilières) est hors périmètre par arbitrage du 30/07/2026**,
   parce qu'il relève de la transaction. Or une agence qui fait de la transaction *et*
   de la gérance est classée en 68.31Z et détient les deux mentions T et G. Le
   croisement des chiffres CCI le montre : 41 471 mentions T pour 43 886 cartes, soit
   94 % des cartes portant la transaction — la gérance est très majoritairement une
   activité *seconde* d'une agence, pas l'activité principale d'un cabinet dédié.
2. **La cible exclut les tranches `NN` et `00`.** Un titulaire de carte G exerçant sans
   salarié en est sorti par construction.

Conséquence à retenir pour les autres secteurs : **l'écart NAF / réalité n'a pas de
signe prévisible.** Sur 68.32A les SCI gonflaient le décompte brut ; sur la carte G le
NAF le dégonfle. Le contrôle par une source métier indépendante n'est pas une
précaution, c'est une nécessité.

**Cible réaliste retenue : 15 430** (titulaires d'une mention G au 1.1.2026), avec
5 061 pour le sous-marché syndic de copropriété.

## 2. Éditeurs en place

Les deux métiers ne se vendent pas au même client et n'utilisent pas le même logiciel.
Trois familles, pas deux — la troisième n'est pas dans la cible mais pèse sur les prix.

| Éditeur / entité | Marque(s) | Métier servi | Créé en | CA (exercice) | Effectif | Prix d'entrée | Source du CA |
|---|---|---|---|---|---|---|---|
| **SEPTEO ADB (SPI)** — SIREN 412259715 | SPI Syndic, SPI Gestion Locative, SPI Transaction by Netty, SPI Location Saisonnière, INCH | **Syndic + gérance** + transaction | 1997 | **27 393 570 €** (2024) | 100–199 | 119 € HT/mois | [API](https://recherche-entreprises.api.gouv.fr/search?q=412259715) |
| **SEIITRA RESEAU** (groupe Orisha) — SIREN 383003423 | Thétrawin, Powimo | **Syndic** | 1991 | **21 436 821 €** (2023) | 100–199 | sur devis | [API](https://recherche-entreprises.api.gouv.fr/search?q=383003423) |
| **ORISHA TRANSACTION** (ex-Immofacile) — SIREN 478601826 | Immofacile | Transaction | 2004 | **27 394 485 €** (2020) | 50–99 | sur devis | [API](https://recherche-entreprises.api.gouv.fr/search?q=478601826) |
| **ORISHA PROPERTY MANAGEMENT** — SIREN 439737222 | Kolimmo, gestion locative | **Gérance + syndic** | 2001 | **11 302 722 €** (2023) | 50–99 | sur devis | [API](https://recherche-entreprises.api.gouv.fr/search?q=439737222) |
| **MUST INFORMATIQUE** (groupe Orisha) — SIREN 410321533 | Must | Gestion immobilière | 1997 | **8 911 321 €** (2024) | 50–99 | sur devis | [API](https://recherche-entreprises.api.gouv.fr/search?q=410321533) |
| **GERCOP DIGITAL** (MOJO.IMMO) — SIREN 802055111 | Y15 Syndic | **Syndic + gérance** | 2014 | **2 893 277 €** (2023) — **entité cessée** | 20–49 | sur devis | [API](https://recherche-entreprises.api.gouv.fr/search?q=802055111) |
| **VILOGI** — SIREN 528341571 | La Copropriété Digitale, La Gérance Mobile | **Syndic + gérance** | 2010 | **INCONNU** (`ca`=0 en 2024 ; résultat net 143 574 €) | 20–49 | sur devis | [API](https://recherche-entreprises.api.gouv.fr/search?q=528341571) |
| **UBLO** — SIREN 888056751 | Ublo | **Gérance** (bailleurs sociaux et privés) | 2020 | **INCONNU** (`ca`=0 en 2023 ; résultat net −316 165 €) | 20–49 | sur devis | [API](https://recherche-entreprises.api.gouv.fr/search?q=888056751) |
| **TIMCI** | Gimini, Syndi | **Syndic** | INCONNU | INCONNU | INCONNU | sur devis | — |
| Matera *(hors cible — voir ci-dessous)* | Matera | Copropriétés en direct | 2017 | INCONNU | INCONNU | sur devis | — |
| Copriciel *(segment bénévole)* | Copriciel | Syndic bénévole | INCONNU | INCONNU | INCONNU | 120 € TTC/an | — |
| MonSyndicBénévole *(segment bénévole)* | — | Syndic bénévole | INCONNU | INCONNU | INCONNU | 360 €/an (10 lots) | — |
| Diacamma *(segment bénévole)* | Diacamma | Syndic bénévole | INCONNU | INCONNU | INCONNU | **gratuit, open source, auto-hébergé** | — |

Éditeurs supplémentaires relevés au comparatif de presse IRC n° 648 (mai 2019), non
instruits financièrement faute de budget de requêtes : ADB Solution, H2I (Aramis),
Groupe Agile (AG.Syndic), Immonouveau (Comptacop), JLB Logiciels & Services (Coprolib),
Crypto, Dometech, Geasteam Services (Gesteam), ICS (Informatique Conseils Services),
Isis/Idealsoft (Immopen), Groupe Kel (Syndic360), Krier (Kristina), Dourlen Immobilier
(LOCKimmo), MoSoft (Ma copro en ligne), PartnerImmo, Actif Systèmes (Syco).
**21 éditeurs listés en 2019 ; six ans plus tard, la moitié au moins a été absorbée.**

**Offre gratuite détectée : NON sur la cible professionnelle.** Le seul gratuit réel est
**Diacamma**, open source et auto-hébergé, qui vise le **syndic bénévole** — pas le
titulaire de carte G ou S. Le comparatif Coprolab constate au 10/05/2026 que la mention
« Copriciel gratuit » qui circule **ne correspond plus à l'offre 2026** (120 € TTC/an).
Aucun acteur établi du segment professionnel ne propose d'offre gratuite complète.
**Éliminatoire n° 2 : franchi.**

**Levées de fonds :**
- **Matera : 35 M€**, annoncés le 25/05/2021, investisseurs Bpifrance, Mubadala Capital,
  Burda Principal Investment — `https://immo2.pro/actualite-immobilier/la-startup-matera-leve-35-millions-deuros-pour-accelerer-sa-croissance/`,
  consulté le 30/07/2026. **Cette levée n'est pas retenue pour l'éliminatoire n° 4**, et
  c'est un point à ne pas escamoter : Matera ne vend pas de logiciel aux syndics
  professionnels, il **remplace** le syndic auprès de la copropriété. Ses 35 M€ ne
  financent pas une force de vente dirigée contre un éditeur, ils financent la
  réduction du nombre de clients possibles. C'est une menace sur la cible, pas un
  concurrent produit. L'éliminatoire se déclenche ailleurs, sur une mesure plus nette.
- **Ublo : 1,8 M€**, après 625 k€ initiaux. Sous le seuil de 5 M€.
- **Orisha (ex-DL Software) : sous LBO du fonds américain TA Associates depuis avril
  2021**, puis structure de reprise **TANGO BIDCO** (SIREN 930667019, créée le
  03/07/2024). **Ce n'est pas une levée** au sens du § 2 de CLAUDE.md : rachat par un
  fonds, l'argent va aux cédants. Consigné comme **changement d'actionnariat**.
- **Septeo : entrée de Bpifrance au capital** relevée sans montant vérifié →
  **INCONNU**, non utilisé.

### Lecture du plafond de marché

La grille de l'étape 3 donne « Trois acteurs > 20 M€, ou levées > 5 M€ → **Éliminatoire —
ils gagnent par la distribution** ». Le constat est plus lourd que le seuil :

**Le secteur s'est refermé sur deux groupes sous LBO.**

- **Orisha Real Estate** — « la première acquisition (Seiitra) au premier trimestre
  [2025] a permis au groupe de **dépasser les 100 M€ de revenus** », CFNews,
  `https://www.cfnews.net/L-actualite/Build-up/Orisha-gere-ses-reseaux-en-immobilier-544980`,
  consulté le 30/07/2026 (extrait libre d'un article payant). L'entité annonce
  elle-même **« +450 collaborateurs »** et **« +75 000 utilisateurs »**
  (`https://realestate.orisha.com/`, 30/07/2026). Le groupe Orisha vise **400 M€** de CA
  en 2026 (CFNews Immo). Marques réunies : Immofacile, Jestimo, **Crypto**, **Gercop**,
  **Seiitra**, Must, Kolimmo.
- **Septeo ADB** — 27 393 570 € (2024), **3 200 agences clientes**, **2 000 000 de lots
  syndic** et **1 000 000 de lots locatifs** gérés (`https://www.septeo-adb.fr/`,
  30/07/2026). Le groupe Septeo déclarait 310 M€ de CA en 2022.

Trois entités du secteur franchissent 20 M€ : Septeo ADB (27,39 M€), Orisha Transaction
(27,39 M€), Seiitra Réseau (21,44 M€). Et le leader dépasse 100 M€, soit **plus de trois
fois** le seuil d'élimination de 30 M€.

**Une observation qui vaut avertissement de méthode.** Le comparatif de presse de 2019
présentait Crypto, Gercop, Seiitra, ICS et SPI comme cinq concurrents distincts. En 2026,
**Seiitra Réseau et Gercop Digital ont le même président (TANGO BIDCO) et le même
commissaire aux comptes (Grant Thornton)** — vérifié par le champ `dirigeants` de l'API.
Un comparatif de logiciels vieux de six ans ne décrit plus une concurrence : il décrit un
portefeuille. **Compter les marques revient à surestimer massivement le nombre
d'acteurs.**

**Éliminatoire n° 4 : DÉCLENCHÉ.**

## 3. Défauts documentés

Corpus : **30 avis lus intégralement** — détail dans `SYNDICS_GESTION_LOCATIVE_avis.md`
Répartition : **0 Trustpilot** (inaccessible, HTTP 403) / **30 stores** (20 Google Play,
10 App Store) / **0 Reddit-forums** / **0 Capterra-G2**

Le corpus atteint tout juste le seuil de 30 du protocole, et repose sur **quatre
applications** dont une seule fournit du volume. La bascule en recherche primaire a été
faite ; elle est documentée dans le fichier d'avis et pèse davantage que le tableau.

| Catégorie | Occurrences (sources fortes) | Occurrences (sources faibles) | Éditeur(s) visé(s) |
|---|---|---|---|
| **bug/fiabilité** | **13** | 0 | Matera (8), Vilogi (4), Timci (1) |
| fonctionnalité manquante | 4 | 0 | Matera |
| ergonomie | 3 | 0 | Matera (2), Vilogi (1) |
| support | 3 | 0 | Matera |
| performance | 2 | 0 | Matera |
| prix caché | 2 | 0 | Matera |
| facturation/résiliation | 1 | 0 | Matera |

**Écart de notation détecté : OUI, et il est interne aux sources fortes.** Matera affiche
**4,8/5 sur l'App Store** (732 avis) et **4,5/5 sur Google Play** (624 avis), mais sur les
20 avis Google Play réellement lisibles, **9 sont notés 1 ou 2 étoiles**, dont quatre
datés de 2025-2026 (crash à l'authentification forte, service client qui ne répond plus,
brouillons perdus). Le § 3 de CLAUDE.md attend cet écart entre Capterra et Trustpilot ;
il se produit ici **entre deux sources fortes**, ce qui n'était pas prévu et mérite
d'être retenu pour les secteurs suivants.

**Second écart, sur les moyens.** Matera : 1 356 avis cumulés, application livrée cette
semaine. Vilogi, éditeur pour professionnels : 10 avis, et **deux applications non mises
à jour depuis juillet 2024**, soit deux ans. Le bug Face ID signalé « depuis plus d'un
an » en décembre 2024 n'a pas pu être corrigé depuis, faute de livraison.

Thèmes dominants, par occurrences en sources fortes uniquement :
1. **bug/fiabilité — 13 occurrences.** Crashs à l'authentification, données perdues,
   synchronisation défaillante. Réparti sur les trois éditeurs du corpus.
2. **fonctionnalité manquante — 4 occurrences.** Recherche dans les e-mails, relevés de
   compteurs, scan de factures, paiement de factures.
3. **ergonomie et support — 3 occurrences chacun.**

## 4. Contraintes réglementaires

| Obligation | Texte | Date d'entrée en vigueur | Qui est concerné |
|---|---|---|---|
| Extranet de copropriété — liste minimale de documents dématérialisés | **Décret n° 2019-502 du 23 mai 2019** | **01/07/2020** (art. 4) | Le **syndic professionnel** |
| Communication des documents au conseil syndical | Décret du 23 mai 2019 (second décret) | 01/07/2020 | Le syndic — astreinte de 15 €/jour de retard |
| Projet de plan pluriannuel de travaux (PPPT) | Loi n° 65-557, art. 14-2 ; CCH art. L721-1 à L721-3 ; décret n° 2022-663 du 25/04/2022 | **01/01/2023** (>200 lots), **01/01/2024** (51–200), **01/01/2025** (≤50) — **toutes échues** | Copropriétés de plus de 15 ans |
| DPE collectif, copropriétés ≤ 50 lots | — | **01/01/2026** — échue | Copropriétés |
| Prêt collectif à adhésion simplifiée | Décret n° 2025-711 du 25/07/2025 (JO 27/07) | 27/07/2025 — échue | Syndics et copropriétaires |
| Diagnostic structurel — modèle-type harmonisé | Arrêté du 22/08/2025 | 31/08/2025 — échue | Syndics, propriétaires de bâtiments collectifs |
| **Registre national d'immatriculation — élargissement des données** | **Décret n° 2025-831 du 19/08/2025** (JO 21/08) | **février 2027** (18 mois après publication) | **Syndics, professionnels et bénévoles** |
| **Registre national d'immatriculation — second palier** (identifiant RNB, systèmes techniques, DPE collectif, avancement PPT, seuil d'impayés porté à « plus de deux trimestres de charges ») | **Arrêté du 23/06/2026** (JO 19/07/2026), CCH art. R. 711-1 à R. 711-21 | **janvier 2028** (18 mois après publication) | **Syndics, professionnels et bénévoles** |
| Travaux de rénovation, immeubles classés E | Cadre PPT | fin 2028 | Copropriétés concernées |

**Le logiciel métier est-il certifié/agréé par l'État ? NON.**

Preuve, source primaire : le décret n° 2019-502 du 23 mai 2019
(`https://www.legifrance.gouv.fr/loda/id/JORFTEXT000038501555/`, consulté le 30/07/2026)
fait peser l'obligation sur **« le syndic professionnel »**, à qui il impose de mettre à
disposition une liste minimale de documents dans un espace en ligne sécurisé. **Il
n'impose aucune certification, homologation, agrément ni référencement de l'outil
informatique ni de l'espace sécurisé lui-même.** Il définit un *contenu à fournir*, pas
une *qualification de l'outil*.

C'est la réponse explicite à la question posée : **loi ALUR, décret sur le conseil
syndical et extranet obligatoire portent tous sur le syndic, aucun sur l'outil.**
Les seuls « agréments » rencontrés sont des reconnaissances par des organisations
professionnelles et des caisses de garantie — privées, facultatives, et non
constitutives d'une barrière d'État.

**Éliminatoire n° 3 : franchi.**

## 5. Ligne de score (à recopier telle quelle dans SYNTHESE.md)

| Champ | Valeur | Barème |
|---|---|---|
| Entreprises cibles | **15 430** (mentions carte G, 1.1.2026) | 15-50k = **2** |
| CA du leader | **> 100 M€** (Orisha Real Estate, 2025) | >30M = **ÉLIMINÉ** |
| Prix plancher constaté | **119 € HT/mois** (Septeo, segment professionnel) | >100€ = **3** |
| Occurrences du reproche dominant (sources fortes) | **13** (bug/fiabilité) | >=10 = **3** |
| Échéance réglementaire exploitable | **janvier 2028** (arrêté du 23/06/2026), ~18 mois | 12-36 mois = **3** |
| Réutilisation du code de l'app BTP | **INCONNU** | aucune = 0, partielle = 2, forte = 3 |
| Certification d'État sur le logiciel | **NON** | NON = **0** |

**Score total : ÉLIMINÉ** (11/18 sur les six champs renseignables, sans effet).

Le champ « réutilisation du code de l'app BTP » reste `INCONNU` : aucune information n'a
jamais été fournie sur cette application (réserve du § 6 de CLAUDE.md). Il n'est pas mis
à 0 par défaut, ce qui ferait passer une absence d'information pour une absence de
réutilisation.

**Le score ne décide pas, les éliminatoires décident.** 11/18 sur les champs mesurables
est un score honorable — le prix plancher est élevé, le reproche dominant est massif et
l'échéance de janvier 2028 tombe pile dans la fenêtre exploitable. Rien de tout cela ne
compte : trois acteurs à plus de 20 M€ et un leader à plus de 100 M€ ferment le secteur.

## 6. Périmètre du MVP, si GO

**Sans objet — le secteur est NO-GO.**

Conformément au § 2 de CLAUDE.md, « un secteur éliminé sur l'un de ces critères est
abandonné, pas noté ». Aucun périmètre de MVP n'est proposé, aucun angle d'entrée n'est
retenu, aucune charge de développement n'est estimée. Produire un plan produit pour un
marché éliminé serait exactement le travail que ce protocole existe pour éviter.

## 7. Fenêtre de lancement

**Sans objet — le secteur est NO-GO.**

Pour mémoire, si le secteur devait être rouvert sur un cycle réglementaire ultérieur,
l'échéance de référence serait **janvier 2028** (arrêté du 23/06/2026, second palier du
registre national d'immatriculation). Le calcul à rebours n'est pas produit ici : il
supposerait une charge de développement V1, qui suppose un périmètre de MVP, lequel n'a
pas lieu d'être défini.

## 8. Distribution

**Sans objet — le secteur est NO-GO.**

## 9. Le test à 48 h

**Sans objet — le secteur est NO-GO.**

Le test à 48 h sert à invalider une hypothèse avant d'écrire du code. Ici l'hypothèse est
déjà invalidée par une mesure : le CA publié du leader. Dépenser 48 heures à le
reconfirmer n'apporterait rien.

## 10. Sources consultées

| URL | Nature | Éditeur du site | Conflit d'intérêt |
|---|---|---|---|
| `https://recherche-entreprises.api.gouv.fr/search` | API publique de décompte et de comptes annuels | DINUM / ministère de l'Économie (données INPI) | **Aucun** — source d'État opposable |
| `https://www.legifrance.gouv.fr/loda/id/JORFTEXT000038501555/` | Texte réglementaire (décret 2019-502) | DILA / Premier ministre | **Aucun** — source primaire |
| `https://www.service-public.gouv.fr/particuliers/vosdroits/F36760` | Fiche pratique PPT, « Vérifié le 08 juin 2026 » | DILA | **Aucun** |
| `https://annuaire-entreprises.data.gouv.fr/entreprise/383003423` | Fiche d'entreprise | DINUM | **Aucun** |
| `https://www.journaldelagence.com/1410307-...` | Presse professionnelle, chiffres CCI 1.1.2026 | Journal de l'Agence | Faible — presse sectorielle, vit de la publicité des éditeurs ; la donnée est attribuée à CCI France |
| `https://www.cnacim.immo/blog/statistiques-2025-...` | Republication d'un tableau UNIS / CCI France | CNACIM | Faible — organisme du secteur ; **le tableau est signé UNIS et sourcé CCI France**, la republication n'altère pas les chiffres |
| `https://www.cfnews.net/...544980` | Presse M&A (extrait libre) | CFNEWS | Faible — presse financière indépendante des éditeurs |
| `https://www.cfnewsimmo.net/...501956` | Presse M&A immobilier (extrait libre) | CFNEWS IMMO | Faible — idem |
| `https://realestate.orisha.com/` | Site de l'éditeur | **Orisha** | **Fort — c'est un acteur mesuré.** Chiffres d'auto-déclaration (450 collaborateurs, 75 000 utilisateurs), utilisés comme tels |
| `https://www.septeo-adb.fr/` et `/mentions-legales.htm` | Site de l'éditeur | **Septeo Solutions ADB** | **Fort — acteur mesuré.** Utilisé pour l'identité légale (SIREN) et les volumes auto-déclarés |
| `https://www.informationsrapidesdelacopropriete.fr/images/pdf/Tableaux.pdf` | Comparatif de 21 solutions, IRC n° 648, mai 2019 | Informations Rapides de la Copropriété | **Moyen — annuaire, pas banc d'essai.** La colonne « Atouts de la solution » est manifestement de la copy fournie par chaque éditeur. Utilisé pour **lister** les acteurs, jamais pour les **juger**. De plus **périmé** : six ans, la moitié des éditeurs a été absorbée depuis |
| `https://coprolab.fr/comparatif-logiciel-syndic/` | Comparatif 2026 | Coprolab, « média indépendant » | **Fort — déclare des programmes d'affiliation actifs et des démarchages commerciaux en cours avec Matera, Bellman, Vilogi.** N'édite pas de logiciel. Retenu uniquement pour le constat vérifiable « tous les éditeurs pro sont sur devis » et pour la correction sur Copriciel |
| `https://www.copro-assist.fr/septeo-le-logiciel-...` | Page tarifaire | Copro Assist' | **Fort — partenaire commercial déclaré de Septeo.** Seule source publique du prix d'entrée de 119 € HT/mois ; à traiter comme un prix d'appel, pas comme un prix payé |
| `https://immo2.pro/actualite-immobilier/la-startup-matera-leve-35-millions-...` | Presse proptech | Immobilier 2.0 | Faible à moyen — média sectoriel, contenu partiellement payant |
| `https://monimmeuble.com/actualite/le-registre-national-...` | Presse copropriété | Monimmeuble | Faible |
| `https://blog.door-in.fr/copropriete-les-nouvelles-obligations-...` | Blog professionnel | **Door-in** (acteur du secteur) | Moyen — les références de textes ont été retenues, pas les commentaires |
| `https://www.vilogi.com/` | Site de l'éditeur | **Vilogi** | **Fort — acteur mesuré.** Utilisé pour constater l'absence de grille tarifaire |
| `https://play.google.com/store/apps/details?id=eu.matera.app` | Avis utilisateurs | Google | **Aucun sur le contenu**, mais Google sélectionne les avis affichés |
| `https://apps.apple.com/fr/app/id1501663391`, `id1556625522`, `id1483199893`, `id1554877565` | Avis utilisateurs | Apple | **Aucun sur le contenu** |
| `https://fr.trustpilot.com/review/...` | Avis utilisateurs | Trustpilot | **Non consultable — HTTP 403** sur 4 URL |
| `https://www.union-habitat.org/.../ush-etude_logiciels_copropriete.pdf` | Étude comparative indépendante, avril 2022 | Union Sociale pour l'Habitat | **Aucun — fédération, pas éditeur.** C'était la meilleure source disponible ; **inaccessible, HTTP 403** en WebFetch comme en curl |
| `https://www.lesformationsdelouis.com/statistiques-agents-immobiliers-france-2026/` | Statistiques | Les Formations de Louis | Moyen — **écarté** : ne donne qu'une estimation « 30 000 à 40 000 », sans ventilation ni source datée |

## 11. Zones d'ombre

1. **Trustpilot n'a pas été mesuré.** HTTP 403 sur les quatre URL testées, y compris
   avec un User-Agent de navigateur. C'est la source la plus haute de la hiérarchie du
   § 3 de CLAUDE.md, et elle est absente du corpus. À rouvrir par un autre moyen si le
   secteur devait être réexaminé.
2. **L'étude comparative de l'Union Sociale pour l'Habitat (avril 2022) est
   inaccessible** (403 en WebFetch et en curl). C'était la seule comparaison
   **indépendante** identifiée — une fédération d'organismes HLM, sans intérêt dans la
   vente de logiciel. Sa perte est la lacune la plus regrettable de cette session.
3. **Le forum UniversImmo et l'ARC n'ont pas été explorés.** Ce sont les deux lieux de
   parole des copropriétaires et conseils syndicaux français, non sollicités par les
   éditeurs, donc sources fortes. Le budget de requêtes a été absorbé par les étapes 3
   et 6. C'est la première piste à ouvrir en cas de réexamen.
4. **Le CA de Vilogi est INCONNU**, et c'est un manque réel : c'est le principal éditeur
   indépendant survivant du segment professionnel. Le champ `finances` donne `ca` = 0
   pour l'exercice 2024, ce qui signifie **non renseigné** et non « zéro » (piège
   consigné au § 5 de CLAUDE.md), avec un résultat net de 143 574 €. Aucun proxy n'a été
   fabriqué.
5. **La ventilation produit du CA de Seiitra Réseau est INCONNUE.** L'entité publie
   21 436 821 € en 2023 sous le code 58.29C, mais la part qui relève du syndic de
   copropriété par rapport aux autres activités du groupe n'est pas établie. Le chiffre
   est publié tel quel, sans répartition inventée.
6. **Le chiffre « > 100 M€ » d'Orisha Real Estate provient de l'extrait libre d'un
   article payant.** Le référent exact de « le groupe » — la business unit immobilier ou
   le groupe Orisha entier — n'est pas certain à 100 %. La lecture retenue est la
   business unit, cohérente avec le fait qu'Orisha vise 400 M€ au niveau groupe. **Le
   verdict ne dépend pas de cette lecture** : Septeo ADB (27,39 M€) et Seiitra Réseau
   (21,44 M€) suffisent à eux seuls à établir la concentration.
7. **Les 16 éditeurs du comparatif IRC 2019 n'ont pas été instruits financièrement.**
   Leur statut actuel — indépendants, absorbés ou disparus — reste à établir. Compte
   tenu du taux d'absorption constaté, l'hypothèse la plus probable est une
   consolidation supplémentaire, ce qui **renforcerait** le verdict plutôt que de
   l'affaiblir. Non vérifié, donc non affirmé.
8. **Le nombre de titulaires détenant à la fois une mention G et une mention S est
   INCONNU.** Les deux populations se recoupent (462 « mention unique S » au 1.1.2025,
   sur 5 088 cartes S). L'union des deux cibles est donc comprise entre **15 430** et
   **20 491**, sans qu'on puisse la situer dans cet intervalle. Le plancher a été retenu.
