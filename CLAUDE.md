# CLAUDE.md — Recherche-Business

Règles de travail pour toute session Claude Code sur ce repo.

## 0. Source de vérité

`PROMPT_RECHERCHE_SECTEUR.md` (racine) est **le protocole**. Il fait foi pour :
les éliminatoires, la hiérarchie des sources d'avis, le barème de score sur 18,
la structure des livrables, le périmètre MVP, la fenêtre de lancement et le
test à 48 h.

- **Ne jamais modifier `PROMPT_RECHERCHE_SECTEUR.md`.** Il est en lecture seule.
  Si son contenu paraît faux ou incomplet, le signaler à l'utilisateur — ne pas
  le corriger.
- **Ne pas le recopier** dans les livrables ni dans ce fichier. Y renvoyer.
- Le lire en entier avant toute étape.

> **ÉTAT AU 30/07/2026 : `PROMPT_RECHERCHE_SECTEUR.md` est PRÉSENT à la racine**
> — 400 lignes, commit `140f10f`. Il était annoncé mais absent jusqu'à cette
> date ; les sections `À COMPLÉTER` des § 2 et 3 de ce fichier ont depuis été
> renseignées à partir de son contenu réel, sans invention.
> Contrôle d'intégrité, à refaire avant de s'appuyer sur lui :
> `grep -c "" PROMPT_RECHERCHE_SECTEUR.md` doit donner **entre 350 et 420**, et
> le fichier doit contenir « /18 », « 3 000 », « Trustpilot » et « 48 h ».
> Le compte de lignes exact n'est pas un critère : un collage par la
> conversation ajoute des lignes vides.

### Instructions qui remplacent le protocole

Deux points où les instructions de l'utilisateur (30/07/2026) priment :

1. **Définition de la cible** : entreprises **actives**
   (`etat_administratif=A`) dont `tranche_effectif_salarie` ∈
   **{01, 02, 03, 11, 12, 21, 22, 31, 32}** — soit 1 à 499 salariés.
   Remplace la procédure de comptage de la section 5 de
   `NOTE_METHODE_API_ET_CODES_NAF.md`. Exclut donc `NN` (effectif non
   renseigné), `00` (0 salarié) et `41`→`53` (500 salariés et plus).
2. **Découpage sectoriel** : cinq unités de comptage pour les secteurs 3 et 6,
   **dix secteurs au total** (cf. § 4).

## 1. Règles absolues sur les données

Non négociables. Elles ont été établies par la vérification documentée dans
`NOTE_METHODE_API_ET_CODES_NAF.md`.

1. **Aucun chiffre sans sa source.** Tout nombre publié porte l'URL complète
   qui l'a produit et la date de la requête. Un chiffre sans URL est un chiffre
   à retirer.
2. **Jamais d'estimation, d'extrapolation, ni de chiffre reconstitué de
   mémoire.** Si la donnée n'a pas été obtenue, écrire `INCONNU`.
3. **`INCONNU` est une réponse valide et préférable à un proxy.** Ne jamais
   fabriquer un ordre de grandeur « comparable » pour remplir une case.
4. **10000 n'est jamais un nombre.** L'API `recherche-entreprises` plafonne
   `total_results` à 10000. Toute valeur égale à 10000 signifie
   « ≥ 10000, valeur inconnue » et s'écrit `>10000 (PLAFOND)`. Preuve : § 2.1
   de la note (68.20B annonce 10000, la somme de ses tranches donne ≥ 25 146).
5. **Tout paramètre d'API doit être validé avant usage** en lui passant une
   valeur absurde. Pas d'erreur ⇒ le paramètre est silencieusement ignoré et le
   chiffre est faux (cf. § 2.6, `&zzzbogus=1`).
6. **Contrôle de cohérence obligatoire** : la somme d'une partition doit égaler
   le total agrégé. Écart > 1 ⇒ ne rien publier et chercher la cause.
   Cette règle a déjà servi : c'est elle qui a fait découvrir, le 30/07/2026, que
   le `total_results` des requêtes à liste de tranches est faux (cf. § 5).
7. **Valider une optimisation de requête sur un volume réaliste.** Une
   équivalence vérifiée sur un code à 59 résultats ne prouve rien pour un code à
   10 000. Le contre-exemple est documenté dans `recherche/JOURNAL.md`.
8. **Un diagnostic est une mesure, pas une impression.** « La commande n'a pas
   répondu » n'est pas « le serveur ne répond pas ». La règle 2 s'applique aussi
   aux causes, pas seulement aux nombres.
9. **Quatre sources externes, une par usage.** Décomptes :
   `https://recherche-entreprises.api.gouv.fr/search`. Libellés NAF :
   `https://www.insee.fr/fr/metadonnees/nafr2/sousClasse/[code]`. Libellés de
   forme juridique : `https://xml.insee.fr/schema/cj-enum.html`
   (attribut `dc:title`). Libellés de tranche d'effectif :
   `https://raw.githubusercontent.com/annuaire-entreprises-data-gouv-fr/search-api/main/app/labels/tranches-effectifs.json`.
10. **Distinguer « le code NAF » de « la cible commerciale ».** Un code peut être
    dominé par des inscriptions sans besoin logiciel. Mais **vérifier avant de le
    répéter** : 68.32A est écrasé par les SCI dans la tranche `NN`, et elles n'y
    pèsent plus que 2,0 % une fois la cible 01–32 appliquée. Le décompte NAF est
    un majorant, pas un marché — et le biais dépend du filtre appliqué.

## 2. Les quatre éliminatoires

Un secteur éliminé sur l'un de ces critères est abandonné, pas noté.

1. **Volume de cibles < 3 000** → éliminé. (Seuil confirmé par la consigne
   d'origine reproduite en § 0 de la note : colonne
   « éliminé (< 3000 cibles) » OUI/NON.) Protocole : étape 1 et § E.
2. **Offre gratuite complète et crédible chez un acteur établi** → éliminé.
   « On ne descend pas sous zéro. » Le périmètre réel de la gratuité doit être
   constaté, pas déduit d'une mention marketing. Relever aussi les pages de
   comparaison tarifaire agressive entre éditeurs : signe d'une guerre de prix
   déjà engagée. Protocole : étape 4 et § E.
3. **Certification, agrément ou référencement d'État portant sur le logiciel
   métier lui-même** → éliminé : un développeur solo ne peut pas l'obtenir.
   À vérifier séparément et explicitement, en cherchant les termes `agrément`,
   `référencement`, `certifié`, `homologué`, `immatriculé`. Protocole : étape 6
   et § E.
4. Trois acteurs à plus de 20 M€ de CA, ou une levée de fonds
   supérieure à 5 M€, ou un leader à plus de 30 M€ → éliminé. Ils
   gagnent par la distribution, pas par le produit.
   Protocole : étape 3 et § 5 du fichier de sortie.

**Le score ne décide pas, les éliminatoires décident.** Un secteur à 17/18 avec
un concurrent gratuit reste NO-GO.

Le § E du protocole n'énumère que les trois premiers. Le quatrième est tranché
par l'utilisateur le 30/07/2026 et compte au même titre. Ne pas le rétrograder
en réserve, ne pas « corriger » le protocole sur ce point.

## 3. Hiérarchie des sources d'avis

Par fiabilité décroissante. C'est le point méthodologique central du protocole
(étape 5).

| Source | Sollicitation par l'éditeur | Poids |
|---|---|---|
| Trustpilot | Rare, avis spontanés | **Fort** |
| Google Play / App Store | Aucune | **Fort** |
| Reddit, forums métier, groupes Facebook | Aucune | **Fort** |
| Capterra / G2 / GetApp | Massive, campagnes d'éditeurs, parfois avec contrepartie | Faible |
| Comparateurs français (lebonlogiciel, logiciels.pro, saask, etc.) | Contenu affilié ou éditeur | Nul |

À appliquer strictement :

- **Une note globale élevée sur Capterra ou G2 n'est pas une information.**
- **Un écart entre une note Capterra élevée et des avis Trustpilot négatifs est
  une information de premier ordre** — le noter explicitement.
- **Exhaustivité obligatoire** : chaque avis est lu individuellement. Aucun
  échantillonnage, aucune synthèse à partir des notes globales. Corpus attendu :
  100 à 400 avis par secteur, parfois moins — le volume est faible, c'est
  précisément pourquoi il faut tout lire.
- Un reproche répété trois fois en source forte pèse plus que quinze avis
  5 étoiles en source faible.
- **Identifier l'éditeur de chaque comparatif consulté** (mentions légales,
  footer) et noter le conflit d'intérêt. Un comparatif d'éditeur n'est pas une
  source sur ses concurrents.
- **Corpus < 30 avis** : l'écrire explicitement, et basculer sur la recherche
  primaire — essais gratuits, changelogs jamais mis à jour, écarts entre pages
  marketing et documentation. Un corpus vide autorise à conclure « pas de
  données publiques — vérification terrain requise », jamais « pas de problème
  détecté ».

## 4. Les dix secteurs et leur statut

Codes NAF arrêtés le 30/07/2026 (arbitrages validés par l'utilisateur).
Nomenclature : **NAF rév. 2 (2008)** — seule acceptée par le filtre
`activite_principale`.

| # | Secteur | Codes NAF retenus | Statut |
|---|---|---|---|
| 1 | SYNDICS_GESTION_LOCATIVE | 68.32A, 68.32B | Compté |
| 2 | TRANSPORT_DERNIER_KM | 49.41A, 49.41B, 49.41C, 52.29A | Compté |
| 3A | SECURITE | 80.10Z, 80.20Z, 80.30Z | Compté |
| 3B | PROPRETE | 81.10Z, 81.21Z, 81.22Z, 81.29A, 81.29B | Compté |
| 3C | INTERIM | 78.10Z, 78.20Z, 78.30Z | Compté |
| 4 | AGRICULTURE_VITICULTURE | 01.11Z, 01.13Z, 01.19Z, 01.21Z, 01.24Z, 01.25Z, 01.41Z, 01.43Z, 01.45Z, 01.46Z, 01.47Z, 01.50Z, 01.61Z, 01.62Z, 01.63Z, 01.64Z, 11.02A, 11.02B | Compté |
| 5 | INDUSTRIE_GMAO_MAINTENANCE | 33.11Z, 33.12Z, 33.13Z, 33.14Z, 33.19Z, 33.20A, 33.20B, 33.20C, 33.20D, 71.20B | Compté — **prestataires de maintenance uniquement**, pas les industriels utilisateurs |
| 6A | ASSOCIATIONS | 88.10A, 88.91A, 88.99A, 88.99B, 93.12Z, 93.19Z, 94.11Z, 94.12Z, 94.20Z, 94.91Z, 94.92Z, 94.99Z | Compté |
| 6B | COLLECTIVITES | 84.11Z, 84.12Z, 84.13Z | Compté |
| 7 | CABINETS_COMPTA_JURIDIQUE | 69.10Z, 69.20Z | Compté |
| 8 | RSE_VSME_QUESTIONNAIRES_FOURNISSEURS | — | **Hors des dix. Dimensionnement `INCONNU`.** Ce n'est pas un secteur NAF : la cible est transverse. Aucun proxy comparable ne doit être inventé. À traiter en dernier. |

**Codes exclus définitivement** (arbitrage du 30/07/2026, ne pas les
réintroduire) : `68.31Z` (agences immobilières — transaction, pas gestion),
`49.42Z` (déménagement), `52.29B` (affrètement), `53.20Z` (autres activités de
poste et de courrier), `70.22Z` (conseil de gestion — trop hétérogène).
Également hors périmètre : `68.10Z`, `68.20A`, `68.20B` (bailleurs et marchands
de biens, pas gestionnaires), `53.10Z`.

## 5. Pièges de l'API `recherche-entreprises.api.gouv.fr`

Tous vérifiés. Détail et preuves : `NOTE_METHODE_API_ET_CODES_NAF.md` § 2.

| Piège | Effet si ignoré |
|---|---|
| **Plafond dur à 10000** sur `total_results` | Un secteur massif est lu comme un secteur de 10 000 cibles |
| **Entreprises cessées incluses par défaut** | Gonflement jusqu'à ~2,4× (80.30Z : 2809 brut = 1153 actives + 1656 cessées). **Toujours `etat_administratif=A`** ; valeurs valides : `A`, `C` |
| **`departement` ne filtre pas sur le siège** | Il matche *tout établissement* de l'unité légale. Sommer les départements double-compte chaque réseau (LAMY = 370 établissements). **Axe interdit dans tout comptage** |
| **Paramètres inconnus silencieusement ignorés** | `&zzzbogus=1` ne déclenche aucune erreur. Un filtre mal orthographié produit un chiffre faux et crédible |
| **Nomenclature NAF** | `activite_principale` n'accepte **que la NAF rév. 2 (2008)**. Un code 2025 (`68.32H`) est rejeté |
| **`activite_principale_naf25` n'est pas un filtre** | Utilisé seul, l'API répond « Veuillez indiquer au moins un paramètre de recherche ». C'est un champ de **sortie** uniquement |
| **Deux nomenclatures en sortie** | Chaque résultat porte `activite_principale` (2008) *et* `activite_principale_naf25` (2025). Ne pas les confondre |
| **Aucun libellé dans l'API** | Ni libellé NAF, ni libellé de forme juridique. Ils viennent d'INSEE |
| **Département 20 n'existe pas** | Corse = `2A` / `2B`. Une boucle `01..95` produit une erreur 400 |
| **Latence très irrégulière** | Mesuré le 30/07/2026 sur 12 requêtes séquentielles identiques : 12/12 réussies, latence médiane **0,22 s**, maximum **40,3 s**. Aucun blocage, aucun HTTP 429 — mais des décrochages de plusieurs dizaines de secondes. Sous concurrence, l'API renvoie en plus des réponses **non-JSON**. Tout appel doit donc avoir `timeout` ≥ 90 s, retry + backoff, et vérifier que `total_results` est un entier. **Ne jamais déduire un blocage d'une commande lente : le mesurer** |
| **La liste séparée par virgules donne un `total_results` FAUX** | `tranche_effectif_salarie=01,02,…` est documentée par la spec OpenAPI et filtre réellement, mais son décompte est erroné d'environ 0,5 %, **dans les deux sens**. Établi par énumération exhaustive de 80.10Z : annoncé 3461, réel 3445 (= somme des 9 requêtes par tranche unique, elle exacte). **Ne jamais publier un chiffre issu d'une requête à liste** |

### Paramètres et valeurs valides

- `etat_administratif` : `A`, `C`
- `tranche_effectif_salarie` : `NN, 00, 01, 02, 03, 11, 12, 21, 22, 31, 32, 41, 42, 51, 52, 53`.
  Champ de **niveau SIREN**, partition mutuellement exclusive. Libellés officiels :
  `https://raw.githubusercontent.com/annuaire-entreprises-data-gouv-fr/search-api/main/app/labels/tranches-effectifs.json`
  (référencé par la spec OpenAPI de l'API). **Un décompte se fait par requêtes à
  tranche unique, sommées — jamais par une requête à liste** (cf. tableau ci-dessus).
- `per_page` : maximum **25**. Énumérer un code coûte donc `ceil(n/25)` requêtes.
- Spec OpenAPI complète : `https://recherche-entreprises.api.gouv.fr/openapi.json`.
  Elle liste des filtres absents de la note (`est_association`,
  `est_collectivite_territoriale`, `est_ess`, `ca_min`/`ca_max`, `id_convention_collective`…).
  **Attention** : comme `departement`, les axes géographiques (`region`, `code_postal`,
  `code_commune`, `epci`) filtrent sur les **établissements** — inutilisables pour un
  décompte d'unités légales.
- `nature_juridique` : 260 valeurs, liste exhaustive renvoyée par le message
  d'erreur sur valeur invalide.
- `categorie_entreprise` : `GE`, `PME`, `ETI` (`PME` et `ETI` plafonnent tous deux).

### Libellés de forme juridique — réserve levée

La réserve du § 2.5 de la note est **fermée**. Source :
`https://xml.insee.fr/schema/cj-enum.html`, consultée le 30/07/2026 ; chaque
code porte son libellé dans l'attribut `dc:title` (307 codes : 9 de niveau 1,
44 de niveau 2, 254 de niveau 3).

- **`6540` = « Société civile immobilière »** — confirmé. Le constat du § 2.5
  (68.32A dominé par les SCI) est donc établi et non plus supposé.
- `5499` = Autre société à responsabilité limitée · `5710` = Société par
  actions simplifiée (SAS) · `5202` = Société en nom collectif ·
  `5385` = Société d'exercice libéral en commandite par action ·
  `6560` = Autre société civile coopérative · `9220` = Association déclarée.
- **Deux écarts entre l'énumération INSEE et l'API, à connaître :**
  - `5720` (SASU) figure dans l'énumération INSEE mais est **rejeté** par
    l'API. Ce n'est pas une erreur de saisie.
  - `1000` est **accepté** par l'API mais **absent** de `cj-enum.html`. Son
    libellé reste donc `INCONNU` au regard de la source retenue.

## 6. Réserves ouvertes

- **Réutilisation du code de l'app BTP** (champ du barème de score) : la valeur
  reste `INCONNU`. Aucune information n'a jamais été fournie sur cette
  application ; le prompt annoncé sur ce point n'est pas arrivé. **Le barème,
  lui, est connu** (protocole, § 5 du fichier de sortie) :
  **aucune = 0, partielle = 2, forte = 3.** Renseigner ce champ exige une
  description de l'app BTP — ne pas le déduire du secteur, ne pas le laisser à 0
  par défaut en faisant passer une absence d'information pour une absence de
  réutilisation.
- **Le plafond de 10000 limite le barème, pas l'éliminatoire.** Il n'empêche
  pas de trancher le seuil de 3 000, mais il peut empêcher de distinguer les
  paliers hauts du barème. La cible restreinte aux tranches 01–32 passe
  toutefois largement sous le plafond sur la quasi-totalité des codes.
- **Cinq cellules de tranche restent plafonnées** : `81.10Z`/01, `01.11Z`/01,
  `94.99Z`/01, `93.12Z`/01, `84.11Z`/02. Elles rendent minorants les totaux des
  secteurs 3B, 4, 6A et 6B. Méthode de levée connue et validée : sous-partition
  par les 260 valeurs de `nature_juridique`, soit 1 300 requêtes. Aucune
  élimination n'en dépend. État exact dans `recherche/PREFILTRE_NAF.md`,
  § « Cellules plafonnées ».
- **Biais NAF à vérifier avant de conclure sur un secteur** : 94.99Z
  (associations dormantes), 84.11Z (petites communes sans budget logiciel).
  Le cas 68.32A est **résolu** : les SCI ne pèsent que 89 unités sur 4 433 dans
  la cible 01–32 (2,0 %), une SCI n'ayant pas de salarié. Le filtre d'effectif
  évacue ce biais ; ne pas le reporter comme s'il subsistait.
- **Aucune donnée d'étape 2 à 6 n'existe.** Aucun éditeur, aucun avis, aucune
  contrainte réglementaire n'a été recherché.

## 7. Git — `main` uniquement

Règle posée par l'utilisateur le 30/07/2026, **postérieure** au PR #1. Ce PR
était le rapatriement d'un fork après un HTTP 403, pas une session parallèle :
son contenu est acquis et ne doit pas être rejoué.

- **`main` uniquement. Jamais de branche de travail, jamais de PR.**
- **Si un `push` échoue : le signaler et s'arrêter.** Ne pas forcer, ne pas
  rebaser, ne pas contourner. Un push rejeté protège du travail distant qu'on
  n'a pas en local — c'est déjà arrivé le 30/07/2026.
- `git fetch` avant toute opération d'écriture git. L'état du distant constaté
  dans un fichier de documentation est un instantané, pas une vérité durable.
