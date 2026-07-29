# Note de passation — Étape 1 (dimensionnement NAF)

**Fichier destiné à être donné tel quel à une autre session Claude Code.**
Il est autonome : aucune information de la conversation d'origine n'est nécessaire pour l'exploiter.

- Rédigé le : 29/07/2026
- API testée le : 29/07/2026
- Source unique des décomptes : `https://recherche-entreprises.api.gouv.fr/search`
- Source unique des libellés NAF : `https://www.insee.fr/fr/metadonnees/nafr2/sousClasse/[code]`
- Statut : **aucun fichier de résultat créé, aucune étape 2 à 6 lancée, aucun secteur traité.**
  Le comptage n'a pas commencé : il attend la validation des codes NAF (section 6).

---

## 0. Consigne d'origine, reproduite intégralement

> Fais uniquement l'étape 1 (dimensionnement NAF) sur les 8 secteurs, et
> arrête-toi là.
>
> Pour chaque secteur : codes NAF retenus, nombre d'entreprises via
> recherche-entreprises.api.gouv.fr, répartition par tranche d'effectif,
> et l'URL + date de chaque requête.
>
> Écris le résultat dans recherche/PREFILTRE_NAF.md, avec une colonne
> « éliminé (< 3000 cibles) » OUI/NON.
>
> Ne lance aucune autre étape. Ne crée aucun fichier secteur.
>
> Avant de commencer, liste-moi les codes NAF que tu comptes utiliser pour
> chaque secteur et attends ma validation.

Puis, en cours de route :

> Vérifie l'hypothèse du plafond : interroge l'API sur un code NAF
> massif (68.20B, location de logements) sans autre filtre. Si
> total_results renvoie encore exactement 10000, c'est un plafond dur
> et non un décompte. Confirme-le avant d'utiliser un seul chiffre.

---

## 1. Réponse rendue, reproduite mot pour mot

Ce qui suit est le texte intégral de la réponse, sans coupe ni reformulation.

---

Confirmé, et la preuve est sans ambiguïté.

**68.20B, sans aucun filtre : `total_results` = 10000, `total_pages` = 10000.** Mais la somme de ses 16 tranches d'effectif — une partition mutuellement exclusive et exhaustive — donne **25 146**. Et deux de ces cellules (`NN` et `01`) plafonnent elles-mêmes à 10000, donc le vrai total est très au-dessus de 25 146.

Un décompte ne peut pas être inférieur à la somme de ses parties. **10000 est un plafond dur, pas un chiffre.** Toute requête renvoyant exactement 10000 signifie « ≥ 10000, valeur inconnue ». Je n'utiliserai aucun `total_results` égal à 10000 comme un nombre.

### Trois autres pièges trouvés en vérifiant

| Piège | Preuve | Conséquence |
|---|---|---|
| **Entreprises cessées incluses par défaut** | 80.30Z : 2809 brut = 1153 actives + 1656 cessées | Sans `etat_administratif=A`, tout est gonflé ~2,4× — de quoi faire passer un secteur mort au-dessus du seuil de 3 000 |
| **`departement` ne filtre pas sur le siège** | `departement=75` renvoie FITECO (siège 53), COGEP (18), RYDGE (92) | Il matche *tout établissement*. Sommer les 101 départements double-compte chaque réseau multi-agences (LAMY = 370 établissements). **Axe inutilisable** |
| **68.32A est noyé de SCI** | Dans 68.32A actives tranche `NN` : `nature_juridique=6540` plafonne à ≥10000, contre 2828 SAS et 2829 SARL | Le code « administration d'immeubles » compte surtout des véhicules patrimoniaux, pas des syndics professionnels. Le NAF brut n'est pas la cible |

### Méthode de comptage que je propose

1. Toujours `etat_administratif=A`.
2. Total = **somme des 16 tranches d'effectif** (axe exclusif au niveau SIREN, vérifié : 80.30Z somme = 1153 = total direct ; 11.02A 409 vs 410, un enregistrement à tranche nulle).
3. Cellule qui plafonne → sous-partition par `nature_juridique` (260 valeurs, exhaustives).
4. Cellule encore plafonnée → écrite `>10000 (PLAFOND)`, jamais un nombre inventé.
5. `departement` : jamais utilisé.

⚠️ Le plafond n'empêche pas de trancher l'éliminatoire à 3 000, mais il empêche de distinguer les paliers 3‑15k / 15‑50k / >50k du barème sur les gros secteurs. La sous-partition par forme juridique est ce qui permettra de récupérer un chiffre exact.

### Codes NAF proposés — à valider

Libellés officiels tirés d'insee.fr/fr/metadonnees/nafr2/sousClasse/[code], consultés le 29/07/2026.

**1. SYNDICS_GESTION_LOCATIVE**

| Code | Libellé officiel | Statut |
|---|---|---|
| 68.32A | Administration d'immeubles et autres biens immobiliers | Cœur |
| 68.32B | Supports juridiques de gestion de patrimoine immobilier | Cœur |
| 68.31Z | Agences immobilières | À décider — transaction, pas gestion |
| 68.20A / 68.20B | Location de logements / de terrains | Proposé exclu — bailleurs, pas gestionnaires |

**2. TRANSPORT_DERNIER_KM** — 49.41A (fret interurbain), 49.41B (fret de proximité), 49.41C (location de camions avec chauffeur), 52.29A (messagerie, fret express) en cœur ; 49.42Z (déménagement), 52.29B (affrètement), 53.20Z (autres activités de poste et de courrier) à décider.

**3. SECURITE_PROPRETE_INTERIM** — trois métiers distincts, je propose de les compter séparément : sécurité 80.10Z / 80.20Z / 80.30Z ; propreté 81.21Z / 81.22Z / 81.29A / 81.29B / 81.10Z ; intérim 78.10Z / 78.20Z / 78.30Z.

**4. AGRICULTURE_VITICULTURE** — viticulture 01.21Z + 11.02A (vins effervescents) + 11.02B (vinification) ; grandes cultures/élevage 01.11Z, 01.13Z, 01.19Z, 01.24Z, 01.25Z, 01.41Z, 01.43Z, 01.45Z, 01.46Z, 01.47Z, 01.50Z ; prestataires 01.61Z à 01.64Z.

**5. INDUSTRIE_GMAO_MAINTENANCE** — ambiguïté à trancher : compter les **prestataires** de maintenance (33.11Z→33.19Z, 33.20A→33.20D, 71.20B) ou les **industriels utilisateurs** de GMAO (divisions 10 à 32, très volumineux) ? Ce ne sont pas les mêmes clients ni le même produit.

**6. ASSOCIATIONS_COLLECTIVITES** — associations 94.99Z, 94.12Z, 94.20Z, 94.11Z, 94.91Z, 94.92Z, 93.12Z, 93.19Z, 88.99A/B, 88.91A, 88.10A ; collectivités 84.11Z, 84.12Z, 84.13Z. Deux cibles très différentes, à compter séparément.

**7. CABINETS_COMPTA_JURIDIQUE** — 69.20Z (activités comptables), 69.10Z (activités juridiques) en cœur ; 70.22Z (conseil de gestion) à décider, très hétérogène.

**8. RSE_VSME_QUESTIONNAIRES_FOURNISSEURS** — **ce n'est pas un secteur NAF.** La cible est transverse (fournisseurs soumis au questionnaire VSME). `categorie_entreprise=PME` et `=ETI` plafonnent tous deux à 10000, et `tranche_effectif_salarie=22` aussi. Je propose de le dimensionner par tranche d'effectif toutes activités confondues (segment 50–250 salariés), en le marquant explicitement comme non comparable aux sept autres.

### Ce dont j'ai besoin pour lancer

1. Les arbitrages « à décider » ci-dessus — ou ton feu vert pour retenir mes propositions par défaut (cœur seulement, périmètres larges exclus).
2. Secteurs 3, 6 : comptage séparé par métier, ou agrégé ?
3. Secteur 5 : prestataires ou industriels ?
4. Secteur 8 : ma méthode de substitution te convient-elle ?

Je n'ai créé aucun fichier et lancé aucune autre étape. J'attends ta validation avant de compter.

---

*Fin de la réponse reproduite mot pour mot.*

---

## 2. Preuves brutes, reproductibles

Chaque constat ci-dessous a été obtenu par la commande indiquée, le 29/07/2026.
Aucun chiffre de cette note n'a été estimé, extrapolé ou reconstitué de mémoire.

### 2.1 Le plafond de 10 000 — preuve décisive

```bash
curl -s "https://recherche-entreprises.api.gouv.fr/search?activite_principale=68.20B&per_page=1"
# -> {'total_results': 10000, 'page': 1, 'per_page': 1, 'total_pages': 10000}
```

Somme de la partition exclusive par tranche d'effectif sur **68.20B**
(sans filtre d'état administratif, tel que testé) :

| Tranche | Décompte |
|---|---|
| NN | **10000 (PLAFOND)** |
| 00 | 1539 |
| 01 | **10000 (PLAFOND)** |
| 02 | 2026 |
| 03 | 799 |
| 11 | 503 |
| 12 | 190 |
| 21 | 46 |
| 22 | 28 |
| 31 | 7 |
| 32 | 3 |
| 41 | 2 |
| 42 | 2 |
| 51 | 0 |
| 52 | 1 |
| 53 | 0 |
| **Somme** | **25 146** |

`total_results` annoncé = 10000. Somme des parties = 25 146, dont deux cellules
elles-mêmes plafonnées. Le vrai total est donc très supérieur à 25 146.
**Un décompte ne peut pas être inférieur à la somme de ses parties : 10000 est un plafond dur.**

Autres codes ayant renvoyé exactement 10000 en `total_results` (donc inutilisables comme chiffres) :
`68.32A`, `43.21A`, `81.21Z`, `69.20Z`, `01.21Z`, `94.99Z` (actives), `68.32A` (actives),
`categorie_entreprise=PME`, `categorie_entreprise=ETI`, `tranche_effectif_salarie=22`.

### 2.2 Entreprises cessées incluses par défaut

```bash
# 80.30Z Activités d'enquête
?activite_principale=80.30Z                        -> 2809
?activite_principale=80.30Z&etat_administratif=A    -> 1153   (actives)
?activite_principale=80.30Z&etat_administratif=C    -> 1656   (cessées)
```

1153 + 1656 = 2809. **59 % du décompte brut est constitué d'entreprises cessées.**

Autre cas mesuré : `11.02A` brut = 531, actives = 410.

Valeurs valides du paramètre : `['A', 'C']`.

### 2.3 `departement` ne filtre pas sur le siège — axe inutilisable

```bash
?activite_principale=69.20Z&etat_administratif=A&departement=75&per_page=5
```

Résultats renvoyés, avec le département réel de leur siège :

| Entreprise | Département du siège |
|---|---|
| SOC FIDUCIAIRE NATIO EXPERTI | 92 |
| RYDGE CONSEIL | 92 |
| FITECO | 53 |
| TGS FRANCE EXPERTISE COMPTAB | 49 |
| COGEP | 18 |

Aucune n'a son siège à Paris. Le filtre matche **n'importe quel établissement**
de l'unité légale. Conséquence : sommer les 101 départements double-compte
chaque entreprise multi-établissements. LAMY (SIREN 487530099) déclare
370 établissements, dont 149 ouverts — elle serait comptée jusqu'à 149 fois.

Confirmation sur un autre jeu :

```bash
?categorie_entreprise=ETI&etat_administratif=A&departement=75  -> 10000
```

Or la France compte de l'ordre de 6 000 ETI au total : le résultat est
structurellement impossible, et l'un des résultats renvoyés (BASIC-FIT FRANCE)
a son siège en département 59.

**Décision : `departement` n'est utilisé dans aucun comptage.**

### 2.4 La partition par tranche d'effectif est, elle, exacte

`tranche_effectif_salarie` est un champ de niveau SIREN, mutuellement exclusif.
Validation sur deux codes dont le total réel est sous le plafond :

| Code (actives) | Total direct | Somme des 16 tranches | Écart |
|---|---|---|---|
| 80.30Z | 1153 | 1153 | **0** |
| 11.02A | 410 | 409 | 1 (un enregistrement à tranche nulle) |

C'est l'axe de partition retenu.

Valeurs valides : `NN, 00, 01, 02, 03, 11, 12, 21, 22, 31, 32, 41, 42, 51, 52, 53`.

### 2.5 68.32A est noyé de SCI

Sous-partition de `68.32A` + `etat_administratif=A` + `tranche_effectif_salarie=NN`
par forme juridique :

| `nature_juridique` | Décompte |
|---|---|
| 6540 | **10000 (PLAFOND)** |
| 5499 | 2829 |
| 5710 | 2828 |
| 1000 | 1160 |
| 9220 | 536 |
| 5202 | 265 |
| 6560 | 40 |
| 5385 | 0 |
| 5720 | valeur invalide (rejetée par l'API) |

Une seule forme juridique (6540) écrase à elle seule toutes les formes
commerciales réunies. Le code « administration d'immeubles » recense donc
majoritairement des véhicules de détention patrimoniale, **pas des syndics
professionnels**.

> ⚠️ Les libellés officiels des codes `nature_juridique` n'ont **pas** pu être
> confirmés par une source : les URL INSEE testées
> (`/metadonnees/cj/niveau3/6540`, `/metadonnees/cjNiveauIII/6540`) renvoient une
> page sans titre exploitable, et la vérification a été interrompue avant d'aboutir.
> Le code 6540 correspond usuellement aux sociétés civiles immobilières, mais
> **cette correspondance est à ce stade `INCONNU` faute de source vérifiée** et
> doit être confirmée avant d'être écrite dans un livrable.
> L'API ne renvoie aucun champ de libellé pour la forme juridique.

Conséquence pour l'étape 1 : la « cible réaliste » du secteur syndics doit être
calculée en sommant les formes juridiques commerciales, et non en prenant le
total NAF. C'est aussi ce qui permet de récupérer un chiffre exact malgré le plafond.

### 2.6 Comportement général de l'API — à connaître avant de compter

| Constat | Détail |
|---|---|
| Nomenclature du filtre | `activite_principale` n'accepte **que la NAF rév.2 (2008)**. Un code NAF 2025 (`68.32H`) est rejeté ; le message d'erreur renvoie la liste exhaustive des valeurs valides |
| `activite_principale_naf25` | **N'est pas un paramètre de filtre.** Utilisé seul, l'API répond « Veuillez indiquer au moins un paramètre de recherche » : il est silencieusement ignoré. C'est seulement un champ de sortie |
| Deux nomenclatures en sortie | Chaque résultat porte `activite_principale` (2008) **et** `activite_principale_naf25` (2025). Exemple : 68.32A → 68.32H, et le siège de LAMY porte 68.31Y. Ne pas les confondre |
| **Paramètres inconnus silencieusement ignorés** | `&zzzbogus=1` ne déclenche aucune erreur et ne change pas le résultat. **Tout paramètre doit être validé en lui passant une valeur absurde : s'il n'y a pas d'erreur, le filtre n'existe pas et le chiffre est faux** |
| Absence de libellé NAF | L'API ne renvoie aucun champ libellé d'activité. Les libellés viennent d'INSEE |
| Département 20 | N'existe pas (Corse = `2A` / `2B`). Une boucle naïve `01..95` produit une erreur 400 sur `20` |
| Nombre de valeurs `nature_juridique` | 260 |
| Valeurs `categorie_entreprise` | `GE`, `PME`, `ETI` |
| Débit | Aucune limitation rencontrée en séquentiel ; 8 requêtes concurrentes tenues sans erreur sur insee.fr |

Méthode de vérification d'un paramètre, à réutiliser systématiquement :

```bash
# Si ceci renvoie une erreur -> le paramètre existe et filtre réellement.
# Si ceci renvoie un résultat normal -> le paramètre est ignoré, le chiffre est faux.
curl -s "https://recherche-entreprises.api.gouv.fr/search?activite_principale=68.32A&LE_PARAM=ZZZZ&per_page=1"
```

---

## 3. Chiffres déjà acquis et réutilisables

Tous mesurés le 29/07/2026. `A` = `etat_administratif=A` (actives).
`PLAFOND` = la valeur 10000 a été renvoyée : le chiffre réel est inconnu et supérieur.

| Code NAF | Brut | Actives (A) | Remarque |
|---|---|---|---|
| 80.30Z | 2809 | **1153** | Exact. Somme des tranches vérifiée = 1153 |
| 11.02A | 531 | **410** | Exact. Somme des tranches = 409 |
| 78.20Z | INCONNU | **6860** | Exact |
| 68.32A | PLAFOND | PLAFOND | Noyé de SCI, cf. 2.5 |
| 94.99Z | INCONNU | PLAFOND | |
| 68.20B | PLAFOND | INCONNU | Somme des tranches ≥ 25 146, cf. 2.1 |
| 43.21A | PLAFOND | INCONNU | Hors périmètre des 8 secteurs (code de contrôle BTP) |
| 81.21Z | PLAFOND | INCONNU | |
| 69.20Z | PLAFOND | INCONNU | |
| 01.21Z | PLAFOND | INCONNU | |

Ne pas réutiliser les décomptes obtenus avec `departement` : ils sont faux (cf. 2.3).

---

## 4. Libellés officiels des 71 codes candidats

Source : `https://www.insee.fr/fr/metadonnees/nafr2/sousClasse/[code]`, consultés le 29/07/2026.
Récupérés depuis la balise `<title>` de chaque page sous-classe (les pages
`/division/[nn]` ne contiennent pas les sous-classes et sont inutilisables pour cela).

| Code | Libellé officiel NAF rév.2 |
|---|---|
| 01.11Z | Culture de céréales (à l'exception du riz), de légumineuses et de graines oléagineuses |
| 01.13Z | Culture de légumes, de melons, de racines et de tubercules |
| 01.19Z | Autres cultures non permanentes |
| 01.21Z | Culture de la vigne |
| 01.24Z | Culture de fruits à pépins et à noyau |
| 01.25Z | Culture d'autres fruits d'arbres ou d'arbustes et de fruits à coque |
| 01.41Z | Élevage de vaches laitières |
| 01.43Z | Élevage de chevaux et d'autres équidés |
| 01.45Z | Élevage d'ovins et de caprins |
| 01.46Z | Élevage de porcins |
| 01.47Z | Élevage de volailles |
| 01.50Z | Culture et élevage associés |
| 01.61Z | Activités de soutien aux cultures |
| 01.62Z | Activités de soutien à la production animale |
| 01.63Z | Traitement primaire des récoltes |
| 01.64Z | Traitement des semences |
| 11.02A | Fabrication de vins effervescents |
| 11.02B | Vinification |
| 33.11Z | Réparation d'ouvrages en métaux |
| 33.12Z | Réparation de machines et équipements mécaniques |
| 33.13Z | Réparation de matériels électroniques et optiques |
| 33.14Z | Réparation d'équipements électriques |
| 33.19Z | Réparation d'autres équipements |
| 33.20A | Installation de structures métalliques, chaudronnées et de tuyauterie |
| 33.20B | Installation de machines et équipements mécaniques |
| 33.20C | Conception d'ensemble et assemblage sur site industriel d'équipements de contrôle des processus industriels |
| 33.20D | Installation d'équipements électriques, de matériels électroniques et optiques ou d'autres matériels |
| 49.41A | Transports routiers de fret interurbains |
| 49.41B | Transports routiers de fret de proximité |
| 49.41C | Location de camions avec chauffeur |
| 49.42Z | Services de déménagement |
| 52.29A | Messagerie, fret express |
| 52.29B | Affrètement et organisation des transports |
| 53.10Z | Activités de poste dans le cadre d'une obligation de service universel |
| 53.20Z | Autres activités de poste et de courrier |
| 68.10Z | Activités des marchands de biens immobiliers |
| 68.20A | Location de logements |
| 68.20B | Location de terrains et d'autres biens immobiliers |
| 68.31Z | Agences immobilières |
| 68.32A | Administration d'immeubles et autres biens immobiliers |
| 68.32B | Supports juridiques de gestion de patrimoine immobilier |
| 69.10Z | Activités juridiques |
| 69.20Z | Activités comptables |
| 70.22Z | Conseil pour les affaires et autres conseils de gestion |
| 71.20B | Analyses, essais et inspections techniques |
| 78.10Z | Activités des agences de placement de main-d'œuvre |
| 78.20Z | Activités des agences de travail temporaire |
| 78.30Z | Autre mise à disposition de ressources humaines |
| 80.10Z | Activités de sécurité privée |
| 80.20Z | Activités liées aux systèmes de sécurité |
| 80.30Z | Activités d'enquête |
| 81.10Z | Activités combinées de soutien lié aux bâtiments |
| 81.21Z | Nettoyage courant des bâtiments |
| 81.22Z | Autres activités de nettoyage des bâtiments et nettoyage industriel |
| 81.29A | Désinfection, désinsectisation, dératisation |
| 81.29B | Autres activités de nettoyage n.c.a. |
| 84.11Z | Administration publique générale |
| 84.12Z | Administration publique (tutelle) de la santé, de la formation, de la culture et des services sociaux, autre que sécurité sociale |
| 84.13Z | Administration publique (tutelle) des activités économiques |
| 88.10A | Aide à domicile |
| 88.91A | Accueil de jeunes enfants |
| 88.99A | Autre accueil ou accompagnement sans hébergement d'enfants et d'adolescents |
| 88.99B | Action sociale sans hébergement n.c.a. |
| 93.12Z | Activités de clubs de sports |
| 93.19Z | Autres activités liées au sport |
| 94.11Z | Activités des organisations patronales et consulaires |
| 94.12Z | Activités des organisations professionnelles |
| 94.20Z | Activités des syndicats de salariés |
| 94.91Z | Activités des organisations religieuses |
| 94.92Z | Activités des organisations politiques |
| 94.99Z | Autres organisations fonctionnant par adhésion volontaire |

---

## 5. Procédure de comptage à appliquer

Pour chaque code NAF retenu, dans cet ordre :

1. **Total actives** : `?activite_principale=[code]&etat_administratif=A`
2. Si le résultat ≠ 10000 → c'est le chiffre. Passer aux tranches.
3. Si le résultat = 10000 → **ne pas l'écrire comme un nombre**. Reconstituer le
   total par la somme des 16 tranches.
4. **Répartition par tranche** : 16 requêtes
   `?activite_principale=[code]&etat_administratif=A&tranche_effectif_salarie=[NN|00|01|02|03|11|12|21|22|31|32|41|42|51|52|53]`
5. Toute cellule de tranche = 10000 → sous-partitionner par `nature_juridique`
   (260 valeurs). Sommer.
6. Cellule encore = 10000 après sous-partition → écrire `>10000 (PLAFOND)`.
7. Ne jamais utiliser `departement`.
8. Consigner l'URL complète et la date pour chaque chiffre publié.

Contrôle de cohérence obligatoire : la somme des tranches doit égaler le total
direct quand celui-ci n'est pas plafonné (tolérance de 1 pour les enregistrements
à tranche nulle, cf. 2.4). Si l'écart est supérieur, ne rien publier et chercher
la cause.

Volume estimé : 17 requêtes par code sans plafond, plus 260 par cellule plafonnée.

---

## 6. Ce qui reste à valider avant de compter

Le comptage est **en attente** sur ces quatre arbitrages.

1. **Inclusions « à décider »** de la section 1 : 68.31Z pour les syndics ;
   49.42Z / 52.29B / 53.20Z pour le transport ; 70.22Z pour compta-juridique.
   Réponse possible : « feu vert sur les propositions par défaut »
   (cœur seulement, périmètres larges exclus).
2. **Secteurs 3 (sécurité/propreté/intérim) et 6 (associations/collectivités)** :
   comptage séparé par métier, ou agrégé ? Ce sont des métiers et des cibles
   distincts ; l'agrégation produirait un chiffre sans signification commerciale.
3. **Secteur 5 (GMAO)** : compter les **prestataires** de maintenance
   (33.11Z→33.19Z, 33.20A→33.20D, 71.20B) ou les **industriels utilisateurs**
   de GMAO (divisions 10 à 32) ? Ce ne sont ni les mêmes clients, ni le même produit.
4. **Secteur 8 (RSE/VSME)** : ce n'est pas un secteur NAF, la cible est transverse.
   Méthode de substitution proposée : dimensionnement par tranche d'effectif
   toutes activités confondues (segment 50–250 salariés), marqué explicitement
   comme non comparable aux sept autres. À confirmer.

## 7. Réserves à ne pas perdre de vue

- **Le plafond de 10 000 n'empêche pas de trancher l'éliminatoire à 3 000**, mais
  il empêche de distinguer les paliers 3‑15k / 15‑50k / >50k du barème de la
  section 5 du protocole tant que la sous-partition par forme juridique n'a pas
  été faite. Sur les gros secteurs, la ligne de score restera partiellement
  `INCONNU` sans ce travail.
- **Le NAF n'est pas la cible commerciale.** Le cas 68.32A le démontre : le code
  est dominé par des véhicules patrimoniaux sans besoin logiciel. Le même biais
  est à attendre sur 68.20A/68.20B, et à vérifier sur 94.99Z (associations
  dormantes) et 84.11Z (petites communes sans budget logiciel).
- **Les libellés `nature_juridique` ne sont pas sourcés** (cf. encadré en 2.5).
  À établir avant tout livrable qui les nomme.
- Le champ « Réutilisation du code de l'app BTP » de la ligne de score du
  protocole ne peut pas être renseigné : aucune information n'a été fournie sur
  cette application. À traiter en `INCONNU` ou à documenter séparément.
- Aucune donnée d'étape 2 à 6 n'a été collectée. Aucun éditeur, aucun avis,
  aucune contrainte réglementaire n'a été recherché.
