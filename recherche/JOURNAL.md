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
