# 🎬 Movie Genre Dashboard (1960–2010)

An interactive Streamlit dashboard for exploring how movie genres have evolved over five decades, based on IMDb data. Compare genres by volume, audience rating, and overall impact, then drill into any single genre to see its trends over time and its top-rated films.

**🔗 Live app:** [movie-dashboard on Streamlit Cloud](https://movie-dashboard-mywqsjtmktnxz4p9wtpvyl.streamlit.app/)

---

## Features

- **Year range filter:** focus on any window between 1960 and 2010.
- **Genre filter:** view all genres together, or select a single genre.
- **Overview mode (All genres)**
  - Genres ranked by **number of movies**
  - Genres ranked by **average rating**
  - Genres ranked by **balance score** (movie count × average rating), which rewards genres that are both popular and well rated
- **Genre detail mode (single genre)**
  - Line chart of **movies released per year**
  - Line chart of **average rating per year**
  - Table of the **top 10 highest-rated movies** in the selected genre and period
- Interactive tooltips on all charts.

## Data

The dashboard uses a cleaned dataset (`1960-2010_Movies.zip`) built in `data_scraping.ipynb` from two public [IMDb datasets](https://developer.imdb.com/non-commercial-datasets/):

| Source file | Contents |
|---|---|
| `title.basics.tsv` | Title, release year, runtime, genres |
| `title.ratings.tsv` | Average rating and vote counts |

**Preparation steps (in the notebook):**

1. Import both IMDb files.
2. Keep titles released between 1960 and 2010.
3. Merge ratings with title details on the title ID (`tconst`).
4. Drop unused columns and standardize column names.
5. Export the result as a single CSV.

**Additional cleaning in the app:**

- Removes TV episode entries (titles beginning with "Episode #").
- Keeps only titles with a runtime of **40 minutes or more**, to exclude shorts.
- Drops records with missing genres or ratings.
- Splits multi-genre titles (e.g., `Action,Drama`) so each movie counts toward every genre it belongs to.

> **Note:** Because movies can belong to several genres, a single film appears once under each of its genres in the genre counts.

## Tech Stack

- [Python](https://www.python.org/)
- [Streamlit](https://streamlit.io/) for the web app
- [pandas](https://pandas.pydata.org/) for data processing
- [Altair](https://altair-chart.streamlit.app/) for visualizations

## Project Structure

```
movie-dashboard/
├── Movie_dashboard.py       # Streamlit app
├── data_scraping.ipynb      # Data import, cleaning, and merging
├── 1960-2010_Movies.zip     # Cleaned dataset used by the app
├── requirements.txt         # Python dependencies
└── README.md
```

## Run Locally

1. **Clone the repository**
   ```bash
   git clone https://github.com/<your-username>/movie-dashboard.git
   cd movie-dashboard
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Start the app**
   ```bash
   streamlit run Movie_dashboard.py
   ```

The app will open at `http://localhost:8501`.

### Regenerating the dataset (optional)

1. Download `title.basics.tsv` and `title.ratings.tsv` from the IMDb datasets page.
2. Update the file paths in the first cells of `data_scraping.ipynb`.
3. Run the notebook to produce a new `1960-2010_Movies.csv`.

## Deployment

The app is deployed on [Streamlit Community Cloud](https://streamlit.io/cloud) directly from this repository. Pushing changes to the main branch triggers an automatic redeploy.

## Data Attribution

Movie data is courtesy of [IMDb](https://www.imdb.com/) and used under their terms for personal, non-commercial use. See the [IMDb non-commercial licensing terms](https://developer.imdb.com/non-commercial-datasets/).

## Author

**Noshin Tasnim**
