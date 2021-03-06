---
title: R Sunburst Charts | Examples | Plotly
name: Sunburst Charts
permalink: r/sunburst-charts/
description: How to make sunburst charts in R with Plotly.
layout: base
thumbnail: thumbnail/sunburst.gif
language: r
has_thumbnail: true
display_as: basic
order: 7.1
output:
  html_document:
    keep_md: true
---


### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.

```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.9.0'
```

### Basic Sunburst Chart


```r
library(plotly)

p <- plot_ly(
  labels = c("Eve", "Cain", "Seth", "Enos", "Noam", "Abel", "Awan", "Enoch", "Azura"),
  parents = c("", "Eve", "Eve", "Seth", "Seth", "Eve", "Eve", "Awan", "Eve"),
  values = c(10, 14, 12, 10, 2, 6, 6, 4, 4),
  type = 'sunburst'
)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = api_create(p, filename="sunburst-basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/5645.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Sunburst with Repeated Labels


```r
library(plotly)

d <- data.frame(
    ids = c(
    "North America", "Europe", "Australia", "North America - Football", "Soccer",
    "North America - Rugby", "Europe - Football", "Rugby",
    "Europe - American Football","Australia - Football", "Association",
    "Australian Rules", "Autstralia - American Football", "Australia - Rugby",
    "Rugby League", "Rugby Union"
  ),
  labels = c(
    "North<br>America", "Europe", "Australia", "Football", "Soccer", "Rugby",
    "Football", "Rugby", "American<br>Football", "Football", "Association",
    "Australian<br>Rules", "American<br>Football", "Rugby", "Rugby<br>League",
    "Rugby<br>Union"
  ),
  parents = c(
    "", "", "", "North America", "North America", "North America", "Europe",
    "Europe", "Europe","Australia", "Australia - Football", "Australia - Football",
    "Australia - Football", "Australia - Football", "Australia - Rugby",
    "Australia - Rugby"
  ),
  stringsAsFactors = FALSE
)

p <- plot_ly(d, ids = ~ids, labels = ~labels, parents = ~parents, type = 'sunburst')

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = api_create(p, filename="pie-styled")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/5368.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>

### Subplots
In order to create sunburst chart subplots, we use the [domain](https://plot.ly/r/reference/#sunburst-domain) attribute and the layout [grid](https://plot.ly/r/reference/#layout-grid) attribute.

```r
library(plotly)

d1 <- read.csv('https://raw.githubusercontent.com/plotly/datasets/master/coffee-flavors.csv')
d2 <- read.csv('https://raw.githubusercontent.com/plotly/datasets/718417069ead87650b90472464c7565dc8c2cb1c/sunburst-coffee-flavors-complete.csv')
p <- plot_ly() %>%
  add_trace(
    ids = d1$ids,
    labels = d1$labels,
    parents = d1$parents,
    type = 'sunburst',
    maxdepth = 2,
    domain = list(column = 0)
    ) %>%
  add_trace(
    ids = d2$ids,
    labels = d2$labels,
    parents = d2$parents,
    type = 'sunburst',
    maxdepth = 3,
    domain = list(column = 1)
  ) %>%
    layout(
      grid = list(columns =2, rows = 1),
      margin = list(l = 0, r = 0, b = 0, t = 0),
      sunburstcolorway = c(
        "#636efa","#EF553B","#00cc96","#ab63fa","#19d3f3",
        "#e763fa", "#FECB52","#FFA15A","#FF6692","#B6E880"
      ),
      extendsunburstcolors = TRUE)
# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = api_create(p, filename="sunburst-large-num-of-slices")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/5647.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>


#Reference

See [https://plot.ly/r/reference/#sunburst](https://plot.ly/r/reference/#sunburst) for more information and chart attribute options!
