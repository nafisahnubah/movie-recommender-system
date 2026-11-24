# Movie Recommender System

Two classic approaches to recommending movies, built and evaluated on the
[MovieLens 100K](https://grouplens.org/datasets/movielens/100k/) dataset:

1. **Content-based item-item recommender**: movies are represented by their title +
   genre text (TF-IDF), and recommendations come from a precomputed item-item cosine
   similarity matrix.
2. **Collaborative filtering**: user-based and item-based, using the rating matrix
   directly rather than any item content.

Two simple baselines (item popularity and per-user average rating) are included for
comparison. Every method is evaluated with RMSE on MovieLens's `u1` train/test split
(80,000 training and 20,000 test ratings).

## Results

| Method | RMSE (lower is better) | Personalized? |
|---|---|---|
| Item-based collaborative filtering | **1.006** | Yes |
| Popularity baseline (item's average rating) | 1.036 | No |
| Content-based item-item (TF-IDF + cosine) | 1.042 | Yes, but content-only |
| User-based collaborative filtering | 1.043 | Yes |
| Per-user average baseline | 1.063 | Yes (user's own average) |

Item-based collaborative filtering has the lowest error, and it is the only method that
clearly beats the non-personalized popularity baseline. Item-item similarities are more
stable and can be precomputed, and item-based CF tends to handle rating sparsity better
than user-based CF. The content-based recommender and user-based CF land just above the
popularity baseline.

See the notebook for the full breakdown, including sample recommendations and a
discussion of each method's strengths, weaknesses, and the cold-start problem.

## Requirements

- Python 3 with Jupyter (JupyterLab, Jupyter Notebook, or VS Code)
- For the automatic dataset download: a Unix-style shell with `mkdir -p`, `curl` and
  `unzip` (Linux, macOS, WSL, or Google Colab). On Windows without these, download
  [ml-100k.zip](https://files.grouplens.org/datasets/movielens/ml-100k.zip) yourself and
  extract it to `data/ml-100k/`.

## Getting started

```bash
pip install -r requirements.txt
```

Start Jupyter from the `notebooks/` folder and run `movie_recommender.ipynb` top to
bottom. The first cell downloads and extracts MovieLens 100K into `data/` at the repo
root (git-ignored). The full notebook takes a couple of minutes on a laptop CPU.

## Project structure

```
movie-recommender-system/
├── notebooks/
│   └── movie_recommender.ipynb   # all the code, results, and analysis
├── requirements.txt
├── LICENSE
└── README.md
```

## Tech stack

Python · pandas · NumPy · scikit-learn · tqdm

## License

[MIT](LICENSE)
