---
layout: default
title: "Homework 5"
permalink: /homework5/
---

<div class="analysis-buttons" style="margin-bottom: 1.5rem;">
  <a class="btn" href="https://raw.githubusercontent.com/UIUC-iSchool-DataViz/is445_data/main/bfro_reports_fall2022.csv" target="_blank" style="display:inline-block;padding:0.5rem 1rem;margin-right:0.5rem;border-radius:4px;border:1px solid #444;text-decoration:none;">DATA</a>
  <a class="btn" href="https://colab.research.google.com/drive/1TLYlsMkoMessy2QUQR9cEbo68HKjBcGn?usp=sharing" target="_blank" style="display:inline-block;padding:0.5rem 1rem;border-radius:4px;border:1px solid #444;text-decoration:none;">ANALYSIS</a>
</div>

The dataset used here comes from the Bigfoot Field Researchers Organization (BFRO) reports and includes information about each reported sighting (date, location, classification) along with weather variables such as temperature, uv index, humidity, and wind speed. In this assignment I focused on the uv-index at the time of each sighting and how it changes over time.

---

## Plot 1 – UV Index of Sightings Over Time

<img src="/IS445-HW5/assets/hw5_uvindex_scatter.png" alt="UV Index of Sightings Over Time" style="max-width:100%; height:auto;">

In this plot, I visualize the relationship between the year of each Bigfoot sighting and the UV Index (uv_index) recorded at the time of that sighting. Each circle represents one report: the x-axis encodes the year of the sighting (a temporal variable), while the y-axis encodes the UV Index (a quantitative environmental variable). A scatter plot is appropriate here because it shows how UV levels vary across decades and allows patterns or clustering to emerge visually.

To prepare the data, I first converted the original date field into a proper datetime object and extracted the year as a new column (df['year'] = df['date'].dt.year). I plotted each sighting with slight transparency (alpha) so overlapping points create darker regions, helping reveal denser clusters. This encoding uses position (x, y) for both temporal and quantitative data, while transparency communicates overlapping density.

Overall, this visualization helps illustrate whether Bigfoot sightings tend to occur under higher or lower UV conditions and whether these environmental patterns change over time. The plot also highlights the growing volume of sighting reports in more recent decades, visible through the increasing density of points toward the right side of the chart.

---

## Plot 2 – Yearly UV Index Summary Statistics (Interactive)

<div style="width:100%; max-width:1000px; margin: 1rem 0;">
  <iframe
    src="/IS445-HW5/assets/hw5_uv_stats.html"
    width="100%"
    height="500"
    style="border:none;"
  ></iframe>
</div>

For this visualization, I compute yearly summary statistics of the UV Index to examine how environmental conditions during Bigfoot sightings change over time. After extracting the year from the date field and filtering the data to include sightings from 1970 onward, I grouped the dataset by year and used describe() to calculate metrics such as count, mean, min, max, standard deviation, and quartiles. These values were reshaped into a long format with columns for year, statistic, and value, and zero values were replaced with NaN to avoid misleading dips. The chart uses year on the x-axis and the statistic value on the y-axis, with each statistic drawn as a separate line and color used to distinguish them. Plotting all statistics together makes it easy to compare how typical UV levels (e.g., the median and quartiles) relate to extremes and annual sighting counts, highlighting strong fluctuations in maximum UV Index values over time while most other metrics remain relatively stable.
---

## Interactivity

To make the visualization more interpretable, I incorporated a dropdown menu that allows viewers to isolate any single statistic. Using an Altair selection_point bound to a dropdown, the selected statistic is displayed in its full color and opacity, while all remaining statistics fade to light gray with reduced opacity. This conditional encoding helps the user cut through visual clutter in a chart that contains many overlapping lines. By interactively highlighting metrics such as "mean" or "max", the chart becomes far easier to explore and supports more targeted insights—for example, observing the steep spike in maximum UV Index around the early 2000s or comparing how quartiles shift relative to extremes. This interactivity enhances the analytical usefulness of the visualization beyond what a static multi-line chart could provide.