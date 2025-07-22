# 🎬 Sparkle Movie — Système de Recommandation de Films

## 1. 📌 Contexte du projet

L'objectif du projet **Sparkle Movie** est de concevoir et évaluer plusieurs systèmes de recommandation de films à l'aide du framework **Apache Spark**, en exploitant le dataset **MovieLens**.  
La volumétrie des données et les enjeux de parallélisation ont motivé le choix de Spark, notamment pour le traitement distribué et les algorithmes collaboratifs.

Le projet explore et compare trois approches de recommandation :
- Le **filtrage collaboratif ALS** (Alternating Least Squares),
- La **similarité entre utilisateurs** via **KNN**,
- Une méthode **basée sur le contenu**, en se basant sur la similarité des genres des films.

---

## 2. 📊 Données et leur analyse

Le jeu de données MovieLens utilisé contient :
- `ratings.csv` : des millions de notes attribuées par les utilisateurs aux films,
- `movies.csv` : métadonnées sur les films (titres et genres).

### Analyse exploratoire

L’analyse exploratoire a permis d’identifier :
- Les films les plus populaires (avec le plus de notes),
- Les genres les mieux notés en moyenne,
- La distribution temporelle des notations.

Les données ont été nettoyées puis divisées en ensembles d'entraînement et de test à l'aide d'un **split temporel**, simulant un scénario réaliste de recommandation future.

---

## 3. 🧠 Algorithmes utilisés

### 🔁 ALS — Filtrage collaboratif

Le modèle ALS a été entraîné sur les données d'entraînement avec **optimisation d’hyperparamètres via CrossValidator** (grid search).  
Évaluation avec :
- RMSE (erreur quadratique moyenne),
- Précision@5 et Rappel@5.

Le modèle final a été sauvegardé et utilisé pour la suite du projet.

### 👥 KNN — Similarité utilisateur

Basé sur les **facteurs latents utilisateurs** extraits du modèle ALS, un système **User-User KNN** a été mis en place avec :
- **Similarité cosinus** pour mesurer la proximité,
- **Locality Sensitive Hashing (LSH)** pour accélérer la recherche de voisins en haute dimension.

### 🎭 Recommandation basée sur le contenu

Une approche plus simple, mais efficace, basée sur la **similarité des genres des films**.  
Pour un film aimé par un utilisateur, le système recommande d’autres films partageant des genres similaires.

---

## 4. ✅ Conclusion

L’évaluation des trois systèmes a révélé les performances suivantes :

| Modèle                        | Précision@5 | Rappel@5 |
|------------------------------|-------------|-----------|
| 🎭 Contenu (Genres)          | **0.0667**  | **0.0067** |
| 🔁 ALS (Collaboratif)        | 0.0005      | 0.0001     |
| 👥 KNN (facteurs ALS)        | 0.0010      | 0.0005     |

### 🧩 Conclusion principale

Le modèle basé sur le **contenu** a surclassé les approches collaboratives, notamment en raison de la **sparsité** du dataset : les utilisateurs similaires n’avaient souvent pas noté les mêmes films, ce qui rendait les recommandations difficiles.

Ce projet montre que, dans un contexte de données peu denses, une méthode simple basée sur le contenu peut s’avérer plus robuste qu’un modèle sophistiqué de filtrage collaboratif.

---

