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
