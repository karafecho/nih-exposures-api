# Green Team Exposure Data and Models

**Last Update**: 06/16/2017

Original document in DropBox: [GreenTeamExposureModels](https://www.dropbox.com/home/DataTranslatorProject/PostAwardDocs/SocioEnvExposureModels?preview=GreenTeamExposureModels_v4_04.20.17.docx) (requires credentials)

## Contents

1. Exposure to Roadways ([road](roadways.md))
2. Exposure to Airborne Particulates ([pm25](airborne-particulates.md))
3. Exposure to Ozone ([o3](ozone.md))
4. Exposure to Hazardous Waste ([haz_waste](hazardous-waste.md))
5. Exposure to Crime/Violence ([crime](crime-violence.md))
6. Exposure to Residential Density ([res_den](residential-density.md))
7. Exposure to Poverty ([poverty](poverty.md))
8. Exposure to Socioeconomic Status ([ses](socioeconomic-status.md))


## General Spatio-temporal Exposure Model

**Goal**: Produce a stratification model for each socioenvironmental and drug exposure measure in order to compare subpopulations based on drug versus drug, drug versus outcome measure (ED visits), etc.

A general spatial-temporal exposure model:[1] A patient will be on a specific drug for a certain time period `[Ts,Te]`.  During that time period, we can consider they spend a portion of their time at different locations `[L1:D1, L2:D2, ..., LN:DN]` where `Lx` is a location of interest (geospatial coordinates) and `Dx` is the percentage of time spent in that location, `n = 1…N`.  For instance, a patient may spend 50% of time at work and 50% at home.  `Ts` and `Te` can be a date or a date and time. 

A (socio)environmental exposure estimate for a patient can then be computed using the input `EXPest = [Ts,Te,L1:D1,L2:D2,...,:LN:DN]`

**Caveat**: This model doesn't explicitly take account of time of day or time of year, but EXPest could be readily be expanded to include those variables.

**Caveat**: The time interval may also involve a specific period of time prior to (or after) diagnosis or adverse event, and we may want to calculate exposure 'scores' during that time interval

**Caveat**: this doesn't handle travel well (e.g., commute routes, or driving along a road(s) unless the road is considered a location)

***Note**: For airborne exposures, we are working with UNC’s Institute for the Environment to develop more complex models that take account factors such as time of day, seasonal conditions, humidity levels, wind flow, etc. (See comment on page 2.)

For several measures, we will want to calculate daily exposure “scores” (`DES`) over the time period `[Ts,Te]`:
For example, for PM2.5, daily exposure ‘scores’ are:[2]

```
DESpm = 1 if 24h max PM2.5 < 4.0 μg/m3
DESpm = 2 if 24h max PM2.5 4.0-7.06 μg/m3
DESpm = 3 if 24h max PM2.5 7.07-8.97 μg/m3
DESpm = 4 if 24h max PM 2.5 8.98-11.36 μg/m3
DESpm = 5 if 24h max PM2.5 > 11.37 μg/m3
```
From the daily scores, we can then calculate exposure scores for a smaller time interval within `[Ts,Te]`.

For example, for PM2.5, we are interested in calculating overall 7- and 14-day `DES` exposure scores:

```
DES7pm = (DESpm1+DESpm2…DESpm7)/7
DES14pm = (DESpm1+DESpm2…DESpm14)/14
```

Note: The 7- and 14-day exposure scores are calculated with respect to the day of interest and the 6- and 13-days prior to that date

Caveat: For certain measures (e.g., poverty/non-poverty), the Expest measure will be the same as the `DES` and `DES7` and `DES14` values.


## References and Notes

[1] Spatial-temporal exposure model is based one developed by: Batterman S, Ganguly R, Isakov V, Burke J, Arunachalam S, Snyder M, Robins T, Lewis T. Dispersion Modeling of Traffic-Related Air Pollutant Exposures and Health Effects among Children with Asthma in Detroit, Michigan. Transp Res Rec. 2014l2452:105–112. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4486042/.

--	Near-roadway EXposure and Urban air pollutant Study (NEXUS) air pollution epidemiology study.

--	AERMOD, CMAQ, R-LINE dispersion models

--	R-LINE treats roadways as line sources and parameterizes the horizontal and vertical spread of the plume.

-	Summary: exposure based on exposure to carbon monoxide, nitrogen oxides, particulate matter under 2.5 microns in diameter (PM2.5), and diesel exhaust emissions near roadways.

- Exposures impact: exacerbation of asthma, asthma onset, impaired lung function, card1iovascular morbidity, and mortality, adverse birth outcomes, and cognitive decline.

- Relevance: In the US, an estimated 40 million people in the U.S. live within 100 m of major roads, railways or, airports and millions more commute on major roads, suggesting the importance of exposure to traffic-related air pollutants for public health.

Important notes:

- Traffic-related air pollutants are elevated levels near roads, including PM2.5, ultrafine PM (currently unregulated), VOCs, NO, and polycyclic aromatic hydrocarbons (PAHs), and pollutant levels demonstrate steep gradients in concentrations and typically reach background levels at distances of 150 to 200 m from the road.

- High traffic/high diesel (HD), defined as homes within 150 m of roads with >6,000 commercial vehicles/day (commercial annual average daily traffic; CAADT) and >90,000 total vehicles/day (annual average daily traffic; AADT). High traffic/low diesel (LD), defined as homes within 150 m of roads with >90,000 AADT and <4,500 commercial vehicles/day. Low traffic (LT) homes located >300 m from roads with >25,000 AADT and greater than 500 m from roads with >90,000 AADT.

- US DOT roadway data include: number of lanes, roadway type (e.g., freeway, arterial), AADT, average speed, and eight vehicle types (heavy duty diesel, light duty gas, etc.).

[2] Mirabelli MC, Vaidyanathan A, Flanders WD, Qin X, Garbe P. Outdoor PM2.5, ambient air temperature, and asthma symptoms in the past 14 days among adults with active asthma. Environ Health Perspect 2016;124(12):1882–1890. https://www.ncbi.nlm.nih.gov/pubmed/27385358.

[3] Bravo M, Schurman S, Garanttziotis S, Strauss B, Miranda ML. Relationships between TLR4 pathways single nucleotide polymorphisms, distance to roadway, and asthma diagnosis and severity. APHA Meeting Abstract, No. 333429, 2015. https://apha.confex.com/apha/143am/webprogram/Paper333429.html.

- Calculated distance from residence to nearest road, classified as <250 meters or >250 meters, including highways, major roads, and secondary/connecting roads

- Residence <250 m from road more likely to report asthma diagnosis.

[4] Chen H, Kwong JC, Copes R, Tu K, Villeneuve PJ van Donkelaar A, Hystad P, Martin RV, Murray BJ, Jessiman B, Wilton AS, Kopp A, Burnett RT. Living near major roads and the incidence of dementia, Parkinson’s disease, and multiple sclerosis: a population-based cohort study. The Lancet 2017;389(10070):718–726. http://www.thelancet.com/journals/lancet/article/PIIS0140-6736(16)32399-6/abstract.

- Distance in meters calculated using ArcGIS and included major roads (i.e., primary urban roads and arterial roads with medium to large traffic capacity) and highways (expressways and primary and secondary highways)

- HR of dementia was 1.07 for persons living <50 meter from major road, 1.04 for 50–100 meters, 1.02 for 101–200 meters, and 1.00 for 201–300 meters. No association between distance to road and PD or MS.

[5] US EPA AQI breakpoints https://en.wikipedia.org/wiki/Air_quality_index[3].

[6] White MC, Etzel RA, Wilcox WD, Lloyd C. Exacerbations of childhood asthma and ozone pollution in Atlanta. Environ Res. 1994;65:56–68. https://www.ncbi.nlm.nih.gov/pubmed/?term=Exacerbations+of+childhood+asthma+and+ozone+pollution+in+Atlanta.

- No effect on hospital visits <1-h max of 0.110 ppm (110 ppb); increased asthma or reactive airway hospital visits day after exposure to >0.110 ppm (110 ppb)

[7] Thurston, G. D.; Lippmann, M.; Scott, M. B.; Fine, J. M. Summertime haze air pollution and children with asthma. Am J Respir Crit Care Med. 1997;155:654–660. https://www.ncbi.nlm.nih.gov/pubmed/9032209.

- Dose-related increase in asthma med use associated with 1-h max ozone: 0, 50, 100, 150, 200 ppb (0, 0.050, 0.100, 0.150, 0.200 ppm)

[8] Sheffield PE, Zhou J, Shmool JLC, Clougherty JE. Ambient ozone exposure and children’s acute asthma in New York City: a case-crossover analysis. Environ Health. 2015;14:25. https://ehjournal.biomedcentral.com/articles/10.1186/s12940-015-0010-2.

- Daily average increases of .013 ppm (13 ppb) associated with increased risk for asthma ED visit; sex and age interactions; 0- to 6-day lag period

[9] Agency for Toxic Substances and Disease Registry, Division of Health Studies. MMWR Weekly 1992;41(05):72–74.

- National Priority List focuses on eliminating health risks of the ~2 million persons living within 1-mile radius of the nearly 1300 hazardous waste sites in US

[10] Vrijheid M. Health effects of residence near hazardous waste landfills: review of epidemiologic literature. Environ Health Perspect 2000;108(suppl 1): 101–112.

- Majority of reviewed studies focused on residence within 1-mile radius of site and found associations with risk of various cancers, congenital malformations and other birth defects, poor pregnancy outcomes, and renal disease.

[11] Hu H, Shine J, Wright RO. The challenge posed to children’s health by mixtures of toxic waste: the Tar Creek Superfund Site as a case-study. Pediatr Clin North Am 2007:54(1):155–173.

- Focused on children living within a 50-mile radius of site

- Variety of negative health impacts identified

[12] Chatham-Stephens K, Caravanos J, Ericson B, Sunga-Amparo J, Susilorini B, Sharma P, Landrigan PJ, Fuller R. Burden of disease from toxic waste sites in India, Indonesia, and the Philippines in 2010. Env Health Perspect 2013;121:791–796.

- Residence ‘near’ toxic waste sites associated with significant disease burden as estimated by a disability-adjusted life year (DALY) estimates

[13] Agency for Toxic Substances and Disease Registry. ATSDR assessment of the evidence for the drinking water contaminants at Camp Lejeune and specific cancers and other diseases. January 13, 2017. ATSDR, US DHHS.

- Significant health impacts established for a variety of toxins

[14] Kirpich A, Leary E. Superfund locations and potential associations with cancer incidence in Florida. Statistics Public Policy 2017:4(1):1–9.

- Significantly increased cancer incidence risk for people living in counties containing Superfund sites

[15] NeighborhoodScout®, 2000-2016. Location, Inc.

[16] Hines R, Markossian T, Johnson A, Dong F, Bayakly R. Geographic residency status and census tract socioeconomic status as determinants of colorectal cancer outcomes. Am J Public Health 2014;104(3):e63–e71. https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3953793/.

[17] Freeman VL, Ricardo AC, Campbell RT, Barrett RE, Warnecke RB. Association of census tract-level socioeconomic status with disparities in prostate cancer-specific survival. Cancer Epidemiol Biomarkers Prev 2011;20(10):2150–2159.https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3189295/.

- US Census tract-level concentrated disadvantage scores based on 1990 US Census data was a simple sum of the following: % in poverty + % unemployed + % female-headed households + (100 - % college graduate)

