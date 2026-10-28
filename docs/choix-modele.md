# Choix du modèle — Prévision des repas servis à la cantine

Date : 28/10/2026 · Groupe : Mohamed Saifeddine / Sara Hajdaoui / Marwa Khabarate / Ilyass Edhoum

## Contexte
Le modèle estime le nombre de repas à préparer à la cantine à partir des informations de calendrier, du menu, des inscriptions et de la météo. La métrique principale est la MAE, car elle exprime directement l'erreur moyenne en nombre de repas.

## Données et découpage
Le fichier `data/cantine_repas.csv` contient 340 observations quotidiennes. Les variables utilisées sont `jour`, `inscrits`, `menu`, `temperature_c`, `pluie_mm`, `examens`, `sortie_scolaire`, `veille_vacances` et `repas_semaine_precedente`. La colonne `date` sert au découpage chronologique et n'est pas une variable d'entrée. Les 272 premières observations servent à l'entraînement ; les 68 dates les plus récentes sont gardées pour le test.

## Résultats sur le jeu de test

| Modèle | MAE (repas) | RMSE (repas) | R² |
|---|---:|---:|---:|
| Baseline (moyenne) | 70,271 | 88,416 | -0,151 |
| Régression linéaire | 22,239 | 28,170 | 0,883 |
| Forêt aléatoire | 31,845 | 41,540 | 0,746 |
| Gradient boosting | 39,015 | 51,049 | 0,616 |

## Décision
Le modèle retenu est la régression linéaire, avec la plus faible MAE. Son erreur est inférieure de 48,032 repas à celle de la baseline, soit une réduction d'environ 68,4 %. Le critère proposé dans l'étude de conception (MAE ≤ 59,730, équivalente à une réduction d'au moins 15 %) est atteint avec une MAE de 22,239. Comme le seuil a été ajouté après l'entraînement, cette comparaison ne vaut pas validation indépendante du critère.

## Limites
Le test ne porte que sur 68 jours et sur une seule période temporelle ; les résultats peuvent changer avec une autre période ou de nouvelles habitudes de fréquentation. Les données manquantes des variables sont imputées par le pipeline. La source et la licence d'origine du CSV restent à confirmer par le groupe. L'entraînement peut afficher des avertissements numériques sur la régression linéaire ; les scores ci-dessus sont ceux produits lors de l'exécution, mais ce point mérite une vérification complémentaire.
