# Movie Recommender System

Two classic approaches to recommending movies, built and evaluated on the
[MovieLens 100K](https://grouplens.org/datasets/movielens/100k/) dataset:

1. **Content-based item-item recommender** — movies are represented by their title +
   genre text (TF-IDF), and recommendations come from a precomputed item-item cosine
   similarity matrix.
2. **Collaborative filtering** — user-based and item-based, using the rating matrix
   directly rather than any item content, plus non-personalized baselines (global
   popularity, per-user average) for comparison.

Both approaches are evaluated with RMSE on a held-out test split.

## Results

| Method | RMSE | Personalized? |
|---|---|---|
| Content-based item-item (TF-IDF + cosine) | 1.04 | Yes, but content-only |
| User-based collaborative filtering | 1.11 | Yes |
| Item-based collaborative filtering | **1.01** | Yes |

Item-based collaborative filtering edges out the other two on this dataset — item-item
similarities are more stable and can be precomputed, and it tends to handle rating
sparsity better than user-based CF. The content-based recommender is close behind despite
using no collaborative signal at all, which says a lot about how much genre/title text
alone captures about a movie's audience.

See the notebook for the full breakdown, including sample recommendations and a
discussion of each method's strengths, weaknesses, and the cold-start problem.

## Getting started

```bash
pip install -r requirements.txt
```

The MovieLens 100K dataset is downloaded and extracted automatically by the first cell of
the notebook.

Run `notebooks/movie_recommender.ipynb` top to bottom.

## Project structure

```
movie-recommender-system/
├── notebooks/
│   └── movie_recommender.ipynb   # all the code, results, and analysis
├── requirements.txt
└── README.md
```

## Tech stack

Python · pandas · NumPy · scikit-learn · tqdm
