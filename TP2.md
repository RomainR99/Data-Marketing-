# TP2 - Segmentation RFM & Lumina & Co

#### Contexte

Vous avez maintenant une base propre. Le CMO attend une réponse à sa question : *"Qui sont nos clients ?"* Pas en termes démographiques vagues, mais en segments actionnables avec des recommandations concrètes.

#### Étape 1 : Construction des features RFM

À partir de `transactions.csv` nettoyé, calculez pour chaque client :

- **Récence** : nombre de jours entre son dernier achat et la date de référence (date max du dataset)
- **Fréquence** : nombre de factures distinctes sur la période complète
- **Montant** : somme totale des `line_total` sur la période complète

La date de référence doit être fixée une fois pour toutes, c'est le *"snapshot date"*. Utiliser la date du jour serait une erreur : les données ne vont pas jusqu'à aujourd'hui.

Enrichissez si vous le souhaitez avec une ou deux features simples supplémentaires (panier moyen, ancienneté), sans obligation d'en faire une liste exhaustive.

#### Étape 2 : Scoring RFM et segments

Attribuez les scores R, F, M de 1 à 5 par quintiles. Créez les segments RFM et répondez :

- Combien de *"Champions"* (score 555 ou proche) ? Quelle part du CA représentent-ils ?
- Combien de clients *"À risque"* (forte valeur historique, faible récence) ?
- Quelle proportion de la base est *"Perdue"* (111) ? Quelle action pour ce segment ?

Ces trois questions ne couvrent que les cas extrêmes. La majorité de vos clients ne collera à aucun de ces trois profils. Une fois ces 3 segments identifiés, comment amélioreriez-vous la segmentation pour couvrir le reste de la base ? Définissez vos propres règles par plage, documentez vos seuils, et justifiez pourquoi vous les avez placés à cet endroit plutôt qu'un autre s'il y a une raison.

Visualisez la distribution des scores et la matrice RFM

#### Étape 3 : Visualisation et profilage

- Profil démographique de chaque segment (pays, ancienneté)
- Scatter plot récence × montant, coloré par segment

> Attention à la relation non linéaire entre récence et valeur : des clients très récents et très anciens peuvent tous deux avoir un fort potentiel

#### Étape 4 : Recommandations marketing par segment

Pour chacun des 5 à 8 segments obtenus, rédigez une fiche :

- Qui sont-ils (profil comportemental)
- Leur potentiel (valeur actuelle et potentielle)
- Le risque (churn, inactivité)
- L'action recommandée (campagne email, offre, exclusion des campagnes coûteuses...)

Puis, classez vos segments par ordre de priorité de traitement (1 = à traiter en premier). Pour chaque rang, nommez explicitement le critère qui justifie cet ordre (valeur, risque de perte, potentiel de croissance). Vérifiez enfin que le temps ou le budget que vous consacreriez réellement à chaque segment reflète bien cet ordre : si vos segments classés 1 et 4 recevraient le même traitement dans la pratique, votre priorisation n'est que théorique.

Si vous le souhaitez, ajoutez une métrique de succès par segment (ex : taux de réactivation, commandes dans les 30 jours suivants). Ce n'est pas obligatoire à ce stade, mais bienvenu si vous avez le temps.

> **Pour aller plus loin :** le scoring par quintiles suppose une base assez grande pour que "20% des clients" ait un sens. Réfléchissez à comment vous adapteriez cette méthode sur une base de 50 clients seulement, par exemple celle d'un auto-entrepreneur. Quels paliers fixeriez-vous à la main ?

> **Pour aller plus loin :** segmentation insight-driven. Le RFM segmente sur le comportement d'achat (combien, quand, à quelle fréquence), pas sur qui est le client ni pourquoi il achète. `customers.csv` contient 4 colonnes de préférences déclarées via un quiz de bienvenue (`declared_preference`, `age_bracket`, `life_stage`, `urban_density`), sparse mais exploitables sur le sous-ensemble de clients qui y ont répondu.

- Choisissez un de vos segments RFM et croisez-le avec un des champs zero-party disponibles
- Le croisement révèle-t-il un profil plus précis que le RFM seul ?
- Si oui, comment ça changerait le message ou le canal utilisé pour les activer, par rapport à une action RFM générique ?

---

## Livrables de fin de journée à publier sur GitHub

1. Notebook de segmentation : scores RFM, visualisations, matrice RFM
2. Carte des segments : 5 à 8 segments nommés avec profils et recommandations
