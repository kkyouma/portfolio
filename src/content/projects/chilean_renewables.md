---
title: "Renewable Energy Time Series Analysis in Chile"
description: "Exploratory Data Analysis (EDA) phase of a broader project aimed at identifying strategies to enhance energy production from renewable technologies."
url: "https://github.com/UCM-Industrial/Forecast_J.Troncoso/"
githubUrl: "https://github.com/UCM-Industrial/Forecast_J.Troncoso/"
featured: true
techs: ["Python", "Pandas", "Data Analysis"]
imagePath: "/images/projects/2024_hourly_seasonal.png"
---

## Project Purpose

This exploratory analysis is part of the thesis project titled _"Development of a tool for the decomposition of seasonal patterns in multi-source energy time series"_. Its purpose is to characterize the seasonal behavior of different energy sources (solar, wind, hydroelectric, and thermal) in the Chilean electrical system, through visual and statistical inspection of time series with hourly, daily, and monthly granularity. This phase is crucial for validating assumptions prior to decomposition (seasonality, trend, residuals), identifying outliers, assessing data quality, and defining initial parameters for modeling.

## Expected Results

- Identification of differential seasonal patterns by technology (e.g., higher solar variability, weekly wind seasonality).
- Detection of anomalies or breaks in series associated with climatic events or measurement errors.
- Initial assessment of dataset quality and coverage.
- Definition of optimal granularities and frequencies for the subsequent STL decomposition.
- Empirical justification for the inclusion of certain exogenous variables in explanatory models.

## EDA

### Understanding the dataset

After cleaning the dataset (blank, null and duplicates values), there is needed to check the columns and the format.
Initially the dataset have a [long format](https://www.statology.org/long-vs-wide-data/), but we need to see the production of each technology and their value for each day.

<div class="table-container" style="overflow-x: auto;">

|     | fecha_opreal        | hora_opreal | nemotecnico | nombre             | central_nombre      | central_infotecnica_id | coordinado        | central_tipo | central_tipo_nemotecnico | subtipo | subtipo_nemotecnico | grupo_reporte_nombre | generacion_real_mwh | generacion_real_ernc_mwh | year | month | day |
| --: | :------------------ | ----------: | :---------- | :----------------- | :------------------ | ---------------------: | :---------------- | :----------- | :----------------------- | :------ | :------------------ | :------------------- | ------------------: | -----------------------: | ---: | ----: | --: |
|   0 | 2024-12-05 00:00:00 |           5 | eerinome    | PMGD PFV Erinome   | PMGD PFV ERINOME    |                   1909 | LUCIANO SOLAR SPA | Solar        | solar                    | Solar   | solar               | PMGD PFV Erinome     |                   0 |                        0 | 2024 |    12 |   5 |
|   1 | 2024-07-23 00:00:00 |           3 | eel-cuervo  | PMGD PFV El Cuervo | PMGD PFV EL CUERVO  |                   2062 | PFV EL CUERVO SPA | Solar        | solar                    | Solar   | solar               | PMGD PFV El Cuervo   |                   0 |                        0 | 2024 |     7 |  23 |
|   2 | 2024-04-09 00:00:00 |           4 | eportezuelo | PORTEZUELO         | PMGD PFV PORTEZUELO |                    519 | TRALKA SPA        | Solar        | solar                    | Solar   | solar               | PMGD PFV Portezuelo  |                   0 |                        0 | 2024 |     4 |   9 |

</div>

### The energy production across the time

After pivoting the table by technology and the production (MWh), we can see the general behavior of the time series. A simple view the Solar (yellow) production have a powerful stationality for year period and a growing trend across the time.

The Wind (blue) production also have a growing trend, but the stationality is not too powerful or evident. And finally the Hydro (green) production have an irregular pattern, that could be dependant of exogenous variables

<img class="inline-image" src="/images/projects/historic_energy_production.png" alt="Daily stationality pattern" width="600" height="auto">

### The patterns

After checking the historic production behavior for the technologies, we could chech more granularity which are exactily the patterns hidden. Initially we could check the hourly common behavior.

<img class="inline-image" src="/images/projects/2024_hourly_seasonal.png" alt="Daily stationality pattern" width="600" height="auto">

- Solar: Exhibits a distinct bell curve, peaking significantly during daylight hours (approximately 8 AM to 6 PM). Its generation is negligible during nighttime. This is characteristic of solar power.
- Eólica (Wind): Shows variability, with higher generation during early morning and late evening hours, and a dip during midday. This pattern can be influenced by typical wind patterns.
- Hidráulica (Hydroelectric): Maintains a relatively consistent and high level of generation throughout the day, with a slight decrease in the late evening. Hydroelectric power can often provide a stable baseload.
- Térmica (Thermal): Shows a gradual increase in generation from morning until evening, peaking in the later hours. This might indicate its use to meet peak demand or to compensate for the decline in solar power.
- Geotérmica (Geothermal): Provides a constant, low level of baseload generation throughout the day, as expected from geothermal source

### Dynamics between technologies

<img class="inline-image" src="/images/projects/corr_matrix.png" alt="Daily stationality pattern" width="600" height="auto">
