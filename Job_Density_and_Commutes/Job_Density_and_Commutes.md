
Since I've already made significant progress on my final project, and have discussed what I'm doing with you at some length, I decided, in liue of a one-page overview of what I propose to do, to submit a somewhat shorter overview followed by what I have done so far.

My goal is to analyze the job distribution in the Washington-Baltimore-Arlington Combined Statistical Area, which I refer to in the following report as "the CSA" (despite the unfortunate acronym) or "the Baltimore-Washington area."  I am focusing on using Census LODES data to understand the distribution of job density, clustering of jobs, and commuter patterns for jobs in different portions of the region.

My report will have three sections:
- First, I will process LODES workplace location data, along with additional data on the location of military and security-related civillian Federal jobs to produce maps of job density in the CSA as a whole and in sub-regions within it
	- Maps will be made for Greater Baltimore, Greater Washington, and smaller cities including Frederick and Annapolis, and there will be some discussion of the different patterns in these areas.
	- Data processing for this section is complete, but my office computer can't load the full map, so exporting images will have to wait until this coming week.
- Second, I will use Moran's I autocorrelation and spatial correlation analyses in GeoDa to identify the locations of job clusters.
	- This analysis is complete and fully written up.
	- Unfortunately, while this did succeed in identifying many job clusters, it did not seem to provide a good list of clusters to analyze in the third part.
- Third, I will map and characterize the commutersheds for some of the largest job clusters.
	- I have only started the data analysis, identifying eight clusters in the Baltimore area, fifteen in the DC area, and three in other small cities, to be used for analysis.  Given this, I'm a lot less sure about the details.
	- I'm not sure whether it makes sense to group together some of these employment clusters to reduce the number I'm working with.
	- My current goals are to make population dot maps, find centroids of worker locations and compare them to the locations of the clusters, and to determine the median commute distance for each cluster.

I'm not certain whether Section 1 is involved enough to count toward the requirement for three non-trivial components from the class.  If it isn't, I can create a 3D map as well.  What currently strikes me as interesting would be a 3D map of activity density (sum of jobs and workers divided by area) color-coded by ratio of jobs to workers.

As for why this project is more involved than the labs, the answer is largely the amount of processing needed to get from the raw data to something usable.  Each section ends in a subsection discussing the data analysis.  To produce the maps used in Sections 1 and 2, I had to assemble data (sometimes available by county and sometimes by state) from the whole CSA and limit it to only cover those counties included in the CSA and use SQL scripts to tablulate workers and jobs by block group.

In addition, for Section 1, I attempted to correct for the missing security-related jobs with Census shapefiles of military bases and information on the workforce at each base found via a number of online sources.







## 1: Mapping Job Density

The most common way to map the density of urban areas is to map their population density.  This is easily done, since essentially all national governments perform regular censuses that record the number of residents within relatively small tracts covering the whole country.

While population density is an important metric, it is not the only useful way to evaluate the density of urban areas.  For some purposes, the density of jobs is more important than population density.  For example, in many cases, local governments get an outsized proportion of their tax revenue from commercial uses, both due to higher property tax rates and land values and because of sales and corporate taxes and income being taxed where it is earned rather than where the earner resides.

In addition, the highest job densities in an area will usually be higher than the high end of residential densities, and the most transit ridership and transportation congestion will be found in these areas of densely clustered jobs.

While the US Census does not directly ask residents where they work, it does put out data products on employment based on data it acquires from other Federal and state government agencies.  The Longitudinal Employer-Housing Dynamics program's [LEHD Origin-Destination Employment Statistics (LODES)](https://lehd.ces.census.gov/data/) reports the location of each job and worker covered by state unemployment compensation programs, as well as most Federal jobs.  (Not all Federal jobs are included: military and some security-related civillian jobs are omitted.)

For the purpose of mapping job density, it was possible to partly correct for the omission of military and security-related civillian jobs.  As detailed in Section 1.5.3, The Census provides a shapefile of military bases and I was able to determine the approximate number of employees on most of these bases within the CSA.  I also was able to find the appxoimate number of employees in several of the larger DOD-related job sites not part of military bases.

The maps shown in this section include the job densities on these military bases and other work sites superimposed over the job densities by block group calculated from LODES data.

### 1.1: Jobs in the Combined Statistical Area as a Whole

### 1.2: Jobs in Greater Baltimore

### 1.3: Jobs in Greater Washington

### 1.4: Jobs in Smaller Cities

### 1.5: Data Sources and Processing

The data analyzed in this project is from the US Census's Longitudinal Employer-Housing Dynamics program's [LEHD Origin-Destination Employment Statistics (LODES)](https://lehd.ces.census.gov/data/) data from 2015 (the most recent year available) for the [Washington-Baltimore-Arlington Combined Statistical Area](https://en.wikipedia.org/wiki/Baltimore%E2%80%93Washington_metropolitan_area).

Census 2018 [TIGER/Line](https://www.census.gov/geo/maps-data/data/tiger-line.html) shapefiles for Census block groups, military bases and water areas were used to produce the maps.

Using QGIS 3.4.2, I assembled the LEHD datasets from the states included in the Washington-Baltimore-Arlington Combined Statistical Area ("the CSA") and TIGER/Line block group shapefiles for the counties included in the CSA into single shapefiles.

#### 1.5.1: Processing Water Features

Census block groups include both land and water area—sometimes significant water area—so, to produce a block group connectivity map that better reflects transportation connectivity, I decided to subtract off large water features from the block group shapefile before performing my analyses.

I downloaded Census 2018 TIGER/Line surface water shapefiles for each county in the CSA.  To make the difference operation take a reasonable amount of time on the computers available, all features under 1,000,000 m^2 were removed from the combined shapefile.

Once small features has been removed, I dissolved together all water features and subtracted the combined feature from the block group map to eliminate fictitious continuity across water boundaries.

#### 1.5.2: Tabulating Jobs and Workers by Block Group

The Census reports LODES data tabulated by Census tabulation blocks, and provides crosswalk files to show which tabulation blocks are components of each larger geometry.

To produce a vector layer with numbers of jobs and workers in each Census block group, I combined the crosswalk files for the states included in the CSA into a single shapefile and loaded the combined crosswalk file, the combined jobs and workers data files, and the modified block group shapefile discussed above into a SpatiaLite SQL database.

Using the following SQL query, I created a new vector layer consisting of the block group geometry

- with the land area in acres
- the number of jobs
- the number of jobs per acre
- the number of workers residing
- the number of workers residing per acre
- the number of jobs per worker residing
- the number of excess jobs (jobs minus workers residing)

for each block group.

```sql
select
	bg.geoid,
	(bg.aland+0.0)/4046.86 as "area in acres",
	ifnull(sum(wac.c000),0) as "jobs",
	ifnull((sum(wac.c000)+0.0)
		/((bg.aland+0.0)/4046.860),0) as "jobs per acre",
	ifnull(sum(rac.c000),0) as "workers",
	ifnull((sum(rac.c000)+0.0)
		/((bg.aland+0.0)/4046.86),0) as "workers per acre",
	ifnull((sum(wac.c000)+0.0)/(sum(rac.c000)+0.0),0)
    as "jobs per worker",
  ifnull((sum(wac.c000)+0.0)-(sum(rac.c000)+0.0),0)
    as "excess jobs",
	bg.geometry
from blockgroup_csa_clipped as bg
left join crosswalk_csa as xwalk
	on xwalk.bgrp = bg.geoid
left join wac_s000_jt00_2015_csa as wac
	on wac.w_geocode = xwalk.tabblk2010
left join rac_s000_jt00_2015_csa as rac
	on rac.h_geocode = xwalk.tabblk2010
group by bg.geoid order by "jobs per acre" desc
```

#### 1.5.3: Federal Jobs in LODES Data

LODES data from 2010 forward includes [all jobs covered by state unemployment insurance programs and _most_ civillian Federal jobs](https://lehd.ces.census.gov/doc/help/onthemap/FederalEmploymentInOnTheMap.pdf).  It does not include military jobs (which means that military bases with large employment may not show up as job concentrations), and is missing several Federal agencies seen as security-critical, which is a particular concern in the DC area because it contains the headquarters of many of these agencies.

While a number of the agencies not included in LODES data have their headquarters in downtown DC, where they make up a very small fraction of the jobs present and their workers presumably have the same commuting patterns as other workers employed in downtown DC, several major agencies have headquarters in suburban locations.

Most of the agencies headquarted outside of downtown DC are located on military bases, which also have substantial numbers of military employees.  In addition to local military bases, however, the CIA's headquarters and the Pentagon have substantial concentrations of employees not shown in LODES data.

To account for these job clusters, I estimated the total number of jobs at the following military/classified job clusters:
- [Fort Meade](https://installations.militaryonesource.mil/in-depth-overview/fort-george-g-meade) - 53,000 military and civillian employees, including the NSA and smaller agencies
- [Fort Belvoir](https://en.wikipedia.org/wiki/Fort_Belvoir) - 51,000 military and civillian employees
- [Marine Corps Base Quantico](https://installations.militaryonesource.mil/in-depth-overview/marine-corps-base-quantico) - 26,000 military and civillian employees
- [The Pentagon](https://en.wikipedia.org/wiki/The_Pentagon) - 23,000 military and civillian employees
- [George Bush Center for Intelligence (CIA)](https://en.wikipedia.org/wiki/George_Bush_Center_for_Intelligence) - 15,000 employees, based on the 230,000 m^2 floor area and the agency's roughly 21,000 employees.
- [Naval Air Station Patuxent River](https://installations.militaryonesource.mil/in-depth-overview/naval-air-station-patuxent-river) - 18,500 military and civillian employees
- [Joint Base Anacostia-Bolling](https://installations.militaryonesource.mil/in-depth-overview/joint-base-anacostia-bolling) - 17,000 military and civillian employees
- [Aberdeen Proving Ground](https://installations.militaryonesource.mil/in-depth-overview/aberdeen-proving-ground) - 15,500 military and civillian employees
- [Joint Base Andrews](https://installations.militaryonesource.mil/in-depth-overview/joint-base-andrews-naval-air-facility-washington) - 14,000 military and civillian employees
- [Fort Detrick](https://installations.militaryonesource.mil/in-depth-overview/fort-detrick) - 10,000 military and civillian employees
- [Naval Surface Warfare Center Indian Head](https://en.wikipedia.org/wiki/Indian_Head_Naval_Surface_Warfare_Center) - 2,000 military and civillian employees

I downloaded the Census's TIGER/Line shapefile for military bases and added a column for jobs to allow me to calculate jobs per acre for each of the bases.  This shapefile was then superimposed over the block group shapefile to produce maps of job distribution and density.  Since the Pentagon and CIA Headquarters aren't included in the shapefile, I added entries to the military bases layer for them with approximate areas and numbers of jobs.

Since jobs at these facilities aren't included in the LODES data, I don't know where their workers live, and so excluded them from my analysis of commutersheds.


## 2: Identifying Job Clusters via Moran's I Analysis

To identify job clusters in an objective manner, I decided to perform several Moran's I autocorrelation tests on the LODES data discussed in Section 1.  I did not include the additional jobs not found in LODES that I added to my maps in Section 1, however, since I have those jobs indexed by military base, not block group, and most of the bases cover a number of block groups.  In addition, I don't have worker location information for those jobs as I do for the jobs included in LODES.

Three Moran's I analyses were performed to identify job clusters.  The simplest option was a univariate Moran's I of job density.  This was useful for identifying urban downtowns, but runs into the problem that a high job density may be more a consequence of a dense built environment than of an area that many people commute to.

To correct for this, I also performed a univariate Moran's I analysis on the "excess" job density, which I defined as the number of jobs minus the number of workers in a block group, divided by the block group's area.

Finally, I used a bivariate Moran's I analysis on job density and worker density to look for clusters with excesses of either jobs or workers.

### 2.1: Univariate Moran's I of Job Density

The univariate Moran's I autocorrelation map for job density turned out to mostly show interesting features in the Washington, DC area.  Of smaller cities in the CSA, only Frederick and Annapolis show clusters of dense jobs: other small cities show up, if at all, only as areas that aren't part of the background cluster of low job density.

In Annapolis only one block group registered as the core of such a cluster, apparently corresponding to Annapolis Mall and the surrounded suburban office parks.  In Frederick, there were two small cores of two block groups each, one in the historic downtown and one consisting of office parks near the core.

The situation in Baltimore was, unsurprisingly, a bit more interesting.  Still, only three clusters of high job density were identified in the Baltimore area.  The largest one consisting of downtown Baltimore, broadly defined, and including Mount Vernon, Fells Point, and the Johns Hopkins medical campus.  A second cluster within the City of Baltimore seems to correspond to the Johns Hopkins main campus, and a larger cluster (geographically about half the size of the downtown cluster) is present in Towson.

![Univariate Moran's I analysis of jobs per acre in Baltimore](Maps/jobs_per_acre_high-res_Baltimore_cropped.png)
A univariate Moran's I autocorrelation analysis of job density in Baltimore.  Dark red indicates the cores of clusters of high job density.  Only three such clusters are visible: the largest one, at bottom, is downtown Baltimore including Fells Point and the Johns Hopkins Medical Campus; the cluster near the top is Towson, in Baltimore County; and the cluster just north of downtown Baltimore appears to be in the vicinity of the Johns Hopkins main campus in Hamden-Charles Village.

The DC area, however, showed a much larger number of suburban clusters, besides the main downtown DC cluster, which includes the Shaw-Howard University area, Georgetown, NoMa, Capitol Hill, and L'Enfant Plaza.

Six clusters in Montgomery County, Maryland are visible, while the only high-job-density block group visible in Prince George's County, Maryland is the one containing the Suitland Federal Center, which is surrounded by low-job-density areas.


![Univariate Moran's I analysis of jobs per acre in DC](Maps/jobs_per_acre_high-res_DC_cropped.png)
A univariate Moran's I autocorrelation analysis of job density in DC at the same resolution as the one of Baltimore.  Dark red indicates the cores of clusters of high job density.  Here, in addition to downtown DC, a number of suburban clusters of high job density are seen in Montgomery County, Maryland (Friendship Heights, Silver Spring, Bethesda, Twinbrook-White Flint, Downtown Rockville, Gaithersburg) and Northern Virginia (Tysons Corner, Reston, Fair Oaks, Springfield, the Rosslyn-Ballston Corridor, South Arlington, and East Alexandria).

### 2.2: Univariate Moran's I of Excess Job Density

In an attempt to identify job clusters that did not show up in the autocorrelation analysis of job density, I performed a second univariate Moran's I analysis of _excess_ job density, defined as the density of jobs minus workers.  The justification for this analysis was that it might turn up job clusters in lower-density suburban areas that are still notable for being primarily commercial or industrial rather than residential.

In the Baltimore area, the changes from the original analysis were relatively minor.  The downtown Baltimore cluster is nearly identical, while the Towson cluster is rather larger and no longer discontinuous.  In this analysis, several block groups that have notably higher excess job density than their surroundings turned up.  Oddly, the largest ones seem to correspond to parkland; this may indicate a problem in the underlying data.

![](Maps/excess_jobs_per_acre_high-res_Baltimore_cropped.png)
A univariate Moran's I autocorrelation analysis of excess job density (density of jobs minus workers) in Baltimore.  Dark red indicates the cores of clusters of high job density.  Gray indicates block groups adjacent to cores.  The large cluster in the upper portion of the image is Towson; the large cluster in the lower portion is downtown Baltimore.

The excess job density autocorrelation map for DC is—as it was for job density—much more interesting than the map for Baltimore.  The largest clusters are in Tysons Corner and Downtown DC.  The Rosslyn-Ballston Corridor is visible but mut less prominent and East Alexandria and South Arlington both show up, along with Reston and Fair Oaks.

More notable is the fact that the I-395 corridor from DC to Springfield starts to be visible, mostly as a number of idependent block groups with high excess job density surrounded by clusters of block groups with highly negative excess job density (i.e. dense residential areas).

![](Maps/excess_jobs_per_acre_high-res_DC_cropped.png)
A univariate Moran's I autocorrelation analysis of excess job density (density of jobs minus workers) in DC.  Dark red indicates the cores of clusters of high job density.  Gray indicates block groups adjacent to cores.

This excess job density map is perhaps even more interesting in the Maryland suburbs, as it makes several relatively dense but primarily residential suburban clusters with some jobs appear.  Burtonsville, White Oak, and College Park-Langley Park all show up as a single block group with higher-than-surroundings excess job density along with larger clusters of negative excess job density.

Likewise, the Mid-City and far northern parts of the 16th Street Corridor in DC proper show up as large clusters of negative excess job density, as does part of the Georgia Avenue corridor in DC.  These areas were historically developed as dense streetcar suburbs and still have quite high residential densities while lacking jobs other than in local neighborhood shops, since they were fully built-out before the transition to car-focused suburban offices and industry.

The analysis of Annapolis is notably different in that it shows three cores: one consisting of three block groups in or near the historic downtown, one consisting of a single block group near Annapolis Mall, and one consisting of a single block group containing the Annapolis Technology Park.

![](Maps/excess_jobs_per_acre_high-res_Annapolis_cropped.png)
A univariate Moran's I autocorrelation analysis of excess job density (density of jobs minus workers) in Annapolis.  Dark red indicates the cores of clusters of high job density.  Gray indicates block groups adjacent to cores.  The cluster to the right is historic downtown Annapolis, the one in the center is in the vicinity of Annapolis Mall, and the one to the lower left seems to correspond to Annapolis Technology Park.

In Frederick, this analysis does not seem to provide significantly different results from those found in the analysis of job density alone.  However, the cluster that was in the historic downtown in that analysis seems to have shifted to the right, perhaps because the historic downtown has fairly dense rowhouse neighborhoods.

![](Maps/excess_jobs_per_acre_high-res_Frederick_cropped.png)
A univariate Moran's I autocorrelation analysis of excess job density (density of jobs minus workers) in Frederick.  Dark red indicates the cores of clusters of high job density.  Gray indicates block groups adjacent to cores.  As before, two clusters appear: this time, one just to the east of the historic downtown and one just south of it.

The fact that historic downtown Annapolis, but not historic downtown Frederick, shows up as a core of high excess job density is likely because downtown Annapolis contains a number of government office buildings and also has significantly fewer residences than downtown Frederick, which is largely made up of small stores and rowhouses.

### 2.3: Bivariate Moran's I Comparing Job and Worker Density

In addition to the univariate Moran's I autocorrelation analyses, I performed a bivariate Moran's I correlation analysis comparing job density to worker density.  It is important to note that the color coding of the following maps is different to that in the previous two sections: dark red means high job _and_ worker density, light red means high job and low worker density, light blue means low job and high worker density, and dark blue means low job and low worker density.

As with the initial job density autocorrelation analysis, only Washington, Baltimore, and their suburbs show interesting patterns in this analysis.  While both cities' downtowns do show up, the patterns in these maps are quite different, and a number of major clusters in the autocorrelation analyses are completely missing, while some new areas of job density seem to have appeared.

In the Baltimore area bivariate correlation map, Towson seems to have completely vanished, but clusters of high job density in comparison to worker density are seen in several locations in the suburbs, including Lutherville-Timonium, the Columbia Gateway business park, and a number of other sites I haven't been able to identify.

![](Maps/jobs-workers_per_acre_high-res_Baltimore_cropped.png)
A bivariate Moran's I correlation analysis of the Baltimore area with the first (red) variable as job density and the second (blue) variable as worker density.

Zooming in more closely on the City of Baltimore shows more interesting behavior.  The heart of downtown doesn't show up at all, while the Inner Harbor, Fells Point, Mount Vernon, and the Johns Hopkins main campus and medical campus all show up as concentrations of high density jobs and workers.  The fact that downtown is missing from the map is confusing, and I don't have a good explanation for it.

![](Maps/jobs-workers_per_acre_very-high-res_Baltimore_cropped.png)
A bivariate Moran's I correlation analysis of Baltimore proper with the first (red) variable as job density and the second (blue) variable as worker density.

There are similar oddities in the map of the DC area.  Tysons Corner—the largest suburban job cluster in the region, with 80,000 to 100,000 jobs depending on how the cluster is defined seems to be completely missing.  Downtown Rockville and the Twinbrook-White Flint area are completely missing as well, and Eastern Alexandria is much reduced and seems to consist primarily of workers rather than jobs.

![](Maps/jobs-workers_per_acre_high-res_DC_cropped.png)
A bivariate Moran's I correlation analysis of the DC area with the first (red) variable as job density and the second (blue) variable as worker density.

In the closer-in Maryland suburbs, Bethesda is visible but much reduced in size, while Silver Spring is, if anything, more prominent.  Interestingly, White Oak and Olney, which were barely visible in the other analyses seem somewhat more notable here, and Langley Park appears as a cluster of both jobs and workers.  (It in fact is a very dense residential area but, while it has a number of stores, it is not particularly job-dense other than in comparison to the entirely residential neighborhoods near it.)

Downtown DC, South Arlington, and the Rosslyn-Ballson corridor show up largely as before and, again, the I-395 corridor between Springfield and DC seems quite prominent, with clusters both of high job and worker density and of low job but high worker density.

![](Maps/jobs-workers_per_acre_very-high-res_DC_cropped.png)
A bivariate Moran's I correlation analysis of the DC area somewhat more zoomed in with the first (red) variable as job density and the second (blue) variable as worker density.

Overall, it is clear that the bivariate correlation analysis in this section is not a good way to identify suburban job clusters.  Both the job density and excess job density analysis did a better job of doing so, with excess job density probably the most useful overall.  However, even excess job density missed some notable suburban job clusters that should be included in the commutershed analysis in Section 3.

### 2.4: Data Analysis

Moran's I analyses were performed using GeoDa 1.12.1.131 with queen connectivity and a 100 m error margin on the shapefile of jobs data with water areas removed, discussed in section 1.5.2.

Analyses were performed with 99,999 permutations, the maximum permitted in this version of GeoDa, and a p < 0.05 condition was used.


## 3: Commutersheds for Large Job Clusters

In addition to providing locations of jobs, LODES includes origin-destination data that allows a user to determine how many people commute from a given home Census area to any given workplace Census area and vice versa.  This means that, as well as identifying locations with significant clusters of jobs, it is possible to try to understand the patterns of where people in each cluster commuted from based on this data.

To do this, LODES data on the number of people commuting between each pair of block groups in the CSA was used.  A number of job clusters, including the downtowns (or portions thereof) of Washington and Baltimore, suburban job clusters near each city, and smaller cities in the CSA were selected, and the home locations of each commuter from a given job cluster was identified.

Since LODES data alone was used for this analysis, the military and security-related Federal jobs discussed in Section 1.5.3 are not included in this analysis.

### 3.1: Selection of Job Clusters

While the Moran's I analyses in Section 2 were considered in identifying job clusters, they were only one factor in selecting clusters.  In addition, a desire for an understanding of jobs in a broader portion of the Washington and Baltmore suburbs led to the addition of several clusters that were not identified by autocorrelation analyses.

Furthermore, to maximize the number of jobs considered—important to get a statistically meaningful distribution of commuters—while minimizing computation time, each cluster was defined as a group of nearby (but not necessarily bordering) block groups satisfying two constraints: a job density of at least 1.5 jobs per acre (based on the Census population density definition of non-rural areas) and a total of at least 1,000 jobs in each block group.

The job clusters selected, with the number of jobs included, are listed below.  Each cluster name links to a CSV file showing the block groups in the cluster along with its area in acres, jobs, jobs per acre, workers, workers per acre, jobs per worker, and excess jobs (jobs minus workers).
- Baltimore Area
	- Baltimore City
		- [Downtown Baltimore](ClusterData/Downtown_Baltimore.csv) — 156,558 jobs
		- [Pikesville-Fallstaff](ClusterData/Pikesville-Fallstaff.csv) (Reistersown Plaza) — 28,115 jobs
		- [Hamden-Charles Village](ClusterData/Hamden-Charles_Village.csv) (Hopkins Main Campus) — 22,495 jobs
	- Baltimore Suburbs
		- [Lutherville-Timonium](ClusterData/Lutherville-Timonium.csv) — 62,274 jobs jobs
		- [Columbia](ClusterData/Columbia.csv) — 53,792
		- [Towson](ClusterData/Towson.csv) — 50,877 jobs
		- [White Marsh-Rossville](ClusterData/White_Marsh-Rossville.csv) — 35,609 jobs
		- [South Baltimore County](ClusterData/South_Baltimore_County.csv) — 29,222 jobs
- Washington Area
	- District of Columbia
		- [Old Downtown DC](ClusterData/DC_Old_Downtown.csv) (west of 16th St NW) — 243,054 jobs
		- [New Downtown DC](ClusterData/DC_New_Downtown.csv) (east of 16th St NW) — 167,265 jobs
		- [L'Enfant Plaza-Capitol Hill](ClusterData/LEnfant-Capitol_Hill.csv) (south of the Mall) — 54,379 jobs
		- [Georgetown](ClusterData/Georgetown.csv) — 32,647 jobs
	- Maryland
		- [Gaithersburg](ClusterData/Gaithersburg.csv) — 76,193 jobs
		- [Rockville Pike](ClusterData/Rockville_Pike.csv) — 67,958 jobs
		- [Bethesda](ClusterData/Bethesda.csv) — 63,029 jobs
		- [College Park-Hyattsville](ClusterData/College_Park-Hyattsville.csv) — 31,965 jobs
		- [Silver Spring](ClusterData/Silver_Spring.csv) — 24,761 jobs
	- Northern Virginia
		- [Tysons Corner](ClusterData/Tysons_Corner.csv) — 111,096 jobs
		- [Reston](ClusterData/Reston.csv) — 98,845 jobs
		- [Fair Oaks](ClusterData/Fair_Oaks.csv) — 75,159 jobs
		- [Rosslyn-Ballston Corridor](ClusterData/Rosslyn-Ballston_Corridor.csv) — 74,205 jobs
		- [East Alexandria](ClusterData/East_Alexandria.csv) (Old Town and Potomac Yard) — 46,318 jobs
		- [South Arlington](ClusterData/South_Arlington.csv) (Crystal City and Pentagon City) — 33,361 jobs
- Small Cities
	- [Annapolis, Maryland](ClusterData/Annapolis.csv) — 56,331 jobs
	- [Frederick, Maryland](ClusterData/Frederick.csv) — 47,846 jobs
	- [Hagerstown, Maryland](ClusterData/Hagerstown.csv) — 39,390 jobs

I believe that all clusters of at least 40,000 jobs in the CSA are included in this list.  With the exception of Silver Spring (which seems oddly underestimated by this methodology) and Southern Baltimore County (which was included because it includes UMBC), each of these clusters has at least 30,000 jobs, and many have far more: four, Downtown Baltimore, two portions of Downtown DC, and the suburban edge city of Tysons Corner, each have over 100,000 jobs.



### 3.2: Commuter Dot Maps for Job Clusters

**INCOMPLETE: I intend to create dot maps with one dot per residence location of a commuter to each of the larger job clusters.  (Actually, this will need to be done for each cluster as part of the preparation for Section 3.3, but they won't all be included, at least not on the main page.)**

**Another map could show color-coded dots for commuters to the largest job clusters, though only about four or five clusters could be shown: one option is to group together nearby clusters.**

### 3.3: Commuter Centroids for Job Clusters

**INCOMPLETE: I will make a map showing the commuter centroid for each job cluster, possibly along with the center of the cluster itself and the distance between them.**

### 3.4: Median Commute Distance for Job Clusters

**INCOMPLETE: I will calculate the median commute distance for each job cluster and see if any interesting patterns are evident.**

### 3.x: Data Analysis

Query used to add block group labels to origin-destination data.

```sql
select
	od.ogc_fid as "fid",
	od.h_geocode as "h_tbblk",
	od.w_geocode as "w_tbblk",
	xwalk_h.bgrp as "h_bgrp",
	xwalk_w.bgrp as "w_bgrp",
	od.s000 as "workers"
from od_jt00_2015_csa as od
left join crosswalk_csa as xwalk_h
	on xwalk_h.tabblk2010 = od.h_geocode
left join crosswalk_csa as xwalk_w
	on xwalk_w.tabblk2010 = od.w_geocode
```
