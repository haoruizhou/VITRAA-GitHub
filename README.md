# VITRAA - Visualized Interactive Toronto Rapid-Transit Accessibility Analysis 

For Esri Canada ECCE App Challenge 2025
<img width="1673" alt="thumbnail" src="https://github.com/user-attachments/assets/26499c58-950f-4ef0-912c-c63f17ea1638" />


## **Mission Statement**

Toronto offers a diverse array of rapid transit options that empower residents to travel efficiently across the city. This project seeks to rigorously examine the relationship between the walking distance to rapid transit stations and the frequency of transit use in Toronto. Drawing on the methodologies and insights of El‑Geneidy et al. (2014), which emphasize the importance of accurately delineating walking catchment areas to identify gaps and redundancies in transit service, as well as Hao and Peng (2023), who document nonlinear and threshold effects of bus stop proximity on transit use and carbon emissions in developing cities, our study will extend these frameworks to the Toronto context (El-Geneidy et al., 2014; Hao & Peng, 2022).



As the cost of living escalates, a growing number of individuals and families are increasingly dependent on public transit to mitigate transportation expenses. By analyzing how the proximity of transit stations influences ridership patterns, our research aims to provide critical insights into improving transit accessibility—thereby alleviating financial burdens for transit-dependent households—and contribute to the sustainable urban mobility agenda.



## **App Characteristics** (ArcGIS Dashboard)

[View Dashboard](arcgis.com/apps/dashboards/7c71115a8d254fdeb8cba3ec8d42732d)

1. **User-Centric Analysis:** The app provides insights into how transit accessibility impacts commuting behavior, emphasizing equitable access for diverse socioeconomic groups.
2. **Data-Driven Insights:** By leveraging detailed Census data, the analysis quantifies the relationship between transit proximity and mode choice.
3. **Sustainability Focus:** The study underlines how improved transit accessibility can reduce dependency on private vehicles, lower greenhouse gas emissions, and promote sustainable urban mobility.
4. **Reproducible Research:** The organized R code and data retrieval process ensure that the methodology is transparent and reproducible for future studies or policy development.



## **Discussion on Transit Equity and Sustainability**

Transit equity is a fundamental aspect of sustainable urban planning. Ensuring equitable access to transit not only addresses social justice by offering mobility options to all community segments but also enhances environmental sustainability. By facilitating the use of public transit, cities can reduce traffic congestion, lower carbon emissions, and promote healthier lifestyles. This project specifically investigates how distance to transit influences commuting choices, a key determinant of urban mobility patterns and overall sustainability.



## **Data Retrieval and Processing Methodology**

The analysis relies on Census data, retrieved and processed using R. The following sections outline the R code workflow:



**1. Environment Setup and Package Loading**

This initial code block loads necessary libraries and configures settings such as API keys and caching paths:

```R
# Load required packages
library(cancensus)
library(sf)
library(dplyr)

# set_cancensus_api_key("YOUR_API_KEY_HERE")
```

**2. Census Vectors Retrieval**

The following block retrieves available Census vectors from the CA21 dataset and saves the list as a CSV file:

```R
library(cancensus)
list_census_vectors(dataset = "CA21")

# Save the list of Census vectors as a CSV file
census_vectors <- list_census_vectors(dataset = "CA21")
write.csv(census_vectors, "census_vectors.csv", row.names = FALSE)
```

**3. Extracting Toronto Census Data**

This section focuses on extracting Dissemination Area (DA)-level Census 2021 data for the Toronto region, using journey-to-work variable codes:

```R
# Define the Toronto region using its Census Subdivision (CSD) code
toronto_region <- list(CSD = "3520005")

# Define the journey-to-work variable codes of interest
journey_vars <- c(
  ...
  "v_CA21_7644",  # Total - Public transit
  "v_CA21_7645",  # Male - Public transit
  "v_CA21_7646",  # Female - Public transit
  ...
)

# Retrieve DA-level Census 2021 data for Toronto with spatial geometry
toronto_DA <- get_census(
  dataset = "CA21",         # 2021 Census Profile dataset
  regions = toronto_region, # Toronto defined by CSD "3520005"
  level = "DA",             # Dissemination Areas
  vectors = journey_vars,
  geo_format = "sf"         # Return as an sf object (with spatial geometry)
)

# Display the first few rows of the retrieved dataset
head(toronto_DA)
```

**4. Saving Data for Spatial Analysis**

The final block writes the retrieved Toronto Census data to a GeoJSON file for further spatial analysis:

```R
# Save the spatial data to a GeoJSON file
write_sf(toronto_DA, "toronto_DA.geojson", driver = "GeoJSON")
```



**Conclusion**

This project not only explores the influence of transit station proximity on commuting choices but also underscores the broader implications for transit equity and sustainability. The integration of Census data with spatial analysis provides a powerful tool for urban planners and policymakers to design transit systems that are both inclusive and environmentally responsible.

Feel free to modify or expand on any sections as necessary to suit your presentation and analysis needs.



## References

El-Geneidy, A., Grimsrud, M., Wasfi, R., Tétreault, P., & Surprenant-Legault, J. (2014). New evidence on walking distances to transit stops: Identifying redundancies and gaps using variable service areas. *Transportation*, *41*(1), 193–210. https://doi.org/10.1007/s11116-013-9508-z

Hao, Z., & Peng, Y. (2022). Comparing Nonlinear and Threshold Effects of Bus Stop Proximity on Transit Use and Carbon Emissions in Developing Cities. *Land*, *12*(1), 28. https://doi.org/10.3390/land12010028
