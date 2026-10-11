# Where Severe Crashes Concentrate: KSI Collisions in Redondo Beach and Torrance

ArcGIS Pro | SWITRS (via UC Berkeley TIMS), LA County CAMS centerlines, GTFS | GEOG 181A, Summer 2026

## Question
Where do killed-and-severe-injury (KSI) crashes concentrate across Redondo Beach and Torrance, and do the highest-injury corridors coincide with land uses that generate pedestrian activity?

## Data
- Crash records: SWITRS via the Transportation Injury Mapping System (UC Berkeley SafeTREC), 2021 to 2025
- Street centerlines: LA County Countywide Address Management System (CAMS)
- Transit stops: GTFS feeds from LA Metro, Torrance Transit, and Beach Cities Transit
- Schools and parks: digitized manually in ArcGIS Pro from a base map
- All data accessed July 2026. Raw crash records are not included in this repository; request them from TIMS.

## Method
1. Converted crash CSVs (no geometry) to points with XY Table to Point (GCS WGS 1984) and merged the separate city queries.
2. Reviewed points against the street network and removed a small number of records geocoded offshore.
3. Merged the three transit operators' stops and clipped all layers to the two-city boundary with Pairwise Clip.
4. Filtered by collision severity to get 99 KSI crashes (8 fatal, 91 severe injury).
5. Generated a kernel density surface from the KSI points.
6. Spatially joined each crash to its nearest centerline and used summary statistics to rank corridors.
7. Built quarter-mile buffers around schools, parks, and transit stops, dissolved them into one proximity zone, and used Select by Location against the crash points.

## Key findings
- The densest KSI cluster is on the coast of western Redondo Beach near Riviera Village; inland Torrance has much lower density.
- Top corridors: San Diego Freeway 12 (limited-access, not comparable to surface streets), Artesia Boulevard 10, Pacific Coast Highway 8 (segments combined), then Crenshaw and Torrance Boulevards at 3 each.
- 58 corridors had at least one KSI crash, and 41 of them had only one.
- 82 of 99 KSI crashes (82.8%) fell within a quarter mile of a pedestrian generator: 77 near transit stops, 22 near schools, 15 near parks (categories overlap).
- Central insight: the densest cluster (coastal exposure) and the highest-count corridor (Artesia, a wide arterial) are different places, so they likely need different fixes. Coastal areas point to crossings, signal timing, lighting, and lower speeds. Arterials point to lane reconfiguration and turn treatments.

## Maps and charts

**Study area: Redondo Beach and Torrance**<img width="1265" height="1643" alt="study_area" src="https://github.com/user-attachments/assets/9fc367c2-5633-4d2a-bcfa-5e87e6fa8f71" />


**KSI crash density (kernel density)**<img width="1273" height="1649" alt="kde_map" src="https://github.com/user-attachments/assets/318f420a-3fb2-4192-ab06-14c7ce537ce7" />


**High-injury corridors by KSI crash count**<img width="1273" height="1649" alt="corridors_map" src="https://github.com/user-attachments/assets/1964a977-c3d3-4d51-9481-059f7a33bcbd" />


**KSI crashes and pedestrian generator proximity (quarter-mile buffers)**<img width="1265" height="1643" alt="proximity_map" src="https://github.com/user-attachments/assets/554814c2-8570-47b7-b5ca-98fa5885ab98" />


Full report: [KSI_crash_analysis_report.pdf](KSI_crash_analysis_report.pdf)

## Limitations
- Transit proximity is inflated because bus stops cover nearly the whole network; boardings per stop would be a better indicator.
- Freeway crashes were kept rather than excluded, which departs from standard high-injury-network methods, so the freeway is flagged separately.
- Counts are not normalized by traffic or pedestrian volume.
- Five years of data gives small counts per corridor, so one crash can change a ranking.
- Further work could test road width, posted speed, traffic volume, and land use.

Author: Rafael Vieira | UCLA Geography, B.A. 2026
