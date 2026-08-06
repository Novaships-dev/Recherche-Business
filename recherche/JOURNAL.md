# JOURNAL

Journal de bord chronologique. Une entrée par session. On y consigne les
décisions, les vérifications, et surtout **ce qui a été trouvé faux**.

Règle : ce fichier ne se réécrit pas. On ajoute en bas.

---

## 29/07/2026 — Session 1 : méthode API et codes NAF (étape 1, préparation)

Livrable : `NOTE_METHODE_API_ET_CODES_NAF.md` (racine).
Aucun comptage produit. Aucun fichier secteur.

### Établi

- **Le `total_results` de l'API plafonne à 10000.** Preuve : 68.20B annonce
  10000, la somme de ses tranches d'effectif donne ≥ 25 146.
- **Les entreprises cessées sont incluses par défaut.** 80.30Z : 2809 brut
  = 1153 actives + 1656 cessées. `etat_administratif=A` est obligatoire.
- **`departement` ne filtre pas sur le siège** mais sur n'importe quel
  établissement. Axe abandonné définitivement.
- **Les paramètres inconnus sont silencieusement ignorés** (`&zzzbogus=1`).
  Tout paramètre doit être validé par une valeur absurde.
- **68.32A est dominé par une forme juridique unique** (code 6540), qui écrase
  toutes les formes commerciales réunies.
- Libellés officiels des 71 codes NAF candidats relevés sur insee.fr.

### Laissé ouvert

- Libellés `nature_juridique` non sourcés → réserve du § 2.5.
- Quatre arbitrages de périmètre en attente (§ 6).

---

## 30/07/2026 — Session 2 : arbitrages, réserve 2.5, et comptage

### Reçu de l'utilisateur

- **Exclusions définitives** : 68.31Z, 49.42Z, 52.29B, 53.20Z, 70.22Z.
- **Secteurs 3 et 6** : comptage séparé → cinq unités de comptage,
  **dix secteurs au total**.
- **Secteur 5 (GMAO)** : prestataires de maintenance uniquement
  (33.11Z→33.20D, 71.20B), pas les industriels utilisateurs.
- **Secteur 8 (RSE/VSME)** : traité en dernier, dimensionnement `INCONNU`,
  aucun proxy à inventer.
- **Définition de la cible** : actives, `tranche_effectif_salarie` ∈ 01..32.
  Remplace la procédure de comptage de la section 5 de la note.

### Deux éléments annoncés mais jamais reçus

1. **Le prompt sur la réutilisation du code de l'app BTP.** Arrivé comme
   placeholder vide `[le prompt sur la réutilisation du code BTP]`. Le champ
   correspondant du barème reste `INCONNU`.
2. **`PROMPT_RECHERCHE_SECTEUR.md`.** Annoncé comme présent à la racine.
   Vérifié : absent de la racine, absent de tout le disque, arbre git propre.
   Jamais ajouté. Conséquence : dans `CLAUDE.md`, deux des trois éliminatoires
   et la hiérarchie des sources d'avis restent `À COMPLÉTER`. Rien n'a été
   inventé pour combler.

### Réserve du § 2.5 — FERMÉE

Source : `https://xml.insee.fr/schema/cj-enum.html`, consultée le 30/07/2026.
307 codes extraits de l'attribut `dc:title` (9 niveau 1, 44 niveau 2,
254 niveau 3).

- **6540 = « Société civile immobilière ».** Le constat « 68.32A est noyé de
  SCI » est donc établi, plus supposé.
- Deux écarts entre l'énumération INSEE et l'API, tous deux vérifiés :
  - `5720` (SASU) existe chez INSEE mais est **rejeté** par l'API.
  - `1000` est **accepté** par l'API mais **absent** de `cj-enum.html` : son
    libellé reste `INCONNU` au regard de la source retenue.

### Trouvé faux dans la note de la session 1

> **Le § 2.4 de la note affirme que la partition par tranche d'effectif est
> exacte. C'est vrai des requêtes par tranche unique, mais un piège nouveau a
> été trouvé à côté.**

`tranche_effectif_salarie` **accepte une liste séparée par virgules**
(`01,02,…,32`), en OU logique. Elle dédoublonne (`01,01` = `01`) et est
insensible à l'ordre. C'était tentant : une requête au lieu de neuf.

Validée d'abord sur 80.30Z — liste = 59 = somme des 9 tranches, écart nul.
**Cette validation était trompeuse : elle portait sur un effectif trop petit.**

Sur les codes plus volumineux, la liste **désaccorde avec la somme des tranches,
et dans les deux sens** : 68.32A +32, 80.10Z +16, 01.61Z +52 ; 49.41A −56,
78.20Z −45, 01.41Z −29. Le double sens excluait l'explication du chevauchement.

Diagnostic par énumération exhaustive de 80.10Z (139 pages, `per_page=25`) :

| Mesure | Valeur |
|---|---|
| `total_results` de la requête liste | 3461 |
| Lignes réellement énumérées | 3445 |
| SIREN distincts | **3445** |
| Doublons | 0 |
| Résultats hors tranches 01–32 | 0 |
| Somme des 9 requêtes par tranche unique | **3445** |
| Ventilation énumérée vs API, tranche par tranche | **identique sur les 9** |

**Conclusion : la somme des 9 requêtes par tranche unique est exacte ; c'est le
`total_results` de la requête à liste qui est faux.** L'erreur est de l'ordre
de 0,5 % et va dans les deux sens — assez petite pour passer inaperçue, assez
grande pour déplacer un secteur d'un palier de barème.

**Règle retenue : ne jamais utiliser la liste séparée par virgules pour publier
un décompte.** Neuf requêtes par code, sommées. La liste ne sert qu'à détecter
une incohérence.

Leçon de méthode : valider une optimisation de requête sur un cas où
l'effectif est petit ne prouve rien. Le contrôle doit porter sur un volume
comparable à celui de l'usage réel.

### Autres vérifications de la session

- **`per_page` est plafonné à 25** (message d'erreur explicite). L'énumération
  d'un code coûte donc `ceil(n/25)` requêtes.
- **`activite_principale` filtre bien sur le code de l'unité légale**, pas sur
  ses établissements — contrairement à `departement`. Vérifié sur 300 résultats
  (80.10Z, 68.32A, 49.41B) : 300/300 portent exactement le code demandé.
  **Additionner les codes d'un secteur ne double-compte donc pas.**
- **`per_page` est plafonné à 25**, et les axes géographiques (`region`,
  `code_postal`, `code_commune`, `epci`) filtrent sur les établissements comme
  `departement` : aucun ne peut servir de partition. `nature_juridique` reste le
  seul axe exclusif et exhaustif disponible.
- **Les SCI ne polluent plus 68.32A une fois la cible appliquée.** Mesuré :
  `nature_juridique=6540` sur les 9 tranches donne 74+11+2+2+0+0+0+0+0 = **89**,
  sur 4 433 cibles, soit **2,0 %**. Une SCI n'a pas de salarié, donc la
  restriction aux tranches 01–32 l'exclut mécaniquement. La réserve du § 2.5 de
  la note est donc doublement fermée : le libellé 6540 est sourcé, et le biais
  qu'elle signalait ne s'applique pas à la cible retenue.

### Une erreur que j'ai commise en cours de session, et sa correction

Trois scripts de requêtes tournaient en parallèle. Tout est devenu très lent, la
sous-partition des cellules plafonnées n'avançait plus, et une commande `curl` de
contrôle n'a pas rendu la main en 120 s. **J'en ai conclu que l'API m'avait
bloqué, et je l'ai écrit dans les trois livrables.**

C'était faux. Cette même commande `curl` avait en réalité répondu **HTTP 200 en
0,24 s** — je l'ai vu en relisant sa sortie. Mesure faite ensuite,
proprement, sur 12 requêtes séquentielles identiques :

| Mesure | Valeur |
|---|---|
| Requêtes réussies | **12 / 12** |
| Latence médiane | **0,22 s** |
| Latence minimale | 0,06 s |
| Latence maximale | **40,32 s** |

**Il n'y a pas de blocage.** Il y a une latence très irrégulière, avec des
décrochages de plusieurs dizaines de secondes, et des réponses non-JSON sous
concurrence. Le § 2.6 de la note (« aucune limitation rencontrée en séquentiel »)
est donc à nuancer, pas à contredire.

Les trois fichiers ont été corrigés. Deux leçons :

1. **Ne pas lancer plusieurs campagnes de requêtes concurrentes sur la même
   API.** Elles se privent mutuellement de débit, et le backoff transforme le
   problème en simple lenteur, donc invisible.
2. **Un diagnostic est une mesure, pas une impression.** « La commande n'a pas
   répondu » n'est pas « le serveur ne répond pas ». La règle du repo qui interdit
   de publier un chiffre non mesuré vaut aussi pour les causes, pas seulement pour
   les nombres.

### Produit

- `CLAUDE.md`
- `recherche/JOURNAL.md` (ce fichier)
- `recherche/PREFILTRE_NAF.md` — 62 codes NAF, 10 secteurs, 9 tranches par code.
  Journal d'audit complet des requêtes conservé hors repo pendant la session.

---

## 30/07/2026 — Session 3 : étapes 2 à 6 sur GMAO / MAINTENANCE (prestataires)

Premier secteur instruit au-delà de l'étape 1.

### Trouvé faux dans le journal de la session 2

> **L'entrée du 30/07 affirme : « Il n'y a pas de blocage », « Aucun blocage,
> aucun HTTP 429 ». C'est contredit par la mesure.**

Deux **HTTP 429 Too Many Requests** obtenus le 30/07/2026 sur
`recherche-entreprises.api.gouv.fr`, en appels **séquentiels**, sans aucune
concurrence, avec l'en-tête **`Retry-After: 4`**. Les deux ont été suivis d'un
succès à la reprise, sans autre changement que le délai.

L'entrée de la session 2 n'est pas réécrite : elle était exacte pour ce qu'elle
mesurait — 12 requêtes séquentielles identiques, 12/12 réussies. Elle en tirait
une conclusion trop large. **Le plafond de débit existe ; il ne s'était pas
manifesté sur ce protocole de mesure.** La leçon de la session 2 tient toujours
(un diagnostic est une mesure), et elle s'applique ici à sa propre conclusion :
« je n'ai pas rencontré de 429 » n'est pas « il n'y a pas de 429 ».

Conduite à tenir : respecter `Retry-After`, garder le séquentiel, et ne pas
conclure d'une absence d'erreur sur 12 appels qu'aucune limite n'existe.

### Deux pièges de données découverts sur le champ `finances` de l'API

1. **`ca: 0` ne signifie pas « zéro », mais « non renseigné ».** ADALGO
   (Organilog, SIREN 804963957) publie un exercice 2025 avec `ca` = 0 et
   `resultat_net` = 216 363 €. Une société de 20 à 49 salariés dégageant ce
   résultat n'a pas un chiffre d'affaires nul. Même famille de piège que le
   plafond à 10000. À publier `INCONNU`.
2. **`finances: null` ne signifie pas « pas d'activité », mais « comptes non
   publiés ou confidentiels ».** C'est le cas de PRAXEDO (479788689), 100 à 199
   salariés. La FAQ de l'Annuaire des Entreprises l'explique : une PME peut
   demander que ses comptes restent confidentiels. Corroboré par societe.com,
   qui s'arrête à l'exercice 2014 pour la même société.

### Méthode qui fonctionne pour l'étape 3

`pappers.fr`, `verif.com` et `infogreffe.fr` renvoient **HTTP 403** au robot.
`lesechos.fr` **bloque explicitement le crawler**. La voie qui marche :

```
mentions légales de l'éditeur  →  SIREN
  →  https://recherche-entreprises.api.gouv.fr/search?q=[SIREN]
  →  champ "finances" (base des comptes annuels INPI, republiée par le
     ministère de l'Économie sur data.gouv.fr)
```

Source d'État, opposable, et déjà autorisée dans ce repo.

### Le fait structurel du secteur : Nomadia consolide

`NOMADIA GROUP` (SIREN 884911116), holding créée le 06/07/2020, détenue par
`NEREUS TOPCO` (953661816). Au moins dix filiales identifiées dans l'Annuaire.
Chronologie des rachats, d'après fusacq.com et cfnews.net, consultés le
30/07/2026 :

| Date | Opération |
|---|---|
| printemps 2021 | Fusion de **Geoconcept**, **Danem** et **B&B Market** → Nomadia |
| 2023 | **Synchroteam** |
| 2024 | **Nomadvantage**, **Coredinate** (Allemagne, présence DACH) |
| annoncé le 24/02/2025 | **7Opteam** (fondée 2013, 25 experts) et **Gazoleen** / Smart Source Development |

**Gazoleen est un acteur direct du segment cible** : interventions de
maintenance en chauffage-climatisation, « plus de 1 000 entreprises clientes ».

Le CA **consolidé** du groupe reste `INCONNU`. Les 4 705 941 € de CA 2024 de la
holding sont ses comptes **sociaux** — des honoraires de gestion, pas
l'activité du groupe. Ne jamais les présenter comme le CA de Nomadia.

### Ce que Reddit rend

**Rien.** `site:reddit.com` sur le vocabulaire GMAO et gestion d'intervention ne
renvoie aucun résultat Reddit. Consigné tel quel, non compensé par une
surpondération de Capterra.

### Une limite de source annoncée avant d'être contournée

L'App Store FR de Praxedo affiche **918 avis, 4,5/5**, mais la page web n'en
expose que quatre : **l'App Store web ne pagine pas les avis**. Un volume
annoncé mais illisible se consigne comme tel. L'étape 5 bascule sur les sources
fortes réellement paginables.

### Étape 5 : les quatre sources fortes sont épuisées, corpus = 4

| Source | Résultat |
|---|---|
| Trustpilot | **Aucune fiche n'existe** pour Praxedo, Organilog, Yuman, Bob! Desk |
| Google Play | **Illisible par fetch** — rendu côté client, deux locales tentées |
| App Store | 918 avis annoncés, **4 exposés**, aucune pagination |
| Reddit et forums métier | **Aucun résultat**, aucune discussion de pairs |

**4 avis lisibles**, tous sur un seul éditeur, un par catégorie de reproche. Le
seuil de 30 du protocole n'est pas approché. Bascule en recherche primaire.
Capterra et G2 **volontairement non dépouillés** : ne pas compenser l'absence de
sources fortes par des sources faibles.

Ce que la recherche primaire a rendu, elle : **Bob! Desk se présente comme « le
1er logiciel GMAO gratuit » alors que son offre est un essai de 14 jours**, et
**Praxedo affiche « à partir de 35 € » avec un minimum de 5 utilisateurs**, soit
175 €/mois réels. Deux écarts marketing constatés sur pièces, là où les clients
n'ont rien écrit.

### Réglementaire : la fenêtre, et l'éliminatoire évité

Facturation électronique — **01/09/2026** : toutes les entreprises doivent
pouvoir **recevoir** ; **01/09/2027** : les PME et micro-entreprises doivent
**émettre**. Source : economie.gouv.fr et impots.gouv.fr, 30/07/2026.

**Ce sont les PDP qui sont immatriculées par la DGFiP, pas les logiciels
métier.** Un outil de gestion se connecte à une PDP. L'éliminatoire n° 3 ne se
déclenche donc pas — vérifié explicitement avec les termes `immatriculé` et
`agréé`, parce que le contraire aurait tué le secteur.

### Verdict du secteur

**À CREUSER, 12/18.** Aucun des quatre éliminatoires ne se déclenche. Le point
décisif n'est pas un éliminatoire mais un vide : **il n'existe pas de corpus de
défauts documentés**, et le protocole interdit d'en conclure « pas de problème ».
Livrables : `recherche/GMAO_MAINTENANCE.md` et
`recherche/GMAO_MAINTENANCE_avis.md`.

**L'appel le plus serré a été l'éliminatoire n° 2** : Organilog a bien un palier
permanent à 0 € chez un éditeur établi, mais avec **72 heures d'archivage**. Un
prestataire ne peut pas perdre ses rapports d'intervention en trois jours :
l'offre n'est pas complète, l'éliminatoire ne se déclenche pas. Décision à
réexaminer si Organilog élargit ce palier.

---

## 30/07/2026 — Session 4 : étapes 2 à 6 sur SYNDICS / GESTION LOCATIVE

Étape 1 reprise telle quelle de `PREFILTRE_NAF.md` (4 743), non recomptée.
Contrôle d'intégrité du protocole refait avant de commencer : 400 lignes,
« /18 », « 3 000 », « Trustpilot » et « 48 h » tous présents.

### Le NAF sous-compte — l'écart va dans le sens inverse de celui attendu

C'était la question posée en priorité, et elle pouvait clore le secteur en dix
requêtes. Elle a fait l'inverse : elle l'a élargi.

| Mesure | Valeur | Rapport |
|---|---|---|
| Cible NAF 68.32A + 68.32B, tranches 01–32 | 4 743 | référence |
| Mentions carte G (gestion immobilière), 1.1.2026 | **15 430** | **× 3,25** |
| Mentions carte S (syndic), 1.1.2026 | 5 061 | × 1,07 |

Deux sources indépendantes concordent sur deux dates différentes : tableau UNIS
sourcé CCI France pour 1.1.2024 et 1.1.2025 (15 613 puis 15 437), Journal de
l'Agence pour 1.1.2026 (15 430). Trajectoire de lent déclin, cohérente.

**Cause de l'écart, et elle est structurelle** : `68.31Z` (agences
immobilières) est exclu du périmètre par l'arbitrage du 30/07/2026 parce qu'il
relève de la transaction. Or 41 471 mentions T pour 43 886 cartes — 94 % des
cartes portent la transaction. La gérance est très majoritairement une activité
**seconde** d'une agence classée 68.31Z, pas l'activité principale d'un cabinet
dédié. S'ajoute l'exclusion des tranches `NN` et `00`.

**À retenir pour les secteurs suivants : l'écart NAF / réalité n'a pas de signe
prévisible.** Sur 68.32A les SCI gonflaient le décompte brut (session 2) ; sur
la carte G le NAF le dégonfle d'un facteur 3. Le contrôle par une source métier
indépendante n'est pas une précaution, c'est une nécessité.

Détail de méthode : le tableau CCI n'existait qu'en **image**. Téléchargé puis
lu directement. Une donnée dans un JPEG reste une donnée sourçable.

### Une erreur que j'ai commise, et que l'utilisateur a coupée

En annonçant le plan, j'ai écrit « par exemple 4 743 NAF pour ~2 500 cartes G ».
Ce nombre ne venait de nulle part. L'utilisateur l'a immédiatement interdit
d'usage tant qu'il n'avait pas d'URL. Il avait raison, et la mesure l'a démenti
dans des proportions massives : 15 430, pas 2 500 — et dans l'autre sens.

Un chiffre glissé comme « illustration de raisonnement » est un chiffre de
mémoire déguisé. La règle 2 ne fait pas d'exception pour les exemples.

### Le fait structurel du secteur : deux consolidateurs sous LBO

| Entité | SIREN | CA | Exercice | Groupe |
|---|---|---|---|---|
| SEPTEO ADB (SPI) | 412259715 | **27 393 570 €** | 2024 | Septeo |
| ORISHA TRANSACTION (ex-Immofacile) | 478601826 | **27 394 485 €** | 2020 | Orisha |
| SEIITRA RESEAU | 383003423 | **21 436 821 €** | 2023 | Orisha |
| ORISHA PROPERTY MANAGEMENT | 439737222 | 11 302 722 € | 2023 | Orisha |
| MUST INFORMATIQUE | 410321533 | 8 911 321 € | 2024 | Orisha |
| GERCOP DIGITAL (MOJO.IMMO) | 802055111 | 2 893 277 € | 2023 | Orisha, **cessée** |

Orisha Real Estate a **dépassé 100 M€ de revenus** au T1 2025 après absorption
de Seiitra (CFNews, extrait libre d'un article payant), annonce
« +450 collaborateurs ». Septeo ADB : 3 200 agences, 2 M de lots syndic.

**Éliminatoire n° 4 déclenché** — leader > 30 M€, et trois entités > 20 M€.

### Le piège du comparatif périmé, à consigner

Le comparatif de presse IRC n° 648 (mai 2019, PDF, 21 solutions) présentait
Crypto, Gercop, Seiitra, ICS et SPI comme cinq concurrents distincts. En 2026,
**Seiitra Réseau et Gercop Digital ont le même président (TANGO BIDCO) et le
même commissaire aux comptes (Grant Thornton)** — établi par le champ
`dirigeants` de l'API, pas par la presse.

**Compter les marques revient à surestimer le nombre d'acteurs.** Un comparatif
de logiciels de six ans ne décrit plus une concurrence, il décrit un
portefeuille. Toujours recouper la marque par le SIREN et le dirigeant.

Autre piège du même document : sa colonne « Atouts de la solution » est
manifestement de la copy fournie par les éditeurs. C'est un annuaire payant, pas
un banc d'essai. Utilisable pour **lister**, jamais pour **juger**.

### Les deux pièges du champ `finances` se sont redéclenchés

- **VILOGI** (528341571) : `ca` = 0 en 2024, résultat net **143 574 €**.
  → CA **INCONNU**, pas « zéro ». Principal indépendant survivant du segment
  professionnel : son chiffre manque, et c'est une vraie lacune.
- **UBLO** (888056751) : `ca` = 0 en 2023, résultat net **−316 165 €**.
  → **INCONNU**.

La méthode d'étape 3 de la session 3 a de nouveau fonctionné telle quelle :
mentions légales → raison sociale + SIREN → champ `finances`. Septeo ADB s'est
résolu en deux requêtes par ce chemin.

Confirmation supplémentaire du § 5 : `q=NETTY`, `q=INCH`, `q=LA SOLUTION CRYPTO`,
`q=POWIMO` ne rendent **aucune** entité pertinente. `POWIMO` rend
`total_results: 0`. Un nom de marque n'est pas une dénomination légale.

### Un MBO/LBO de plus, et la règle tient

Orisha (ex-DL Software) est sous LBO du fonds américain TA Associates depuis
avril 2021, puis repris via **TANGO BIDCO** (930667019, créée le 03/07/2024).
Consigné comme **changement d'actionnariat**, jamais comme levée — arbitrage du
30/07/2026 sur le cas Praxedo, appliqué à l'identique.

### Une levée de 35 M€ que je n'ai délibérément pas retenue

Matera a levé **35 M€** le 25/05/2021 (Bpifrance, Mubadala, Burda). Au-dessus du
seuil de 5 M€, donc tentante pour l'éliminatoire n° 4. **Écartée** : Matera ne
vend pas de logiciel aux syndics professionnels, il **remplace** le syndic
auprès de la copropriété. Ses 35 M€ ne financent pas une force de vente dirigée
contre un éditeur, ils réduisent le nombre de clients possibles. Menace sur la
cible, pas concurrent produit.

L'éliminatoire se déclenche de toute façon sur une mesure plus nette — le CA du
leader — donc rien ne dépendait de cet arbitrage. Il est consigné pour que le
raisonnement soit rejouable, pas parce qu'il a changé le verdict.

### Trois familles de logiciels, pas deux

À distinguer systématiquement, comme les deux familles du secteur GMAO :

1. **Syndic de copropriété professionnel** (carte S, 5 061) — Septeo SPI Syndic,
   Seiitra/Thétrawin, Vilogi, Gercop Y15, Timci.
2. **Gestion locative / gérance professionnelle** (carte G, 15 430) — Septeo SPI
   Gestion Locative, Orisha Property Management, Vilogi, Ublo.
3. **Syndic bénévole et bailleur particulier** — hors cible NAF et hors carte,
   mais c'est **là que vivent les offres gratuites** (Diacamma, open source
   auto-hébergé) et les prix bas (Copriciel 120 € TTC/an).

L'éliminatoire n° 2 ne se déclenche pas, parce qu'aucune gratuité ne vise le
professionnel. Vérification faite : Coprolab corrige explicitement que « la
mention Copriciel gratuit qui circule ne correspond plus à l'offre 2026 ».

### Réglementaire : éliminatoire évité, et une fenêtre qui existe

**Éliminatoire n° 3 : NON.** Source primaire, décret n° 2019-502 du 23 mai 2019
sur Legifrance : l'obligation pèse sur **« le syndic professionnel »**, à qui il
impose un *contenu* à mettre en ligne. **Aucune certification, homologation,
agrément ni référencement de l'outil.** Loi ALUR, décret sur le conseil syndical
et extranet obligatoire portent tous sur le syndic, jamais sur le logiciel.
Vérifié explicitement, parce que le contraire aurait tué le secteur.

Échéances : les trois paliers du PPT (2023, 2024, 2025) et le DPE collectif
≤ 50 lots (01/01/2026) sont **tous échus**. Restent deux paliers du registre
national d'immatriculation : **février 2027** (décret n° 2025-831 du 19/08/2025)
et **janvier 2028** (arrêté du 23/06/2026, JO du 19/07/2026). Le second tombe à
~18 mois, dans la fenêtre 12-36 mois du barème.

Mais le comparatif IRC de 2019 portait déjà une colonne « Immatriculation »
renseignée chez la grande majorité des 21 solutions. **La conformité
réglementaire n'est pas un angle d'entrée, c'est un prérequis acquis depuis six
ans.**

### Étape 5 : corpus de 30, tout juste, et Trustpilot fermé

Corpus : **30 avis lus un par un**, tous en source forte, tous sur stores.
0 Trustpilot, 0 Reddit, 0 Capterra.

**Trustpilot renvoie HTTP 403 sur 4 URL testées** (matera.eu, www.vilogi.com,
bailfacile.fr, rentila.com), y compris avec un User-Agent de navigateur. Testé
avant d'être annoncé — un « ça n'a pas répondu » n'est pas une mesure (règle 8).
La source la plus haute de la hiérarchie est absente du corpus.

Google Play sert ses avis en JavaScript : WebFetch ne rend que la coquille. Les
20 avis Matera ont été extraits du **JSON embarqué dans la page**, avec note et
horodatage d'origine. Méthode réutilisable pour les secteurs suivants.

Reproche dominant : **bug/fiabilité, 13 occurrences** sur 30 avis.

**Un écart de notation entre deux sources fortes**, ce que le § 3 de CLAUDE.md
n'anticipe pas : Matera affiche 4,8/5 (App Store, 732 avis) et 4,5/5 (Play,
624 avis), mais sur les 20 avis Play réellement lisibles, **9 sont à 1 ou
2 étoiles**, dont quatre en 2025-2026. La note agrégée et le contenu récent ne
disent pas la même chose. Le mécanisme attendu entre Capterra et Trustpilot se
produit ici **à l'intérieur des sources fortes**.

Signal de recherche primaire, plus parlant que le corpus : **les deux
applications Vilogi n'ont pas été mises à jour depuis juillet 2024**, soit deux
ans. Le bug Face ID signalé « depuis plus d'un an » en décembre 2024 n'a pas pu
être corrigé faute de livraison.

### Deux sources perdues, à consigner comme telles

- **Étude comparative de l'Union Sociale pour l'Habitat (avril 2022)** :
  HTTP 403 en WebFetch **et** en curl avec User-Agent navigateur. C'était la
  seule comparaison **indépendante** identifiée — une fédération, sans intérêt
  dans la vente de logiciel. La lacune la plus regrettable de la session.
- **Forum UniversImmo et ARC** : non explorés, budget de requêtes absorbé par
  les étapes 3 et 6. Première piste à ouvrir en cas de réexamen.

Aucune des deux ne change le verdict, qui se joue sur une mesure de CA. Elles
changeraient la finesse du diagnostic produit.

### Verdict du secteur

**NO-GO, éliminé.** Éliminatoire n° 4 (concentration) : leader > 100 M€, trois
entités > 20 M€, deux groupes sous LBO. Les trois autres éliminatoires sont
franchis — volume largement suffisant (15 430), aucune gratuité visant le
professionnel, aucune certification d'État.

Score sur les six champs renseignables : 11/18. Sans effet : les éliminatoires
décident, pas le score. Sections 6 à 9 du fichier de sortie laissées **sans
objet**, conformément au § 2 de CLAUDE.md — « un secteur éliminé est abandonné,
pas noté ».

Livrables : `recherche/SYNDICS_GESTION_LOCATIVE.md` et
`recherche/SYNDICS_GESTION_LOCATIVE_avis.md`.

---

## 30/07/2026 — Session 5 : étapes 2 à 6 sur TRANSPORT DERNIER KM

### L'ordre du protocole a été inversé, et c'est ce qui a payé

Instruction de l'utilisateur en début de session : exécuter **l'étape 6 avant
l'étape 2**. Motif énoncé — « sur les deux secteurs précédents on a payé le plein
tarif avant de trouver le motif d'élimination, autant chercher d'abord là où ça
peut fermer ».

Résultat : le secteur est tombé en **25 requêtes**, sans qu'aucun éditeur, aucun
CA, aucun prix ni aucun avis n'ait eu à être instruit. Les sessions 3 et 4
avaient coûté l'intégralité du protocole pour un NO-GO chacune.

**À généraliser pour les secteurs restants** : quand une hypothèse d'éliminatoire
n° 3 est identifiable dès le plan de campagne, l'étape 6 passe en premier. C'est
la seule étape qui peut conclure seule, et c'est la moins chère.

### Le fait structurel du secteur : eFTI certifie le logiciel, pas l'entreprise

Vérifié sur le texte, comme demandé, et pas sur des articles. Règlement (UE)
2020/1056 :

- **Art. 3, pt 11** — est « développeur de plateforme eFTI » quiconque a
  développé une plateforme « **or for putting that platform on the market** ».
  Un éditeur de logiciel est dedans par définition.
- **Art. 4 § 2** — l'opérateur qui transmet une information réglementaire par
  voie électronique à une autorité « **shall do so on the basis of data processed
  on a certified eFTI platform and, if applicable, by a certified eFTI service
  provider** ».
- **Art. 11** — les organismes d'évaluation de la conformité sont accrédités au
  titre du règlement (CE) 765/2008 ; chaque État désigne une autorité qui publie
  la liste **sur un site officiel de l'État**.
- **Art. 12** — certification **de la plateforme**, marque de certification,
  et **réévaluation obligatoire à chaque révision des spécifications techniques**
  (§ 4).
- **Art. 13** — certification **du prestataire de services**.

Réponse à la question posée par l'utilisateur : **la certification porte sur les
deux**, par deux articles distincts. Et elle porte sur le logiciel lui-même, ce
qui est exactement la formulation de l'éliminatoire n° 3.

### Le point qu'on aurait manqué en s'arrêtant au règlement de 2020

L'annexe I partie B du règlement de 2020 est **vide à l'origine** : elle est
remplie par acte délégué avec les droits nationaux notifiés. Lue seule, elle
laissait croire que le transport intérieur français était hors périmètre et que
seul l'international était visé.

Le **règlement délégué (UE) 2024/2025 du 15 juillet 2024** la remplit. L'entrée
« France » y inscrit **l'article R3411-13 du code des transports** et **l'arrêté
du 9 novembre 1999 relatif aux documents de transport devant se trouver à bord** :
la lettre de voiture nationale. Les 22 323 cibles sont donc concernées, sans
rouler à l'international.

**Règle à retenir : un règlement européen dont une annexe renvoie à des actes
délégués n'est pas lisible sans ses actes délégués.** Le texte de base peut
inverser le sens de la conclusion.

### La date d'échéance, recalculée depuis les textes et non reprise

L'art. 5 § 1 ne donne pas de date : il dit « 30 mois après l'entrée en vigueur du
premier des actes délégués et d'exécution visés aux art. 7 et 8 ». Le règlement
d'exécution (UE) 2024/1942 a été publié au JOUE le **20/12/2024** et entre en
vigueur le vingtième jour suivant, soit le **09/01/2025**. Plus 30 mois =
**9 juillet 2027**.

Ce calcul, fait sur les textes, tombe exactement sur la date annoncée par la
page eFTI de la Commission. Les deux se confirment mutuellement.

### Un second motif d'élimination, indépendant du premier

Fenêtre de lancement à rebours depuis le 9 juillet 2027 : mise en ligne cible au
**9 juillet 2026**, soit **21 jours avant la date de la session**. Le début du
développement est donc passé lui aussi.

Les deux motifs sont autonomes. Lever la certification ne rouvrirait pas le
secteur, et inversement. C'est la première fois qu'un secteur est fermé deux
fois par des causes sans rapport.

### Les deux hypothèses d'éliminatoire de l'utilisateur : une bonne, une écartée

L'utilisateur avait désigné le chronotachygraphe comme « le point qui peut fermer
le secteur ». Il ne le ferme pas. Vérifié sur le texte primaire, l'**arrêté du
6 juillet 2005** n'impose **aucun agrément ni homologation sur le logiciel** de
téléchargement et d'archivage : seulement des fréquences (28 jours carte
conducteur, 95 jours mémoire de masse), une conservation de 365 jours et une
structure de nom de fichier (`.C1B`, `.V1B`). Le seul « organisme agréé » du
texte est un atelier, saisi sur le véhicule en cas d'échec de téléchargement.

Le **registre des transporteurs et la licence de transport intérieur** ne ferment
rien non plus : ils portent sur l'entreprise (honorabilité, capacité
professionnelle, capacité financière), délivrés par le préfet de région.

C'est eFTI qui ferme — le point ajouté au plan de campagne, pas ceux qui étaient
attendus. **À consigner : l'éliminatoire n'était pas là où le secteur le
signalait.**

### EUR-Lex est fermé au robot — et le contournement est validé

`eur-lex.europa.eu` renvoie **HTTP 202 avec un corps vide** sur les formats HTML
et PDF, cinq tentatives, en `curl` comme en `WebFetch`. Comportement
d'anti-robot, à ranger avec les 403 de `pappers.fr`, `verif.com` et
`infogreffe.fr`.

**Voie d'accès au droit de l'Union pour ce repo, testée et opérationnelle :**

```
http://publications.europa.eu/resource/celex/[CELEX]
  -H "Accept: application/xhtml+xml"
  -H "Accept-Language: fra"
```

L'API cellar de l'Office des publications sert le texte officiel intégral, en
français, en une requête. Elle a rendu 32024R2025, 32025R2243 et 32024R1942.
Attention : `Accept: text/html` et `Accept: application/pdf` renvoient **404** —
seul `application/xhtml+xml` fonctionne.

Second recours, utilisé pour le règlement de base 32020R1056 :
`legislation.gov.uk/eur/2020/1056/adopted`, version « as adopted by EU »,
miroir d'État réutilisé sous décision 2011/833/UE. Valable pour les textes
antérieurs au 31/12/2020 uniquement.

### Un piège de source, évité de justesse

Le premier PDF récupéré, annoncé par la recherche comme le règlement eFTI et
hébergé sur `transport-community.org`, s'est révélé être un **diaporama de
présentation** de novembre 2021. 12 pages, 7 980 caractères — soit 665 caractères
par page, densité incompatible avec un texte juridique. C'est ce ratio qui a
déclenché la vérification.

**Contrôle à systématiser** : après extraction d'un PDF censé être un texte de
loi, mesurer les caractères par page avant de lire. Un texte réglementaire tourne
autour de 3 000 ; en dessous de 1 500, c'est autre chose.

### Réutilisation du code de l'app BTP : le champ n'est plus INCONNU

Les briques ont été communiquées par l'utilisateur en début de session. Sur ce
secteur, **trois transposent pleinement** — Factur-X, suivi documentaire des
sous-traitants avec vigilance en cascade, application terrain hors-ligne — une
quatrième transpose techniquement mais atterrit dans la zone soumise à
certification (génération de documents et signature = lettre de voiture), une
transpose à moitié (devis oui, situations de travaux non : le transport se
facture à l'envoi, pas à l'avancement), une pas du tout (corps de métier BTP).

**Note 3.** Meilleur score de réutilisation obtenu à ce jour, sur un secteur
fermé. À consigner comme tel : la réutilisabilité du code n'ouvre pas un marché.

### Verdict du secteur

**NO-GO, éliminé.** Éliminatoire n° 3 (certification d'État sur le logiciel
métier) : règlement (UE) 2020/1056, art. 12 et 13, avec le droit français notifié
à l'annexe I partie B par le règlement délégué (UE) 2024/2025. Second motif
indépendant : fenêtre de lancement fermée depuis le 9 juillet 2026.

Éliminatoire n° 1 franchi (22 323 cibles, 7,4 × le seuil). **Éliminatoires n° 2
et n° 4 non vérifiés** — étapes 2, 3 et 4 non exécutées. À ne pas reporter comme
« franchis » dans la synthèse.

Score : non calculable. Six points acquis sur les trois champs instruits
(cibles 2, échéance 1, réutilisation BTP 3), trois champs `INCONNU`. Le total
sur 18 ne doit pas être publié ni comparé.

Livrables : `recherche/TRANSPORT_DERNIER_KM.md` et
`recherche/TRANSPORT_DERNIER_KM_avis.md`.

## 30/07/2026 — Session 6 : étapes 6, 3, 2 et 4 sur SÉCURITÉ PRIVÉE

Premier secteur traité entièrement dans l'ordre inversé du § 0 point 3 de
`CLAUDE.md` : étape 6, puis étape 3, puis étapes 2 et 4. Étape 1 non recomptée
(4 775 cibles, reprises de `PREFILTRE_NAF.md`). 58 requêtes.

### L'ordre inversé a bien fonctionné, mais pas comme prévu

Sur TRANSPORT, l'étape 6 avait fermé le secteur seule, en 25 requêtes. Ici elle
**n'a rien fermé** — et c'est un résultat utile en soi : elle a coûté environ
25 requêtes pour établir un `NON` solide sur l'éliminatoire n° 3, ce qui a permis
d'aborder l'étape 3 en sachant que la seule question restante était la puissance
de feu des concurrents.

C'est la démonstration que « chercher d'abord là où ça ferme » ne garantit pas
une fermeture précoce, mais borne le coût dans les deux cas.

### Éliminatoire n° 3 : NON — et la méthode qui l'a établi

Le secteur est saturé de contenu réglementaire écrit par des éditeurs de
logiciel. Deux d'entre eux affirment une obligation légale de dématérialisation
**sans citer un seul texte** :

- SEKUR (`LE WEB FRANCAIS SAS`) : « les registres de main-courante doivent être
  numériques, infalsifiables et horodatés », « la transition vers le "Zéro
  Papier" est désormais actée ». Aucun décret, aucun article cité.
- La même affirmation circule sur plusieurs sites d'éditeurs.

**Ce qui a permis de trancher : une convergence contre-intérêt.** Un troisième
éditeur, MC TRACKER, qui aurait exactement le même intérêt commercial à affirmer
l'obligation, écrit l'inverse : « le Code de la sécurité intérieure n'impose pas
de format spécifique ». Recoupé sur Légifrance (art. R631-16 et R631-17, neutres
technologiquement) et sur une analyse d'avocate (Myrina Prestel, cabinet Squair).

**À systématiser** : quand toutes les sources d'un secteur sont en conflit
d'intérêt, chercher celle qui parle **contre** son propre intérêt. C'est la seule
qui a une valeur probante sans source primaire — et elle oriente ensuite la
vérification sur la source primaire.

### Deux erreurs de référence corrigées

1. **Livre III → Livre VI.** La consigne de session situait les activités privées
   de sécurité au livre III du code de la sécurité intérieure. C'est le **livre
   VI** (L611-1 à L648-1, R611-1 à R648-2). Signalé à l'utilisateur, corrigé dans
   le livrable.
2. **« NF 525 étendue aux logiciels de paie » : FAUX.** Affirmation trouvée sur
   plusieurs fermes de contenu. NF 525 vise les systèmes de caisse. Aucune de ces
   pages ne cite de texte. Ne pas propager.

### La CCN ne crée aucune obligation logicielle — distinction posée

Arbitrage de l'utilisateur, appliqué : qu'une convention rende le calcul des
heures complexe **ne crée aucune obligation portant sur l'outil**. L'éliminatoire
n° 3 ne se déclenche que si un texte impose une caractéristique au logiciel.

La CCN IDCC 1351 est objectivement lourde — vacations de 6 à 12 h, 329 h de
contingent annuel, majorations nuit +10 %, dimanche +10 %, férié +100 %, taux
renforcés en sûreté aéroportuaire. Rien de tout cela n'atteint l'outil :
l'obligation de conformité pèse sur l'employeur (Cass., 28/02/2018, responsabilité
maintenue malgré l'externalisation de la paie). **La complexité est un argument de
vente, pas une barrière.**

### Le terme « immatriculé » a un sens unique, et il ne bloque pas

Seul régime d'immatriculation trouvé : la **Plateforme Agréée** (PA, ex-PDP) de
la facturation électronique, immatriculée par la DGFiP — 129 immatriculées
définitivement au 05/05/2026. **Un logiciel métier n'a pas à l'être** : il peut
être un simple opérateur de dématérialisation (OD) raccordé à une PA. Aucune
barrière pour un développeur seul.

À réutiliser tel quel sur les secteurs suivants : la facturation électronique
n'est jamais un éliminatoire n° 3, sauf à vouloir être la plateforme elle-même.

### Éliminatoire n° 4 : DÉCLENCHÉ par une levée, pas par un CA

**SENEF SOFT (529974511) — 6,5 M€, Isatis Capital, 02/05/2023, série A.**

Qualification faite selon le § 2 de `CLAUDE.md` (arbitrage Praxedo). Deux sources
concordantes : *L'Usine Digitale* (« premier financement » d'une société qui
« fonctionne sans lever de fonds depuis 2011 »), *FrenchWeb* (titre « [Série A] »,
emploi des fonds : « renforcer ses équipes, se développer à l'international et
diversifier son offre vers des secteurs connexes »). Argent frais entrant. Ni
MBO, ni LBO, ni OBO, ni cession de titres. **Cela compte.**

**Le point qui a demandé le plus de soin** : l'article de 2023 ne mentionne pas
la sécurité privée — Senef éditait alors Progisap (services à la personne) et
Progiclean (propreté, hôtellerie). La sécurité privée est arrivée **après**, via
Seenet, c'est-à-dire qu'elle est précisément l'un des « secteurs connexes » que
la levée devait financer. Vérification faite par les mentions légales de
`seenet-securite.fr` : **même SIREN, 529974511**. L'éditeur du produit sécurité
est bien celui qui a levé.

**Leçon** : une levée de fonds antérieure à l'entrée sur le secteur ne sort pas
l'acteur du périmètre de l'éliminatoire — elle peut au contraire être ce qui a
financé cette entrée. Vérifier l'identité d'entité par les mentions légales, pas
la chronologie des communiqués.

### Ce que le champ `dirigeants` a rendu

Méthode du § 5 appliquée dans l'ordre, `dirigeants` avant `finances` :

- **KELIO (538209594) a pour président BODET SA (775610504)** — personne morale.
  Un seul groupe, pas deux acteurs. CA non sommés (règle 6).
- **HOROQUARTZ (399243922)** : `IKOMA SUSUMU` administrateur et `PEIRSMAN BERT`
  président du conseil — gouvernance étrangère sur une SA française. Confirme le
  rattachement au groupe japonais **AMANO** (depuis 2008, ~5 000 personnes).
  Une signature de contrôle étranger lisible dans le seul champ `dirigeants`.
- **SEKUR** : président = `HOLDING COCORICO` (890022023, NAF 66.30Z, 2020).
- **AEXAE (394128466)** est elle-même en **64.20Z**, code de holding, pas
  d'édition. Dernier exercice publié : **2021**.

### Deux pièges de nommage confirmés, et un nouveau

- « Bodet Software » n'existe pas : la société est **KELIO** depuis le 16/09/2022.
- « Hector Solution » n'existe pas : l'éditeur est **VIGIFORMATION** (991136508),
  en NAF **85.59B** — formation, pas édition.
- **Nouveau** : VIGIFORMATION s'annonce « entreprise individuelle » dans ses
  mentions légales alors que l'API porte un « Président de SAS ». Contradiction
  non tranchée, consignée en zone d'ombre. Les mentions légales ne sont pas
  toujours exactes non plus — les croiser avec l'API, systématiquement.

### `ca: 0` de nouveau rencontré, et de nouveau écrit INCONNU

`SENEF SOFT` : `{"2020": {"ca": 0, "resultat_net": 309145}}` pour une société de
50 à 99 salariés. Troisième occurrence du piège documenté au § 5 de `CLAUDE.md`.
Écrit `INCONNU`. Le fondateur a par ailleurs refusé de communiquer son CA à la
presse en 2023 tout en annonçant vouloir « dépasser 20 M€ sous deux ans » —
annonce, pas chiffre, non repris comme donnée.

### Un secteur d'entrants très récents

`MC TRACKER` créée le **12/02/2026**, `VIGIFORMATION` le **03/09/2025** — moins
d'un an chacune, aucun compte publié. Sept éditeurs verticaux identifiés, dont
deux nés dans l'année. La barrière technique est basse, ce qui est une mauvaise
nouvelle et non une opportunité : ce qu'un solo peut construire ici, plusieurs le
construisent simultanément.

### Registre officiel (règle 10) : non mesurable

Le site du CNAPS (`cnaps.interieur.gouv.fr`) a renvoyé `socket hang up` sur
**quatre tentatives** — mesure, pas impression (règle 8). Des sources secondaires
annoncent 12 500 entreprises autorisées ; **non repris**, faute de source primaire.
L'écart registre / NAF reste `INCONNU` pour ce secteur. Ce qui a pu être établi
via la presse spécialisée : 70 000 cartes professionnelles délivrées en 2025,
plus de 300 000 agents habilités.

À reprendre quand le site sera joignable — c'est la seule des quatre sources
externes du § 1 qui ait échoué à ce jour.

### Réutilisation du code de l'app BTP : 3, et pour la première fois sans zone barrée

Quatre briques transposent pleinement : Factur-X, suivi documentaire des
sous-traitants avec contrôle de validité en cascade, application terrain
hors-ligne, **génération de documents et signature**. Une transpose à moitié
(devis oui, situations de travaux non : on facture des heures de vacation, pas un
avancement). Une pas du tout (corps de métier BTP contre qualifications APS /
SSIAP / cynophile).

**Le contrôle du § 6 a été fait, et il passe pour la première fois.** Sur
TRANSPORT, « génération de documents et signature » atterrissait sur la lettre de
voiture, objet même de la certification eFTI — zone barrée. Ici elle atterrit sur
le mémento émargé de l'art. R631-16 et les registres du livre VI, que les textes
laissent explicitement sans format. La brique la mieux ajustée est la n° 2 : le
décret du 26/12/2025 oblige à « vérifier régulièrement la validité des titres »
des salariés, ce qui est exactement le contrôle de validité en cascade.

**Meilleur score de réutilisation obtenu à ce jour, et quatrième secteur d'affilée
où il ne décide rien.** Le § 6 de `CLAUDE.md` se vérifie une quatrième fois.

### Verdict du secteur

**NO-GO, éliminé.** Éliminatoire n° 4 : levée de 6,5 M€ (> 5 M€) par SENEF SOFT,
éditeur présent sur le secteur via Seenet. S'y ajoutent, sans être nécessaires au
verdict, KELIO (83 769 181 € de CA 2024) et HOROQUARTZ (81 459 537 €), tous
secteurs confondus — leur part sur la sécurité privée est `INCONNU`.

**Second motif indépendant : fenêtre de lancement fermée.** L'échéance du décret
n° 2025-1344 tombe le **01/10/2026**, dans deux mois. Pic d'achat (échéance − 6
mois) et mise en ligne cible (échéance − 12 mois) sont tous deux dépassés.

Éliminatoires n° 1 (4 775 cibles), n° 2 (aucune gratuité pérenne) et n° 3 (aucune
certification d'État sur le logiciel) **franchis et vérifiés**. C'est le premier
secteur où les quatre éliminatoires sont instruits sans qu'aucun ne reste
`INCONNU`.

**Étape 5 non menée** — corpus de 0 avis, sans valeur de décision après
déclenchement de l'éliminatoire. À ne pas reporter comme « 0 reproche » dans
`SYNTHESE.md` : la valeur est `INCONNU`.

Score : non totalisé, secteur éliminé. Sept points sur cinq champs renseignés
(cibles 1, prix plancher 2, échéance 1, réutilisation BTP 3, certification 0),
un champ `INCONNU`. Le total sur 18 ne doit être ni publié ni comparé.

Livrables : `recherche/SECURITE_PRIVEE.md` et `recherche/SECURITE_PRIVEE_avis.md`.

## 31/07/2026 — Session 7 : étapes 6 et 3 sur AGRICULTURE / VITICULTURE

Ordre inversé du § 0 point 3 de `CLAUDE.md` : étape 6, puis étape 3. Étape 1 non
recomptée (≥ 72 866 cibles, reprises de `PREFILTRE_NAF.md` § 4). Étapes 2, 4 et 5
non menées. **30 requêtes web et 5 requêtes API.**

Session la moins chère des trois menées dans l'ordre inversé, après TRANSPORT
(25 requêtes) et SÉCURITÉ PRIVÉE (58).

### L'étape 6 n'a pas fermé, l'étape 3 a fermé en une requête

Troisième comportement différent de l'ordre inversé en trois secteurs :

| Secteur | Ce qu'a fait l'étape 6 | Ce qui a fermé | Coût |
|---|---|---|---|
| TRANSPORT | a fermé seule | éliminatoire n° 3 (eFTI) | 25 requêtes |
| SÉCURITÉ PRIVÉE | n'a rien fermé, a établi un `NON` solide | éliminatoire n° 4 (levée 6,5 M€) | 58 requêtes |
| AGRICULTURE | n'a rien fermé, mais a produit le **second motif** du verdict | éliminatoire n° 4 (CA 144,9 M€) | 30 requêtes |

L'étape 3 a déclenché l'éliminatoire sur **la toute première requête API**, celle
sur le SIREN d'ISAGRI. L'hypothèse de l'utilisateur était juste, et l'instruire en
premier a économisé le reste de l'étape.

### Le champ `dirigeants` a rendu deux consolidations sur deux éditeurs

Méthode du § 5 de `CLAUDE.md` appliquée telle quelle, `dirigeants` avant
`finances`, sans requête supplémentaire.

- `ISAGRI` (327733432) → président **`GROUPE ISA`** (379163546), personne morale.
- `SMAG` (430406918) → président **`INVIVO AG`** (801076274), personne morale.

Deux sur deux. Le taux commence à être significatif sur l'ensemble de l'étude :
sur les syndics, `TANGO BIDCO` ; ici, une holding et une union de coopératives.
**Sur ce marché, un éditeur indépendant est l'exception, pas la règle.**

### Un piège nouveau : le champ `nom_complet` déclare le portefeuille

L'API a rendu, sans qu'on le demande :

```
nom_complet: ISAGRI (ISAGRI, AGIRIS, TERRE-NET, SO'NEO, PROMIZE, C2J INFO, I-CONE)
```

**Le champ `nom_complet` liste les noms commerciaux de l'entité.** C'est
l'inverse exact du piège documenté au § 5 de `CLAUDE.md` (« un nom de marque
n'est pas une dénomination légale », qui oblige à passer par les mentions
légales pour aller de la marque vers le SIREN). Ici, une fois le SIREN connu, le
chemin retour est **gratuit** : l'API donne les marques.

À utiliser systématiquement à l'étape 3 : sur un SIREN d'éditeur, lire
`nom_complet` avant de partir chercher des comparatifs. Il a rendu ici en une
ligne ce qu'un comparatif de presse aurait rendu faux (cf. le constat du § 5 sur
le comparatif IRC n° 648).

### Terre-net appartient à Isagri — piège de source majeur

Conséquence directe de la ligne ci-dessus, et elle a failli passer inaperçue :
**Terre-net, l'un des principaux médias agricoles français, est une marque de
l'entité 327733432**, c'est-à-dire d'ISAGRI.

Un article de Terre-net avait été ouvert pendant l'étape 6 pour le calendrier
réglementaire. Le calendrier est factuel et a été recoupé sur Légifrance et sur
la DRAAF, donc rien n'est à retirer. Mais **tout contenu de Terre-net portant sur
un logiciel agricole est publié par le leader du secteur sur ses concurrents** :
poids **nul** au sens du § 3 de `CLAUDE.md`. Consigné dans le fichier d'avis pour
la prochaine session qui rouvrirait le secteur.

C'est la deuxième fois que la propriété d'un média ou d'un comparatif change la
lecture d'une source. La règle générale se confirme : **identifier l'éditeur du
site avant de lire son contenu, pas après.**

### L'État en concurrent gratuit — une forme d'éliminatoire n° 2 non prévue

Le fait le plus lourd de l'étape 6, et il ne vient d'aucun éditeur.

> « Le ministère de l'agriculture développe en partenariat avec chambre
> d'agriculture France un outil numérique accessible à tous et qui sera mis à
> disposition courant 2026 gratuitement. » — DRAAF Centre-Val de Loire

Les Chambres d'agriculture France le disent **« opérationnel en janvier 2027 »**,
c'est-à-dire **à la date exacte de l'obligation** qu'il sert à remplir (registre
phytosanitaire au format électronique, arrêté du 24/12/2025).

**Le protocole ne prévoit pas ce cas.** Son éliminatoire n° 2 vise « une offre
gratuite complète et crédible chez un **acteur établi** » — donc un éditeur. Ici
le fournisseur gratuit est l'État, et il est aussi l'auteur de l'obligation.

Ce qui a été écrit dans le livrable, et qu'il faut tenir : **`INCONNU`, avec un
signal fort documenté.** Pas « franchi », pas « déclenché ». Le périmètre
fonctionnel de l'outil n'est pas publié — registre seul, ou gestion parcellaire
complète ? — et c'est ce périmètre qui déciderait.

**Point de méthode à retenir pour les secteurs restants :** quand une échéance
réglementaire est identifiée à l'étape 6, chercher **dans la même passe** si
l'État accompagne l'obligation d'un outil. Une échéance réglementaire n'est une
opportunité que si personne ne distribue gratuitement le moyen de s'y conformer.
Ce contrôle n'avait été fait sur aucun des quatre secteurs précédents.

### Deux confusions écartées, dont une venue du moteur de recherche

1. **Le moteur a affirmé que l'outil gratuit du ministère « s'appelle
   MesParcelles ».** C'est faux. Les Chambres d'agriculture France présentent
   elles-mêmes MesParcelles comme une **alternative** à l'outil ministériel
   (« ou un logiciel de gestion parcellaire comme MesParcelles »), et
   MesParcelles est payant. La synthèse du moteur a été rejetée et la question
   tranchée sur la page des Chambres. **Une synthèse de moteur de recherche
   n'est pas une source** — elle conflate, et elle conflate au pire endroit.
2. **Les déclarations viticoles ne barrent pas le logiciel.** C'était
   l'hypothèse de fermeture n° 1 en entrant dans l'étape 6. La page officielle
   de la DGDDI n'emploie aucun des termes `agréé`, `certifié`, `homologué`,
   `référencé` pour un intermédiaire : le dépôt se fait directement sur le
   portail. Un canal EDI à prestataire certifié existe, mais c'est une
   commodité, pas une condition d'accès au marché. Hypothèse écartée sur pièce.

### Éliminatoire n° 3 : il fallait le scinder en deux

Erreur évitée de justesse — la réponse « OUI » et la réponse « NON » coexistent
dans ce secteur, sur deux objets différents.

- **Registre phytosanitaire → NON.** L'arrêté du 24/12/2025 impose un **format**
  (« électronique, lisible par machine », annexe II) et **aucun agrément
  d'éditeur**. Les tableurs Excel sont explicitement acceptés. Différence de
  nature avec eFTI sur TRANSPORT : le texte contraint **le fichier**, pas
  **l'éditeur**.
- **Notification d'identification animale → un agrément existe.** « Dans le cas
  d'une édition par un logiciel, il faut utiliser une application agréée par
  l'Institut de l'Elevage » (FRGDS AURA). Mais `agriculture.gouv.fr` n'emploie
  « agréés » que pour les **boucles auriculaires**, pas pour les logiciels, et
  `idele.fr` est fermé au robot (page « connection verification / haphash »).

Conclusion écrite : **`NON` sur le registre phyto (établi sur le texte),
`INCONNU` sur la notification animale.** Ce n'est pas un éliminatoire constaté,
c'est une restriction fonctionnelle de portée non mesurée. **Ne jamais répondre
à l'éliminatoire n° 3 par un OUI/NON unique quand le secteur couvre plusieurs
métiers réglementés séparément.**

### La règle de rétrécissement a été appliquée, et elle n'a rien rendu

Nouvelle règle de l'utilisateur (31/07/2026) : un éliminatoire qui ne frappe
qu'un sous-segment ne ferme pas le secteur, il le **rétrécit** — nommer le
sous-segment, retirer ses codes NAF, recalculer le résidu, continuer ; NO-GO
seulement si le résidu passe sous 3 000.

Le contrôle a été fait explicitement et il échoue : **la gamme ISAGRI couvre les
18 codes NAF du secteur** (Geofolia pour les cultures, ISAVIGNE/ISACUVE pour la
viticulture, Troup'O/Pig'UP/ISAOVIN/ISACHEVRE pour l'élevage). **Résidu : 0.**

La règle est bonne et doit être conservée — mais elle mord sur les éliminatoires
n° 2 et n° 3, qui sont souvent adossés à une réglementation de métier, beaucoup
moins sur le n° 4, où un éditeur généraliste couvre par construction tout ce qui
est adressable.

### Le volume n'a toujours rien prédit

72 866 cibles : le plus gros volume de l'étude, cinq fois SÉCURITÉ PRIVÉE.
**Cinquième secteur d'affilée où l'éliminatoire n° 1 est franchi et où le secteur
tombe pour autre chose.** Le seuil de 3 000 n'a encore jamais rien éliminé.

Ici le volume joue même à l'envers : c'est parce que le marché fait 72 866
exploitations employeuses qu'il nourrit un éditeur de 1 000 à 1 999 salariés à
144,9 M€ de CA. **Un gros marché est une raison d'attendre un gros concurrent,
pas une raison d'espérer.**

### Règle 10 : le NAF sous-compte d'un facteur 5,7, et la cause est connue

Recensement agricole 2020 (Agreste) : **416 054 exploitations en activité**
(France entière), ~389 000 en métropole. Cible NAF 01–32 : **≥ 72 866**.

Contrairement au cas des syndics — où le NAF sous-comptait parce qu'un code
pertinent était hors périmètre — la cause est ici entièrement dans la
**définition de la cible** : les tranches `00` et `NN` sont exclues, or la très
grande majorité des exploitations françaises n'ont aucun salarié.

Les 72 866 ne sont donc pas « les exploitations agricoles » mais **les
exploitations employeuses**. Ce n'est pas une erreur — une exploitation sans
salarié est une cible commerciale plus faible — mais l'écart doit être publié et
ne pas être lu comme une réserve de clients.

### Réutilisation du code de l'app BTP : 3, et le pire atterrissage à ce jour

**Cinquième 3 consécutif, cinquième fois que le champ ne décide rien.** Le § 6 de
`CLAUDE.md` se vérifie une cinquième fois.

Mais le contrôle « vers **quoi** la brique transpose-t-elle » a rendu ici son
résultat le plus net, et le plus mauvais :

- **App terrain mobile hors-ligne** — la meilleure transposition du lot, la
  parcelle étant au réseau ce que le chantier est au BTP — atterrit **exactement
  sur le registre phyto**, c'est-à-dire sur l'objet de l'outil gratuit du
  ministère.
- **Factur-X** atterrit sur la gestion commerciale viticole, où ISAVIGNE annonce
  plus de 7 000 utilisateurs.
- **Génération de documents et signature** atterrit sur les déclarations
  viticoles (qui se déposent sur le portail douane, pas s'impriment) et sur la
  notification animale (application agréée Idele).
- Seule la brique n° 2 — **suivi documentaire avec contrôle de validité en
  cascade** — atterrit en zone libre, vers les Certiphyto et les documents des
  saisonniers.

Trois briques sur quatre qui transposent le mieux tombent en zone barrée ou
occupée. C'est le cas le plus démonstratif rencontré depuis le piège eFTI sur
TRANSPORT.

### Verdict du secteur

**NO-GO, éliminé.** Éliminatoire n° 4 : **ISAGRI SAS (327733432), CA 2024 =
144 887 287 €**, soit 4,8 fois le seuil de 30 M€, résultat net 11 375 410 €,
1 000 à 1 999 salariés. Au niveau groupe, **GROUPE ISA (379163546), CA 2024 =
340 980 000 €**, soit 11,4 fois le seuil. Source : champ `finances` de
`recherche-entreprises.api.gouv.fr`, alimenté par les comptes annuels INPI.

Réserve portée dans le livrable, sans effet sur le verdict : la part de ce CA
réalisée sur le seul logiciel d'exploitation agricole est **`INCONNU`**, l'entité
portant aussi AGIRIS et Terre-net.

**Second motif indépendant : fenêtre de lancement fermée.** Échéance du registre
phyto numérique au **01/01/2027**, dans 5 mois. Pic d'achat (− 6 mois) et mise en
ligne cible (− 12 mois) sont tous deux dépassés. Ce motif tiendrait même si
ISAGRI n'existait pas.

Éliminatoire n° 1 (≥ 72 866 cibles) **franchi et vérifié**.

**Éliminatoires n° 2 et volet animal du n° 3 : `INCONNU`, pas franchis.** À ne
pas reporter comme acquis dans `SYNTHESE.md`.

**Étape 5 non menée** — corpus de 0 avis. Valeur à reporter : `INCONNU`, jamais 0.

Score : **non totalisé, secteur éliminé.** Sept points sur cinq champs renseignés
(cibles 3, échéance 1, réutilisation BTP 3, certification 0, CA du leader
éliminatoire), deux champs `INCONNU` (prix plancher, reproche dominant). Le total
sur 18 ne doit être ni publié ni comparé.

Livrables : `recherche/AGRICULTURE_VITICULTURE.md` et
`recherche/AGRICULTURE_VITICULTURE_avis.md`.

---

## 31/07/2026 — Session 8 : nouvelle phase, recherche par irritant (protocole suspendu)

Livrables : `recherche/PISTES_APPS.md` et `recherche/TEST_TERRAIN_A1.md`.

### Ce qui change, sur instruction de l'utilisateur

**`PROMPT_RECHERCHE_SECTEUR.md` est suspendu.** Les règles de données du § 1 de
`CLAUDE.md` restent intégralement applicables ; les quatre éliminatoires du § 2
sont remplacés par trois. Ne restent éliminatoires : la certification d'État sur
le besoin, l'outil gratuit public ou consulaire sur le besoin, le concurrent
gratuit crédible d'un acteur établi. **Ne sont plus éliminatoires** : la présence
d'un gros éditeur (reformulée en « couvre-t-il CE besoin ? ») et un marché sous
3 000 entreprises. Nouveau seuil : 500 clients à 50 €/mois, soit 300 k€/an.

Recherche **par irritant**, sur 27 métiers hors BTP, et non plus par code NAF.
Consigne complémentaire du même jour : **privilégier les irritants transverses**,
un irritant touchant cinq métiers d'une famille valant mieux que la meilleure
niche mono-métier. Livrable classé en deux parties.

### Établi

- **L'API `recherche-entreprises` ne sait pas compter les indépendants, et le
  plafond ne se casse pas sur cette cible.** La tranche `NN` plafonne à 10000 sur
  **20 des 21 codes NAF testés** (seule exception : 01.62Z, 6 319). Deux voies de
  sous-partition ont été essayées sur 74.20Z et **échouent toutes les deux** :
  `nature_juridique=1000` (entrepreneur individuel) rend 10000, et
  `est_entrepreneur_individuel=true` rend 10000. La spec OpenAPI n'offre **aucun
  filtre de date de création** qui aurait donné une partition propre. Les axes
  géographiques restent interdits (ils filtrent sur les établissements).
  **Conséquence durable : pour toute cible de micro-entrepreneurs, le décompte
  NAF est un minorant « au moins un salarié », et rien d'autre.**
- **L'open data Urssaf remplace utilement l'API sur cette cible.** Jeu
  `auto-entrepreneurs-par-secteur-dactivite`, dernier trimestre **31/12/2025**,
  **2 430 751** micro-entrepreneurs administrativement actifs, ventilés en 30
  secteurs. **La colonne à retenir est « économiquement actifs »**, pas
  « administrativement actifs » : seuls 49,8 % des micro-entrepreneurs déclarent
  un CA positif. Prendre la mauvaise colonne double presque la cible.
- **Indy ferme à lui seul tout le territoire de la facturation.** Offre
  « Essentiel » à 0 €/mois, non bridée, facture électronique via plateforme
  agréée DGFiP comprise. Éliminatoire « concurrent gratuit crédible » déclenché
  sur toute piste dont le cœur est devis + facture + compta.
- **La facturation électronique est un chemin d'État, pas un marché ouvert.**
  Réception obligatoire au 01/09/2026, émission micro-entreprises au 01/09/2027,
  via PDP **immatriculée** — soit un agrément d'État portant sur le logiciel.
- **L'irritant le mieux prouvé de la session est aussi le plus périmé.**
  Doctolib a exclu **5 700 praticiens bien-être** (2 700 hypnothérapeutes,
  1 500 sophrologues, 800 naturopathes), source Le Quotidien du Médecin — poids
  fort. Mais c'était en 2022, et quatre acteurs occupent désormais le besoin,
  dont **Zen Agenda, gratuit**. Un irritant excellemment sourcé ne vaut rien si
  la fenêtre s'est refermée : à retenir pour les prochaines sessions.

### Trouvé faux, ou corrigé

- **Reddit est inaccessible à l'agent**, et pas seulement lent : `reddit.com`
  est refusé à la fois par la recherche (`API Error 400 : domains not accessible
  to our user agent`) et par la récupération de page. La source forte n° 3 de la
  hiérarchie du § 3 de `CLAUDE.md` est donc **structurellement absente** de tout
  corpus produit depuis cet environnement. Ce n'est pas un incident de session,
  c'est une contrainte permanente à déclarer dans chaque livrable.
- **Conséquence directe, et point faible assumé du livrable** : sur une
  recherche par irritant, les sources disponibles sont massivement des **blogs
  d'éditeurs de logiciel**, qui décrivent le manque que leur produit comble —
  poids faible à nul au sens du § 3. Chaque fiche porte donc une ligne
  « Poids de la preuve ». **La piste A3 est retenue avec la mention explicite que
  son irritant n'est pas prouvé en source forte.**

### Résultat

**15 pistes instruites, 4 retenues.** Classement : A2 avance immédiate de crédit
d'impôt SAP pour le prestataire solo (0,66 % de pénétration requise sur 75 300
organismes NOVA — la meilleure économie du fichier) · A1 dossier client conforme
du professionnel non-médical · A3 prestation à date unique · B1 devis traiteur au
convive.

Onze écartées, dont sept par l'éliminatoire du concurrent gratuit : Indy sur la
facturation, Zen Agenda et Fit'Distance sur les forfaits et le RDV bien-être,
trois applications HACCP gratuites sur les registres alimentaires.

**Une écartée à réexaminer en priorité** : B2, bonus réparation QualiRépar.
Écartée uniquement faute de preuve d'irritant sourcée, alors que le dispositif
pèse 715 200 réparations en 2024 (×4 en un an) et 512 M€ sur 2022-2028.

### Laissé ouvert

- **Le risque n° 1 de la piste A2 n'est pas levé** : l'habilitation de l'éditeur
  à l'API Tiers de prestation de l'Urssaf est un filtre d'État sur le logiciel.
  Aucune homologation, audit, coût ni exigence de taille n'est documenté, et de
  très petits éditeurs l'ont obtenue — mais **cela reste à confirmer avant toute
  ligne de code**. C'est binaire et gratuit à instruire.
- **Deux gratuités ont fermé des pistes sans être vérifiées par essai** : Zen
  Agenda et Fit'Distance sont crédités sur leur seule déclaration d'éditeur, ce
  que le § 2 de `CLAUDE.md` interdit de tenir pour acquis. À constater.
- **Trois chiffres reposent sur des sources secondaires** et doivent être repris
  sur leur source primaire : les 82 776 organismes SAP (publication DGE), les
  15 000 tatoueurs (SNAT), les élevages félins (LOOF).

### Protocole de terrain sur A1

`recherche/TEST_TERRAIN_A1.md`, écrit à la demande de l'utilisateur, **sans
aucune recherche web supplémentaire** — le constat étant que ce qui manque sur
A1 n'est pas dans les sources publiques : un professionnel ne publie pas qu'il
est en infraction.

Trois partis pris à conserver s'il est réutilisé sur d'autres pistes :

1. **Seuils fixés avant la collecte**, et non renégociables après. Un résultat
   entre les bornes vaut `INCONNU` et impose une nouvelle collecte.
2. **Deux seuils, pas un.** Le support (papier / photos) ne suffit pas : c'est
   le **test de récupération** — « combien de temps pour retrouver un dossier de
   2023 » — qui décide. Franchir le premier seul signifie « ils sont sur papier
   et ça leur va très bien », soit le contresens que le test existe pour éviter.
3. **La question porte sur le lieu d'un objet précis et récent**, jamais sur un
   ressenti : « votre dernier client de la semaine dernière, sa décharge est où
   en ce moment ? ». Les mots « logiciel », « outil », « conforme », « RGPD » et
   « est-ce que vous paieriez » sont interdits avant la dernière question.

**Aucun nom de groupe Facebook ni de compte Instagram n'a été inventé.** Les
entités citées sont marquées ✅ (rencontrées par requête le 31/07/2026, URL
reproduite) ou ⬜ (cible de recherche, à confirmer à l'ouverture). Là où je ne
savais pas, le fichier donne la requête exacte, pas un nom vraisemblable.

**Un risque nouveau, identifié en écrivant le protocole et non instruit** : la
CNIL publie des modèles et outils gratuits de registre des traitements. S'ils
couvrent l'obligation telle qu'elle pèse sur un praticien, **l'éliminatoire de
l'outil public gratuit est déclenché sur la branche bien-être d'A1**, qui se
réduirait alors aux tatoueurs et aux métiers du vivant animal. Ce contrôle est
placé au même rang de priorité que les 18 ARS.

---

## 31/07/2026 — Session 9 : § 5 du protocole A1 exécuté (ARS, CNIL, contrôles adjacents)

Livrables : `recherche/TEST_TERRAIN_A1.md` § 5 bis et § 5 ter, puis report dans
`recherche/PISTES_APPS.md`. **Seul le § 5 a été exécuté** — les § 1 à 4 du
protocole (entretiens, seuils, Clic2Sign) restent entiers, et ce sont eux qui
décident.

### Établi

- **18 ARS sur 18 instruites, aucun outil qualifiant.** Aucune ne distribue de
  registre ni de fiche de traçabilité client. Ce qu'elles distribuent :
  déclarations d'activité, listes de formations habilitées et de prestataires
  DASRI, déclarations d'effet indésirable, affiches. **La réserve « contrôle ARS
  non exhaustif » de `PISTES_APPS.md` est levée.**
- **Le motif vaut mieux qu'une absence de résultat** : les ARS **prescrivent**
  explicitement la traçabilité client sans fournir le document. Occitanie décrit
  jusqu'au contenu attendu du registre ; le guide de 25 pages de
  Nouvelle-Aquitaine impose « une fiche de traçabilité […] pour chaque
  désinfection » et la conservation des consentements de mineurs pendant 3 ans,
  et **aucune de ses 7 annexes** n'est un registre, une fiche de traçabilité ou
  un consentement. C'est la ligne « informer n'est pas outiller », du bon côté.
- **Le modèle de domaine ARS était faux sur un point** : `ile-de-france` n'existe
  pas, le domaine réel est `iledefrance` (sans tirets). Deux exceptions au modèle
  `[région].ars.sante.fr`, pas une : `paca` et `iledefrance`.
- **CNIL : éliminatoire déclenché sur une obligation, et une seule** — le
  registre des activités de traitement, pour lequel elle publie un modèle
  simplifié gratuit destiné aux TPE. Pas sur l'information du client
  (« illustrations à adapter […] non des modèles universels »), pas sur la
  réponse aux demandes d'accès (une page pédagogique, aucun outil), pas sur le
  dossier client, qui est le cœur d'A1.
- **Le fait nouveau, et il joue en faveur d'A1** : le référentiel CNIL
  « cabinets médicaux et paramédicaux » — seul instrument adaptant le RGPD au
  dossier patient — **s'adresse nommément aux seuls professionnels de santé
  exerçant à titre libéral**. Naturopathes, sophrologues et hypnothérapeutes en
  sont exclus, pour le motif exact qui les a fait sortir de Doctolib. Assujettis
  comme les médecins, privés de l'instrument construit pour l'être : **le
  contrôle a élargi l'écart d'A1 sur cette branche au lieu de le réduire.**
- **Agriculture / DDPP et service-public.fr : non déclenchés.** L'arrêté du
  3 avril 2014 prescrit la forme du registre d'élevage — « côté, tenu sans
  blanc, ni rature, ni surcharge », « indélébile », corrections motivées
  séparément — sans fournir de support. C'est le cahier des charges d'un journal
  inaltérable, qu'un registre numérique satisfait mieux que le papier.

### Deux méthodes qui ont servi et qui resserviront

1. **Un PDF illisible par l'outil de récupération n'est pas une donnée
   manquante** : le guide ARS Nouvelle-Aquitaine et le référentiel CNIL ont été
   **extraits en local** pour être tranchés. Les deux pièces les plus difficiles
   à écarter sont celles qu'il fallait lire.
2. **Vérifier un domaine par requête HTTP avant de le publier.** Cinq domaines
   étaient vérifiés, treize inférés d'un modèle — le modèle était faux une fois
   sur treize. Une inférence de forme n'est pas une source (§ 1.2 de
   `CLAUDE.md`).

### Reporté dans `PISTES_APPS.md` (06/08/2026)

- **Le registre des traitements RGPD est exclu de la proposition de valeur
  d'A1**, explicitement et par écrit — avec l'AIPD (logiciel PIA). La CNIL le
  fait gratuitement et mieux. Ce qui reste, et que personne ne couvre : le
  **dossier client opposable**.
- **La branche bien-être est notée AMAIGRIE, non supprimée.** A1 conserve ses
  cinq métiers ; le recalcul de population n'est pas appliqué, sa condition
  n'étant pas remplie. Les chiffres de contingence sont conservés au § 5ter.5
  du protocole pour que la décision reste auditable.
- **Réserve résiduelle ouverte et nommée : les CMA régionales et
  départementales.** Seul le portail national `artisanat.fr` a été balayé — il
  ne rend que des services génériques. Le réseau est `INCONNU`. C'est le seul
  trou du contrôle, porté au § « Ce qui reste à faire » au même rang que
  l'habilitation Urssaf sur A2.

### Ce que cette session ne dit pas

Elle établit qu'aucun outil public gratuit ne couvre le dossier client. **Elle
ne dit rien de l'irritant lui-même.** La mauvaise tenue du dossier reste non
prouvée en primaire, et c'est toujours la réserve la plus lourde d'A1.

---

## 06/08/2026 — Session 10 : deuxième passe par irritant, 30 métiers nouveaux

**Livrable : `recherche/PISTES_APPS_2.md`.** Même méthode que `PISTES_APPS.md`
(protocole sectoriel suspendu, trois éliminatoires, seuil 500 clients à
50 €/mois, transverses d'abord). Aucun des 30 métiers n'avait été traité.

### Le résultat principal : un irritant enfin mesuré par l'État

Quatre enquêtes DGCCRF indépendantes, sur quatre secteurs sans rapport, mesurent
le même échec — le document réglementaire à remettre au client avant la
prestation n'est pas tenu :

| Secteur | Année | Contrôlés | En anomalie | Taux |
|---|---|---:|---:|---:|
| Dépannage à domicile | 2023 | 548 | 350 | 64 % |
| Réparation automobile | 2024 | ~1 600 | ~640 | ~40 % |
| Optique et audioprothèse (100 % santé) | 2023-24 | 700+ | 514 | 72 % |
| Prestations funéraires | 2017-18 | `INCONNU` | `INCONNU` | 66 % **NON VÉRIFIÉ** |

C'est la première fois dans ce corpus qu'un irritant repose sur une **mesure
d'État chiffrée** et non sur un blog d'éditeur. Les deux premières lignes ont
été lues directement (DREETS Pays de la Loire, UFC-Que Choisir) ; la ligne
automobile est relayée par **Movalib, éditeur de logiciel de garage** — conflit
d'intérêt noté dans la fiche.

**Réserve de fond, écrite dans le livrable :** un taux d'anomalie mesure la
non-conformité, pas la douleur. La DGCCRF relève dans le même mouvement des
fraudes délibérées. **La part subie de la non-conformité est `INCONNU`** — c'est
la question que ce fichier ne peut pas trancher.

### Trois pistes retenues, une non instruite

- **A1 — Devis conforme de l'intervention technique** (plombier, serrurier,
  garagiste, carrossier, deux-roues + électricien, vitrier, couvreur).
  **≥ 88 377 entreprises à ≥ 1 salarié, pénétration requise ≤ 0,57 %** — la plus
  basse des deux passes. Trois éliminatoires francs. **Réutilisation BTP forte
  (3/3)**, et pour la première fois les corps de métier concernés sont *déjà*
  écrits dans l'app existante.
- **A2 — Le formulaire imposé par arrêté** (opticien, audioprothésiste, pompes
  funèbres, agence de voyage). L'éliminatoire n° 1 (agrément CNDA) ferme la
  facturation mais **pas le devis normalisé**, qui s'impose y compris hors
  remboursement. L'éliminatoire n° 2 est **partiellement déclenché** : l'État
  fournit le formulaire vierge — précédent CNIL de la session 9 appliqué tel quel.
- **A3 — Le bien confié** (pressing, cordonnier, horloger, encadreur, garage,
  deux-roues). Mécanique juridique commune établie sur l'INC (arrêté du
  27 mars 1987, loi du 31 décembre 1903 modifiée en 2016, présomption de
  responsabilité, délais 2 mois / 1 an). **Irritant non prouvé côté professionnel.**
- **A4 — Fluides frigorigènes : NON INSTRUITE.** Publiée pour ne pas être perdue,
  ses trois éliminatoires sont `INCONNU`, pas franchis.

### Quatre fermetures nettes, obtenues à bas coût

- **Vétérinaire : fermé deux fois en deux requêtes.** n° 1 — tous les éditeurs de
  logiciels vétérinaires **doivent faire qualifier leur logiciel**, liste publiée
  par l'Ordre (17 produits). n° 2 — **CalypsoVet**, gratuit, porté par l'Ordre
  (cotisation obligatoire), le ministère de l'Agriculture et le FTAP.
- **Apiculture : fermée deux fois.** Téléprocédure d'État gratuite pour la
  déclaration de ruches, et **Beekube** gratuit et illimité pour le registre
  d'élevage réglementaire.
- **Déménagement : fermé.** **Mobilio** annonce devis, lettre de voiture,
  factures, calcul de volume et déclaration de valeur **gratuits**.
- **Boucher / boulanger : fermé alors que c'est la plus grosse population du
  fichier** (34 806 à ≥ 1 salarié). Trois applications HACCP gratuites héritées
  de la session 8. **La taille du marché ne compense jamais un éliminatoire.**

### Deux acquis de méthode

1. **La tranche `NN` est redevenue exploitable.** Elle rend une valeur réelle sur
   **27 des 40 codes** testés (75.00Z = 9 361, 47.22Z = 9 430, 96.01B = 8 459),
   là où elle plafonnait presque partout au 31/07/2026. Les populations
   d'indépendants sont donc connues sur la majorité de ces métiers.
2. **Un faux irritant intercepté avant publication.** La DRM aux douanes,
   envisagée pour les cavistes, **ne les concerne pas** : c'est le statut
   douanier du vin en droits suspendus qui déclenche l'obligation, pas le métier.
   Et pour ceux qui y sont soumis, le dépôt passe par **CIEL**, téléprocédure
   gratuite de la douane. Vérifier à qui s'applique une obligation avant d'en
   faire une piste.

### Trois limites, à connaître avant d'exploiter le fichier

1. **Reddit reste inaccessible** (`API Error 400`, retesté le 06/08/2026), comme
   en session 8.
2. **Les forums métier testés sont fermés** : `apiculture-france.com` et
   `ruches-apiculture.com` ne rendent que leur page de connexion. Aucun fil de
   forum métier n'a pu être lu dans cette session.
3. **`economie.gouv.fr` renvoie HTTP 403 à l'agent** (Cloudflare), en récupération
   de page comme en `curl` avec en-tête de navigateur. **Trois chiffres du
   livrable sont marqués `NON VÉRIFIÉ`** et ne doivent pas ressortir ailleurs :
   66 % funéraire, 55 % agences de voyage, et le chiffrage alternatif
   « 1 300 contrôlés / 75 % » du 100 % santé.

---

## 06/08/2026 — Session 11 : exécution des § 4 et § 5 de TEST_TERRAIN_P2A1

Deux volets desktop de la piste A1 de la deuxième passe, ceux qui pouvaient la
tuer avant tout entretien. **Un des deux a mordu.**

### Le fait : CMA France distribue un outil de devis gratuit

**Éliminatoire n° 2 DÉCLENCHÉ.** CMA France a retenu **Abby** à l'issue d'un
**marché public** pour déployer, sous marque CMA, un outil de gestion dont
l'offre **Basique est à 0 €/mois, sans engagement, sans carte bancaire, avec
« devis et factures illimités »** et « facturation électronique conforme ». La
CMA affiche « Un conseiller CMA pour vous accompagner ». Site dédié
`cma-gestion.fr` ; relais constatés en Martinique, La Réunion, Île-de-France,
Nouvelle-Aquitaine, Grand Est, Aude, Aveyron.

La CMA est financée par la taxe pour frais de chambres de métiers : c'est la
deuxième forme de l'éliminatoire n° 2 (§ 2 de `CLAUDE.md`).

**Ce que ça retire à A1** : la brique « produire un devis et une facture », et
— Abby étant une plateforme agréée par l'État — la brique « facturation
électronique », barrée une seconde fois par l'éliminatoire n° 1. **Même
traitement que le registre RGPD retiré d'A1 en session 9.** Ce qui reste : une
couche de conformité seule (barème, rétractation, double devis pièce de
réemploi, traçabilité du refus), posée sur un socle gratuit que la chambre
consulaire pousse à tous les artisans.

### Ce qui n'a pas pu être tranché

**Éliminatoire n° 3 : `INCONNU`.** Le § 4 demandait un **essai réel** des offres
gratuites. Aucun compte n'a été créé : ce qui a été mené est un contrôle
documentaire, que le § 2 de `CLAUDE.md` juge explicitement insuffisant. Huit à
dix cases sur dix restent `INCONNU` chez les quatre produits. **La règle de
décision du § 4.2 n'a donc pas été appliquée** — lire « aucun ne dépasse 3 cases
donc non déclenché » aurait été convertir un `INCONNU` en « non ».

**Il reste deux heures de travail, quatre comptes gratuits, et cette tâche
décide seule du sort d'A1.** Les entretiens terrain (§ 1 à 3, deux jours) ne
doivent pas être lancés avant.

### La leçon de méthode : le modèle de domaine est faux, encore

Comme les ARS en session 9, mais pire : **le modèle `cma-[région].fr` est faux
dans 12 cas sur 18.** Cinq formes coexistent (`cma-`, `crma-`, `cmar-`,
`artisanat-`, et des domaines sans racine commune : `cma.corsica`,
`artisanat974.re`, `cmarguadeloupe.org`, `cma-martinique.com`). La liste réelle
des 17 domaines est au § 5bis.1 de `TEST_TERRAIN_P2A1.md`.

**Et c'est ce test de domaine qui a produit la découverte** : sans lui, les CMA
de Martinique et de La Réunion — deux des domaines les moins prévisibles —
n'auraient pas été interrogées, et le partenariat Abby serait passé inaperçu.

### Restes `INCONNU`, écrits comme tels

- **Mayotte** : aucune CMA de région instruite, 6 domaines candidats testés,
  tous morts.
- **`artisanat.fr`** : HTTP 429 à trois tentatives espacées.
- **DGCCRF** : contrôle adjacent n° 1 non exécuté, HTTP 403 (Cloudflare) en
  récupération de page comme en `curl`.
- **Neuf CMA sur dix-sept** n'ont pas rendu de recherche interne exploitable.
  Leur silence n'est pas une absence d'outil.
- **Le périmètre réel de la gratuité d'Abby n'est pas constaté par essai** — il
  est établi sur trois pages concordantes, dont deux tenues par des CMA.

### Portée au-delà d'A1

Le réseau des CMA est désormais établi comme un **distributeur actif d'outils
gratuits**, pas comme un émetteur de brochures. **Toute piste future dont le
cœur est un document commercial d'artisan doit être testée contre CMA × Abby en
premier.** La réserve « CMA » de `PISTES_APPS.md` est annotée en conséquence.
