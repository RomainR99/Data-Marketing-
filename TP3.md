# TP3 - Attribution Multicanal Lumina & Co

#### Contexte

Le dataset `touchpoints.csv` contient l'historique de tous les points de contact entre Lumina & Co et ses clients, sur les 6 campagnes menées entre l'été 2025 et l'été 2026. `campaigns.csv` contient les métriques agrégées par campagne.

Le CMO reçoit chaque semaine des rapports contradictoires de ses différents canaux. Votre mission : lui donner des chiffres clairs et une première lecture critique de ce qu'ils veulent vraiment dire.

#### Étape 1 : KPIs par canal et par campagne

À partir de `campaigns.csv` et `touchpoints.csv`, calculez pour chaque canal : le CAC, le CPA, le ROAS, le taux de conversion.

Classez les canaux du plus au moins performant selon chaque métrique. Le classement est il le même selon la métrique choisie ? Pourquoi ?

Le display ne devrait pas être jugé sur sa conversion directe. Qu'est-ce que ça implique pour la lecture de votre classement ? Étudiez le classement de ce canal.

`campaigns.csv` indique un `primary_channel` par campagne. Ce champ désigne-t-il le canal le plus performant, ou autre chose ? Comparez-le à votre propre classement sur CAC, CPA, ROAS et taux de conversion : `primary_channel` arrive-t-il en tête sur ces métriques aussi ?

CAC ≠ CPA. Le CAC ne compte que les nouveaux clients, le CPA compte toute conversion, y compris le réachat d'un client déjà fidèle. Sur les mêmes données, le CAC sera systématiquement plus élevé que le CPA, puisqu'il porte sur un sous-ensemble plus restreint de conversions pour un coût total identique. Si vos deux chiffres sont proches, vérifiez votre filtre sur les primo-achats.

Comment repérer un primo-achat : une conversion dans `touchpoints.csv` référence un `invoice_id`, que vous pouvez relier à `transactions.csv` pour obtenir sa date. Comparez cette date à `first_purchase` du client dans `customers.csv` : si elles sont égales, c'est un primo-achat.

Vanity metrics : parmi les colonnes de `touchpoints.csv` (nombre de touchpoints, nombre de clics, coût, conversions), lesquelles seraient de simples métriques de vanité si on les regardait isolément ? Qu'est-ce qui les transforme en KPI une fois combinées ?

> **Pour aller plus loin (optionnel) :** vous avez déjà calculé le CAC par canal. Estimez la CLTV des clients acquis via chaque canal (méthode simplifiée vue en cours : rythme de dépense annualisé × durée de vie estimée × marge assumée), puis calculez le ratio LTV:CAC. Un canal avec un bon CAC est-il toujours un bon canal une fois la CLTV prise en compte ? Le classement change-t-il par rapport à celui ci-dessus ?

#### Étape 2 : Comparaison first touch vs last touch

Avant de comparer les modèles, un coup d'œil rapide à `touchpoints.csv` pour vous orienter : combien de touchpoints par parcours en moyenne, quels canaux reviennent le plus souvent en première position, lesquels en dernière position avant conversion.

Implémentez ensuite les deux modèles heuristiques les plus simples :

- **First touch :** 100% du crédit va au premier point de contact observé du parcours
- **Last touch :** 100% du crédit va au dernier point de contact avant l'achat

Pour chaque modèle, calculez la répartition du budget attribué par canal (en % et en valeur).

**Analyse :**

- Quels canaux sont favorisés par le first touch ? Par le last touch ?
- Si le CMO basait ses décisions budgétaires uniquement sur le last touch, quels canaux seraient sous-investis ?
- Est ce cohérent avec le rôle réel de chaque canal dans le parcours (découverte vs closing) ?

**Refléxion personnelle :** Que peut-on raisonnablement conclure sur la performance d'un canal quand on ne peut pas le comparer aux autres de cette façon ? Un auto-entrepreneur n'a en général pas de vision croisée de ses canaux, chacun est mesuré séparément dans son propre outil (Meta Business Suite, Google Analytics).

→ Quel modèle d'attribution conseillez-vous, modèle unique ou multi-touch à partir des données sur lesquelles vous travaillez ?

---

## Livrables de fin de journée à publier sur GitHub

1. Notebook KPIs : tableau comparatif des canaux, classement selon chaque métrique
2. Notebook attribution : comparaison first touch vs last touch, recommandation argumentée
