# Atelier Préparation de Données Textuelles

## Contexte

Une entreprise souhaite classer automatiquement des avis clients afin d'identifier leur sentiment (positif, neutre, negatif). Les avis proviennent de plusieurs sources (site web, application mobile, formulaire de satisfaction, réseaux sociaux, service client) et présentent une qualité variable : textes vides, doublons, fautes de frappe, majuscules/minuscules, caractères spéciaux, emojis, URLs, mentions, répétitions de caractères, textes très courts ou très longs.

Ce dépôt contient le pipeline complet de préparation des données textuelles, de l'exploration du corpus brut jusqu'à la vectorisation, en vue d'un futur modèle de classification (ML/DL).

## Structure du projet

```
atelier_prepa_donnees_textuelles/
│
├── notebooks/
│   └── atelier_prepa_donnees_textuelles.ipynb
│
└── data/
    ├── smart_reviews_raw.csv
    ├── smart_reviews_cleaned.csv
    └── tfidf_matrix.npz
```

## Pipeline

1. **Exploration du corpus** — dimensions, valeurs manquantes, types de texte particuliers (URLs, mentions, hashtags, emojis, majuscules, répétitions de caractères), distribution des longueurs, doublons, équilibre des classes.
2. **Nettoyage** — suppression des textes manquants et des doublons, retrait des URLs, traitement des mentions/hashtags, normalisation des espaces, réduction de la ponctuation répétée → colonne `texte_clean`.
3. **Tokenisation** — avec NLTK (`word_tokenize`), statistiques sur le nombre de tokens par avis.
4. **Normalisation** — mise en minuscules, suppression des stop words (négations conservées), lemmatisation avec spaCy → colonne `texte_final`.
5. **Découpage Train/Test** — 80/20, stratifié par sentiment, reproductible (`random_state=42`).
6. **Vectorisation** — comparaison Bag of Words, TF-IDF, TF-IDF (unigrams + bigrams) ; sauvegarde de la matrice retenue dans `tfidf_matrix.npz`.
7. **Bonus** — détection des incohérences note/sentiment, analyse des mots les plus fréquents par classe.

## Installation

```bash
pip install pandas numpy matplotlib scikit-learn nltk spacy langdetect wordcloud
python -m spacy download fr_core_news_sm
```

## Auteur

Rokhaya — Orange Digital Center (ODC), formation IA
