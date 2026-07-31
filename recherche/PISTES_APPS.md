# PISTES_APPS — applications à créer pour TPE, artisans hors BTP, freelances

Session du **31/07/2026**. Recherche **par irritant**, pas par code NAF.
Le protocole sectoriel (`PROMPT_RECHERCHE_SECTEUR.md`) est **suspendu** pour
cette phase, sur instruction de l'utilisateur. Les règles de données du § 1 de
`CLAUDE.md` restent intégralement applicables : aucun chiffre sans URL et sans
date, `INCONNU` autorisé et préférable à un proxy, 10000 n'est jamais un nombre.

---

## 0. Méthode, périmètre et limites — à lire avant les fiches

### Critères appliqués (remplacent les quatre éliminatoires du protocole)

**Restent éliminatoires :**
1. un logiciel **certifié ou agréé par l'État** sur ce besoin précis ;
2. un **outil gratuit** fourni par l'État, une chambre consulaire ou un
   organisme financé par cotisation obligatoire, **sur ce besoin précis** ;
3. un **concurrent gratuit crédible et pérenne** d'un acteur établi.

**Ne sont plus éliminatoires :** la présence d'un gros éditeur (question
reformulée : *couvre-t-il CE besoin, ou seulement le métier en général ?*), et
un marché sous 3 000 entreprises.

**Seuil retenu :** 500 clients à 50 €/mois, soit **300 k€/an**. Chaque fiche
donne la **pénétration requise** = 500 ÷ population, parce que c'est le seul
chiffre qui se discute honnêtement quand le taux d'équipement est inconnu.

**Consigne du 31/07/2026 :** privilégier les irritants **transverses**. Le
fichier est donc en deux parties — transverses d'abord, mono-métier ensuite —
et chaque irritant a été testé sur les autres métiers de sa famille avant
d'être rangé comme spécifique.

### Trois limites de cette session, à connaître avant d'exploiter les fiches

1. **Reddit est inaccessible à l'agent.** `reddit.com` est refusé à la fois par
   l'outil de recherche (`API Error 400 : domains not accessible to our user
   agent`) et par la récupération de page. La source forte n° 3 de la
   hiérarchie du § 3 de `CLAUDE.md` est donc **absente de ce corpus**.
   Les groupes Facebook, également prévus au plan de recherche, ne sont pas
   récupérables sans authentification.
2. **Le poids des sources d'irritant est très inégal, et c'est le point faible
   du livrable.** Une partie substantielle des « preuves » disponibles sur ces
   métiers sont des **blogs d'éditeurs de logiciel** — poids **faible à nul**
   au sens du § 3 de `CLAUDE.md`, puisque l'éditeur décrit le manque que son
   produit comble. Chaque fiche porte donc une ligne **« Poids de la preuve »**
   explicite. Une piste dont l'irritant n'est étayé que par des sources
   éditeurs est signalée comme telle et **ne doit pas être engagée sans
   vérification primaire** (essais, entretiens).
3. **L'API `recherche-entreprises` ne sait pas compter les indépendants.** La
   tranche d'effectif `NN` (effectif non renseigné) — où se trouvent les
   micro-entrepreneurs, c'est-à-dire précisément la cible — **plafonne à 10000
   sur presque tous les codes testés**. Vérifié le 31/07/2026 : la
   sous-partition par `nature_juridique=1000` (entrepreneur individuel) et le
   filtre `est_entrepreneur_individuel=true` **plafonnent aussi** sur 74.20Z.
   Le plafond n'a donc **pas pu être cassé**. Les décomptes NAF ci-dessous sont
   des **minorants** portant sur les entreprises d'**au moins un salarié**, et
   la population réelle est dimensionnée par l'**open data Urssaf**.

### Socle de population — sources communes à plusieurs fiches

**A. Micro-entrepreneurs par secteur, Urssaf open data.** Requête du
31/07/2026 sur le jeu `auto-entrepreneurs-par-secteur-dactivite`, dernier
trimestre disponible **31/12/2025** :
`https://open.urssaf.fr/api/explore/v2.1/catalog/datasets/auto-entrepreneurs-par-secteur-dactivite/records?order_by=dernier_jour_du_trimestre%20desc&limit=30`

| Secteur Urssaf | Administrativement actifs | **Économiquement actifs** |
|---|---:|---:|
| S3 — Autres services personnels | 184 529 | **113 136** |
| PZ — Enseignement | 166 623 | **103 047** |
| S2 — Coiffure et soins du corps | 136 726 | **98 817** |
| QZ — Santé | 120 372 | **92 573** |
| M4 — Design, graphisme | 83 187 | **45 062** |
| IZ2 — Restauration et débits de boissons | 65 142 | **32 475** |
| S1 — Réparations hors automobile | 35 634 | **23 294** |
| HZ1 — Taxis · VTC | 33 526 | **16 445** |
| AZ — Agriculture, sylviculture, pêche | 3 496 | **2 393** |
| **Tous secteurs** | **2 430 751** | — |

> **La colonne qui compte est « économiquement actifs ».** L'Urssaf publiait
> par ailleurs que **seuls 49,8 % des micro-entrepreneurs déclarent un chiffre
> d'affaires positif** (`https://tpeactu.fr/2026/01/29/auto-entrepreneurs-chiffre-affaires-urssaf-2025/`,
> consulté le 31/07/2026 — **source de presse, pas la publication Urssaf
> elle-même**). Dimensionner sur les « administrativement actifs » double
> presque la cible et serait une estimation déguisée en fait.

**B. Décomptes NAF, minorants.** API `recherche-entreprises.api.gouv.fr`,
requêtes du 31/07/2026, `etat_administratif=A`, **somme des tranches
`01`+`02`+`03`+`11`+`12`** prises **une par une** (jamais en liste — piège
documenté au § 5 de `CLAUDE.md`). Forme de la requête :
`https://recherche-entreprises.api.gouv.fr/search?activite_principale=[CODE]&etat_administratif=A&tranche_effectif_salarie=[T]&per_page=1`

| Code | Libellé court | Somme 01→12 (≥ 1 salarié) | Tranche `NN` |
|---|---|---:|---|
| 74.20Z | Activités photographiques | 1 446 | >10000 (PLAFOND) |
| 90.01Z | Arts du spectacle vivant | 10 131 | >10000 (PLAFOND) |
| 90.02Z | Soutien au spectacle vivant | 2 028 | >10000 (PLAFOND) |
| 56.21Z | Services des traiteurs | 3 627 | >10000 (PLAFOND) |
| 56.10C | Restauration de type rapide | 30 720 *(minorant, 2 tranches plafonnées)* | >10000 (PLAFOND) |
| 96.02B | Soins de beauté | 9 966 | >10000 (PLAFOND) |
| 96.09Z | Autres services personnels n.c.a. | 4 090 | >10000 (PLAFOND) |
| 85.51Z | Enseignement de disciplines sportives | 4 434 | >10000 (PLAFOND) |
| 85.59B | Autres enseignements | 4 355 | >10000 (PLAFOND) |
| 81.30Z | Services d'aménagement paysager | 14 914 | >10000 (PLAFOND) |
| 95.11Z | Réparation d'ordinateurs | 1 077 | >10000 (PLAFOND) |
| 95.29Z | Réparation d'autres biens personnels | 1 260 | >10000 (PLAFOND) |
| 47.79Z | Commerce de détail de biens d'occasion | 1 884 | >10000 (PLAFOND) |
| 49.32Z | Transport de voyageurs par taxis | 9 320 | >10000 (PLAFOND) |
| 85.53Z | Enseignement de la conduite | 5 499 | >10000 (PLAFOND) |
| 86.90E | Rééducation, appareillage, podologues | 5 569 | >10000 (PLAFOND) |
| 86.90F | Santé humaine non classée ailleurs | 1 015 | >10000 (PLAFOND) |
| 74.10Z | Activités spécialisées de design | 3 794 | >10000 (PLAFOND) |
| 01.62Z | Soutien à la production animale | 987 | **6 319** *(non plafonné)* |

**C. Deux gratuités établies qui ferment plusieurs pistes d'un coup.**

- **Indy — offre « Essentiel » à 0 €/mois**, non bridée : devis et factures
  illimités, comptabilité automatisée, synchronisation bancaire,
  **facturation électronique via plateforme agréée DGFiP**, application mobile.
  Seules les déclarations fiscales sont payantes (9 € à 49 €/mois).
  `https://www.indy.fr/tarifs/`, consulté le 31/07/2026.
  → **Toute piste dont le cœur est « devis + facture + compta pour le métier X »
  est morte.** L'éliminatoire n° 3 est déclenché par un acteur établi qui a
  choisi la gratuité comme modèle, y compris sur l'obligation 2026-2027.
- **Facturation électronique — l'obligation est un chemin d'État, pas un
  marché ouvert.** Réception obligatoire au **1er septembre 2026**, émission
  pour les micro-entreprises au **1er septembre 2027**, via une **plateforme
  agréée (PDP) immatriculée** ; le Portail Public de Facturation n'est plus
  qu'un annuaire et concentrateur.
  `https://www.portail-autoentrepreneur.fr/academie/gestion-auto-entreprise/facturation/facture-electronique-obligatoire`
  et `https://kpmg.com/av/fr/avocats/eclairages/2024/10/facturation-electronique-le-schema-initialement-prevu-est-modifie.html`,
  consultés le 31/07/2026.
  → **Éliminatoire n° 1 déclenché** sur ce besoin précis : l'immatriculation PDP
  est un agrément d'État portant sur le logiciel lui-même.

---

# PARTIE A — PISTES TRANSVERSES

---

## A1. Le dossier client conforme du professionnel non-médical

- **Métiers visés** — tatoueurs et perceurs · praticiens du bien-être
  (naturopathes, sophrologues, hypnothérapeutes, réflexologues) ·
  esthéticiennes pratiquant des actes à effraction ou à appareils ·
  pet-sitters et pensions · éleveurs canins et félins. Point commun : **une
  obligation légale de recueillir, formaliser et conserver un document par
  client, sans aucune profession organisée en ordre pour fournir l'outil.**

- **Population** —
  · Tatoueurs : **au moins 15 000 en activité principale en 2024** selon le
  Syndicat National des Artistes Tatoueurs, chiffre que la source qualifie
  elle-même d'**approximatif** (fondé sur les données des distributeurs) —
  `https://www.evotattoo.fr/blog/tendances-marche-tatouage-france-europe-etats-unis-2013-2023`,
  consulté le 31/07/2026. *Reprise par un blog, pas la publication du SNAT.*
  · Praticiens bien-être : **5 700 retirés de Doctolib**, dont 2 700
  hypnothérapeutes, 1 500 sophrologues, 800 naturopathes —
  `https://www.lequotidiendumedecin.fr/actus-medicales/esante/naturopathes-hypnotherapeutes-sophrologues-doctolib-fait-le-menage-et-exclut-les-5-700-praticiens`,
  consulté le 31/07/2026. C'est un **sous-ensemble** (ceux qui étaient sur une
  seule plateforme), donc un minorant net de la population.
  · Élevages félins : **9 299, dont 2 576 éleveurs professionnels** (LOOF), via
  `https://www.beatricesconseilscanins.fr/blog/elevage-de-chat-en-france.html`,
  consulté le 31/07/2026 — *source secondaire, à reprendre sur le LOOF.*
  · Pet-sitters : `INCONNU`. Deux chiffres incompatibles circulent (230 000 en
  2020 ; 35 000 en 2025) sur la même source
  `https://www.snobdogacademy.fr/p1/les-chiffres-du-secteur-du-pet-sitting` —
  un écart d'un facteur 6,6 non expliqué. **Ne pas s'en servir.**
  · **Population agrégée retenue : `INCONNU`, minorée à ~20 000** par la somme
  des seuls chiffres défendables (15 000 tatoueurs + 5 700 praticiens ex-Doctolib).

- **L'irritant** — *ces professionnels doivent produire et archiver pendant des
  années un dossier par client engageant leur responsabilité pénale, et le font
  sur papier ou en fichiers épars.*
  · Tatoueurs : les formulaires doivent porter « les mentions légales du Code de
  la santé publique, la gestion des mineurs avec autorisation parentale, la
  **traçabilité des encres (REACH)**, les alertes sanitaires RappelConso et un
  **archivage conforme de 5 ans** » —
  `https://tattoobon.fr/blog/obligations-legales-tracabilite-france-2026`,
  consulté le 31/07/2026.
  · Praticiens bien-être : durcissement CNIL fin 2025 — obligation de « tenir un
  **registre des traitements**, d'informer chaque client de ses droits d'accès et
  de suppression, et de répondre à toute demande sous un mois », tout bilan de
  vitalité contenant des **données de santé** au sens du RGPD ; amendes jusqu'à
  4 % du CA —
  `https://www.france-epargne.fr/news/naturopathes-et-praticiens-du-bien-etre-face-a-un-durcissement-reglementaire-en-2026`,
  consulté le 31/07/2026.
  · Pet-sitters : le **contrat écrit est obligatoire** pour toute garde
  rémunérée, au titre de l'**article L214-6-1 du Code rural et de la pêche
  maritime** —
  `https://www.dogsitting.fr/guide/guide-aspects-pratiques-juridiques-garde-animaux.asp`
  et `https://comdewouf.fr/contrat-pet-sitter`, consultés le 31/07/2026.

- **Poids de la preuve** — **Moyen.** L'obligation légale est solide et
  vérifiable (textes cités, ARS, Code rural, CNIL) ; **le fait que les
  professionnels la gèrent mal ne l'est pas** — il vient de blogs sectoriels et
  d'éditeurs. C'est la vérification primaire n° 1 à faire.

- **Ce qu'ils utilisent aujourd'hui** — classeurs papier de décharges signées,
  photos de formulaires dans la pellicule du téléphone, Google Forms,
  fichiers Word imprimés, cahier de traçabilité manuscrit.

- **Outils existants sur ce besoin précis, et ce qui leur manque** —
  **Clic2Sign** (`https://clic2sign.com/`, consulté le 31/07/2026) est le seul
  produit trouvé qui attaque frontalement le besoin, et il est **mono-métier**
  (PMU, tatouage, piercing). Aucun équivalent trouvé pour les praticiens
  bien-être, les pet-sitters ou les éleveurs. Les logiciels de RDV du secteur
  (Zen Agenda, Resalib, Crenolib) gèrent l'agenda et la facturation, **pas le
  consentement horodaté, la traçabilité de lot, ni l'archivage probant**.
  Ce qui manque partout : la **valeur probante** (horodatage inaltérable,
  export opposable en cas de contrôle ARS / DDPP / CNIL).

- **Prix et revenu** — 25 à 40 €/mois. Un tatoueur facture le tatouage plusieurs
  centaines d'euros ; 30 €/mois est marginal. **500 clients à 50 €/mois =
  300 k€/an** ; à 30 €/mois il faut **833 clients**. Sur une base minorée de
  20 000 professionnels, cela demande **4,2 %** de pénétration à 30 €, ou
  **2,5 %** à 50 €.

- **Éliminatoires** —
  1. *Certification d'État sur le logiciel* : **NON déclenché.** La formation
     hygiène et salubrité et la déclaration ARS pèsent sur **le professionnel**,
     jamais sur l'outil (`https://www.paca.ars.sante.fr/activite-de-tatouage-percage-corporel-et-maquillage-permanent-0`,
     consulté le 31/07/2026).
  2. *Outil public gratuit* : **NON déclenché** — aucun outil d'État ou
     consulaire trouvé sur le consentement ou la traçabilité de ces métiers.
     ⚠️ **Contrôle non exhaustif** : les ARS sont régionales, une initiative
     locale n'est pas exclue. À reprendre région par région avant d'engager.
  3. *Gratuit crédible d'un acteur établi* : **NON déclenché** sur ce besoin.

- **Charge de développement, dev seul** — **10 à 14 semaines** pour un MVP
  mono-métier (tatoueur) : formulaires de consentement paramétrables, signature
  sur écran, photo, horodatage, coffre d'archivage, export PDF de contrôle.
  **+6 à 8 semaines** par métier supplémentaire (les gabarits réglementaires
  diffèrent, le moteur non).

- **Verdict — À CREUSER.** C'est la seule piste du corpus où une obligation
  légale opposable, transverse à cinq métiers, ne rencontre qu'un seul produit
  mono-métier ; réserve : la mauvaise tenue du dossier reste à prouver en primaire.

---

## A2. L'avance immédiate de crédit d'impôt pour le prestataire solo

- **Métiers visés** — professeur particulier à domicile · coach sportif à
  domicile · jardinier / petits travaux · assistance informatique à domicile ·
  esthétique à domicile pour publics fragiles · garde d'enfants · ménage.
  Point commun : **le crédit d'impôt de 50 % est l'argument commercial du
  métier, et le prestataire seul ne sait pas le servir en temps réel.**

- **Population** — **82 776 organismes de services à la personne déclarés dans
  la base NOVA au 1er janvier 2025, dont 91 % d'entreprises (micro-entrepreneurs
  inclus)**, soit ≈ 75 300 entreprises ; +18 % en un an.
  `https://tool-advisor.fr/blog/chiffres-service-a-la-personne/`, consulté le
  31/07/2026 — **le chiffre est attribué à la DGE / base NOVA mais je l'ai lu
  sur un site tiers ; la publication DGE primaire n'a pas été atteinte.**
  Cadrage cohérent côté Urssaf : PZ Enseignement **103 047** micro-entrepreneurs
  économiquement actifs et S3 Autres services personnels **113 136** au
  31/12/2025 (socle A), dont une fraction inconnue relève du SAP.
  **Pénétration requise : 500 ÷ 75 300 = 0,66 %.** La plus basse de tout le
  fichier.

- **L'irritant** — *un indépendant ne peut pas offrir l'avance immédiate sans
  passer par un logiciel lui-même habilité par l'Urssaf, et la conséquence
  documentée est qu'il renonce et sous-traite sa relation client à une agence.*
  « Il peut être préférable pour les professeurs particuliers indépendants de
  s'associer à des organismes de soutien scolaire agréés (SAP) […] tout en
  continuant à leur fournir un service de cours particuliers de qualité, **sans
  être tourmenté par le côté administratif** » —
  `https://groupe-reussite.fr/ressources/donner-cours-faire-beneficier-clients-credit-impots/`,
  consulté le 31/07/2026.
  Verrou technique confirmé : « **Sans logiciel habilité, il n'est pas possible
  de transmettre les demandes de paiement à l'Urssaf** » —
  `https://www.avance-immediate.fr/blog/comment-obtenir-api-tiers-de-prestation`,
  consulté le 31/07/2026. L'API est technique et **n'offre aucune interface
  utilisateur** : sans éditeur, il n'y a pas de saisie manuelle possible.

- **Poids de la preuve** — **Faible sur le vécu, fort sur le verrou.** La
  citation clé provient d'un **organisme de soutien scolaire qui a intérêt à ce
  que les professeurs passent par lui** — conflit d'intérêt direct, à noter au
  sens du § 3 de `CLAUDE.md`. Le verrou technique, lui, est établi.

- **Ce qu'ils utilisent aujourd'hui** — le CESU classique (crédit d'impôt
  l'année suivante, donc l'avantage n'est pas visible à l'achat), ou l'adossement
  à une agence qui prélève sa marge, ou le renoncement pur au dispositif.

- **Outils existants, et ce qui leur manque** — **espace très encombré** :
  Sinao, Abby, Axonaut, VosFactures, Evoliz, avancio.fr, NeedMe. Ce sont
  majoritairement des **outils de facturation généralistes qui ont ajouté un
  module**. Ce qui manque : le **parcours d'entrée** — obtenir le numéro SAP via
  NOVA, monter le dossier d'habilitation (attestation de régularité fiscale,
  RIB, maquette), inscrire le premier client. C'est là que le solo décroche, et
  aucun outil ne prend l'utilisateur par la main sur cette séquence.

- **Prix et revenu** — 20 à 35 €/mois, avec une justification économique
  imparable (le crédit d'impôt vaut 50 % du prix de chaque prestation).
  **500 × 50 € = 300 k€/an** ; à 25 €/mois il faut **1 000 clients**, soit
  **1,3 %** des 75 300 entreprises SAP.

- **Éliminatoires** —
  1. *Certification d'État* : **frôlé, non déclenché.** L'éditeur doit être
     **habilité à l'API Tiers de prestation** — c'est bien un filtre d'État sur
     le logiciel. Mais aucune homologation, audit, coût ni exigence de taille
     n'est documenté : la condition est technique (OAuth2, format JSON défini par
     l'Urssaf) et sanctionnée par la remise d'un Client ID / Client Secret
     (`https://www.data.gouv.fr/dataservices/api-tiers-de-prestation`, redirigé
     depuis `api.gouv.fr`, consulté le 31/07/2026). Des éditeurs de très petite
     taille l'ont obtenue (Sinao, VosFactures), ce qui prouve l'accessibilité à
     un dev seul. **C'est néanmoins le risque n° 1 de cette piste et il doit
     être levé en premier, avant toute ligne de code.**
  2. *Outil public gratuit* : **NON déclenché.** L'Urssaf fournit l'API
     gratuitement mais **aucune interface de saisie** pour le prestataire.
  3. *Gratuit crédible* : **NON déclenché** — tous les outils habilités trouvés
     sont payants.

- **Risque hors éliminatoires, à ne pas ignorer** — le crédit d'impôt SAP est
  **politiquement instable**. Des amendements au PLF proposaient un passage de
  50 % à 40 %, une limitation des activités éligibles et une baisse du plafond
  (`https://www.coursprofs.fr/blog/reforme-credit-impot-cours-particuliers.php`,
  publié le 09/07/2025, consulté le 31/07/2026). **Une app dont toute la valeur
  dérive d'un avantage fiscal hérite du risque législatif de cet avantage.**

- **Charge de développement, dev seul** — **8 à 12 semaines**, dont une part
  substantielle non technique : montage du dossier d'habilitation, recette avec
  l'Urssaf, gestion des rejets de demandes de paiement.

- **Verdict — À CREUSER**, avec deux réserves lourdes : l'habilitation éditeur
  à lever d'abord, et une valeur adossée à un crédit d'impôt sous menace politique.

---

## A3. La prestation à date unique : verrouiller la date, l'acompte et le contrat

- **Métiers visés** — photographe · DJ et musicien · traiteur · food truck ·
  loueur de matériel événementiel · décorateur · officiant. Point commun :
  **une ressource unique et non duplicable — une date — vendue plusieurs mois à
  l'avance, dont la perte est sèche.**

- **Population** — décomptes NAF du 31/07/2026 (socle B), **minorants
  ≥ 1 salarié** : photographie 1 446 · spectacle vivant 10 131 · soutien au
  spectacle 2 028 · traiteurs 3 627 · restauration rapide 30 720. Les tranches
  `NN` de ces cinq codes sont **toutes >10000 (PLAFOND)** : la population
  d'indépendants est **`INCONNU` et très supérieure**. Cadrage Urssaf : M4
  Design/graphisme **45 062** et IZ2 Restauration **32 475** micro-entrepreneurs
  économiquement actifs au 31/12/2025.
  **Population agrégée `INCONNU`, minorée à 47 952** (somme des cinq codes NAF).
  **Pénétration requise ≤ 1,0 %.**

- **L'irritant** — *le devis, le contrat, l'acompte et le calendrier vivent dans
  quatre outils qui ne se parlent pas, et la brique la plus utilisée du métier
  ignore les trois autres.* « Beaucoup de photographes utilisent des galeries en
  ligne comme Pixieset, Pic-Time ou Dropbox […] ces galeries sont parfaites pour
  livrer les photos, **mais ne gèrent ni les devis, ni les factures, ni les
  contrats** » — `https://www.helpho.io/blog/outil-gestion-photographe-independant-guide`,
  consulté le 31/07/2026. Contexte juridique réel : « un accord oral n'a aucune
  valeur juridique », l'acompte impose « une facture d'acompte à la signature du
  contrat **et** une facture de solde à la fin »
  (`https://www.leguideduphotographedemariage.fr/juridique-faq/`, consulté le
  31/07/2026), et les litiges de non-livraison sont documentés
  (`https://www.litige.fr/articles/prestataire-mariage-photographe-retard-non-conformite`,
  consulté le 31/07/2026).

- **Poids de la preuve** — **FAIBLE, et c'est disqualifiant en l'état.** La
  citation centrale vient de **Helpho, qui vend exactement le produit décrit** —
  poids nul au sens du § 3 de `CLAUDE.md`. Les autres sources sont des guides
  professionnels décrivant le **droit**, pas la **souffrance**. Le forum
  `communaute.mariages.net` consulté est peuplé de **mariés**, pas de
  prestataires. **Je n'ai pas de preuve d'irritant en source forte sur cette
  piste**, et l'absence de Reddit y est directement responsable.

- **Ce qu'ils utilisent aujourd'hui** — agenda Google pour bloquer la date,
  Word pour le contrat, virement pour l'acompte, tableur pour le suivi,
  WhatsApp pour tout le reste. Pixieset/Pic-Time côté livraison.

- **Outils existants, et ce qui leur manque** — Helpho et Livoria (France),
  Studio Ninja, Iris Works et HoneyBook (États-Unis). Les outils américains
  ignorent la cession de droits d'auteur au sens de l'**article L131-3 du Code
  de la propriété intellectuelle**, qui impose que chaque droit cédé fasse
  l'objet d'une mention distincte (`https://www.helpho.io/blog/contrat-cession-droits-image-guide-complet`,
  consulté le 31/07/2026 — *source éditeur*). Ce qui manque surtout :
  **rien ne couvre à la fois le photographe, le DJ et le traiteur**, alors que
  la mécanique de date, d'acompte et d'annulation est identique.

- **Prix et revenu** — 30 à 45 €/mois. **500 × 50 € = 300 k€/an** ; à 35 €/mois
  il faut **714 clients**, soit **1,5 %** de la base minorée.

- **Éliminatoires** — n° 1 **NON déclenché** · n° 2 **NON déclenché** ·
  n° 3 **NON déclenché** (Helpho, Livoria, Studio Ninja sont tous payants ;
  aucune offre gratuite crédible trouvée sur ce besoin).

- **Charge de développement, dev seul** — **12 à 16 semaines** : catalogue de
  prestations, devis, signature électronique, échéancier acompte/solde,
  calendrier de dates verrouillées, relances.

- **Verdict — À CREUSER SOUS RÉSERVE EXPRESSE.** Les trois éliminatoires sont
  francs et la mécanique est réellement transverse, mais **l'irritant n'est pas
  prouvé en source forte** — à confirmer par entretiens avant tout engagement.

---

## A4. Le suivi des forfaits et séances prépayées — **ÉCARTÉ**

- **Métiers visés** — coach sportif, praticien bien-être, professeur
  particulier, moniteur, ostéopathe. Le carnet de 10 séances est le format de
  vente standard de toute cette famille (forfait 10 séances à domicile ≈ 485 €,
  `https://mondevis.com/blog/forfait-10-seances-coach/`, consulté le 31/07/2026).

- **L'irritant supposé** — savoir combien de séances restent, à qui, et depuis
  quand, sans le tenir de tête ni sur un carnet.

- **Éliminatoires** — **n° 3 DÉCLENCHÉ, deux fois.**
  · **Zen Agenda** annonce une application **« 100 % gratuite »** pour praticiens
  bien-être incluant agenda, clients, **facturation conforme**, rappels SMS
  inclus, réservation en ligne 24/7, **gestion des soins et des forfaits**, sans
  commission ni engagement — `https://www.zen-agenda.com/fonctionnalites`,
  consulté le 31/07/2026.
  · **Fit'Distance** annonce « l'accès à **99 % de ses fonctionnalités
  gratuitement à vie** » pour les coachs sportifs indépendants —
  `https://fitdistance.io/fr/`, consulté le 31/07/2026.
  ⚠️ Ces deux gratuités sont **déclarées par les éditeurs eux-mêmes** et n'ont
  pas été vérifiées par essai. Le périmètre réel devrait être constaté avant de
  refermer définitivement (§ 2 de `CLAUDE.md` : « le périmètre réel de la
  gratuité doit être constaté, pas déduit d'une mention marketing »).

- **Verdict — ÉCARTÉ** : deux acteurs revendiquent la gratuité pérenne sur
  exactement ce besoin, dans deux des métiers les plus peuplés de la famille.

---

## A5. Les registres réglementaires numériques — **ÉCARTÉ**

- **Métiers visés** — brocanteur et dépôt-vente (livre de police), restaurateur
  et food truck (PMS / HACCP), éleveur (registre d'élevage).

- **L'irritant** — réel et documenté : « les PMS papier vieillissent mal :
  dossiers incomplets, relevés oubliés, dates rectifiées », alors que les
  relevés de température sont obligatoires **deux fois par jour** et
  **conservés 3 ans** (`https://www.kooklin.fr/registre-haccp/` et
  `https://octopus-haccp.com/plan-de-maitrise-sanitaire-pdf-vierge/`, consultés
  le 31/07/2026). Le livre de police numérique impose numérotation continue
  inaltérable et horodatage automatique (`https://registeo.fr/livre-de-police`,
  consulté le 31/07/2026).

- **Éliminatoires** — **n° 3 DÉCLENCHÉ sur l'HACCP.** Au moins trois
  applications gratuites occupent le besoin : **HACCP Facile** (version gratuite
  à 4 modules dont températures de frigos, `https://www.haccp-facile.com/`),
  **Hygie HACCP** (`https://hygiesolution.com/telecharger-application-haccp-hygie/`),
  et `https://app-haccp-gratuite.fr/`, consultés le 31/07/2026.
  Sur le **livre de police**, l'éliminatoire n° 3 n'est pas déclenché, mais le
  besoin est **déjà servi par des spécialistes** (Registeo, livre-de-police.com,
  Tracely) sur une base de **1 884** entreprises à ≥ 1 salarié en 47.79Z
  (socle B) — trop étroit et trop occupé pour 500 clients.

- **Verdict — ÉCARTÉ** : gratuité installée côté HACCP, marché déjà servi et
  étroit côté livre de police.

---

## A6. La facturation et la comptabilité de l'indépendant — **ÉCARTÉ**

- **Métiers visés** — tous. C'est l'irritant le plus cité de toute la recherche,
  sur VTC comme sur musicien, photographe ou paysagiste.

- **Éliminatoires** — **n° 3 DÉCLENCHÉ frontalement** par l'offre Essentiel
  d'Indy à 0 €/mois, non bridée, facture électronique conforme comprise
  (socle C, `https://www.indy.fr/tarifs/`). Et **n° 1 DÉCLENCHÉ** sur le volet
  facturation électronique : l'immatriculation PDP est un agrément d'État
  portant sur le logiciel (socle C).

- **Verdict — ÉCARTÉ.** Les deux éliminatoires les plus durs tombent ensemble.
  **Conséquence pour tout le fichier : aucune piste ne doit reposer sur la
  facturation comme cœur de valeur.** Elle ne peut être qu'un accessoire.

---

## A7. La prise de rendez-vous des praticiens exclus des plateformes santé — **ÉCARTÉ**

- **Métiers visés** — naturopathes, sophrologues, hypnothérapeutes,
  réflexologues, magnétiseurs, étiopathes.

- **L'irritant** — **le mieux documenté de toute la session.** Doctolib a
  décidé de ne plus référencer aucun praticien sans numéro RPPS ou ADELI, et
  **5 700 praticiens ont disparu de la plateforme** — 2 700 hypnothérapeutes,
  1 500 sophrologues, 800 naturopathes — avec « six mois pour trouver une autre
  solution ». Motif déclaré : « Nous avons décidé de nous recentrer exclusivement
  sur les professionnels référencés par les autorités de santé. »
  `https://www.lequotidiendumedecin.fr/actus-medicales/esante/naturopathes-hypnotherapeutes-sophrologues-doctolib-fait-le-menage-et-exclut-les-5-700-praticiens`,
  consulté le 31/07/2026. **Source de presse professionnelle : poids fort.**

- **Pourquoi c'est écarté quand même** — **le marché a déjà répondu, et l'une
  des réponses est gratuite.** Resalib (inscription gratuite, prise de RDV à
  partir de ≈ 29,99 €/mois, **80 000 praticiens inscrits** revendiqués —
  `https://www.resalib.fr/`), Crenolibre (32 à 47 €/mois), Medoucine (119 €/mois
  TTC, plus de 2 000 praticiens), et surtout **Zen Agenda, gratuit, avec
  réservation en ligne, rappels SMS et facturation**
  (`https://www.zen-agenda.com/fonctionnalites`), tous consultés le 31/07/2026.
  **Éliminatoire n° 3 déclenché.** L'exclusion Doctolib date de 2022 : la
  fenêtre s'est refermée.

- **Verdict — ÉCARTÉ** : irritant excellemment prouvé, mais quatre ans trop tard
  et un concurrent gratuit installé sur le besoin.
  **Note pour A1 :** cette population reste intéressante — pas sur le
  rendez-vous, mais sur la conformité RGPD / données de santé, où rien ne la sert.

---

# PARTIE B — PISTES MONO-MÉTIER

---

## B1. Le devis du traiteur événementiel : au convive, pas au forfait

- **Métier et population** — traiteurs, **3 627** entreprises actives à
  ≥ 1 salarié en 56.21Z (socle B, 31/07/2026), tranche `NN`
  **>10000 (PLAFOND)**. Population réelle `INCONNU`.
  **Pénétration requise ≥ 13,8 %** sur la base minorante — élevé, mais la base
  est fausse par construction (le plafond masque les indépendants).

- **L'irritant** — le devis traiteur se recalcule intégralement à chaque
  changement du nombre de convives, et le tableur ne suit pas les allergènes :
  « **Excel ne gère pas les 14 allergènes majeurs**, et si un convive fait une
  réaction allergique sans traçabilité alimentaire, le risque est sanitaire et
  juridique » ; manquent aussi les « fiches techniques et fiches labo avec
  **calcul du coût matière par couvert**, pas seulement par prestation globale ».
  `https://www.skello.io/blog/logiciel-traiteur-comparatif-2026-et-guide-pour-bien-choisir`,
  consulté le 31/07/2026.

- **Poids de la preuve** — **Faible.** Skello est un éditeur. Le fond
  réglementaire (14 allergènes, règlement INCO) est vrai indépendamment.

- **Ce qu'ils utilisent** — Excel, et des devis retapés à chaque variation.

- **Outils existants** — helloharel (ERP traiteur), Skello (planning). Ce qui
  manque : un outil **à l'échelle d'un traiteur seul**, pas un ERP.

- **Prix et revenu** — 40 à 60 €/mois (le devis moyen se compte en milliers
  d'euros). **500 × 50 € = 300 k€/an.**

- **Éliminatoires** — n° 1 NON · n° 2 NON · n° 3 NON. Attention toutefois :
  la brique HACCP adjacente est, elle, couverte par des gratuits (A5).

- **Charge de développement** — **10 à 14 semaines.**

- **Verdict — À CREUSER**, en veillant à ne pas déborder sur l'HACCP où la
  gratuité est installée.

---

## B2. Le montage des demandes de bonus réparation (QualiRépar)

- **Métier et population** — réparateurs labellisés : **environ 6 500 fin 2025**,
  pour près de 10 000 points de réparation ; **715 200 réparations** ont
  bénéficié du bonus en 2024, presque 4 fois plus qu'en 2023 ; enveloppe de
  **512 M€ sur 2022-2028**.
  `https://www.label-qualirepar.fr/`, consulté le 31/07/2026.
  Cadrage Urssaf : S1 Réparations hors automobile, **23 294** micro-entrepreneurs
  économiquement actifs au 31/12/2025 (socle A).
  **Pénétration requise : 500 ÷ 6 500 = 7,7 %** sur les labellisés seuls —
  élevé ; le gisement est dans les non-encore-labellisés.

- **L'irritant** — chaque réparation subventionnée suppose un devis préalable,
  des pièces documentées (origine, qualité), une garantie de 3 mois, puis une
  demande de remboursement auprès d'un éco-organisme. Le label lui-même coûte
  **≈ 450 € HT pour un artisan**, pris en charge à 70 % par le Fonds Réparation,
  et se renouvelle par audit tous les 3 ans
  (`https://www.agc-perspectives.fr/bonus-reparation-obtenir-label-qualirepar.html`
  et `https://reparea.fr/blog/comment-obtenir-label-qualirepar`, consultés le
  31/07/2026).

- **Poids de la preuve** — **Insuffisant.** Je n'ai **aucune source** montrant
  qu'un réparateur souffre de la gestion des demandes de bonus. Le dispositif est
  décrit, le volume est réel, la douleur ne l'est pas.

- **Éliminatoires** — n° 1 **NON déclenché** : le label QualiRépar porte sur le
  **réparateur**, pas sur le logiciel, et il est explicitement ouvert aux
  artisans indépendants sans exigence de taille ni d'ancienneté. n° 2 et n° 3 :
  `INCONNU` — non instruits, la piste s'arrêtant sur l'absence de preuve.

- **Charge de développement** — `INCONNU` (dépend d'API éco-organismes non
  instruites).

- **Verdict — ÉCARTÉ** : pas de preuve d'irritant sourcée, conformément à la
  consigne. **À réexaminer en priorité** si un contact réparateur confirme la
  douleur — le volume budgétaire et la croissance ×4 en un an sont remarquables.

---

## B3. Le musicien et le DJ : du devis au cachet déclaré

- **Métier et population** — 90.01Z arts du spectacle vivant, **10 131**
  entreprises à ≥ 1 salarié ; 90.02Z soutien au spectacle, **2 028** (socle B,
  31/07/2026). Tranches `NN` **>10000 (PLAFOND)** pour les deux.
  **Pénétration requise ≤ 4,1 %.**

- **L'irritant** — le musicien vend une prestation à un client qui ne sait pas
  qu'il devient employeur. « Les clients ne refusent pas toujours de déclarer par
  mauvaise foi ; souvent ils ne comprennent pas ce qu'on leur demande, craignent
  de se tromper, ou découvrent trop tard que le prix annoncé n'était pas le coût
  réel total » — `https://doctor.yohmss.eu/comprendre-le-guso-guide-complet/`,
  consulté le 31/07/2026. Le statut lui-même est un nœud : les fils
  d'Audiofanzine sur l'arbitrage auto-entrepreneur / intermittent / artiste-auteur
  courent sur plusieurs pages et plusieurs années —
  `https://fr.audiofanzine.com/autoproduction-business/forums/t.675991,statut-d-auto-entrepreneur-pour-un-musicien-solo-occasionnel-concerts-dans-les-bars.html`,
  consulté le 31/07/2026. **Audiofanzine est un forum métier : poids fort.**

- **Poids de la preuve** — **Moyen à fort.** Le forum est une source forte, mais
  les fils portent sur le **choix de statut**, pas sur un outil manquant.

- **Ce qu'ils utilisent** — le GUSO pour la déclaration, Word pour le contrat,
  rien pour relier les deux.

- **Outils existants** — Indy-Booking (`https://indy-booking.app/`). Ce qui
  manque : le devis qui **affiche au client le coût total employeur** avant
  signature — c'est-à-dire exactement le point de friction cité.

- **Prix et revenu** — 15 à 25 €/mois (revenus faibles : cachet minimal
  ≈ 105-120 € brut en 2026 selon
  `https://www.tempoformation.com/guso-cachet-intermittent-spectacle-guide-2026/`,
  consulté le 31/07/2026). À 20 €/mois il faut **1 250 clients** pour 300 k€ —
  **10,3 %** de la base minorée. **Le prix plafonne bas et c'est le problème.**

- **Éliminatoires** — n° 1 NON · **n° 2 : le GUSO est un guichet d'État gratuit,
  mais il ne couvre QUE la déclaration du cachet** — ni le devis, ni le planning,
  ni le contrat, ni le suivi (arbitrage de l'utilisateur du 31/07/2026 :
  instruire le besoin, pas le métier). **NON déclenché sur le besoin visé.**
  n° 3 NON.

- **Charge de développement** — **8 à 10 semaines.**

- **Verdict — ÉCARTÉ** : irritant réel et gratuité publique correctement écartée,
  mais **la capacité à payer ne permet pas d'atteindre 50 €/mois**, et il faudrait
  1 250 clients sur une base minorée de 12 159.

---

## B4. Le photographe : cession de droits et livraison

- **Métier et population** — 74.20Z, **1 446** entreprises actives à ≥ 1 salarié
  (socle B, 31/07/2026) ; `NN` **>10000 (PLAFOND)**. Population réelle `INCONNU`.
  Cadrage Urssaf : M4 Design/graphisme, **45 062** micro-entrepreneurs
  économiquement actifs — **surensemble large**, le photographe n'y est
  qu'une fraction inconnue.

- **L'irritant** — l'article **L131-3 du Code de la propriété intellectuelle**
  impose que chaque droit cédé fasse l'objet d'une mention distincte dans l'acte
  de cession ; les outils américains l'ignorent
  (`https://www.helpho.io/blog/contrat-cession-droits-image-guide-complet`,
  consulté le 31/07/2026).

- **Poids de la preuve** — **Nul à faible** : source éditeur exclusivement.

- **Verdict — ÉCARTÉ en tant que piste autonome.** Population trop incertaine et
  irritant non prouvé en source forte. **Le besoin est absorbé par A3**, où il
  devient une brique parmi d'autres au lieu d'un produit.

---

## B5. Le VTC — **ÉCARTÉ**

- **Population** — HZ1 Taxis · VTC : **16 445** micro-entrepreneurs
  économiquement actifs au 31/12/2025 (socle A) ; 49.32Z, **9 320** entreprises
  à ≥ 1 salarié (socle B).

- **Éliminatoires** — **n° 3 déclenché** : Indy propose une offre VTC dédiée
  adossée à son offre gratuite (`https://www.indy.fr/comptabilite-vtc/`), et le
  besoin est déjà couvert par des spécialistes payants (Updrive, VTC Planner),
  tous consultés le 31/07/2026.

- **Verdict — ÉCARTÉ** : besoin réel, entièrement servi, et la gratuité d'Indy
  ferme le cœur de valeur.

---

## B6. L'éleveur canin et félin — **ÉCARTÉ, à réexaminer**

- **Population** — **9 299 élevages félins, dont 2 576 professionnels** (LOOF),
  via `https://www.beatricesconseilscanins.fr/blog/elevage-de-chat-en-france.html`,
  consulté le 31/07/2026 — *source secondaire*. Élevages canins : `INCONNU`,
  I-CAD ne publiant pas ce décompte dans les documents atteints.
  01.62Z Soutien à la production animale : **987** à ≥ 1 salarié et **6 319** en
  `NN` — **la seule tranche `NN` non plafonnée de tout le corpus** (socle B).

- **L'irritant** — obligations réelles et empilées : certificat ou attestation de
  cession pour toute cession, certificat vétérinaire obligatoire même à titre
  gratuit, identification avant 4 mois (chien) ou 7 mois (chat), déclaration sur
  la base nationale des opérateurs
  (`https://www.i-cad.fr/articles/attestation-de-cession` et
  `https://www.i-cad.fr/actualites/Ceder_acquerir_animal`, consultés le
  31/07/2026). **Sources d'État : poids fort sur l'obligation.**

- **Pourquoi écarté** — **aucune source ne montre que les éleveurs en souffrent**,
  et la population professionnelle défendable (2 576 félins + `INCONNU` canins)
  ne permet pas d'établir les 500 clients. **Pénétration requise > 19 %** sur les
  seuls éleveurs félins professionnels.

- **Verdict — ÉCARTÉ** : dimensionnement non établi et irritant non prouvé.
  Le besoin rejoint utilement **A1**, où l'éleveur est un métier parmi cinq.

---

## B7. Le brocanteur et le livre de police — **ÉCARTÉ**

- **Population** — 47.79Z, **1 884** entreprises à ≥ 1 salarié (socle B).

- **Pourquoi écarté** — obligation réelle (articles **321-7 et 321-8 du Code
  pénal**, arrêté du 24 juillet 2009), mais besoin **déjà servi par au moins
  trois spécialistes** — Registeo, livre-de-police.com, Tracely
  (`https://registeo.fr/livre-de-police`, consulté le 31/07/2026) — sur une base
  qui ne permet pas 500 clients (**26,5 % de pénétration requise**).

- **Verdict — ÉCARTÉ** : marché trop étroit et déjà occupé par des spécialistes.

---

## B8. Le food truck et l'HACCP — **ÉCARTÉ**

Voir **A5**. Éliminatoire n° 3 déclenché par au moins trois applications HACCP
gratuites. La population est pourtant la plus large du fichier (56.10C :
**30 720** à ≥ 1 salarié, minorant, deux tranches plafonnées).

- **Verdict — ÉCARTÉ** : gratuité installée sur exactement ce besoin.

---

# CLASSEMENT PAR ATTRACTIVITÉ

## Retenues — À CREUSER

| Rang | Piste | Type | Population défendable | Pénétration pour 500 clients | Éliminatoires | Ce qui la porte / ce qui la fragilise |
|---|---|---|---|---|---|---|
| **1** | **A2 — Avance immédiate SAP pour le prestataire solo** | Transverse (7 métiers) | **75 300** entreprises SAP déclarées NOVA | **0,66 %** | 3 franchis, n° 1 **frôlé** | Meilleure économie du fichier et verrou technique réel qui écarte les généralistes · mais habilitation Urssaf à obtenir d'abord, valeur adossée à un crédit d'impôt sous menace politique, et espace encombré |
| **2** | **A1 — Dossier client conforme du professionnel non-médical** | Transverse (5 métiers) | **`INCONNU`, ≥ 20 000** | **≤ 2,5 %** | **3 franchis** | Seule piste où une obligation légale opposable transverse ne rencontre qu'un produit mono-métier (Clic2Sign) · mais la mauvaise tenue du dossier n'est pas prouvée en primaire |
| **3** | **A3 — Prestation à date unique** | Transverse (7 métiers) | **`INCONNU`, ≥ 47 952** | **≤ 1,0 %** | **3 franchis** | Mécanique réellement commune à des métiers que personne ne sert ensemble · mais **irritant non prouvé en source forte** — c'est la réserve la plus lourde du fichier |
| **4** | **B1 — Devis traiteur au convive** | Mono-métier | **≥ 3 627** | 13,8 % *(base faussée par le plafond)* | 3 franchis | Contrainte allergènes réelle et prix mensuel élevé soutenable · mais mono-métier, preuve d'éditeur, et HACCP adjacent verrouillé |

## Écartées, et pourquoi

| Piste | Motif d'écartement |
|---|---|
| **A6 — Facturation / compta de l'indépendant** | Éliminatoires n° 1 **et** n° 3 : Indy gratuit non bridé, et immatriculation PDP = agrément d'État sur le logiciel |
| **A7 — RDV des praticiens exclus de Doctolib** | Éliminatoire n° 3 : Zen Agenda gratuit sur le besoin ; et l'exclusion date de 2022, la fenêtre s'est refermée |
| **A4 — Forfaits et séances prépayées** | Éliminatoire n° 3 déclenché deux fois : Zen Agenda et Fit'Distance annoncent la gratuité pérenne sur ce besoin |
| **A5 / B8 — Registres réglementaires et HACCP** | Éliminatoire n° 3 : au moins trois applications HACCP gratuites ; livre de police déjà servi par des spécialistes |
| **B3 — Musicien et DJ** | Capacité à payer trop faible : 1 250 clients nécessaires à 20 €/mois sur une base minorée de 12 159 |
| **B5 — VTC** | Éliminatoire n° 3 : offre VTC d'Indy adossée à son gratuit ; besoin déjà servi |
| **B7 — Brocanteur** | Marché trop étroit (1 884) et occupé par trois spécialistes |
| **B2 — Bonus réparation QualiRépar** | Pas de preuve d'irritant sourcée. **À réexaminer en priorité** : 715 200 réparations en 2024, ×4 en un an, 512 M€ sur 2022-2028 |
| **B4 — Photographe (droits et livraison)** | Preuve d'irritant de source éditeur uniquement ; le besoin est absorbé par A3 |
| **B6 — Éleveur canin et félin** | Dimensionnement non établi et irritant non prouvé ; rejoint A1 |

---

## Ce qui reste à faire avant d'engager quoi que ce soit

1. **Lever l'habilitation éditeur à l'API Tiers de prestation (A2)** — c'est
   binaire, c'est gratuit à instruire, et cela décide de la piste n° 1. À faire
   en premier, avant toute ligne de code.
2. **Prouver l'irritant en primaire sur A1 et A3.** Reddit et les groupes
   Facebook étant inaccessibles à l'agent, ces deux pistes reposent sur des
   obligations légales vérifiées et des sources d'éditeurs. Cinq à dix entretiens
   par métier trancheraient, là où aucune requête supplémentaire ne le fera.
3. **Constater le périmètre réel des gratuités de Zen Agenda et Fit'Distance.**
   Deux pistes (A4, A7) sont fermées sur des déclarations d'éditeurs non
   vérifiées par essai — ce que le § 2 de `CLAUDE.md` interdit explicitement de
   tenir pour acquis.
4. **Reprendre les chiffres secondaires sur leur source primaire** : les
   82 776 organismes SAP sur la publication DGE, les 15 000 tatoueurs sur le
   SNAT, les élevages félins sur le LOOF.
