# Sécurité privée

Recherche effectuée le : 30/07/2026
Requêtes web effectuées : 58 (25 WebSearch, 25 WebFetch dont 7 en échec réseau, 8 requêtes API)

Ordre d'exécution appliqué : **étape 6 d'abord, puis étape 3**, conformément au
§ 0 point 3 de `CLAUDE.md`. Le secteur a été fermé à l'étape 3.

## Verdict

**NO-GO** — un éditeur présent sur le secteur a levé 6,5 M€ d'argent frais pour
financer précisément sa diversification vers les secteurs connexes, et deux
éditeurs de gestion des temps dépassant 80 M€ de CA sont opposés en concurrence
directe par les acteurs verticaux eux-mêmes.

Critère décisif : **éliminatoire n° 4** (levée de fonds > 5 M€). SENEF SOFT
(SIREN 529974511), éditeur du logiciel de sécurité privée Seenet, a levé
**6,5 M€ auprès d'Isatis Capital le 2 mai 2023**, en série A — donc en argent
frais entrant dans l'entreprise, et non en cession de titres. Au sens du § 2 de
`CLAUDE.md`, cela **compte**.

### État des quatre éliminatoires

| # | Éliminatoire | État | Étape |
|---|---|---|---|
| 1 | Volume < 3 000 | **NON** — 4 775 cibles | 1 (faite antérieurement) |
| 2 | Offre gratuite complète et crédible | **NON** — aucune gratuité pérenne constatée | 4 (menée, bornée) |
| 3 | Certification d'État sur le logiciel | **NON** — vérifié sur source primaire | 6 (menée en premier) |
| 4 | Trois acteurs > 20 M€, ou levée > 5 M€, ou leader > 30 M€ | **OUI — DÉCLENCHÉ** | 3 |

Aucun éliminatoire n'est laissé `INCONNU` : les quatre ont été instruits. En
revanche l'**étape 5 (corpus d'avis) n'a pas été menée** — elle n'a plus de
valeur de décision une fois l'éliminatoire n° 4 déclenché, et c'est l'étape la
plus coûteuse. Voir `SECURITE_PRIVEE_avis.md`.

## 1. Dimensionnement

Codes NAF retenus : `80.10Z`, `80.20Z`, `80.30Z`
Entreprises cibles : **4 775** (source : `https://recherche-entreprises.api.gouv.fr/search`, 30/07/2026)

Chiffres repris de `recherche/PREFILTRE_NAF.md` sans recomptage, à la demande de
l'utilisateur. Cible = entreprises actives (`etat_administratif=A`) de tranche
d'effectif `01` à `32`, soit 1 à 499 salariés.

| Code | Libellé officiel NAF rév. 2 | 01 | 02 | 03 | 11 | 12 | 21 | 22 | 31 | 32 | **Cible** | Actives (toutes tranches) |
|---|---|---|---|---|---|---|---|---|---|---|---|---|
| `80.10Z` | Activités de sécurité privée | 585 | 525 | 513 | 633 | 697 | 277 | 139 | 34 | 42 | **3 445** | >10000 (PLAFOND) |
| `80.20Z` | Activités liées aux systèmes de sécurité | 450 | 311 | 177 | 162 | 114 | 39 | 10 | 5 | 3 | **1 271** | 5 060 |
| `80.30Z` | Activités d'enquête | 38 | 10 | 2 | 3 | 3 | 1 | 1 | 1 | 0 | **59** | 1 153 |
| | **TOTAL SECTEUR** | | | | | | | | | | **4 775** | |

Cible réaliste (segment adressable) : **3 445**, soit le seul `80.10Z`. Motif :
`80.30Z` ne pèse que 59 unités, négligeable. `80.20Z` regroupe l'installation
d'alarmes et la télésurveillance — un métier d'installateur et d'exploitant de
station, dont le besoin logiciel (supervision d'alarmes, levée de doute) n'a
rien à voir avec la planification de vacations d'agents. Les confondre
gonflerait la cible de 37 % sans fondement.

### Registre officiel — application de la règle 10 de `CLAUDE.md`

La profession dispose d'un registre d'État : les autorisations d'exercice
délivrées par le CNAPS. La règle impose de publier les deux chiffres et l'écart.

| Mesure | Valeur | Source |
|---|---|---|
| Cible NAF 01–32 | 4 775 | API recherche-entreprises, 30/07/2026 |
| Agents habilités (cartes professionnelles en cours) | > 300 000 | Rapport d'activité 2025 du CNAPS, via `anews-securite.fr` (22/04/2026) |
| Cartes professionnelles délivrées en 2025 | 70 000 | idem |
| **Entreprises autorisées par le CNAPS** | **INCONNU** | voir ci-dessous |

**Le nombre d'entreprises autorisées n'a pas pu être établi.** Des sources
secondaires l'annoncent à 12 500, mais le site du CNAPS
(`cnaps.interieur.gouv.fr`) a renvoyé une erreur réseau (`socket hang up`) sur
**quatre tentatives** de récupération, le 30/07/2026 — mesure, pas impression
(règle 8). Le chiffre de 12 500 n'est donc pas repris comme acquis : il n'a pas
de source primaire vérifiée, et l'écart avec le NAF n'est pas mesurable en
l'état. Ne pas présumer de son sens.

## 2. Éditeurs en place

Étape menée en second, réduite à ce qui alimente l'étape 3 — conformément au
§ 0 point 3. Deux populations nettement distinctes, qu'il faut séparer.

### 2a. Éditeurs verticaux (spécialistes de la sécurité privée)

| Éditeur | Dénomination légale | SIREN | Créé en | NAF | Effectif | CA (exercice) | Prix d'entrée | Source |
|---|---|---|---|---|---|---|---|---|
| Seenet (Senef) | SENEF SOFT | 529974511 | 2011 | 62.01Z | 50–99 | **INCONNU** (`ca: 0` en 2020) | non affiché | API, 30/07/2026 |
| Comète | AEXAE | 394128466 | 1994 | 64.20Z | NN | 3 925 343 € (2021) | 150 €/mois, 36 mois | API, 30/07/2026 |
| Trackforce Valiant | ALPHA SYSTEM | 432430304 | — | 62.01Z | 10–19 | **13 261 410 €** (2024) | 200 €/mois, 24 mois | API, 30/07/2026 |
| SEKUR | LE WEB FRANCAIS | 813316882 | 2015 | 62.01Z | 6–9 | **INCONNU** (`finances: null`) | non affiché | API, 30/07/2026 |
| MC Tracker | MC TRACKER | 101200244 | **12/02/2026** | 58.29C | NN | **INCONNU** (`finances: null`) | non affiché | API, 30/07/2026 |
| Hector Solution | VIGIFORMATION | 991136508 | **03/09/2025** | 85.59B | NN | **INCONNU** (`finances: null`) | non affiché | API, 30/07/2026 |
| BanetteOne | **INCONNU** | — | — | — | — | **INCONNU** | 69 €/mois, sans engagement | mentions légales introuvables |

### 2b. Éditeurs horizontaux de gestion des temps, opposés en concurrence

Instruits en priorité à la demande de l'utilisateur.

| Éditeur | Dénomination légale | SIREN | NAF | Effectif | CA 2024 | Résultat net 2024 |
|---|---|---|---|---|---|---|
| Bodet Software | **KELIO** | 538209594 | 62.02A | 250–499 | **83 769 181 €** | 9 471 542 € |
| Horoquartz | HOROQUARTZ (H Q) | 399243922 | 58.29C | 250–499 | **81 459 537 €** | 10 834 520 € |
| (holding) | BODET SA | 775610504 | 70.10Z | 50–99 | 151 251 000 € | 11 619 000 € |

**Ces CA sont tous secteurs confondus, pas la sécurité privée.** La part
réalisée sur le secteur est `INCONNU` et n'a pas de source publique. Ne pas les
lire comme des « CA du marché du logiciel de sécurité privée ».

Offre gratuite détectée : **NON**. Aucune gratuité pérenne chez un acteur
établi. Ce qui est présenté comme gratuit relève de trois catégories, toutes
disqualifiantes : essais bornés (BanetteOne 5 jours, Organilog 14 jours puis
19 €/utilisateur/mois), outils génériques détournés (Google Forms + Sheets,
Notion, Airtable, Trello), et cahier papier scanné. Périmètre réel constaté, pas
déduit d'une mention marketing.

Levées de fonds : **UNE, décisive.**

- **SENEF SOFT — 6,5 M€, Isatis Capital, 2 mai 2023, série A.** Argent frais.
  Qualification vérifiée sur deux sources : *L'Usine Digitale* parle d'un
  « premier financement » pour une entreprise qui « fonctionne sans lever de
  fonds depuis 2011 » ; *FrenchWeb* titre « [Série A] » et indique un emploi des
  fonds tourné vers l'interne — « renforcer ses équipes, se développer à
  l'international et **diversifier son offre vers des secteurs connexes** ».
  Ce n'est ni un MBO, ni un LBO, ni un OBO, ni une cession de titres : au sens du
  § 2 de `CLAUDE.md`, **cela compte**.

Lecture du plafond de marché (grille de l'étape 3) : le secteur ne correspond à
aucune ligne proprement. Le vertical seul ressemble à la ligne « aucun compte
publié, tous micro-entreprises — ambigu », avec un unique CA vertical publié à
13,3 M€. Mais cette lecture est fausse dès qu'on ajoute la capacité de feu
réelle : un acteur financé à 6,5 M€ et deux GTA à plus de 80 M€.

### Ce que la consolidation a démasqué (champ `dirigeants`, avant les CA)

Méthode appliquée dans l'ordre prescrit au § 5 de `CLAUDE.md` : `dirigeants`
d'abord, `finances` ensuite, sur la même requête.

- **KELIO a pour président BODET SA** (personne morale, SIREN 775610504). Kelio
  et Bodet SA sont **un seul groupe**, pas deux acteurs. Leurs CA ne sont pas
  sommés : les flux intra-groupe double-compteraient (règle 6).
- **HOROQUARTZ est détenu par le groupe japonais AMANO depuis 2008.** Signature
  visible dans le champ `dirigeants` : `IKOMA SUSUMU`, administrateur, et
  `PEIRSMAN BERT`, président du conseil d'administration — soit une gouvernance
  étrangère sur une SA française. Confirmé par la presse M&A (Oaklins). Amano
  emploie environ 5 000 personnes dans le monde.
- **SEKUR a pour président HOLDING COCORICO** (SIREN 890022023, NAF 66.30Z,
  créée le 15/09/2020), dirigée par Adrien SAIX. Structure de portage.
- **AEXAE est elle-même en NAF 64.20Z**, code de holding, et non en édition de
  logiciel. Son seul exercice publié remonte à **2021**.

**Deux pièges de nommage confirmés**, cohérents avec le § 5 :
« Bodet Software » n'est pas une dénomination légale — la société s'appelle
**KELIO** depuis le 16/09/2022. « Hector Solution » non plus : l'éditeur est
**VIGIFORMATION**, dont les mentions légales s'annoncent en « entreprise
individuelle » alors que l'API porte un « Président de SAS » — contradiction
non résolue, à ne pas trancher sans pièce.

### Un signal à ne pas surinterpréter

Deux des sept éditeurs verticaux ont **moins d'un an d'existence** : MC TRACKER
créée le 12/02/2026, VIGIFORMATION le 03/09/2025. La barrière à l'entrée
technique est donc basse, ce qui est en soi une mauvaise nouvelle : ce qu'un
solo peut construire, six autres le construisent en même temps. Aucun de ces
entrants n'a de comptes publiés ; leur viabilité est `INCONNU`.

## 3. Défauts documentés

**Corpus : 0 avis lus.** Étape 5 non menée — le secteur a été fermé à l'étape 3
par l'éliminatoire n° 4, et le § 0 point 3 de `CLAUDE.md` prescrit de ne pas
payer le protocole entier après une fermeture.

Ceci n'autorise pas à conclure « pas de problème détecté ». Détail et pistes
dans `SECURITE_PRIVEE_avis.md`.

| Catégorie | Occurrences (sources fortes) | Occurrences (sources faibles) | Éditeur(s) visé(s) |
|---|---|---|---|
| — | INCONNU | INCONNU | — |

Écart de notation détecté : **INCONNU** — non instruit.

Thèmes dominants : **INCONNU** — non instruit.

## 4. Contraintes réglementaires

Étape menée **en premier**. Elle n'a pas fermé le secteur.

| Obligation | Texte | Date d'entrée en vigueur | Qui est concerné |
|---|---|---|---|
| Créer un compte dans le téléservice Dracar Ultimate | Décret n° 2025-1344 du 26/12/2025, CSI art. R. 611-2-1 | Mise en service du téléservice, **au plus tard le 01/10/2026** | Personnes morales et exploitants individuels |
| **Déclarer ses salariés, tenir la liste à jour, et vérifier régulièrement la validité de leurs titres** | idem, CSI art. R. 621-1-1 et R. 625-3-1 | idem — **01/10/2026** pour les entreprises déjà enregistrées | Personnes morales exerçant une activité privée de sécurité |
| Fournir une photo d'identité (future carte professionnelle sécurisée) | idem | Dès que le téléservice le permet, au plus tard le 01/10/2026 | Personnes physiques |
| Disposition à date fixée par arrêté | idem, art. 7 | Au plus tard le **31/12/2026** | idem |
| Registre des contrôles internes + mémento des consignes, en français, émargé | CSI art. R631-16 (décret n° 2014-1253 du 27/10/2014) | En vigueur | Entreprises de sécurité privée |
| Registre d'utilisation et d'entretien des équipements | CSI art. R631-17 | En vigueur | idem |
| Registre unique du personnel | CSI art. L611-2 ; C. trav. art. L1221-13, D1221-23 | En vigueur | idem |
| Vacation minimale de 6 h continues (temps plein), max 12 h | CCN prévention-sécurité, IDCC 1351 | **01/03/2026** | Employeurs de la branche |
| Réception obligatoire des factures électroniques | Réforme de la facturation électronique | **01/09/2026** | Toutes les entreprises |
| Émission obligatoire des factures électroniques | idem | **01/09/2027** | PME et micro-entreprises |

Nomenclature : le Livre visé est le **Livre VI** du code de la sécurité
intérieure (art. L611-1 à L648-1 et R611-1 à R648-2), et non le Livre III.
La consigne de session mentionnait le Livre III ; c'est une erreur de référence,
corrigée ici sur Légifrance.

### Le logiciel métier est-il certifié/agréé par l'État ? **NON.**

Les quatre questions posées ont été instruites séparément. Réponses :

**1. Le CNAPS porte-t-il une obligation sur le logiciel ?** Non. Le décret
n° 2025-1344 du 26/12/2025 — lu sur Légifrance, source primaire — crée des
obligations **administratives pesant sur l'entreprise** : créer un compte,
déclarer ses salariés, vérifier la validité de leurs titres. Le seul outil
informatique qu'il mentionne est « un téléservice mis en œuvre par le Conseil
national des activités privées de sécurité », c'est-à-dire l'outil du CNAPS
lui-même. Aucun logiciel tiers n'est prescrit, ni format d'échange, ni
interface, ni homologation. L'autorisation d'exercice et la carte
professionnelle portent sur **l'entreprise, ses dirigeants et ses agents** —
jamais sur un outil.

**2. Les registres du Livre VI imposent-ils un format ou un outil agréé ?** Non.
Les art. R631-16 et R631-17 exigent un contenu et une tenue à jour, et restent
neutres technologiquement : ni « informatisé », ni « agréé », ni « certifié ».
Deux sources indépendantes convergent — la lecture directe des articles sur
Légifrance, et une analyse d'avocate (Myrina Prestel, cabinet Squair, barreau de
Bordeaux) qui conclut que « le texte ne spécifie ni format numérique
obligatoire, ni logiciel homologué ». La main courante elle-même n'est pas un
registre statutairement obligatoire mais un outil opérationnel, dont
l'obligation dérive des art. L612-1 et suivants ; sa durée de conservation est
de 5 ans.

**3. La convention collective exige-t-elle un logiciel conforme ?** Non — et la
distinction demandée par l'utilisateur est ici exactement le bon fil.
La CCN IDCC 1351 rend le calcul objectivement complexe : vacations de 6 à 12 h,
48 h hebdomadaires et 46 h en moyenne sur 12 semaines, contingent annuel de
329 h supplémentaires, majorations nuit +10 %, dimanche +10 %, férié +100 %,
avec des taux renforcés en sûreté aéroportuaire (nuit +25 %, dimanche +50 %),
prime d'ancienneté de +2 % à +12 %, panier repas au-delà de 6 h continues.
**Rien de tout cela n'impose une caractéristique à l'outil.** L'obligation de
conformité pèse sur l'employeur, pas sur son logiciel ; la jurisprudence le
confirme dans ce sens (Cass., 28/02/2018 : l'entreprise reste responsable même
en ayant externalisé la paie). **La complexité est un argument de vente, pas une
barrière réglementaire** — et elle ne déclenche pas l'éliminatoire n° 3.

> Piège écarté au passage : plusieurs pages affirment que « la norme NF 525
> applicable aux systèmes de caisse s'étend désormais aux logiciels de paie ».
> C'est **faux** — NF 525 vise les systèmes de caisse. Toutes les pages portant
> cette affirmation sont des fermes de contenu sans référence de texte. Ne pas
> la propager.

**4. Balayage lexical séparé.** Résultats terme par terme :

| Terme | Résultat sur le périmètre sécurité privée |
|---|---|
| `agrément` | Porte sur l'**entreprise** et ses **dirigeants** (autorisation d'exercice, agrément dirigeant), jamais sur un outil |
| `certifié` | APSAD R31 / I31 (stations de télésurveillance), délivrée par CNPP Cert. — **certification de service, non obligatoire légalement**, exigée par les assureurs. Porte sur l'organisation, les compétences du personnel, la continuité de service et les moyens de secours de la station. Pas sur un produit logiciel |
| `homologué` | Aucune occurrence sur le secteur. Le seul régime d'homologation trouvé est l'homologation de sécurité ANSSI, qui vise les systèmes d'information des entités publiques et des opérateurs sous contrat avec le ministère des Armées — hors périmètre |
| `référencement` | Aucun référencement d'éditeur par le CNAPS. Aucune liste d'outils référencés |
| `immatriculé` | Sens précis et unique : la **Plateforme Agréée (PA, ex-PDP)** de la facturation électronique, immatriculée par la DGFiP — 129 immatriculées définitivement au 05/05/2026. **Un logiciel métier n'a pas à être immatriculé** : il peut être un simple opérateur de dématérialisation (OD) raccordé à une PA. C'est le régime de la majorité des logiciels de facturation. Aucune barrière pour un solo |

**Une réserve, honnêtement formulée.** La certification APSAD R31 n'est pas une
barrière à l'édition d'un logiciel, mais elle n'est pas neutre : le référentiel
audite « les procédures utilisées » et « la continuité du service » d'une station
de télésurveillance. Un outil vendu à une station certifiée entre donc dans le
périmètre audité **de son client**. C'est une friction commerciale réelle, pas
un éliminatoire — et elle ne concerne que `80.20Z`, écarté de la cible réaliste
en section 1.

## 5. Ligne de score (à recopier telle quelle dans SYNTHESE.md)

| Champ | Valeur | Barème |
|---|---|---|
| Entreprises cibles | 4 775 | 3-15k = **1** |
| CA du leader | Levée 6,5 M€ (Senef Soft) ; Kelio 83,8 M€ et Horoquartz 81,5 M€ tous secteurs | >30M ou levée >5M = **ÉLIMINÉ** |
| Prix plancher constaté | 49 €/mois (Organilog) | 30-100€ = **2** |
| Occurrences du reproche dominant (sources fortes) | INCONNU — étape 5 non menée | non noté |
| Échéance réglementaire exploitable | 01/10/2026, soit 2 mois | <12 mois = **1** |
| Réutilisation du code de l'app BTP | 4 briques sur 6 transposent pleinement | forte = **3** |
| Certification d'État sur le logiciel | NON | **0** |

**Score total : NON TOTALISÉ — secteur éliminé.**

Le total serait de toute façon incalculable : un champ est `INCONNU`. Les points
partiels (1 + 2 + 1 + 3 + 0 = 7 sur 5 champs renseignés) n'ont aucune valeur de
classement et ne doivent pas être reportés comme un score.

Le prix plancher de 49 €/mois provient d'un comparatif **édité par BanetteOne**,
qui s'y classe premier — conflit d'intérêt majeur, chiffre à traiter comme
indicatif. À noter aussi : PlanningPME est facturé 4 €/agent/mois, un modèle qui
place le plancher réel bien plus bas pour une petite agence.

### Réutilisation du code de l'app BTP — détail brique par brique

Barème du protocole : aucune = 0, partielle = 2, forte = 3. Soit **3 dès que
trois briques transposent**. Instruite ici en vérifiant, pour chacune, **vers
quoi** elle transpose et si la cible d'arrivée est barrée — le piège constaté sur
TRANSPORT.

| # | Brique BTP | Transpose vers | Verdict | Zone barrée ? |
|---|---|---|---|---|
| 1 | **Factur-X / facturation électronique** | Facturation mensuelle par site et par vacation. Échéances 01/09/2026 (réception) et 01/09/2027 (émission PME) | **Pleinement** | Non — un OD raccordé à une PA suffit, aucune immatriculation requise |
| 2 | **Suivi documentaire de sous-traitants, relances, contrôle de validité en cascade (vigilance rang 2+)** | Suivi de validité des cartes professionnelles CNAPS, des agréments dirigeants, des qualifications (APS, SSIAP, cynophile) et des habilitations des sous-traitants. La sous-traitance en cascade est structurelle dans le secteur | **Pleinement — la mieux ajustée des six** | Non. C'est même exactement l'obligation créée par le décret du 26/12/2025 : « vérifier régulièrement la validité des titres de leurs salariés », sans aucune contrainte d'outil |
| 3 | **Devis, chantiers, situations de travaux** | Devis → devis. Chantier → site ou poste de garde. **Situations de travaux → rien** : la sécurité facture des heures de vacation réalisées, pas un avancement de travaux | **Partiellement** | Non |
| 4 | **App terrain mobile hors-ligne** | Rondes, pointage sur site, main courante saisie au poste. Le hors-ligne n'est pas un confort : parkings, sous-sols, sites isolés | **Pleinement** | Non |
| 5 | **Génération de documents et signature** | Mémento des consignes émargé par l'agent (exigé par l'art. R631-16), rapports d'intervention, registre des contrôles internes | **Pleinement** | **Non — et c'est le point à souligner.** Sur TRANSPORT, cette même brique atterrissait sur la lettre de voiture, objet de la certification eFTI. Ici elle atterrit sur des registres que les textes laissent explicitement sans format |
| 6 | **Corps de métier structurés** (carrelage, couverture, électricité…) | Rien. Le référentiel métier de la sécurité privée (APS, SSIAP 1/2/3, cynophile, agent de recherches privées, télésurveillance) n'a aucun contenu commun avec les corps d'état du bâtiment. La *structure* de référentiel typé à validité transpose, mais elle est déjà comptée dans la brique 2 — la compter deux fois gonflerait le score | **Aucune** | — |

**Score : 3** (quatre briques transposent pleinement, seuil de trois atteint).

**Ce 3 ne décide rien, et c'est le quatrième secteur d'affilée où il ne décide
rien.** C'est le meilleur score de réutilisation obtenu jusqu'ici — meilleur que
les 3 de TRANSPORT, puisqu'ici aucune brique n'atterrit en zone barrée — et le
secteur est fermé par ailleurs. Conformément au § 6 de `CLAUDE.md` : ce champ
départage des secteurs viables, il n'en ouvre aucun. Ne pas laisser ce 3
infléchir la lecture de l'éliminatoire n° 4.

## 6. Périmètre du MVP, si GO

**Sans objet — secteur NO-GO.** Rien n'est proposé ici : le § 2 de `CLAUDE.md`
est explicite, les éliminatoires décident, et proposer un MVP sur un secteur
éliminé reviendrait à le rouvrir par la bande.

Pour mémoire seulement, si l'éliminatoire venait à être infirmé (voir § 11) :
l'angle le plus solide serait le **module réglementaire que les gros ne
maintiennent pas** — le suivi de validité des titres CNAPS imposé au 01/10/2026,
qui est précisément la brique BTP n° 2. Il n'est pas retenu, et ne doit pas être
développé sur cette base.

## 7. Fenêtre de lancement

| Jalon | Date |
|---|---|
| Échéance réglementaire | 01/10/2026 (décret n° 2025-1344) |
| Pic d'achat estimé (échéance − 6 mois) | 01/04/2026 — **déjà passé** |
| Mise en ligne cible (échéance − 12 mois) | 01/10/2025 — **déjà passé** |
| Début du développement (mise en ligne − charge V1) | antérieur à 2025 — **largement passé** |

**Le secteur est raté sur ce cycle réglementaire**, indépendamment de
l'éliminatoire. L'échéance du décret Dracar Ultimate est dans deux mois : le pic
d'achat a eu lieu, et les éditeurs verticaux — dont deux créés en 2025 et 2026 —
l'ont manifestement joué. C'est un second motif de NO-GO, autonome du premier.

## 8. Distribution

**Sans objet — secteur NO-GO.** Non instruit, et à ne pas reporter comme
« aucun canal trouvé ». Aucune recherche de canal n'a été menée.

Prix de lancement proposé : **sans objet.**

## 9. Le test à 48 h

**Sans objet pour un lancement.** Un seul test conserve une utilité, et il porte
sur l'éliminatoire lui-même, pas sur l'opportunité :

Test : demander à Isatis Capital ou à Senef Soft la ventilation de l'emploi des
6,5 M€ — et en particulier si la ligne « sécurité privée / Seenet » a été
financée par cette levée ou par l'autofinancement antérieur.
Résultat qui invalide le NO-GO : **la preuve documentée que Seenet a été lancé
avant mai 2023 et n'a reçu aucune part de la levée** — ce qui sortirait Senef du
périmètre de l'éliminatoire n° 4. Cela laisserait subsister Kelio et Horoquartz,
dont l'exposition au secteur reste `INCONNU`, ainsi que la fenêtre de lancement
fermée (§ 7). L'invalidation est donc peu probable et, même acquise, ne suffit
pas à rouvrir le secteur.

## 10. Sources consultées

| URL | Nature | Éditeur du site | Conflit d'intérêt |
|---|---|---|---|
| `https://www.legifrance.gouv.fr/jorf/id/JORFTEXT000053176690` | Texte du décret n° 2025-1344 | État (DILA) | **Aucun — source primaire** |
| `https://www.legifrance.gouv.fr/codes/section_lc/LEGITEXT000025503132/LEGISCTA000029656360/` | CSI art. R631-1 à R631-33 | État (DILA) | **Aucun — source primaire** |
| `https://recherche-entreprises.api.gouv.fr/search` | Décomptes, dirigeants, finances | État (DINUM / INPI) | **Aucun — source primaire opposable** |
| `https://www.village-justice.com/articles/entreprises-securite-privee-services-internes-securite-les-cahiers-registres,52523.html` | Analyse juridique des registres obligatoires | Village de la Justice — auteure : Myrina Prestel, cabinet Squair | Faible — avocate, pas éditrice de logiciel |
| `https://lessordelasecurite.org/cnaps-un-nouveau-decret-lie-a-dracar-ultimate/` | Presse spécialisée sécurité | L'Essor de la Sécurité | Faible |
| `https://www.anews-securite.fr/articles/.../rapport-d-activite-2025-du-cnaps-...` | Compte rendu du rapport CNAPS 2025 | AN News Sécurité | Faible |
| `https://www.frenchweb.fr/serie-a-senef-soft-leve-65-millions-deuros-aupres-disatis-capital/442456` | Annonce de levée de fonds | FrenchWeb | Faible — presse startup, reprend le communiqué |
| `https://www.usine-digitale.fr/article/senef-soft-leve-6-5-millions-...N2127966` | idem | L'Usine Digitale | Faible |
| `https://www.oaklins.com/fr/en/deals/3716/` | Opération Horoquartz / Amano | Oaklins (banque d'affaires) | Moyen — conseil sur l'opération |
| `https://seenet-securite.fr/` et `/mentions-legales/` | Site produit | **SENEF SOFT — éditeur, acteur instruit** | **Fort** |
| `https://www.horoquartz.com/mentions-legales/` | Mentions légales | **HOROQUARTZ — éditeur instruit** | **Fort** |
| `https://sekur.fr/` (3 pages) | Site produit et « comparatif » | **LE WEB FRANCAIS SAS — éditeur** | **Fort — affirme une « exigence légale » de main courante numérique sans citer un seul texte** |
| `https://banetteone.com/` (3 pages) | « Comparatifs » de prix et de gratuité | **BanetteOne — éditeur, se classe premier** | **Fort** |
| `https://hector-solution.fr/` (2 pages) | Site produit et « comparatif » | **VIGIFORMATION — éditeur, se classe premier** | **Fort** |
| `https://mctracker.fr/` (2 pages) | Site produit | **MC TRACKER SAS — éditeur** | **Fort — mais conclut lui-même à l'absence de format imposé** |
| `https://www.logiciel-comete.fr/mentions-legales/` | Mentions légales | **AEXAE — éditeur instruit** | **Fort** |
| `https://www.cnpp.com/tester-certifier/certifier-prestations-service-apsad-surete/telesurveillance` | Référentiel APSAD R31 | CNPP | Moyen — organisme certificateur, vend la certification |
| `https://cnaps.interieur.gouv.fr` | Source primaire d'État | CNAPS | **Aucun — mais INJOIGNABLE, 4 échecs réseau le 30/07/2026** |

**Observation méthodologique.** Sur ce secteur, la quasi-totalité de la
documentation « réglementaire » disponible en ligne est écrite par des éditeurs
de logiciel. Deux d'entre eux affirment une obligation légale de dématérialisation
sans référence de texte. Le point remarquable est qu'un troisième éditeur
(MC Tracker), qui aurait le même intérêt à l'affirmer, écrit l'inverse : « le
Code de la sécurité intérieure n'impose pas de format spécifique ». C'est cette
convergence contre-intérêt, recoupée sur Légifrance, qui a permis de trancher
l'éliminatoire n° 3.

## 11. Zones d'ombre

Par ordre d'impact décroissant sur la décision.

1. **Part du CA de Kelio et Horoquartz réalisée sur la sécurité privée :
   `INCONNU`.** Aucune source publique ne la donne. C'est la seule inconnue qui
   pourrait faire basculer la lecture de l'éliminatoire n° 4 vers un déclenchement
   *plus* large encore (trois acteurs > 20 M€) ou, à l'inverse, montrer que ces
   deux-là sont marginaux sur le secteur. Ne change pas le verdict, qui repose
   sur la levée Senef. À qui poser la question : les directions commerciales de
   Kelio et d'Horoquartz, ou un cabinet d'AMOA GTA comme Temps d'Avance.
2. **Nombre d'entreprises autorisées par le CNAPS : `INCONNU`.** Le site du
   CNAPS est resté injoignable. À reprendre depuis le rapport d'activité 2025
   (publié le 16/04/2026) une fois le site accessible, ou par demande directe au
   CNAPS. Permettrait de mesurer l'écart registre / NAF exigé par la règle 10.
3. **CA de SENEF SOFT : `INCONNU`.** Le champ `finances` ne porte qu'un exercice
   2020 avec `ca: 0`, qui signifie « non renseigné » et non « zéro ». Le fondateur
   a refusé de communiquer son CA à la presse en 2023, tout en annonçant vouloir
   dépasser 20 M€ sous deux ans — annonce, pas chiffre. À obtenir via les comptes
   déposés à l'INPI si l'entreprise ne les a pas rendus confidentiels.
4. **Corpus d'avis entièrement non constitué.** Voir `SECURITE_PRIVEE_avis.md`.
5. **Statut juridique réel de VIGIFORMATION** (Hector Solution) : ses mentions
   légales annoncent une entreprise individuelle, l'API un « Président de SAS ».
   Contradiction non tranchée. Sans effet sur le verdict.
6. **Éditeur de BanetteOne : `INCONNU`.** Aucune mention légale exploitable
   trouvée sur le site, alors que le même site publie des comparatifs de prix
   largement cités. Un éditeur qui compare ses concurrents sans se déclarer.
