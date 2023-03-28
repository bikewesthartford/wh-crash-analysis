# wh-crash-analysis
preliminary analysis of WH crashes

## method overview
- Draw major corridors using either https://GeoJSON.io or https://Placemark.io tool
  - Inside the tool, create a 'corridor' property and name each one (Main St, etc.)
- Download corridors in GeoJSON format and name file: `corridors.geojson`
- Download crash data CSV and remove points with Interstate Highway codes
- Rename file to `crashes.csv` and upload to https://mapshaper.org tool
- Click to open Console in Mapshaper to convert CSV to points on map with command:
  - `-points x=Longitude y=Latitude`
- Upload `corridors.geojson` to Mapshaper
- Join the polygons (corridors) to specific crash points using console command:
  - `-join corridors fields='corridor'`
- In Mapshaper, inspect features of points to see new 'corridor' column (with either corridor name, such as 'Main St' or blank if none)
- In Mapshaper, rename 'crashes' file to 'crashes-corridors' and export in CSV format
- Import 'crashes-corridors.csv' file to Google Sheets and create pivot table to identify corridors with highest count of crashes
