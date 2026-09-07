# Rapport EDA — Lumina & Co

## Sommaire

- [Clients one-shot vs récurrents](#clients-one-shot-vs-recurrents)
- [Distribution de `n_orders`](#distribution-de-n_orders)
- [Pays `EIRE`](#pays-eire)
- [Volumes de ventes par `category`](#volumes-de-ventes-par-category)
- [`bins` et `kde`](#bins-et-kde)
  - [`bins`](#bins)
  - [`kde`](#kde)

---

## Clients one-shot vs récurrents

Nombre total de clients : **50 295**

- Clients avec une seule transaction : **14 460 (28,75 %)**
- Clients récurrents : **35 835 (71,25 %)**

30 % de clients n’ayant fait qu’une seule transaction paraît peu.

---

## Distribution de `n_orders`

Statistiques descriptives pour le `n_orders` (nombre de commandes par client) :

| Stat | Valeur |
| --- | ---: |
| count | 50 295 |
| mean | 4,59 |
| 25 % | 1 |
| 50 % (médiane) | 3 |
| **75 %** | **6** |
| max | 373 |

**Lecture du 75 % :** trois quarts des clients font **6 commandes ou moins**. Ce n’est pas « la majorité fait exactement 6 commandes ».

- La **majorité** (au moins 50 %) fait **3 commandes ou moins** (médiane = 3).
- 25 % des clients font **plus de 6** commandes (jusqu’à 373).

La distribution est donc concentrée sur les petits volumes : beaucoup de clients peu fréquents, une petite queue de très gros acheteurs.

---

## Pays `EIRE`

**EIRE** (ou **Éire**) est le nom irlandais de l’**Irlande**.

Dans les CRM, le e-commerce et des jeux de données type Online Retail, on le trouve souvent à la place de `Ireland` ou `IE`. Ce n’est pas un autre pays : c’est l’Irlande, écrite avec le toponyme gaélique.

Dans les données Lumina, un gros client est déjà tagué comme ça (par ex. `customer_id` 14911, 373 commandes). Pour une carte ou un regroupement géo, on peut le recoder en **Ireland**.

---

## Volumes de ventes par `category`

Chiffre d’affaires (`ca_eur`) et volume de lignes par catégorie produit :

- **Catégorie dominante :** Visage (**31,9 %** du CA)
- **Top 3 cumulé :** **73,5 %** du CA (Visage + Coffret + Corps)

| category | ca_eur | % CA | n_lignes | % lignes |
| --- | ---: | ---: | ---: | ---: |
| Visage | 12 749 132,41 | 31,91 | 344 257 | 28,31 |
| Coffret | 8 315 224,73 | 20,81 | 98 225 | 8,08 |
| Corps | 8 284 291,87 | 20,74 | 288 865 | 23,76 |
| Cheveux | 4 501 341,42 | 11,27 | 173 786 | 14,29 |
| Accessoire | 3 253 444,38 | 8,14 | 164 986 | 13,57 |
| Bain | 2 833 117,13 | 7,09 | 142 475 | 11,72 |
| Frais | 12 354,35 | 0,03 | 3 279 | 0,27 |

**Lecture :**

- **Visage** domine (31,9 % du CA, ~28 % des lignes).
- Le **top 3** (Visage, Coffret, Corps) concentre **73,5 %** du CA.
- **Coffret** et **Corps** pèsent ~21 % du CA chacun, mais le coffret le fait avec beaucoup moins de lignes (8 %) : panier unitaire plus élevé.
- Cheveux, Accessoire et Bain se partagent le reste.
- `Frais` (frais de port / ajustements) est négligeable.

---

## `bins` et `kde`

```python
sns.histplot(customers_df_cleaned['n_orders'], bins=70, kde=True)
```

### `bins`

`bins` = le **nombre de barres** de l'histogramme.

Seaborn découpe l'axe des x (ici le nombre de commandes, de 1 à 373) en **70 intervalles** de même largeur. Chaque barre compte combien de clients tombent dans cet intervalle.

Exemple : avec `n_orders` entre 1 et 373, chaque barre couvre environ `(373 - 1) / 70 ≈ 5` commandes. La première barre regroupe les clients qui ont 1 à ~6 commandes, la suivante ~7 à 12, etc.

- **Peu de bins** (ex. `bins=10`) : histogramme lisse, on voit la forme globale, mais on perd du détail.
- **Beaucoup de bins** (ex. `bins=70`) : plus fin, on distingue mieux le pic des petits `n_orders`, mais le graphique peut devenir bruité.

### `kde`

`kde=True` superpose une **courbe lissée** (Kernel Density Estimate) par-dessus les barres.

Ce n'est pas lié à `bins` : les barres restent un comptage par intervalle, la courbe estime la distribution en continu.
