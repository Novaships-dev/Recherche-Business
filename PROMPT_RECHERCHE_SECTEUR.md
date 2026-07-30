# Prompt de recherche sectorielle — logiciel métier France

## Utilisation

Placer ce fichier à la racine du repo. Lancer **une session Claude Code par secteur** :

```
Lis PROMPT_RECHERCHE_SECTEUR.md et exécute la recherche complète
pour le secteur : SYNDICS_GESTION_LOCATIVE
```

Secteurs à traiter (un par session) :

```
SYNDICS_GESTION_LOCATIVE
TRANSPORT_DERNIER_KM
SECURITE_PROPRETE_INTERIM
AGRICULTURE_VITICULTURE
INDUSTRIE_GMAO_MAINTENANCE
ASSOCIATIONS_COLLECTIVITES
CABINETS_COMPTA_JURIDIQUE
RSE_VSME_QUESTIONNAIRES_FOURNISSEURS
```

---

## Mission

Déterminer si le secteur assigné contient une opportunité exploitable par un
développeur solo, sans financement, sans équipe commerciale. La réponse par
défaut est **NON**. Il faut des preuves pour conclure autrement.

Ne pas chercher à être encourageant. Un « non » documenté a plus de valeur
qu'un « oui » optimiste : il économise des mois de développement.

---

## Règles absolues sur les données

1. **Tout chiffre doit être accompagné de son URL source et de la date de
   consultation.** Sans source → écrire `INCONNU`.
2. **Ne jamais estimer, extrapoler ou reconstituer un chiffre de mémoire.**
   `INCONNU` est une réponse acceptable et attendue.
3. **Identifier l'auteur de chaque comparatif consulté.** Les comparatifs de
   logiciels métier sont majoritairement écrits par des éditeurs qui se
   classent premiers. Vérifier systématiquement l'éditeur du site (mentions
   légales, footer) et noter le conflit d'intérêt dans le fichier de sortie.
   Un comparatif d'éditeur n'est pas une source sur ses concurrents.
4. **Distinguer prix affiché et prix réel.** Noter la présence d'options
   payantes, de frais de mise en service, d'engagement annuel.
5. Si une recherche ne donne rien, l'écrire. L'absence de résultat est une
   information (marché inexistant, ou vocabulaire métier mal deviné).

---

## Protocole de recherche, dans cet ordre

### Étape 1 — Dimensionner le segment (aucune clé API requise)

API publique ouverte, sans authentification :

```bash
curl "https://recherche-entreprises.api.gouv.fr/search?activite_principale=68.32A&page=1&per_page=1"
```

Le champ `total_results` donne le nombre d'entreprises. Utiliser
`tranche_effectif_salarie` pour segmenter par taille.

Trouver d'abord les codes NAF du secteur (recherche web sur la nomenclature
NAF 2008/2025), puis compter pour chacun.

Produire : nombre d'entreprises total, et répartition par tranche d'effectif.

**Seuil d'arrêt : moins de 3 000 entreprises dans la cible → arrêter la
recherche ici et conclure NON.** Le marché ne peut pas nourrir un éditeur.

### Étape 2 — Identifier les éditeurs en place

Recherches web à effectuer, en variant le vocabulaire métier réel (pas le
vocabulaire logiciel) :

- `logiciel [métier] comparatif`
- `logiciel [métier] avis`
- `logiciel [métier] alternative`
- `[métier] alternative à [nom du leader identifié]`
- `[métier] logiciel gratuit`

Viser 8 à 15 éditeurs. Pour chacun : nom, URL, cible annoncée, année de
création.

### Étape 3 — Mesurer le plafond du marché (le critère décisif)

Pour chaque éditeur identifié, chercher ses comptes publiés via WebFetch sur
`pappers.fr`, `societe.com`, ou `annuaire-entreprises.data.gouv.fr`. Relever
chiffre d'affaires, effectif, année du dernier exercice publié, et toute levée
de fonds mentionnée dans la presse.

Interprétation (à reporter telle quelle dans le fichier de sortie) :

| Constat | Lecture |
|---|---|
| Leader < 2 M€ de CA après 10 ans d'existence | Plafond de verre — la niche ne nourrit personne |
| Leader 5–30 M€, second < 3 M€ | **Cible idéale** — marché prouvé, mal desservi |
| Trois acteurs > 20 M€, ou levées de fonds > 5 M€ | Éliminatoire — ils gagnent par la distribution |
| Aucun compte publié, tous micro-entreprises | Ambigu — micro-marché ou marché vierge, creuser |

### Étape 4 — Détecter la guerre des prix

Relever le prix d'entrée réel de chaque éditeur (page tarifs, ou demande de
devis mentionnée si le prix est caché).

**Éliminatoire immédiat : la présence d'une offre gratuite complète et
crédible chez un acteur établi.** On ne descend pas sous zéro. Noter aussi si
plusieurs éditeurs se citent mutuellement dans des pages de comparaison
tarifaire agressive — c'est le signe d'une guerre déjà engagée.

### Étape 5 — Corpus exhaustif d'avis

C'est l'étape la plus longue. Ne pas l'abréger, ne pas échantillonner.

**Contexte de volume à connaître.** Le logiciel métier B2B français a très peu
d'avis. Un leader avec 5 000 clients plafonne autour de 100 avis toutes
plateformes confondues. Le corpus attendu par secteur est de l'ordre de 100 à
400 avis, parfois moins. Ce volume est faible, donc **l'exhaustivité est
obligatoire : lire chaque avis individuellement, aucun échantillonnage,
aucune synthèse à partir des notes globales.**

**Hiérarchie des sources, par fiabilité décroissante.** C'est le point
méthodologique central :

| Source | Sollicitation par l'éditeur | Poids |
|---|---|---|
| Trustpilot | Rare, avis spontanés | **Fort** |
| Google Play / App Store | Aucune | **Fort** |
| Reddit, forums métier, groupes Facebook | Aucune | **Fort** |
| Capterra / G2 / GetApp | Massive, campagnes d'éditeurs, parfois avec contrepartie | Faible |
| Comparateurs français (lebonlogiciel, logiciels.pro, saask, etc.) | Contenu affilié ou éditeur | Nul |

**Conséquence à appliquer strictement :** une note globale élevée sur Capterra
ou G2 n'est pas une information. Un écart entre une note Capterra élevée et
des avis Trustpilot négatifs est, lui, une information de premier ordre — le
noter explicitement.

Pour chaque plateforme et chaque éditeur identifié à l'étape 2, parcourir
toutes les pages d'avis disponibles jusqu'à épuisement (suivre la pagination).
Chercher aussi :

- `[nom du logiciel] avis`, `[nom du logiciel] problème`, `[nom du logiciel] bug`
- `[nom du logiciel] résilier`, `[nom du logiciel] arnaque`, `alternative à [nom]`
- `site:reddit.com [métier] logiciel` et les subreddits français du métier
- Forums et syndicats du métier, groupes Facebook professionnels

**Produire un fichier de données brutes** `recherche/[SECTEUR]_avis.md`
contenant chaque avis retenu, sous forme de tableau :

| # | Éditeur | Plateforme | Note | Date | Reproche en une phrase | Catégorie | URL |
|---|---|---|---|---|---|---|---|

Catégories à utiliser : `support`, `bug/fiabilité`, `ergonomie`, `prix caché`,
`fonctionnalité manquante`, `mobile/terrain`, `migration/import`,
`facturation/résiliation`, `performance`.

Reformuler chaque reproche en une phrase — ne pas recopier les avis
verbatim au-delà de quelques mots.

**Puis, dans le fichier principal, agréger** : nombre d'occurrences par
catégorie, en distinguant les sources fortes des sources faibles. Un reproche
répété trois fois sur Trustpilot pèse plus que quinze avis 5 étoiles sur
Capterra.

**Si le corpus total est inférieur à 30 avis**, l'écrire explicitement et
basculer sur la recherche primaire, qui devient la source principale :

- Ouvrir les essais gratuits des 3 principaux éditeurs et documenter les
  frictions réellement constatées (inscription, import de données, premier
  document généré, mobile)
- Relever les fonctionnalités annoncées sur les pages marketing mais absentes
  de la documentation ou du changelog
- Lire les changelogs et notes de version : ce qui n'est jamais mis à jour
  indique un module abandonné
- Identifier les groupes professionnels et fédérations où poser directement la
  question, et les lister dans les zones d'ombre

Un corpus d'avis vide n'autorise pas à conclure « pas de problème détecté ».
Il autorise seulement à conclure « pas de données publiques — vérification
terrain requise ».

### Étape 6 — Contraintes réglementaires

Chercher les obligations légales du secteur avec une **date d'entrée en vigueur
entre 2026 et 2029**. Pour chacune : intitulé, texte de référence, date, qui
est concerné.

Vérifier séparément et explicitement : **le logiciel métier lui-même est-il
soumis à un agrément, un référencement ou une certification d'État ?**
Si oui → éliminatoire, un solo ne peut pas l'obtenir. Chercher les termes
`agrément`, `référencement`, `certifié`, `homologué`, `immatriculé`.

---

## Fichier de sortie

Créer `recherche/[NOM_SECTEUR].md` avec exactement cette structure :

```markdown
# [Secteur]

Recherche effectuée le : [date]
Requêtes web effectuées : [nombre]

## Verdict

[GO / NO-GO / À CREUSER] — [une phrase de justification]

Critère décisif : [lequel, et pourquoi]

## 1. Dimensionnement

Codes NAF retenus : [liste]
Entreprises totales : [nombre] (source : recherche-entreprises.api.gouv.fr, [date])

| Tranche d'effectif | Nombre |
|---|---|

Cible réaliste (segment adressable) : [nombre] — [justification]

## 2. Éditeurs en place

| Éditeur | Créé en | Cible | CA (exercice) | Effectif | Prix d'entrée | Source |
|---|---|---|---|---|---|---|

Offre gratuite détectée : OUI/NON — [lequel, et périmètre réel]
Levées de fonds : [détail ou AUCUNE TROUVÉE]

Lecture du plafond de marché : [selon la grille de l'étape 3]

## 3. Défauts documentés

Corpus : [nombre] avis lus intégralement — détail dans `[SECTEUR]_avis.md`
Répartition : [n] Trustpilot / [n] stores / [n] Reddit-forums / [n] Capterra-G2

| Catégorie | Occurrences (sources fortes) | Occurrences (sources faibles) | Éditeur(s) visé(s) |
|---|---|---|---|

Écart de notation détecté : [note Capterra/G2 vs contenu Trustpilot/stores —
ou AUCUN]

Thèmes dominants : [3 maximum, par occurrences en sources fortes uniquement]

## 4. Contraintes réglementaires

| Obligation | Texte | Date d'entrée en vigueur | Qui est concerné |
|---|---|---|---|

Le logiciel métier est-il certifié/agréé par l'État ? OUI/NON — [preuve]

## 5. Ligne de score (à recopier telle quelle dans SYNTHESE.md)

Renseigner ces sept champs, et rien d'autre. Ce sont eux qui permettent de
comparer les secteurs entre eux.

| Champ | Valeur | Barème |
|---|---|---|
| Entreprises cibles | | <3k = éliminé, 3-15k = 1, 15-50k = 2, >50k = 3 |
| CA du leader | | <2M = 1, 5-30M = 3, >30M ou levée >5M = éliminé |
| Prix plancher constaté | | gratuit = éliminé, <30€ = 1, 30-100€ = 2, >100€ = 3 |
| Occurrences du reproche dominant (sources fortes) | | 0-2 = 1, 3-9 = 2, >=10 = 3 |
| Échéance réglementaire exploitable | | aucune = 0, >36 mois = 1, 12-36 mois = 3, <12 mois = 1 |
| Réutilisation du code de l'app BTP | | aucune = 0, partielle = 2, forte = 3 |
| Certification d'État sur le logiciel | | OUI = éliminé, NON = 0 |

**Score total : /18**

Le score ne décide pas. Les éliminatoires décident. Un secteur à 17/18 avec un
concurrent gratuit reste NO-GO.

Note sur l'échéance : une deadline à moins de 12 mois vaut peu de points, car
il n'y a plus le temps de construire et de se faire connaître avant que le
marché soit équipé.

## 6. Périmètre du MVP, si GO

**Le plus petit périmètre facturable** — ce pour quoi un pro paierait dès le
premier jour, sans le reste. Pas une vision produit, une liste de ce qui doit
exister à la V1.

| Fonction | Indispensable V1 | Justification (avis ou obligation) |
|---|---|---|

Ce qui est explicitement **hors** V1 : [liste]
Estimation de charge de développement : [semaines, pour un développeur seul]

Angle d'entrée retenu, un seul parmi :
- Segment sous le plancher tarifaire des acteurs en place
- Module réglementaire que les gros ne maintiennent pas
- Intégration entre deux outils qui s'ignorent

Pourquoi les acteurs en place ne le font pas : [raison structurelle, pas
« ils n'y ont pas pensé »]

## 7. Fenêtre de lancement

Calcul à rebours depuis l'échéance réglementaire la plus proche :

| Jalon | Date |
|---|---|
| Échéance réglementaire | |
| Pic d'achat estimé (échéance − 6 mois) | |
| Mise en ligne cible (échéance − 12 mois) | |
| Début du développement (mise en ligne − charge V1) | |

Si le début du développement calculé est déjà passé : le noter, et considérer
le secteur comme raté sur ce cycle réglementaire.

## 8. Distribution

| Canal | Où précisément | Coût | Testable en combien de temps |
|---|---|---|---|

Interdits : « SEO », « LinkedIn », « réseaux sociaux », « bouche-à-oreille ».
Exiger des noms : quelle fédération, quel syndicat, quel groupe, quel salon,
quelle newsletter métier, quel prescripteur (expert-comptable, OPCO,
certificateur, organisation professionnelle).

Prix de lancement proposé : [montant] — [positionnement vs plancher constaté]

## 9. Le test à 48 h

La chose la moins chère à faire pour invalider l'hypothèse avant d'écrire une
ligne de code. Une seule, exécutable en deux jours.

Test : [lequel]
Résultat qui invalide : [critère chiffré et non ambigu]

## 10. Sources consultées

| URL | Nature | Éditeur du site | Conflit d'intérêt |
|---|---|---|---|

## 11. Zones d'ombre

[Ce qui n'a pas pu être établi et qu'il faudrait vérifier autrement —
appels, essais gratuits, entretiens avec des professionnels du secteur]
```

---

## Après le dernier secteur

Créer `recherche/SYNTHESE.md`, qui est le **document de décision**. Il ne
résume pas les recherches, il dit quoi lancer, quand, et dans quel ordre.

### A. Tableau de comparaison

Une ligne par secteur, colonnes strictement identiques à la ligne de score de
la section 5, plus le verdict et le score total. Trié par score décroissant,
les NO-GO en bas avec la mention de l'éliminatoire qui les a sortis.

| Secteur | Cibles | CA leader | Prix plancher | Reproche dominant | Échéance | Réutil. BTP | Score | Verdict | Éliminatoire |
|---|---|---|---|---|---|---|---|---|---|

### B. Séquencement

Contrainte à respecter : **un seul développeur, déjà engagé sur l'application
BTP.** Pas de lancement parallèle. Le séquencement est donc strictement série,
et la question est l'ordre, pas la simultanéité.

| Rang | Secteur | Début dev | Mise en ligne | Pourquoi à ce rang |
|---|---|---|---|---|

Règle d'arbitrage entre deux secteurs de score proche : celui dont la fenêtre
de lancement se ferme le plus tôt passe en premier. Un bon secteur dont
l'échéance est dans 30 mois attendra ; un secteur moyen dont l'échéance est
dans 15 mois n'attendra pas.

### C. Plan des 30 prochains jours

Uniquement des actions exécutables, avec une sortie vérifiable. Pas de
« réfléchir à », pas de « approfondir ».

| Semaine | Action | Sortie attendue | Ce qui invalide |
|---|---|---|---|

Y inclure les tests à 48 h (section 9) des deux premiers secteurs du
classement, **avant** toute décision de développement.

### D. Ce qui reste à vérifier hors ligne

Liste consolidée des zones d'ombre de tous les secteurs, triée par impact sur
la décision. Pour chacune : la question exacte, et à qui la poser.

### E. Rappel des éliminatoires

Ne pas classer un secteur GO s'il ne passe pas les trois éliminatoires :
plus de 3 000 entreprises cibles, aucune offre gratuite crédible d'un acteur
établi, aucune certification d'État sur le logiciel.

Si aucun secteur ne ressort GO, l'écrire clairement et le dire en une phrase en
tête du document. C'est un résultat valide, et le plus utile de tous s'il est
vrai.
