# NBA 2023–24 Season Totals: Scrape, Clean, Explore

This repository contains a Jupyter notebook that scrapes 2023–24 NBA totals from Basketball-Reference, performs data cleaning, computes basic statistics, and generates exploratory visualizations (distributions, correlations, and position-wise scatterplots) intended as a quick-start template for basic sports analytics and EDA on season-level player statistics.

## Features

- Automated data retrieval from Basketball-Reference 2024 totals page.
- Robust parsing and cleaning: removes header-duplication rows, resets index, converts numeric columns with error coercion, handles missing values via numeric means, and de-duplicates rows.
- Descriptive statistics and column-wise averages.
- Visual EDA: histograms + KDE for PTS/TRB/AST, position-colored scatterplots (PTS vs AST, PTS vs TRB), and a correlation heatmap (PTS, TRB, AST).

## Data source

- Basketball-Reference totals page for the 2023–24 NBA season (Totals table).
- URL is embedded in the notebook and fetched via pandas.read_html.
- Note: Basketball-Reference may update table formatting; small adjustments to column names or filters might be required in the future.

## Requirements

- Python 3.9+
- Jupyter Notebook or JupyterLab
- Python packages: pandas, numpy, matplotlib, seaborn

## Install

`pip install pandas numpy matplotlib seaborn`

### Optional Environment Setup

`python -m venv .venv
source .venv/bin/activate # Windows: .venv\Scripts\activate
pip install -r requirements.txt`

## If using requirements.txt:

`
pandas
numpy
matplotlib
seaborn`


## Project Structure

├── nba_scraped_stats.ipynb # 
├── README.md # This file
└── ss

## How It Works

### Scrape

- Uses `pandas.read_html` to load the Totals table from Basketball-Reference.
- Selects the first table, drops repeated header rows (`Rk == 'Rk'`), and resets the index.

### Clean

- Defines non-numeric vs numeric columns.
- Converts numeric columns with `errors='coerce'`.
- Fills NA for numeric columns with column means (`numeric_only=True`).
- Removes duplicates.

### Explore

- Prints column names and head rows to confirm parsing.
- Computes column-wise means and `DataFrame.describe()` for numeric columns.
- Visualizations:
  - Histograms with KDE for PTS, TRB, AST.
  - Scatterplots (PTS vs AST; PTS vs TRB) colored by player position.
  - Correlation heatmap for PTS, TRB, AST.

## Running the Notebook
`jupyter notebook`

- Open `nba_scraped_stats.ipynb` and run all cells (Kernel → Restart & Run All).
- Plots will display inline; adjust matplotlib backend or figure size if needed.

## Columns You'll Commonly Use

- **Metadata**: Rk, Player, Team (or Tm), Age, Pos, G, GS, MP.
- **Shooting**: FG, FGA, FG%, 3P, 3PA, 3P%, 2P, 2PA, 2P%, eFG%.
- **Free Throws**: FT, FTA, FT%.
- **Counting Stats**: ORB, DRB, TRB, AST, STL, BLK, TOV, PF, PTS.
- **Other**: Trp-Dbl, Awards (often sparse).

Note: The notebook normalizes numeric columns and fills missing numeric values with column means. For strict NA handling or different imputation, modify the fill step.

## Customization Tips

- **Position normalization**: Harmonize Tm vs Team, and handle traded-player totals as needed.
- **Feature engineering**: Add per-game rates by dividing by G after cleaning.
- **Filtering**: Exclude very low MP or G to reduce outliers.
- **Persistence**: Export cleaned DataFrame to CSV for downstream modeling:

` df.to_csv('nba_2024_totals_clean.csv', index=False)`

## Troubleshooting

- **ValueError in read_html**: Page structure changed. Inspect with `tables = pd.read_html(url)`, check `len(tables)`, and confirm the correct table index.
- **Column name mismatches**: Print `df.columns.tolist()` and update non-numeric/numeric column lists accordingly.
- **Mixed-type columns**: `to_numeric(..., errors='coerce')` forces numeric parsing; adjust if some columns should remain categorical.
- **Slow/blocked scraping**: Basketball-Reference can rate-limit; consider caching HTML locally for development.
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

**Note**: While this code is MIT licensed, please respect Basketball-Reference's terms of service when scraping their data.

## Acknowledgments

- Data courtesy of Basketball-Reference (Sports Reference LLC).
- Visualization and EDA powered by pandas, matplotlib, and seaborn.


