\# **MADRID GREENSPACES CONNECTIVITY ANALYSIS**



\## PROJECT OVEREVIEW

This project analyzes greenspace connectivity and accessibility in Madrid's Centro district using spatial network analysis, geoprocessing, and interactive visualization techniques. The analysis identifies connectivity gaps and potential areas for greenspace improvement through systematic geospatial workflows.



\## OBJECTIVES

1\. \*\*Greenspace Hierarchy Classification\*\*: Categorize vegetation types with priority rankings

2\. \*\*Connectivity Gap Analysis\*\*: Identify areas poorly connected to existing greenspaces

3\. \*\*Interactive Visualization\*\*: Create web maps for exploratory analysis

4\. \*\*Network Analysis\*\*: Evaluate pedestrian accessibility via road networks

5\.  \*\* Equitability analysis\*\*: Propose new locations for greenspaces



\## PROJECT STRUCTURE



Madrid\_Greenspaces/

├── Madrid\_Greenspaces.ipynb # Main Jupyter notebook

├── test.ipynb # Testing and validation notebook

├── data/

│ ├── Vegetation\_Merged.shp # Greenspace polygons

│ ├── DISTRITOS.shp # District boundaries

│ ├── population.shp # Population data

│ ├── complete\_buildings.shp # Building footprints

│ └── 20240101\_estructura\_demografica\_barrio.shp # Neighborhood demographics

├── outputs/

│ └── greenspace\_gap\_grid.gpkg # Generated connectivity analysis results

└── README.md # This file





\## TECHNICAL STACKS



**### Core Libraries**

\- \*\*GeoPandas\*\*: Geospatial vector data processing and CRS management

\- \*\*Shapely\*\*: Geometric operations (concave hulls, spatial relationships)

\- \*\*NetworkX \& OSMnx\*\*: Spatial network analysis and routing

\- \*\*scipy.spatial.KDTree\*\*: Efficient nearest-neighbor searches

\- \*\*Folium\*\*: Interactive web map generation



**### Supporting Libraries**

\- \*\*NumPy \& Pandas\*\*: Numerical and tabular data handling

\- \*\*Mapclassify\*\*: Choropleth map classification



**## Data Sources**

All spatial data is provided in the `data/` directory:

\- \*\*Vegetation\_Merged.shp\*\*: Greenspace polygons with vegetation types

\- \*\*DISTRITOS.shp\*\*: Madrid district boundaries

\- \*\*population.shp\*\*: Population distribution data

\- \*\*complete\_buildings.shp\*\*: Building footprints

\- \*\*Neighborhood data\*\*: Demographic structure by neighborhood

**## Data Access**
The input datasets required to run this project can be downloaded from [https://drive.google.com/file/d/1ermYG0H-sWE5HSJ_TxI6XVn0h-DTlAIZ/view?usp=drive_link]

**## Main Workflow**



\### 1. Configuration \& Data Loading (`Config` class)

\- Sets project parameters (CRS, district selection, analysis thresholds)

\- Loads and projects all input datasets to EPSG:25830

\- Fetches road network data from OpenStreetMap via OSMnx



\### 2. GREENSPACE HIERARCHY SYSTEM

```python

class GreenspaceClass(Enum):

&nbsp;   PARK = "park"      # Priority rank: 2

&nbsp;   FOREST = "forest"  # Priority rank: 1

Each class has associated friction costs and connectivity thresholds

Higher rank indicates higher priority for accessibility analysis



3\. CONNECTIVITY GAP ANALYSIS

**Methodology:**

Generate 100m grid over AOI (Centro district)

Compute distance from each grid cell to nearest greenspace using KDTree

Classify cells as "far from greenspace" (>300m threshold)

Output results as GeoPackage for visualization



**Key Metrics:**

dist\_to\_greenspace\_m: Distance to nearest greenspace

far\_from\_greenspace: Binary flag (1 if >300m)

nearest\_gclass: Type of nearest greenspace



4\. INTERACTIVE VISUALIZATION

Creates a Folium web map with:

Base layer: CartoDB Positron

Greenspace gap grid (choropleth by distance)

District boundary overlay

Interactive tooltips with distance information



**Configuration Parameters**

Parameter	Default	Description

crs\_epsg	25830	Projected CRS (UTM zone 30N)

district\_name	"Centro"	Target district for analysis

walk\_speed\_kmh	5.0	Pedestrian walking speed

grid\_size	100	Analysis grid resolution (meters)

top\_k	2	Number of top candidate locations to select

min\_dist\_m	500.0	Minimum distance between candidate sites



**Analysis Outputs**

Primary Outputs:

Greenspace Gap Grid (outputs/greenspace\_gap\_grid.gpkg):

Regular grid with connectivity metrics

Spatial distribution of accessibility gaps

Classification of underserved areas

Interactive Web Map:

Visual exploration of connectivity patterns

Layer toggling and zoom capabilities

Distance-based color coding



**Derived Metrics:**

Accessibility Scores: Combined ranking based on greenspace type and area

Connectivity Weights: Movement friction factors for different greenspace types

Gap Thresholds: Maximum acceptable distances by greenspace class



**Key Insights \& Applications**

Urban Planning Applications:

Priority Areas: Identify neighborhoods with poor greenspace access

Network Optimization: Suggest locations for new green corridors

Resource Allocation: Guide investment in greenspace development

Policy Support: Provide evidence-based recommendations



ANALYTICAL CAPABILITIES:

Multi-scale analysis: From individual grid cells to district-level patterns

Class-based prioritization: Different strategies for parks vs. forests

Network-aware evaluation: Considers actual pedestrian routes

Interactive exploration: Support for stakeholder engagement



SETUP AND USAGE

**Installation:**

bash

pip install networkx osmnx geopandas folium mapclassify



**Running the Analysis:**

Ensure all data files are in the data/ directory

Open Madrid\_Greenspaces.ipynb in Jupyter

Run cells sequentially (dependencies are automatically installed)

Interactive map will display automatically in the notebook

Results are saved to outputs/ directory



**Customization:**

Modify Config parameters for different districts or thresholds

Adjust grid\_size for finer/coarser analysis resolution

Update greenspace hierarchy definitions in GreenspaceClass enum



**Methodological Notes**

Spatial Analysis Approach:

CRS Consistency: All data projected to EPSG:25830 for accurate distance measurements

Edge Cases: Buffer operations prevent topology errors

Performance: KDTree enables efficient nearest-neighbor queries over large datasets



**Limitations \& Assumptions**:

Network Simplification: Road network may not include all pedestrian paths

Static Analysis: Does not account for temporal variations in accessibility

Binary Classification: Simple distance threshold for "far from greenspace" classification



**Extensions \& Future Work**

Potential Enhancements:

Multi-modal Accessibility: Include public transport networks

Temporal Analysis: Hourly/daily variations in accessibility

3D Analysis: Incorporate building heights and topography

Social Equity Metrics: Combine with demographic vulnerability indices

Ecological Connectivity: Assess wildlife corridor potential



**Integration Possibilities:**

Real-time data feeds for dynamic analysis

Machine learning for predictive modeling

Web dashboard for ongoing monitoring

API endpoints for programmatic access



please paste this in the last parts of the readme, from the contributors: 
 
**Contributors \& Acknowledgments**
 
Primary Developer: \[Carolina Rivas and Zillah Sabuni/ITC, University of Twente]
 
 
 
**Data Sources:**
 
Madrid City Council (spatial data)
 
OpenStreetMap (road network)
 
 
 
**Technical Acknowledgments:**
 
ITC Masters Program, Year 1, Scientific Programming for Geospatial Science
 
Open-source geospatial Python community
 
 
 
**License**
 
\[MIT]
 
 
 
**Contact**
 
For questions, suggestions, or collaboration opportunities:
 
Email: \[{Zillah Sabuni <z.sabuni@student.utwente.nl>}, {Carolina Rivas <c.s.rivasfajardo@student.utwente.nl>}]
 
GitHub: \[ZillahS333, carsriva93]
 
 
 
Last Updated: \[11/01/2026]
 
Project Status: Active Development
