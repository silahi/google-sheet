---
layout: default
title: Cours Google Sheets
---

# Cours Google Sheets

[Accueil](index.md) | [Atelier pratique](atelier.md)


# Atelier pratique Google Sheets — Analyse de transactions
**Auteur :** Ali Houssene Silahi  
**Contact :** silahi.alihoussene@gmail.com  
**Jeu de données :** `Transactions_Atelier.csv` (1000 transactions)


[📥 Télécharger Transactions_Atelier.csv](https://raw.githubusercontent.com/silahi/google-sheet/main/Transactions_Atelier.csv)

## Table des matières
1. [Importation et nettoyage](#importation-et-nettoyage)
2. [Fonctions de base](#fonctions-de-base)
3. [Fonctions conditionnelles](#fonctions-conditionnelles)
4. [Fonctions logiques](#fonctions-logiques)
5. [Fonctions de recherche](#fonctions-de-recherche)
6. [Automatisation](#automatisation)
7. [Query](#query)
8. [Questions pratiques](#questions-pratiques)

---

## Importation et nettoyage
- Importer le fichier `Transactions_Atelier.csv` dans Google Sheets.
- Vérifier les colonnes : `Date | Type | Montant | Statut | Client_ID | Région`
- Supprimer les doublons (`Données → Supprimer les doublons`)
- Vérifier les valeurs manquantes
- Créer une **plage nommée** pour Montant → `Montants` 

## Fonctions de base
- Somme totale : `=SUM(C2:C1001)`
- Moyenne : `=AVERAGE(C2:C1001)`
- Maximum / Minimum : `=MAX(C2:C1001)` / `=MIN(C2:C1001)`
- Compter les cellules numériques : `=COUNT(C2:C1001)`


## Fonctions conditionnelles
- Somme des transactions réussies : `=SUMIF(D2:D1001, "Succès", C2:C1001)`
- Compter transactions échouées : `=COUNTIF(D2:D1001, "Échec")`
- Catégorisation montant : `=ARRAYFORMULA(IF(C2:C1001>2000, "Gros montant", "Petit montant"))`


## Fonctions logiques
- Vérification validité : Montant > 1000 ET Statut = "Succès"
```text
=ARRAYFORMULA(IF((C2:C1001>1000)*(D2:D1001="Succès"), "Valide", "À vérifier"))
```
- Vérification région Dakar ou Thiès :
```text
=ARRAYFORMULA(IF(OR(F2:F1001="Dakar", F2:F1001="Thiès"), "Région cible", "Autre"))
```

## Fonctions de recherche
- INDEX + MATCH pour retrouver le montant de CL150 :
```text
=INDEX(C2:C1001, MATCH("CL150", E2:E1001, 0))
```
- Lister toutes les transactions du client CL150 :
```text
=FILTER(A2:F1001, E2:E1001="CL150")
```

## Automatisation
- Marquer transactions réussies > 3000 :
```text
=ARRAYFORMULA(IF((C2:C1001>3000)*(D2:D1001="Succès"), "Important", "Normal"))
```

## Query
- Somme par type :
```text
=QUERY(A1:F1001, "SELECT B, SUM(C) GROUP BY B", 1)
```
- Somme par région (succès) et tri décroissant :
```text
=QUERY(A1:F1001, "SELECT F, SUM(C) WHERE D='Succès' GROUP BY F ORDER BY SUM(C) DESC", 1)
```

## Questions pratiques
1. Quelle est la **somme totale** des transactions ?  
2. Quel est le **montant moyen** ?  
3. Combien de transactions ont été **réussies** et combien **échouées** ?  
4. Quelle est la **transaction maximale et minimale** ?  
5. Classer les transactions en **Gros montant** et **Petit montant**.  
6. Identifier les transactions **valides** selon le critère : Montant > 1000 ET Statut = "Succès".  
7. Retrouver le **montant total** pour un client spécifique (`CL150`) avec INDEX+MATCH.  
8. Lister toutes les transactions d’un client (`CL150`) avec FILTER.  
9. Marquer toutes les transactions réussies **supérieures à 3000** comme “Important”.  
10. Faire la **somme des montants par type de transaction** avec QUERY.  
11. Faire la **somme des montants par région** pour les transactions réussies, triées par ordre décroissant.
