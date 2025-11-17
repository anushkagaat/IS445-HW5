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

For this visualization, I compute and display yearly summary statistics of the UV Index to understand how environmental conditions during Bigfoot sightings change over time. After extracting the year column from the date field, I restricted the dataset to sightings from 1970 onward, which removes sparse early-year data and yields a more interpretable timeline. I then grouped the dataset by year and calculated descriptive metrics for the uv_index variable—such as count, mean, min, max, standard deviation, and quartiles—using describe(). These results were reshaped into a tidy long format with columns year, Stat, and Value, enabling multiple statistics to be plotted together on a single chart. Zero values were replaced with NaN to prevent artificial dips that would imply UV Index readings of zero when no valid measurement existed.
In the chart, the x-axis encodes year as a temporal continuous variable, while the y-axis encodes the numeric value of each summary statistic. A line mark is used for each statistic, and color serves as a nominal channel to distinguish the individual metrics such as "50%", "mean", "max", "min", "count", "25%", and "75%". Plotting all metrics together on the same coordinate system allows the viewer to compare how typical UV values (e.g., the median or quartiles) relate to annual extremes (the maximum and minimum) as well as the number of sightings per year. The chart’s tall scale highlights strong variations in the maximum UV Index over time, while lower-range statistics remain more stable and clustered near the bottom of the plot.

---

## Interactivity

To make the visualization more interpretable, I incorporated a dropdown menu that allows viewers to isolate any single statistic. Using an Altair selection_point bound to a dropdown, the selected statistic is displayed in its full color and opacity, while all remaining statistics fade to light gray with reduced opacity. This conditional encoding helps the user cut through visual clutter in a chart that contains many overlapping lines. By interactively highlighting metrics such as "mean" or "max", the chart becomes far easier to explore and supports more targeted insights—for example, observing the steep spike in maximum UV Index around the early 2000s or comparing how quartiles shift relative to extremes. This interactivity enhances the analytical usefulness of the visualization beyond what a static multi-line chart could provide.