# Hex-Grid
Tools related to the GNRC Hex Gridded System developed by Sam W. et. al. 

Hexagons are the Bestagons: Aggregate Data to Hex
Version: 1.0
Date: April 28, 2025
Contact: Will Rogers III, Safety Planning Coordinator
README Written by Will & Gemini

1. Purpose
This ArcGIS Pro tool aggregates numeric data from an overlaying feature layer (either polylines like roads or polygons like census blocks) onto a specified hexagon grid layer. It calculates a single, representative value for each hexagon based on the spatial relationship and values of the overlapping features.

Specifically:
For Polyline overlays (e.g., roads), it calculates a length-weighted average of a chosen numeric field (like Speed Limit or Crash Rate).
For Polygon overlays (e.g., population density zones), it calculates an area-proportional sum of a chosen numeric field (estimating the total value within the hexagon based on overlap).

2. Need / Background
This tool was developed to automate a common workflow that previously required multiple manual steps in ArcGIS Pro. Performing length-weighted averages or area-proportional sums often involved a sequence like:
Running Intersect or Union --> Calculating segment lengths or intersection areas --> Calculating proportions (for polygons) --> Calculating weighted values or allocated values per piece --> Running Dissolve or Summary Statistics to aggregate results back to the original hexagon IDs --> Joining results back to the original hexagon layer

This manual process is time-consuming and more prone to human errors. This tool encapsulates that logic into a single, reusable geoprocessing tool, saving significant time and ensuring consistency.

3. How it Works
The tool takes the GNRC-specific hexagon layer (e.g., 1/8 mi) and the polyline or polygon overlay layer (e.g., wetlands) as input.
It performs an Intersect operation in the background to determine where the overlay features fall within the hexagons and calculates the length (for polylines) or area (for polygons) of these intersections.
Based on whether the overlay layer is polyline or polygon, it applies the appropriate calculation (length-weighted average or area-proportional sum) using the user-selected numeric field.
It creates a new output feature class (a copy of the input hexagons) containing all original attributes plus a new field holding the calculated aggregate value for each hexagon.

4. How to Use
Add the toolbox (.atbx) to your ArcGIS Pro project --> Open the tool from the Geoprocessing pane --> Fill in the parameters and run

Example Use Cases for Transportation Planning
Calculating the average speed limit for roads within each 1/4-mile hexagon.
Estimating the total number of crashes (from a point layer converted to density polygon, or using crash rates on road segments) within each 1-mile hexagon.
Aggregating population or employment data from census blocks into a consistent hexagon grid for accessibility analysis.
Compare a Pedestrian Level of Service model (using Open Street Map network) with a Pedestrian Level of Traffic Stress model (using TDOT's LRS) to compare how they align and differ.

Please contact wrogers@gnrc.org with any questions or issues.
