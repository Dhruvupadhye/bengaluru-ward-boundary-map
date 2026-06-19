# 🗺️ Bengaluru Ward Boundary Analysis & Interactive Map

An end-to-end data analytics project on Bengaluru's 198 municipal wards — covering data cleaning, feature engineering, EDA, and an interactive geospatial map visualization.

---

## 📌 Project Goal

To analyze Bengaluru ward boundary data and build an **interactive map** that reveals:
- Which wards cover the **largest geographic area**
- Which wards have the **most mapped regions**
- A **visual breakdown** of all 198 wards by size and mapping detail

---

## 📂 Dataset

- **Source:** GeoJSON file containing Bengaluru ward boundaries
- **Format:** GeoJSON (FeatureCollection)
- **Records:** 198 wards
- **Original Features:**
  - `WARD_NO` — Ward number
  - `WARD_NAME` — Ward name
  - `MOVEMENT_ID` — Movement identifier
  - `DISPLAY_NAME` — Mapped address
  - `geometry` — MultiPolygon boundary coordinates

---

## 🛠️ Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data loading, cleaning, manipulation |
| `shapely` | Geometric calculations (area, centroid) |
| `geopandas` | Geospatial data handling |
| `folium` | Interactive map visualization |
| `json` | JSON file parsing |

---

## 🔄 Project Workflow

### 1. Data Loading
```python
import pandas as pd
sample = pd.read_json('dataset.json')
df = pd.json_normalize(sample['features'])
```

### 2. Data Cleaning
- Fixed datatypes (`ward_id`, `movement_id` to `int`)
- Dropped redundant columns (`movement_id`, `type`, `geometry.type`)
- Removed special characters from `ward_name` and `address`
- Standardized `address` to title case
- Fixed addresses starting with numeric prefixes

### 3. Feature Engineering
- Renamed columns to simpler names
- Extracted **geographic area** from polygon geometry using `shapely`
- Extracted **centroid latitude & longitude** for each ward
- Engineered **mapped regions** count from address detail level

### 4. EDA Findings

#### 📐 Area
- Largest ward: **Hemmigepura** (0.002369)
- Smallest ward: **Padarayanapura** (0.000027)
- Largest wards are on the **outskirts** of Bengaluru
- Smallest wards are in the **city center** (dense urban areas)

#### 🗺️ Mapped Regions
| Mapped Regions | Ward Count |
|---|---|
| 2 (Very sparse) | 3 |
| 3 (Sparse) | 17 |
| 4 (Moderate) | 94 |
| 5 (Good) | 75 |
| 6 (Highly mapped) | 9 |

### 5. Interactive Map
Built using `folium` with:
- Color-coded ward boundaries by area size
- Hover tooltips showing ward name, ID, area, and mapped regions
- Markers for top 10 largest wards
- Legend for area size reference

---

## 🏆 Key Insights

- 🏙️ **Central wards are smaller** but more densely packed and urbanized
- 🌳 **Peripheral wards are larger** — more open/undeveloped land
- 🗺️ **Mapping is uneven** — only 9 wards are fully mapped with 6 address parts
- 📍 **Top 3 largest wards** — Hemmigepura, Varthuru, Bellanduru (all on city outskirts)
- 📍 **Most mapped wards** — Byatarayanapura, A Narayanapura, HBR Layout

---

## 🚀 How to Run

1. Clone the repository
```bash
git clone https://github.com/yourusername/bengaluru-ward-map.git
cd bengaluru-ward-map
```

2. Install dependencies
```bash
pip install pandas geopandas shapely folium
```

3. Run the notebook
```bash
jupyter notebook bengaluru_ward_analysis.ipynb
```

4. Open the map
```
Open bengaluru_wards_map.html in your browser
```

---

## 📁 Project Structure

```
bengaluru-ward-map/
│
├── dataset.json                  # Original GeoJSON dataset
├── bengaluru_ward_analysis.ipynb # Main analysis notebook
├── bengaluru_wards_map.html      # Interactive map output
└── README.md                     # Project documentation
```

---

## 📊 Final Dataframe Structure

| Column | Type | Description |
|---|---|---|
| `ward_id` | int | Ward number (1-198) |
| `ward_name` | str | Name of the ward |
| `address` | str | Mapped address |
| `area` | float | Geographic area of ward |
| `mapped_regions` | int | Address detail level |
| `latitude` | float | Centroid latitude |
| `longitude` | float | Centroid longitude |
