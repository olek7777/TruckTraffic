# 📂 Data Source

## Synthetic European Road Freight Transport Flow Data

**Source:** [Mendeley Data — py2zkrb65h, Version 2](https://data.mendeley.com/datasets/py2zkrb65h/2)  
**Origin:** Based on the [ETISplus](https://www.etisplus.eu/) European Transport and Infrastructure project  
**License:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

> ⚠️ The raw data files are **not included** in this repository due to file size.  
> Please download them directly from the Mendeley link above.

---

## 📋 Dataset Tables

### `01_Trucktrafficflow.csv` — Main fact table
**1,514,573 rows** of directed freight transport flows between NUTS-3 region pairs.

| Column | Description |
|---|---|
| `origin_id` | ID of the origin NUTS-3 region |
| `origin_name` | Name of the origin region |
| `destination_id` | ID of the destination NUTS-3 region |
| `destination_name` | Name of the destination region |
| `path` | Shortest path through the E-road highway network |
| `dist_origin_to_network` | Distance from origin to the highway network (km) |
| `dist_within_network` | Distance within the highway network (km) |
| `dist_network_to_dest` | Distance from the highway network to destination (km) |
| `dist_total` | Total distance of the flow (km) |
| `freight_tons_2010` | Road freight flow in tonnes, year 2010 |
| `freight_tons_2019` | Road freight flow in tonnes, year 2019 |
| `freight_tons_2030` | Road freight flow in tonnes, forecast 2030 |
| `trucks_2010` | Number of trucks, year 2010 |
| `trucks_2019` | Number of trucks, year 2019 |
| `trucks_2030` | Number of trucks, forecast 2030 |

---

### `02_NUTS-3-Regions.csv` — Region reference table
List of all 1,675 NUTS-3 regions included in the model.

| Column | Description |
|---|---|
| `region_id` | Unique region identifier |
| `region_name` | Region name |
| `country_code` | ISO country code |

---

### `03_network-nodes.csv` — Highway network nodes
Information about each node in the modeled E-road highway network.

| Column | Description |
|---|---|
| `node_id` | Unique node identifier |
| `longitude` | Longitude coordinate |
| `latitude` | Latitude coordinate |
| `associated_region` | NUTS-3 region this node belongs to |
| `country_code` | ISO country code |

---

### `04_network-edges.csv` — Highway network edges
Information about each highway segment (edge) in the network.

| Column | Description |
|---|---|
| `edge_id` | Unique edge identifier |
| `length_km` | Length of the edge in km |
| `node_start` | Starting node ID |
| `node_end` | Ending node ID |
| `trucks_2019` | Number of trucks on this edge in 2019 |
| `trucks_2030` | Number of trucks on this edge in 2030 (forecast) |

---

## 🔄 Data Transformations Applied in Power Query

- Loaded `01_Trucktrafficflow` as the main fact table
- Merged with `02_NUTS-3-Regions` twice (for origin and destination country codes)
- Created a `Year` dimension by unpivoting the 2010/2019/2030 columns
- Filtered out self-loops (origin = destination)
- Rounded distance columns to 2 decimal places
- Added a `country_pair` calculated column (`origin_country → destination_country`)

---

## 📎 Citation

> Kröger, L., Zenner, L. (2022).  
> *Synthetic European road freight transport flow data based on ETISplus.*  
> Mendeley Data, V2. https://doi.org/10.17632/py2zkrb65h.2
