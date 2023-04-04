# wh-crash-analysis
preliminary analysis of WH crashes

## method overview
- Draw major corridors using either https://GeoJSON.io or https://Placemark.io tool
  - Inside the tool, create a 'corridor' property and name each one (Main St, etc.)
- Download corridors in GeoJSON format and name file: `corridors.geojson`
- Download crash data CSV and separate out points where Route Class = Interstate, since most are on elevated limited-access highway that is not under control of local municipality and will confuse spatial analysis of local roads (especially those underneath highways)
- Rename file to `crashes.csv` and upload to https://mapshaper.org tool
- Click to open Console in Mapshaper to convert CSV to points on map with command:
  - `-points x=Longitude y=Latitude`
- Upload `corridors.geojson` to Mapshaper
- Select 'crashes' to make it the active layer in Mapshaper
- In Console, join polygons (corridors) to specific crash points with command:
  - `-join corridors fields='corridor'`
- In Mapshaper, inspect features of points to see new 'corridor' column (with either corridor name, such as 'Main St' or blank if none)
- In Mapshaper, rename 'crashes' file to 'crashes-corridors' and export in CSV format
- Import 'crashes-corridors.csv' file to Google Sheets

## Product 1
Create pivot table of 'crashes-corridors.csv' to identify corridors with highest count of crashes, and/or highest percentage of total crashes. See *preliminary* below, not yet final

| Preliminary: Percent of all non-Interstate crashes in WH, 2018-2022 |       |               |
|---------------------------------------------------------------------|-------|---------------|
| corridor                                                            | COUNT | Percent Total |
| New Britain Ave                                                     | 979   | 14.5%         |
| North Main (combined)                                               | 524   | 7.8%          |
| Albany Ave                                                          | 510   | 7.6%          |
| Farmington Ave                                                      | 492   | 7.3%          |
| South Main to NB                                                    | 384   | 5.7%          |
| Prospect Ave                                                        | 344   | 5.1%          |
| New Park Ave                                                        | 281   | 4.2%          |
| Boulevard (combined)                                                | 226   | 3.3%          |
| Quaker Lane South                                                   | 203   | 3.0%          |
| Park Rd (combined)                                                  | 199   | 2.9%          |
| Trout Brook south                                                   | 185   | 2.7%          |
| Asylum Ave                                                          | 102   | 1.5%          |
| Bloomfield Ave                                                      | 93    | 1.4%          |
| Sedgwick Rd                                                         | 42    | 0.6%          |
| Simsbury Rd                                                         | 25    | 0.4%          |
| Other Roads-Streets                                                 | 2161  | 32.0%         |
| Grand Total                                                         | 6750  | 100.0%        |
 
#### Notes
- Removed 1751 WH crashes labeled as Interstate Highway I-84 or entrance/exit ramps, initially about 20 percent of 8501 total
- All crashes reported in UConn Crash Repo for West Hartford 2018-22, based on 22 March 2023 data download. Note that police reports may delayed 1-6 months. 
- Note that several recent fatal crashes (and perhaps others) do NOT yet appear in UConn Crash Repo: 
  - Dec 20th Eugenia Yurovsky (age 89) was killed by a hit-and-run driver while crossing Boulevard at Whiting Lane.
  - Dec 21st Carlos Garlaza (age 60), a roofing contractor, was struck by a driver while helping a resident exit their driveway at Mohegan Drive and Carlyle Road, and died on Dec 21st.
  - Dec 25th 2022 two-car crash with 3 fatalities on Simsbury Road 

 ## Product 2
 Display results of pivot table in a Datawrapper choropleth map, with custom basemap of corridors.geojson
