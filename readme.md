# Interactive 3D Borehole Ground Model

A Streamlit app that visualizes 3D ground surface with borehole logs.

## Features
- Upload your own CSV files (surface points, borehole locations, stratigraphy)
- Horizontal and vertical exaggeration
- Exportable to HTML

## How to Use
1. Upload three CSVs with required columns
2. View interactive 3D model
3. Download as HTML if needed


### Required Input Files (CSV Format)
The app requires **three separate CSV files**. Column names must match **exactly** (case-sensitive).

#### 1. Surface CSV – Ground surface elevation points
Used to interpolate the 3D terrain surface.

| Required Columns | Description                  | Example Data |
|------------------|------------------------------|--------------|
| Easting          | X coordinate (any units, consistent across files) | 500123.45 |
| Northing         | Y coordinate                 | 234567.89 |
| Elevation        | Z coordinate / ground level  | 125.67    |

*Extra columns are ignored.*

**Example rows:**
Easting,Northing,Elevation
500000,200000,100.5
500100,200100,102.3
500200,200000,99.8
#### 2. Boreholes CSV – Borehole locations
Defines where each borehole is located on the surface.

| Required Columns | Description                  | Example Data |
|------------------|------------------------------|--------------|
| BH ID            | Unique borehole identifier   | BH-01       |
| Easting          | X coordinate                 | 500050.0    |
| Northing         | Y coordinate                 | 200050.0    |

**Example rows:**

BH ID,Easting,Northing
BH-01,500050,200050
BH-02,500150,200100
BH-03,500100,200200

#### 3. Borehole Details CSV – Stratigraphy / soil layers
Defines depth intervals and soil types for each borehole.

| Required Columns | Description                          | Example Data |
|------------------|--------------------------------------|--------------|
| BH               | Borehole ID (must match Boreholes CSV) | BH-01       |
| FROM             | Top depth of layer (from ground surface, positive down) | 0.0 |
| TO               | Bottom depth of layer                | 5.0         |
| SOIL TYPE        | Soil/rock description (text)         | CL          |

**Important notes:**
- Depths are measured **downward** from ground level (0 = surface).
- Multiple rows per borehole (one per layer).
- Soil types are case-sensitive. Predefined colors are available for common types (see below). Unknown types will appear black with a warning.

**Example rows:**

BH,FROM,TO,SOIL TYPE
BH-01,0.0,2.5,SM
BH-01,2.5,8.0,CL
BH-01,8.0,12.0,ROCK
BH-02,0.0,1.0,SM
BH-02,1.0,6.5,CH

#### Predefined Soil Type Colors
These common types have nice colors assigned automatically:

| Soil Type | Color Description       | RGB Code          |
|-----------|-------------------------|-------------------|
| SM-ML     | Yellow                  | rgb(255,255,0)    |
| SC        | Tan                     | rgb(210,180,140)  |
| CI        | Green                   | rgb(0,128,0)      |
| SM/SM-ML  | Golden yellow           | rgb(255,215,0)    |
| ROCK      | Brown                   | rgb(139,69,19)    |
| SM        | Light yellow            | rgb(255,255,224)  |
| GP-GM     | Gray                    | rgb(128,128,128)  |
| CH        | Dark green              | rgb(0,100,0)      |
| ML-SM     | Pink                    | rgb(255,192,203)  |
| CL        | Sky blue                | rgb(135,206,250)  |
| GM        | Dark gray               | rgb(169,169,169)  |
| GC        | Slate gray              | rgb(112,128,144)  |
| ML        | Moccasin                | rgb(255,228,181)  |
| SP        | Navajo white            | rgb(255,222,173)  |
| CHAR      | Dark slate              | rgb(47,79,79)     |

Any other soil type → black (with warning).


