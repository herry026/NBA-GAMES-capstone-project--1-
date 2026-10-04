# NBA-GAMES-capstone-project--1-
NBA data manipulation pipeline using Pandas. Implements data ingestion, strict type casting, multi-layered inner joins, and complex conditional querying on 26k+ historical match records (2004–2020).

# NBA Game History: Data Manipulation & Engineering Pipeline

This repository features an end-to-end data processing and transformation pipeline built in Python using **Pandas**. The workflow demonstrates core data engineering techniques—including automated file ingestion, schema validation, type casting, relational merges, and conditional query slicing—on a comprehensive dataset of **26,651 NBA games** spanning from the 2004 season to December 2020.

##  Data Pipeline Lifecycle

The data architecture transforms separate, raw flat files into a unified analytical layer by executing the following chronological pipeline stages tracked in the notebook:

1. **Telemetry Trimming:** Isolates foundational match metrics (scores, wins, dates) from dense game tracking logs.
2. **Strict Schema Normalization:** Upgrades raw object columns into native optimization types:
   - `GAME_DATE_EST` ➡️ `datetime64[ns]`
   - `GAME_STATUS_TEXT`, `CITY`, `NICKNAME` ➡️ `string[python]`
3. **Multi-Key Merging:** Maps and scales team metadata (franchise locations and franchise nicknames) onto game logs using independent left/right inner-join keys for both **Home** and **Away** slots.
4. **Targeted Drop Phase:** Prunes redundant structural keys (`TEAM_ID_home`, `TEAM_ID_away`, `TEAM_ID_x`, `TEAM_ID_y`) to achieve minimum memory footprints.
5. **Feature Engineering:** Derives a computed absolute column `points_total` (`pts_home` + `pts_away`).
6. **Data Serialization:** Exports the final frame cleanly into a flat `games-transformed.csv` bypassing tracking indexing.

##  Exploratory Highlights & Query Slicing

The pipeline wraps up with performance slicing benchmarks to profile historical anomalies within the 26k+ match matrix:
- **Index Swapping:** Validates performance ranges across positional slicing tools (`.loc` vs `.iloc`) under chronological `DatetimeIndex` structures.
- **Anomalous Filtering:** Isolates specific high-scoring instances where a team scored **over 150 points but still lost the game** (only 4 historical games match this criterion!).
- **Magnitude Extraction:** Leverages `.nlargest()` mechanics to extract the absolute highest-scoring games on historical record.

##  Project Structure
- `Practice Exercise.ipynb` — The operational Python execution notebook.
- `games.csv` — Raw match data (Kaggle framework).
- `teams.csv` — Raw NBA franchise identifiers.
- `games-transformed.csv` — The final engineered analytical product.

## 🛠️ Requirements
- Python 3.x
- Pandas
