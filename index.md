---
layout: default
title: Cours Google Sheets
---

# Cours Google Sheets

[Accueil](index.md) | [Atelier pratique](atelier.md) 

---

# Guide pratique Google Sheets — Bases et Analyse de données
**Auteur :** Ali Houssene Silahi  
**Contact :** silahi.alihoussene@gmail.com  
**Rôle :** Data Analyst  
**Jeu de données d'exemple :** `Transactions_Simplifiees` (extraits inspirés de PaySim)


## Table des matières
1. [Bases essentielles](#bases-essentielles)
2. [Fonctions arithmétiques et conditionnelles](#fonctions-arithmetiques-et-conditionnelles)
3. [Fonctions logiques et expressions conditionnelles](#fonctions-logiques-et-expressions-conditionnelles)
4. [Fonctions de recherche et automatisation](#fonctions-de-recherche-et-automatisation)
5. [Fonctions avancées — Query et transformation](#fonctions-avancees--query-et-transformation)
6. [Annexes — Exercices et corrigés rapides](#annexes---exercices-et-corriges-rapides)


## Bases essentielles

### Qu'est-ce qu'un tableur ? Pourquoi Google Sheets est un tableur ?
> **Définition :**  
> Un **tableur** est un logiciel permettant de saisir, organiser, calculer, analyser et visualiser des données structurées en **lignes** et **colonnes**.  
> Google Sheets est un tableur en ligne offrant : accès depuis un navigateur, collaboration en temps réel, fonctions de calcul dynamiques, et intégration avec l'écosystème Google.

### Exemple — Structure du jeu de données
**Table : Transactions_Simplifiees**

| Date       | Type      | Montant | Statut  | Client_ID | Région     |
|------------|-----------|--------:|--------|-----------|-----------|
| 01/10/2025 | Paiement  | 1200    | Succès | CL001     | Dakar     |
| 01/10/2025 | Retrait   | 800     | Échec  | CL002     | Thiès     |
| 02/10/2025 | Paiement  | 3200    | Succès | CL003     | Saint-Louis |
| 02/10/2025 | Transfert | 450     | Succès | CL001     | Dakar     |
| 03/10/2025 | Retrait   | 600     | Succès | CL004     | Kaolack   |
| 03/10/2025 | Paiement  | 5200    | Succès | CL002     | Thiès     |

[📥 Télécharger Transactions_Simplifiees.csv](https://raw.githubusercontent.com/silahi/google-sheet/main/Transactions_Simplifiees.csv)


### Cellule, plage, feuille
> **Définition :**  
> - **Cellule** : intersection d'une ligne et d'une colonne (ex. `B2`)  
> - **Plage** : zone de cellules contiguës (ex. `A1:C10`)  
> - **Feuille** : onglet unique dans un fichier Google Sheets  

> **Astuce :** Plage nommée : `Données → Plages nommées → Ajouter`. Exemple : `C2:C100` nommée `Montants`.

### Références : relative, absolue, mixte, plage nommée
- **Relative** : `A1` — change si copié  
- **Absolue** : `$A$1` — fixe colonne et ligne  
- **Mixte** : `$A1` ou `A$1` — fige colonne ou ligne  
- **Plage nommée** : `Montants` pour `C2:C100`  

**Astuce F4 :** après avoir saisi une référence, appuyer sur F4 pour cycler :  
1. `$A$1` (absolue)  
2. `A$1` (ligne figée)  
3. `$A1` (colonne figée)  
4. `A1` (relative)

### Types de données
- Texte : `"Paiement"`, `"OK"`  
- Nombre : `1200`, `0.85`  
- Date / Heure : `01/10/2025`, `12:30`  
- Booléen : `TRUE`, `FALSE`  
- Formule : commence par `=`

### Formules et fonctions — paramètre obligatoire vs facultatif
> **Définition :**  
> - Formule : expression calculée, commence par `=`  
> - Fonction : primitive prédéfinie (ex. `SUM`, `IF`) avec paramètres  

**Comment reconnaître paramètres obligatoires / facultatifs ?**  
- Obligatoires : sans crochets  
- Facultatifs : entre crochets `[ ]`  
- Exemple : `ROUND(value, [places])` → `value` obligatoire ; `places` facultatif (défaut = 0)

```text
=ROUND(12.345, 2)   -> 12.35
=ROUND(12.345)      -> 12
````

### Expressions logiques

> Une expression logique renvoie `TRUE` ou `FALSE`.

**Exemples :**

```text
=C2>1000
=B2="Paiement"
=AND(C2>1000, D2="Succès")
=OR(E2="Dakar", E2="Thiès")
```

## Fonctions arithmétiques et conditionnelles

### Fonctions de base (SUM, AVERAGE, MIN, MAX, COUNT)

```text
=SUM(C2:C7)        # somme des montants
=AVERAGE(C2:C7)    # moyenne des montants
=MIN(C2:C7)        # minimum
=MAX(C2:C7)        # maximum
=COUNT(C2:C7)      # compte cellules numériques
```

### Variantes conditionnelles

```text
SUMIF(range, critère, [sum_range])
COUNTIF(range, critère)
AVERAGEIF(range, critère, [average_range])
```

**Exemples :**

```text
=COUNTIF(D2:D7, "Succès")
=SUMIF(E2:E7, "=Dakar", C2:C7)
=AVERAGEIF(B2:B7, "Paiement", C2:C7)
```

### Fonctions conditionnelles et critères

> Définition : applique un calcul seulement si un ou plusieurs critères sont satisfaits.

**Exemples de critères :**

* Comparaisons numériques : `">1000"`, `"<5000"`
* Égalités texte : `"Succès"`, `"=Dakar"`
* Expressions combinées : `AND(...)`, `OR(...)`


## Fonctions logiques et expressions conditionnelles

### IF, IFS, AND, OR

```text
=IF(C2>1000, "Gros montant", "Petit montant")
=IFS(C2>5000, "Très élevé", C2>1000, "Moyen", TRUE, "Bas")
=AND(C2>1000, D2="Succès")
=OR(E2="Dakar", E2="Thiès")
```

### IFERROR et ISERROR

```text
=IFERROR(VLOOKUP("CL999", A2:E7, 3, FALSE), "Client inconnu")
```

## Fonctions de recherche et automatisation

### VLOOKUP et HLOOKUP

```text
=VLOOKUP(valeur_recherchée, plage, numéro_colonne, [exact_ou_approx])
```

**Exemple :**

```text
=VLOOKUP("CL001", E2:C7, 3, FALSE)
```

### INDEX + MATCH

```text
=MATCH("CL001", E2:E7, 0)
=INDEX(C2:C7, MATCH("CL001", E2:E7, 0))
```

### ARRAYFORMULA

```text
=ARRAYFORMULA(IF(C2:C>1000, "Gros", "Petit"))
=ARRAYFORMULA(C2:C * 1.18)
```

### Import de données

```text
=IMPORTDATA("https://exemple.com/paysim_sample.csv")
=IMPORTRANGE("url", "Feuille!A1:C100")
=IMPORTXML("url", "xpath")
```

## Fonctions avancées — Query et transformation

### Syntaxe générale

```text
=QUERY(plage, "requête", [nombre_en_tetes])
```

### Clauses importantes

* `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`, `LIMIT`, `OFFSET`, `LABEL`
* Agrégations : `SUM()`, `AVG()`, `MIN()`, `MAX()`, `COUNT()`

### Exemples pratiques

```text
=QUERY(A1:F7,
 "SELECT B, SUM(C)
  WHERE D = 'Succès'
  GROUP BY B
  ORDER BY SUM(C) DESC",
 1)

=QUERY(A1:F7,
 "SELECT E, SUM(C)
  WHERE D = 'Succès'
  GROUP BY E
  ORDER BY SUM(C) DESC
  LIMIT 3",
 1)

=QUERY(A1:F7,
 "SELECT *
  WHERE B = 'CASH_OUT' AND C > 1000",
 1)
```

### FILTER, SORT, VSTACK

```text
=FILTER(A2:F7, C2:C7>1000, D2:D7="Succès")
=SORT(A2:F7, 3, FALSE)
=VSTACK(A2:C5, D2:F5)
```

## Annexes — Exercices et corrigés rapides

### Exercices

1. Nommer la plage des montants `Montants` et calculer la somme totale.
2. Créer `StatutLabel` via ARRAYFORMULA :

```text
=ARRAYFORMULA(IF(ROW(C2:C)-ROW(C2)+1>COUNTA(C2:C), "", IF((D2:D="Succès")*(C2:C>1000), "Valide", "À vérifier")))
```

3. Utiliser INDEX+MATCH pour retrouver le montant de `CL003`.
4. Construire avec QUERY la somme des montants par région pour les transactions réussies.

### Corrigés rapides

```text
=SUM(Montants)
=INDEX(C2:C7, MATCH("CL003", E2:E7, 0))
=QUERY(A1:F7, "SELECT F, SUM(C) WHERE D='Succès' GROUP BY F", 1)
```

> **Remarque finale :** Ce document sert de guide de référence pour les modules 1 à 3. Des exercices avancés peuvent être ajoutés dans des modules complémentaires.

