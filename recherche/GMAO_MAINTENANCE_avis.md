# GMAO / MAINTENANCE (prestataires) — corpus d'avis

Recherche effectuée le : 30/07/2026
Fichier de données brutes. Analyse et agrégation : `GMAO_MAINTENANCE.md`, § 3.

> **Corpus total : 4 avis lisibles.** C'est **très en dessous du seuil de 30**
> fixé par le protocole. Conformément à son étape 5 et au § 3 de `CLAUDE.md`,
> ce constat est écrit explicitement et la recherche primaire devient la source
> principale. Le détail de ce qui a été cherché et de ce qui n'existe pas est au
> § « Ce qui a été cherché et n'a rien donné » ci-dessous — cette partie est
> plus importante que le tableau.

## Avis retenus

| # | Éditeur | Plateforme | Note | Date | Reproche en une phrase | Catégorie | URL |
|---|---|---|---|---|---|---|---|
| 1 | Praxedo | App Store FR | non affichée par avis | 07/07/2026 | Hors couverture réseau, l'application ne permet plus rien — le mode déconnecté ne couvre pas les zones blanches | `mobile/terrain` | https://apps.apple.com/fr/app/praxedo-2026/id1534566584 |
| 2 | Praxedo | App Store FR | non affichée par avis | 07/09/2025 | Bugs sur les photos, impossible de copier-coller du texte, numéros de téléphone et e-mails non cliquables ; adoption difficile par les équipes | `bug/fiabilité` + `ergonomie` | idem |
| 3 | Praxedo | App Store FR | non affichée par avis | 18/07/2025 | Pas de vue hebdomadaire, pas de réglage de taille de police ni de couleurs | `fonctionnalité manquante` | idem |
| 4 | Praxedo | App Store FR | non affichée par avis | 24/11/2025 | Aucun reproche — remerciement pour l'ajout des numéros de semaine | — (positif) | idem |

**Note sur la colonne Note** : la page App Store affiche une note globale de
4,5/5 sur 918 avis, mais **n'expose pas la note étoile de chaque avis
individuel**. Les cases sont donc `non affichée`, et non estimées.

**Réponses de l'éditeur observées** : sur l'avis 2, Praxedo répond que les
numéros et e-mails cliquables arriveront en version 1.53 (22/09/2025) ; sur
l'avis 3, que la vue semaine est prévue pour fin 2026. L'éditeur répond donc
publiquement et s'engage sur des dates — élément à porter au crédit du produit.

## Ce qui a été cherché et n'a rien donné

C'est la partie utile de ce fichier. Chaque ligne est un constat d'absence, pas
un échec de recherche.

| Source (poids § 3 de `CLAUDE.md`) | Ce qui a été tenté | Résultat |
|---|---|---|
| **Trustpilot** — Fort | Recherche de fiches pour Praxedo, Organilog, Yuman, Bob! Desk | **Aucune fiche n'existe.** Le seul « Yuman » présent est *Yuman Coaching*, société sans rapport. Corpus : **0** |
| **Google Play** — Fort | `com.praxedo.pm3` en `hl=fr` puis `hl=en_US` | **Page non lisible par fetch** : Google Play est rendu côté client, seule la navigation du magasin est retournée. Deux tentatives, deux locales. Corpus : **0** |
| **App Store** — Fort | Fiche Praxedo 2026 (`id1534566584`), fiche FreeMaint (`id6757958686`) | Praxedo : **918 avis annoncés, 4 exposés**, l'App Store web **ne pagine pas** les avis. FreeMaint : « This app hasn't received enough ratings or reviews to display an overview » → **0 avis**. Corpus : **4** |
| **Reddit** — Fort | `site:reddit.com` sur « logiciel GMAO », « gestion d'intervention », « maintenance », « retour d'expérience » | **Aucun résultat Reddit.** Le moteur retourne des mémoires universitaires et des pages d'éditeurs. Corpus : **0** |
| **Forums métier, groupes professionnels** — Fort | Recherche de discussions de pairs entre techniciens et responsables de maintenance | **Aucun forum de pairs trouvé.** Les résultats sont exclusivement des blogs d'éditeurs, des comparateurs affiliés et des témoignages publiés par les éditeurs eux-mêmes. Corpus : **0** |
| **Capterra / G2 / GetApp** — Faible | Non dépouillés | Volontairement non exploités : le § 3 de `CLAUDE.md` interdit de compenser l'absence de sources fortes en surpondérant les sources faibles. Une note globale y est explicitement « pas une information » |
| **Comparateurs français** — Nul | lebonlogiciel, logiciels.pro, comparatif-logiciels.fr, appvizer | Notes agrégées rencontrées : 4,63/5 sur « plus de 140 critiques », 4,75/5. **Non retenues, non publiées.** Poids nul par construction |

**Un écart de notation est-il détectable ?** Non — la comparaison suppose des
données des deux côtés. Il n'y a pas de source forte suffisante pour opposer
quoi que ce soit aux notes élevées des comparateurs. **L'écart est donc `INCONNU`,
et non « aucun ».**

## Recherche primaire — ce qu'elle a donné

Substitution prévue par le protocole quand le corpus tombe sous 30.

### Changelog et rythme de mise à jour

| Éditeur | Constat | Source | Date |
|---|---|---|---|
| Praxedo | Version **1.72.0 publiée trois jours avant la consultation**. Historique visible : 1.53.1 (22/09/2025, « Bugfixes »), 1.50.0 (30/06/2025, outils d'annotation de photos, gestion des paramètres de modules externes). **Produit activement maintenu, pas de module abandonné détecté** | App Store FR | 30/07/2026 |
| FreeMaint | Version 1.0 le **27/01/2026**, version 1.0.20 le **05/07/2026**. Produit **de moins d'un an** | App Store US | 30/07/2026 |

### Écarts entre page marketing et réalité constatée

| Constat | Portée |
|---|---|
| **Bob! Desk se présente comme « Le 1er Logiciel GMAO Gratuit » et « Le 1er Logiciel gestion d'intervention Gratuit »**, alors que son offre réelle est un **essai de 14 jours**, sans aucun tarif affiché et avec renvoi sur devis | Écart marketing / réalité **direct**. C'est le reproche `prix caché` le mieux documenté du secteur, mais il est constaté sur pièces, pas rapporté par un client |
| **FreeMaint annonce « gratuit à vie », utilisateurs et actifs illimités** — c'est exact, mais l'éditeur est un développeur individuel dont l'application a moins d'un an et zéro avis | Crédibilité, pas mensonge |
| **Organilog affiche un palier « Basique » à 0 €** dont l'archivage est limité à **72 heures** | Une entreprise ne peut pas conserver ses rapports d'intervention trois jours. Le gratuit est nominal |
| **Praxedo affiche « à partir de 35 € »** mais impose **5 utilisateurs minimum** : le prix d'entrée réel est **175 €/mois** | Écart prix affiché / prix réel, constaté sur la page tarifs de l'éditeur |

### Essais gratuits — non réalisés

Les essais des trois principaux éditeurs **n'ont pas été ouverts**. Ils exigent
une inscription avec une identité et une adresse professionnelle réelles. Cela
reste la première action de vérification terrain à mener, et figure au § 11 du
fichier principal.

## Conclusion de l'étape 5

Le protocole est explicite : *« Un corpus d'avis vide n'autorise pas à conclure
"pas de problème détecté". Il autorise seulement à conclure "pas de données
publiques — vérification terrain requise". »*

**C'est exactement la situation.** Quatre avis, tous sur un seul éditeur, dont
un positif. Le reproche le plus intéressant — l'échec du mode déconnecté en zone
blanche — n'apparaît **qu'une fois**. Il ne peut pas fonder une stratégie
produit, seulement une hypothèse à tester.
