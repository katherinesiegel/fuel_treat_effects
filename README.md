# fuel_treat_effects

## To do:
- currently, overlaps only include fires through 2019. update_mtbs.Rmd makes MTBS file for whole time series (through 2022: "E:/usda_2023/usfs_fuel_treatments/western_us/mtbs_1984_2022_west.shp"). Eventually want to run fuel treatment overlaps with the full fire time series
- also need to restrict control points to USFS land so not comparing across land ownership types


## Table of contents

* update_fuel_treat_cbi.Rmd: Katherine's code for adding composite burn index values to sample points + identifying relevant wildfires  
* co_fuel_treat_for_cbi.Rmd: Katherine's code for adding composite burn index values to sample points  
* fs_fuel_treatment.Rmd: Katherine's code from Aug-Sept 2022 for determining which fuel treatments subsequently burned in MTBS fires  


## Metadata for specific files  

### all_data_cbi.shp  

* uid: unique identifier for the sample points  
* treated_rx: binary, 1 = treated with prescribed fire, 0 = no prescribed fire  
* burned_wf: binary, 1 = burned in subsequent wildfire that affected prescribed fire footprint, 0 = did not burn in subsequent wildfire that affected prescribed fire footprint  
* treat_lvl: combination of rx fire and wildfire exposure  
   - treated_wf: located inside prescribed fire perimeter AND burned in subsequent wildfire  
   - treated_nowf: located inside prescribed fire perimeter but did NOT burn in subsequent wildfire  
   - untreated_wf: located outside prescribed fire perimeter AND burned in subsequent wildfire (only including wildfires that intersect with rx fire treatment footprints)  
   - untreated_nowf: located outside prescribed fire perimeter and did NOT burn in subsequent wildfire (only including wildfires that intersect with rx fire treatment footprints)  
* untreated_nowf: binary, 1 = point received untreated_nowf treatment, 0 = point did not receive that treatment  
* treated_nowf: binary, 1 = point received treated_nowf treatment, 0 = point did not receive that treatment  
* untreated_wf: binary, 1 = point received untreated_wf treatment, 0 = point did not receive that treatment  
* treated_wf: binary, 1 = point received treated_wf treatment, 0 = point did not receive that treatment  
* burned_other_wf: binary, 1 = point was located outside of prescribed fire treatment footprint and did not burn in a wildfire that subsequently affected a prescrbed fire footprint, BUT it burned in a different wildfire  
* cbi_sev: composite burn index severity value for points that burned in wildfires that burned through prescribed fire footprints after prescribed fire treatment occurred (continuous value, 0-3. NA value indicates point was located outside of wildfire)  
* wf_id: MTBS Event_ID code for the wildfire that caused cbi_sev  
* other_cbi_sev: composite burn index severity value for points classified as burned_other_wf (points located outside of the prescribed fire footprints that burned in wildfires that did not affect the prescribed fire footprints) (continuous value, 0-3. NA value indicates point was located outside of wildfire)    
* other_wf_id: MTBS Event_ID code for the wildfire that caused other_cbi_sev  
* other_wf_year: year in which other_wf_id burned

## Associated GEE scripts  
Folder name: fuel_treat_rdd  

* fuel_treat_cbi: CBI code for mtbs and firedpy polygons that intersect with ft polygons  
* fuel_treat_lc: calculates forested area for each fuel treatment in the year before the wildfire  
* ft_forest_pts: extract land cover to sample pts

