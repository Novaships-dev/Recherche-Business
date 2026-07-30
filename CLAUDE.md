# CLAUDE.md

Instructions permanentes pour ce repo.

## Passation

À chaque consigne donnée et réponse rendue, la réponse est **écrite dans un
fichier du repo en plus d'être affichée**. Ce n'est pas optionnel et ne
dépend pas de la taille de la réponse.

### Emplacement et nommage

```
docs/passation/NN_sujet-court.md
```

`NN` = numéro d'ordre à deux chiffres, incrémenté à chaque nouvelle passation.
Vérifier le dernier numéro existant dans `docs/passation/` avant d'écrire,
et ne jamais réutiliser un numéro.

### Contenu obligatoire de chaque fichier

Chaque fichier doit être **autonome** : lisible par quelqu'un qui n'a aucun
accès à la conversation. Il contient, dans cet ordre :

1. **En-tête** : date, numéro, sujet en une ligne, et l'état du repo au moment
   de l'écriture — ce qui existe, ce qui a été lancé, ce qui ne l'a pas été.
2. **La consigne reçue, reproduite intégralement.**
3. **La réponse rendue, reproduite mot pour mot**, sans coupe ni reformulation.
4. **Les preuves brutes** : chaque commande exécutée avec sa sortie réelle, de
   sorte que tout chiffre soit reproductible. **Aucun chiffre sans sa commande.**
5. **Ce qui reste en attente de décision, et ce qui est bloqué.**
6. **Les réserves et pièges découverts**, même mineurs.

### Règles

- **Ne pas répéter** ce qui est déjà écrit dans un fichier de passation
  antérieur. Renvoyer à son numéro.
- **Ne pas résumer, ne pas « nettoyer »** la réponse. Elle est transmise telle
  quelle à un tiers qui doit pouvoir la contredire.
- **Écrire les erreurs et les hypothèses corrigées en cours de route.**
  Une erreur corrigée est une information utile, pas une gêne à effacer.
- Un chiffre sans source s'écrit `INCONNU`. Ne jamais estimer, extrapoler ou
  reconstituer un chiffre de mémoire.

### Index

`docs/passation/00_INDEX.md` est mis à jour **à chaque fois** : une ligne par
fichier, avec numéro, date, sujet et statut.

Statuts : `validé` / `en attente` / `périmé`.
