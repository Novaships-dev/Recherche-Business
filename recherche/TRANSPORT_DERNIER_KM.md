# TRANSPORT DERNIER KM

Recherche effectuée le : 30/07/2026
Requêtes web effectuées : 25 (7 recherches, 5 `WebFetch`, 13 appels `curl` dont 8 en échec)

**Ordre d'exécution modifié sur instruction de l'utilisateur** : l'étape 6
(réglementaire) a été exécutée **en premier**, avant l'identification des
éditeurs. Motif : deux éliminatoires n° 3 potentiels étaient identifiés dès le
plan de campagne. L'un s'est déclenché. Les étapes 2, 3, 4 et 5 n'ont donc pas
été exécutées, et les champs correspondants sont `INCONNU` — pas « néant ».

## Verdict

**NO-GO** — le règlement (UE) 2020/1056 impose une certification par organisme
accrédité **sur la plateforme logicielle elle-même**, et le droit français de la
lettre de voiture a été notifié dans son périmètre.

Critère décisif : **éliminatoire n° 3 — certification d'État sur le logiciel
métier.** Article 12 du règlement (UE) 2020/1056 : « Upon application by an eFTI
platform developer, a conformity assessment body shall assess the compliance of
the eFTI platform […] the conformity assessment body shall issue a compliance
certificate for that eFTI platform. » La certification porte sur le logiciel,
pas sur l'entreprise de transport qui l'utilise.

**Un second motif, indépendant du premier, ferme aussi le secteur** : la fenêtre
de lancement calculée à rebours depuis le 9 juillet 2027 imposait une mise en
ligne au 9 juillet 2026. Elle est passée depuis 21 jours (cf. § 7). Même si la
certification était accessible, le cycle réglementaire serait manqué.

## 1. Dimensionnement

Codes NAF retenus : 49.41A, 49.41B, 49.41C, 52.29A (NAF rév. 2)
Entreprises cibles : **22 323** — repris tel quel de `recherche/PREFILTRE_NAF.md`
§ 2, comptage exact du 30/07/2026 (source : `recherche-entreprises.api.gouv.fr`,
requêtes à tranche unique sommées, `etat_administratif=A`). **Aucun recomptage
effectué dans cette session.**

| Tranche d'effectif | 49.41A | 49.41B | 49.41C | 52.29A | Total |
|---|---|---|---|---|---|
| 01 (1–2 sal.) | 2 699 | 3 478 | 81 | 47 | 6 305 |
| 02 (3–5 sal.) | 1 930 | 2 456 | 77 | 36 | 4 499 |
| 03 (6–9 sal.) | 1 425 | 1 794 | 60 | 45 | 3 324 |
| 11 (10–19 sal.) | 1 576 | 1 843 | 103 | 49 | 3 571 |
| 12 (20–49 sal.) | 1 467 | 1 302 | 158 | 86 | 3 013 |
| 21 (50–99 sal.) | 493 | 344 | 51 | 43 | 931 |
| 22 (100–199 sal.) | 251 | 143 | 40 | 28 | 462 |
| 31 (200–249 sal.) | 43 | 25 | 9 | 9 | 86 |
| 32 (250–499 sal.) | 77 | 29 | 6 | 20 | 132 |
| **Cible** | **9 961** | **11 414** | **585** | **363** | **22 323** |

Cible réaliste (segment adressable) : **22 323**, sans restriction
supplémentaire — mais la structure compte plus que le total. **48,4 % de la
cible (10 804 entreprises) a 5 salariés ou moins**, et 62,3 % en a 9 ou moins.
C'est un secteur d'artisans-transporteurs, pas de logisticiens. Un éditeur qui
viserait ce segment vise des entreprises à faible capacité d'achat logiciel.

Éliminé par le seuil de 3 000 : **NON** (22 323 = 7,4 × le seuil).

## 2. Éditeurs en place

**Étape non exécutée.** Recherche arrêtée à l'étape 6 sur instruction, après
déclenchement de l'éliminatoire n° 3.

| Éditeur | Créé en | Cible | CA (exercice) | Effectif | Prix d'entrée | Source |
|---|---|---|---|---|---|---|
| *(non instruit)* | INCONNU | INCONNU | INCONNU | INCONNU | INCONNU | — |

Offre gratuite détectée : **INCONNU** — non recherché.
Levées de fonds : **INCONNU** — non recherché.
Lecture du plafond de marché : **INCONNU** — étape 3 non exécutée.

Les éditeurs qui devaient être instruits sont listés en § 11 (zones d'ombre).
Deux d'entre eux étaient signalés a priori comme appartenant à des
consolidateurs (Nomadia, déjà rencontré au secteur GMAO ; Transporeon, groupe
Trimble). **Cette hypothèse n'a pas été vérifiée et ne doit pas être reprise
comme un fait.**

## 3. Défauts documentés

**Étape non exécutée.** Corpus : **0 avis** — aucune plateforme d'avis n'a été
consultée. Détail dans `TRANSPORT_DERNIER_KM_avis.md`, qui consigne l'absence
d'instruction.

Ce n'est **pas** « corpus inférieur à 30 » au sens de l'étape 5 du protocole :
la recherche primaire de substitution n'a pas non plus été menée. Aucune
conclusion, ni positive ni négative, ne peut être tirée sur la qualité des
logiciels en place.

Écart de notation détecté : **INCONNU** — non recherché.
Thèmes dominants : **INCONNU** — non recherché.

## 4. Contraintes réglementaires

| Obligation | Texte | Date d'entrée en vigueur | Qui est concerné |
|---|---|---|---|
| Les autorités compétentes doivent accepter les informations réglementaires transmises par voie électronique, et l'opérateur qui transmet doit le faire **sur une plateforme eFTI certifiée** | Règlement (UE) 2020/1056, art. 4 § 2 et art. 5 § 1 | **9 juillet 2027** — 30 mois après l'entrée en vigueur du premier acte d'exécution (2024/1942, en vigueur le 09/01/2025) | Autorités de contrôle de tous les États membres ; tout opérateur qui choisit la voie électronique |
| Le droit français de la lettre de voiture entre dans le périmètre eFTI | Règlement délégué (UE) 2024/2025 du 15/07/2024, annexe I partie B, entrée « France » : code des transports **art. R3411-13** ; arrêté du 9 novembre 1999 relatif aux documents de transport devant se trouver à bord, **art. 4-II, 5-I, 5-II, 6, 4-III, 4-IV** | Publié au JOUE le 20/12/2024 | **Transporteurs routiers de marchandises établis en France, transport intérieur compris** |
| Spécifications fonctionnelles détaillées des plateformes eFTI (pistes d'audit, sécurité, gestion des signatures, sessions de connexion) | Règlement d'exécution (UE) 2025/2243 du 06/11/2025 | Publié au JOUE le 07/11/2025 | Développeurs et opérateurs de plateformes eFTI |
| Chronotachygraphe intelligent 2ᵉ génération sur les VUL de plus de 2,5 t en transport international et en cabotage | Règlement (UE) 165/2014 modifié par le règlement (UE) 2020/1054 — **date relevée en source secondaire uniquement** | 1ᵉʳ juillet 2026 | Transporteurs exploitant des VUL 2,5–3,5 t à l'international |
| Téléchargement des données conducteur (28 j) et de la mémoire de masse (95 j), conservation 365 jours | Arrêté du 6 juillet 2005 relatif aux modalités de téléchargement des données de conduite | En vigueur | Toute entreprise de transport routier |

### Le logiciel métier est-il certifié/agréé par l'État ? **OUI**

Trois questions ont été instruites séparément. Deux répondent NON, une répond
OUI — et c'est celle qui n'était pas la plus attendue.

**a) Registre des transporteurs et licence de transport intérieur → NON.**
L'inscription au registre électronique national des entreprises de transport par
route et la licence délivrée par le préfet de région portent sur **l'entreprise**
(honorabilité, capacité professionnelle, capacité financière), pour dix ans
renouvelables. Aucune obligation ne porte sur un outil logiciel. Source :
`https://www.ecologie.gouv.fr/acces-et-exercice-profession-transporteur-marchandises-0`,
consultée le 30/07/2026. Pas d'éliminatoire.

**b) Chronotachygraphe, téléchargement et archivage des données sociales → NON.**
Point vérifié sur le texte primaire. L'arrêté du 6 juillet 2005
(`https://www.legifrance.gouv.fr/loda/id/JORFTEXT000000607239`, consulté le
30/07/2026) **n'impose aucun agrément, aucune homologation et aucune
certification sur le logiciel ou l'outil de téléchargement et d'archivage.** Il
fixe des fréquences (28 jours pour la carte conducteur, 95 jours pour la mémoire
de masse), une durée de conservation (365 jours) et une structure de nom de
fichier (`.C1B`, `.V1B`). Le seul « organisme agréé » mentionné est un atelier,
saisi en cas d'échec de téléchargement, sur le véhicule — pas sur le logiciel.
Aucune signature électronique n'est exigée. **L'hypothèse de départ était que ce
point pouvait fermer le secteur : elle est écartée.** Pas d'éliminatoire.

**c) Règlement eFTI (UE) 2020/1056 → OUI. Éliminatoire n° 3 déclenché.**

Vérifié sur le texte du règlement, pas sur des articles de presse. La question
posée était : la certification porte-t-elle sur la plateforme, sur le prestataire
de services, ou sur les deux ? **Réponse : sur les deux, par deux articles
distincts.**

| Article | Objet | Qui certifie |
|---|---|---|
| **Art. 11** | Les organismes d'évaluation de la conformité sont **accrédités au titre du règlement (CE) 765/2008** aux fins de la certification des plateformes eFTI et des prestataires de services eFTI. Chaque État membre désigne une autorité qui tient la liste à jour et la publie **sur un site officiel de l'État**. | — |
| **Art. 12** | **Certification de la plateforme eFTI.** Sur demande du *développeur de plateforme eFTI*, l'organisme évalue la conformité de la plateforme aux exigences de l'art. 9 § 1 et délivre un certificat de conformité. Les informations transmises via une plateforme certifiée portent une **marque de certification** (art. 12 § 3). Le développeur doit **demander une réévaluation à chaque révision des spécifications techniques** (art. 12 § 4). | Organisme d'évaluation de la conformité accrédité |
| **Art. 13** | **Certification du prestataire de services eFTI**, aux exigences de l'art. 10 § 1. | Organisme d'évaluation de la conformité accrédité |

**Le caractère obligatoire est posé par l'article 4 § 2**, cité littéralement :

> « Where the economic operators concerned make regulatory information available
> electronically to a competent authority, they shall do so on the basis of data
> processed on a **certified eFTI platform** and, if applicable, by a **certified
> eFTI service provider**. »

**Un éditeur de logiciel de transport tombe-t-il dans le périmètre ? OUI**, dès
lors que son produit sert de canal de transmission d'une information
réglementaire à une autorité de contrôle. La définition de l'art. 3 point 11 est
sans ambiguïté sur ce point :

> « ‘eFTI platform developer’ means a natural or legal person which has developed
> or acquired an eFTI platform either for the purpose of processing regulatory
> information related to its own economic activity **or for putting that platform
> on the market**. »

Mettre une plateforme sur le marché suffit à être développeur de plateforme eFTI.

**Et le transport intérieur français est bien concerné.** C'est le point qui
achève la démonstration, et il ne se lit pas dans le règlement de 2020 : l'annexe I
partie B était vide à l'origine, à remplir par acte délégué. Le **règlement
délégué (UE) 2024/2025 du 15 juillet 2024** l'a remplie avec les droits nationaux
notifiés. L'entrée « France » y inscrit **l'article R3411-13 du code des
transports** et **l'arrêté du 9 novembre 1999 relatif aux documents de transport
devant se trouver à bord des véhicules de transport routier de marchandises** —
c'est-à-dire la lettre de voiture nationale. Les 22 323 cibles y sont donc
soumises, sans qu'il soit besoin qu'elles roulent à l'international.

**Conséquence.** L'unique échéance réglementaire exploitable du secteur entre 2026
et 2029 est le 9 juillet 2027, et c'est précisément celle-là qui est barrée par
une certification portant sur le logiciel. Le module que la réforme rend
obligatoire est celui qu'un développeur solo ne peut pas mettre sur le marché
sans passer par un organisme accrédité, avec réévaluation à chaque révision des
spécifications.

**Réserve honnête, à ne pas gommer.** La certification n'est déclenchée que par
la fonction de transmission à l'autorité. Un logiciel qui se limiterait à
l'affectation, à la facturation ou à l'optimisation de tournées n'y est pas
soumis. Mais un tel produit n'exploite plus aucune échéance réglementaire et
retombe sur un marché de TMS généralistes dont l'étape 2 n'a pas été instruite —
donc sans le moindre élément permettant de conclure GO. **Le coût et le délai
réels d'une certification eFTI sont `INCONNU`** : ils n'ont pas été établis, et
c'est l'objet du test à 48 h (§ 9).

## 5. Ligne de score (à recopier telle quelle dans SYNTHESE.md)

### Réutilisation du code de l'app BTP — détail brique par brique

Le champ n'est plus `INCONNU` : les briques ont été communiquées par
l'utilisateur le 30/07/2026.

| Brique existante | Transpose au transport dernier km ? | Analyse |
|---|---|---|
| **Factur-X / facturation électronique conforme à la réforme française** | **OUI, fortement** | Un transporteur facture ses donneurs d'ordre et subit la réforme dans les mêmes termes que le BTP. Brique réutilisable quasiment telle quelle, le format et le calendrier étant transverses. |
| **Suivi documentaire de sous-traitants, relances automatiques, contrôle de validité en cascade (vigilance rang 2+)** | **OUI, fortement** | C'est la meilleure transposition des six. La sous-traitance en cascade est structurelle dans le transport routier, et le donneur d'ordre doit contrôler chez son sous-traitant la licence de transport, l'attestation de vigilance URSSAF et l'attestation d'assurance. Le mécanisme de contrôle de validité en cascade est identique, seule la liste des pièces change. |
| **Application terrain mobile avec fonctionnement hors-ligne** | **OUI, fortement** | Un chauffeur est un opérateur terrain en connectivité dégradée, exactement comme un compagnon de chantier. Émargement à la livraison, réserves, photos. Brique transposable sans refonte. |
| **Génération de documents et signature** | **OUI, mais dans la zone barrée** | Lettre de voiture, bon de livraison, émargement du destinataire : la brique transpose techniquement. Mais dès que le document généré est la lettre de voiture présentée à un contrôle, on entre dans le périmètre eFTI et la certification s'applique. Elle transpose vers le seul endroit qu'on ne peut pas occuper. |
| **Devis, chantiers, situations de travaux** | **Partiellement** | Le chaînage devis → commande → facture transpose vers devis → ordre de transport → facture. En revanche la **situation de travaux** (facturation à l'avancement) n'a pas d'équivalent : le transport se facture à l'envoi ou au forfait mensuel, pas à l'avancement. Environ la moitié de la brique. |
| **Corps de métier structurés** (carrelage, couverture, électricité, maçonnerie, menuiserie, isolation, façade, chauffage/climatisation) | **NON** | Aucune transposition. Le référentiel équivalent côté transport serait les types de véhicule, de marchandise et de conditionnement — une autre nomenclature, à reconstruire intégralement. |

**Bilan : trois briques transposent fortement et sans réserve (Factur-X,
vigilance sous-traitants, app terrain hors-ligne), une quatrième transpose
techniquement mais atterrit dans la zone soumise à certification, une transpose à
moitié, une pas du tout.** Le barème demande 3 dès trois briques transposables :
**note 3**.

C'est le meilleur score de réutilisation obtenu jusqu'ici, et il ne sauve pas le
secteur. À consigner tel quel : la réutilisabilité du code n'est pas un critère
d'ouverture d'un marché.

### Ligne de score

| Champ | Valeur | Barème |
|---|---|---|
| Entreprises cibles | 22 323 | 15–50k = **2** |
| CA du leader | `INCONNU` — étape 3 non exécutée | non calculable |
| Prix plancher constaté | `INCONNU` — étape 4 non exécutée | non calculable |
| Occurrences du reproche dominant (sources fortes) | `INCONNU` — étape 5 non exécutée | non calculable |
| Échéance réglementaire exploitable | 9 juillet 2027, soit **11,3 mois** | < 12 mois = **1** |
| Réutilisation du code de l'app BTP | forte — 3 briques sur 6 transposent pleinement | **3** |
| Certification d'État sur le logiciel | **OUI** | **éliminé** |

**Score total : non calculable — secteur éliminé.**

Points acquis sur les champs instruits : **6**. Trois champs restent `INCONNU`,
donc le total sur 18 ne doit pas être publié ni comparé aux autres secteurs.
Le score ne décide pas : l'éliminatoire décide.

## 6. Périmètre du MVP, si GO

**Sans objet — verdict NO-GO.**

Aucun périmètre n'est proposé. Le seul angle d'entrée qu'aurait offert le secteur
— « module réglementaire que les gros ne maintiennent pas » — est celui-là même
qui exige la certification.

## 7. Fenêtre de lancement

Calcul à rebours depuis l'échéance réglementaire la plus proche, le 9 juillet 2027.

| Jalon | Date |
|---|---|
| Échéance réglementaire (eFTI, art. 5 § 1) | **9 juillet 2027** |
| Pic d'achat estimé (échéance − 6 mois) | 9 janvier 2027 |
| Mise en ligne cible (échéance − 12 mois) | **9 juillet 2026 — déjà passée depuis 21 jours** |
| Début du développement (mise en ligne − charge V1) | antérieur au 9 juillet 2026, donc passé |

**Le début du développement calculé est déjà passé. Le secteur est raté sur ce
cycle réglementaire**, indépendamment de l'éliminatoire de certification. Les
deux motifs sont autonomes : lever l'un ne rouvrirait pas le secteur.

## 8. Distribution

**Non instruite** — étape sans objet sur un NO-GO.

Deux organisations professionnelles ont été rencontrées incidemment pendant
l'instruction réglementaire et sont notées pour un usage éventuel ailleurs :
**OTRE** (`https://www.otre.org`) et **FNTR**. Elles n'ont pas été évaluées comme
canaux.

Prix de lancement proposé : **sans objet**.

## 9. Le test à 48 h

Le NO-GO repose sur une inférence à vérifier : *la certification eFTI de
l'article 12 est hors de portée d'un développeur seul*. Le règlement l'impose,
mais son coût réel n'a pas été établi. C'est le seul point qui, s'il tombait,
rouvrirait la discussion — la fenêtre de lancement resterait fermée pour autant.

**Test** : écrire le même jour à trois destinataires, avec la même question.
1. **DGITM**, sponsor de l'investigation eFTI de la Fabrique Numérique
   (`victor.dolcemascolo@developpement-durable.gouv.fr`, contact publié sur
   `https://beta.gouv.fr/startups/efti.html`, consulté le 30/07/2026) : quelle
   autorité française a été désignée au titre de l'article 11 § 3, et où la liste
   officielle est-elle publiée ?
2. **COFRAC**, unique organisme d'accréditation français
   (`https://www.cofrac.fr`) : quels organismes d'évaluation de la conformité
   sont accrédités en France pour la certification des plateformes eFTI ?
3. **Un de ces organismes**, s'il en existe : coût et délai d'une certification
   initiale de plateforme au titre de l'article 12, et coût d'une réévaluation au
   titre de l'article 12 § 4.

**Résultat qui invalide le NO-GO** — les trois conditions réunies : au moins un
organisme accrédité en France pour eFTI, **coût de certification initiale
< 15 000 €**, **délai < 4 mois**. Toute autre issue — y compris « aucun organisme
accrédité à ce jour » — confirme le NO-GO.

Coût du test : trois courriels, zéro euro.

## 10. Sources consultées

| URL | Nature | Éditeur du site | Conflit d'intérêt |
|---|---|---|---|
| `https://www.legislation.gov.uk/eur/2020/1056/adopted` | Texte intégral du règlement (UE) 2020/1056, version « as adopted by EU » | The National Archives (gouvernement britannique) | **Aucun.** Miroir d'État d'un texte de l'UE, réutilisé sous décision 2011/833/UE. Utilisé faute d'accès à EUR-Lex (cf. § 11) |
| `http://publications.europa.eu/resource/celex/32024R2025` | Règlement délégué (UE) 2024/2025 — annexe I partie B | Office des publications de l'UE (API cellar) | **Aucun.** Source officielle |
| `http://publications.europa.eu/resource/celex/32025R2243` | Règlement d'exécution (UE) 2025/2243 — exigences fonctionnelles des plateformes | Office des publications de l'UE (API cellar) | **Aucun.** Source officielle |
| `http://publications.europa.eu/resource/celex/32024R1942` | Règlement d'exécution (UE) 2024/1942 — date d'entrée en vigueur, ancre du calcul des 30 mois | Office des publications de l'UE (API cellar) | **Aucun.** Source officielle |
| `https://transport.ec.europa.eu/transport-themes/logistics-and-multimodal-transport/efti-regulation_en` | Page eFTI de la Commission — confirme la date du 9 juillet 2027 et la liste des actes | Commission européenne, DG MOVE | **Aucun.** Auteur du règlement |
| `https://www.legifrance.gouv.fr/loda/id/JORFTEXT000000607239` | Arrêté du 6 juillet 2005, téléchargement des données de conduite | DILA (gouvernement français) | **Aucun.** Source officielle |
| `https://www.ecologie.gouv.fr/acces-et-exercice-profession-transporteur-marchandises-0` | Accès à la profession de transporteur, licence et registre | Ministère de la Transition écologique | **Aucun.** Source officielle |
| `https://beta.gouv.fr/startups/efti.html` | Fiche de l'investigation eFTI, sponsor DGITM, contact | DINUM / beta.gouv.fr | **Aucun.** Source officielle |
| `https://www.otre.org/le-tachygraphe-intelligent-2e-generation-devient-obligatoire-sur-les-vul-25-t-le-1er-juillet-2026/` | Échéance du 1ᵉʳ juillet 2026 sur les VUL > 2,5 t | OTRE, organisation professionnelle de transporteurs | **Faible, à signaler.** Syndicat patronal du secteur, pas éditeur de logiciel. **Source secondaire : la date n'a pas été revérifiée sur le règlement (UE) 2020/1054** |
| `https://www.geotab.com/fr/blog/tachygraphe-intelligent-2-echeance-juillet-2026-pme/` | Même échéance | Geotab, **éditeur de solutions de gestion de flotte** | **Fort.** Vendeur sur ce marché, page à visée commerciale. Non retenue comme source du fait |
| `http://transport-community.org/.../EU-Regulation-20201056-...eFTI.pdf` | Annoncé comme le règlement, s'est révélé être un diaporama de présentation | Transport Community (organisation intergouvernementale) | **Aucun**, mais **document écarté** : ce n'est pas le texte |

Aucun comparatif de logiciels n'a été consulté — l'étape 2 n'a pas été exécutée.
La règle d'identification de l'éditeur de chaque comparatif n'a donc pas eu à
s'appliquer.

## 11. Zones d'ombre

1. **EUR-Lex est fermé au robot.** Cinq tentatives sur
   `eur-lex.europa.eu/legal-content/FR/TXT/HTML/?uri=CELEX:32024R2025` renvoient
   **HTTP 202 avec un corps vide**, comportement d'anti-robot ; le format PDF
   fait de même. À consigner au même titre que les 403 de `pappers.fr` et de
   `infogreffe.fr`. **Contournement validé et à réutiliser** : l'API cellar de
   l'Office des publications, `http://publications.europa.eu/resource/celex/[CELEX]`
   avec l'en-tête `Accept: application/xhtml+xml` et `Accept-Language: fra`,
   sert le même texte officiel. C'est désormais la voie d'accès au droit de
   l'Union pour ce repo.
2. **Coût et délai réels d'une certification eFTI : `INCONNU`.** C'est la seule
   inconnue qui porte sur le verdict. Objet du test à 48 h.
3. **Autorité française désignée au titre de l'article 11 § 3 : `INCONNU`.** Non
   trouvée. La DGITM est le sponsor de l'investigation eFTI côté État, mais celle-ci
   est marquée « investigation non concluante » depuis le 2 octobre 2021.
   Aucun organisme d'évaluation de la conformité accrédité pour eFTI n'a été
   identifié en France — **absence de résultat, pas preuve d'absence**.
4. **Aucun éditeur n'a été instruit.** Les noms qui devaient l'être, et qui
   restent à traiter si le secteur était rouvert : Akanea, DDS Logistics,
   Shiptify, Dashdoc, GEDMOUV, Optilogistic, Sinari, Mapotempo/AntsRoute, Nomadia
   (TourSolver), OptimoRoute, Urbantz, Woop, Transporeon (groupe Trimble), Alpega/
   Teleroute, Trans.eu, B2Pweb, Optac3 (Stoneridge), TIS-Web (Continental VDO),
   Chronoservices, Actia. **L'hypothèse de consolidation autour de Nomadia et de
   Trimble n'a pas été testée** : trois secteurs sur trois avec un consolidateur
   reste à confirmer ou à infirmer.
5. **Aucun avis n'a été lu.** Rien ne peut être dit de la qualité des logiciels
   en place, ni dans un sens ni dans l'autre.
6. **Aucun prix n'a été relevé**, donc l'éliminatoire n° 2 (offre gratuite
   crédible) n'a **pas** été vérifié. Le secteur est éliminé sur l'éliminatoire
   n° 3 seul ; il pourrait l'être aussi sur le n° 2, ce qu'on ignore.
7. **La date du 1ᵉʳ juillet 2026 pour les VUL > 2,5 t repose sur des sources
   secondaires** (OTRE, presse spécialisée). Elle n'affecte pas le verdict et
   n'a pas été revérifiée sur le règlement (UE) 2020/1054. À faire avant tout
   usage de ce chiffre.
8. **Portée exacte de l'article 6 § 1 du règlement CEE n° 11 sur le transport
   purement intérieur : non tranchée.** La question devient sans objet du fait de
   la notification française à l'annexe I partie B, qui couvre explicitement la
   lettre de voiture nationale — mais l'articulation entre les deux n'a pas été
   instruite.
