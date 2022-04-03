# rcode
#fusion chart R code

fusionPlot(data, x, y, type = "column2d", numberSuffix = NULL)

library(fusionchartsR)

# Single
df <- data.frame(label = c("Venezuela", "Saudi", "Canada", "Russia"), value = c(290, 260,180, 115))
df %>%
  fusionPlot(x = "label", y = "value", type = "pie2d") %>%
  fusionTheme(theme = "fusion")

library(fusionchartsR)

# Multiple charts
new.data <- data.frame(
  label = rep(x = c(2012:2016), times = 2),
  seriesname = c(rep("iOS App Store", 5), rep("Google Play Store", 5)),
  values = c(1:10)
)

new.data %>%
  fusionMultiPlot(
    x = "label",
    y = "values",
    col = "seriesname",
    type = "mscolumn2d",
  ) %>%
  fusionTheme(theme = "fusion")


library(fusionchartsR)
df <- data.frame(label = c("Venezuela", "Saudi", "Canada", "Russia"), value = c(290, 260,180, 115))

df %>%
  fusionPlot(x = "label", y = "value", type = "pie2d") %>%
  fusionTheme(theme = "gammel")

df %>%
  fusionPlot(x = "label", y = "value", type = "pie2d") %>%
  fusionPalette(palettecolors = c("5d62b5", "29c3be", "f2726f")) %>%
  fusionTheme(theme = "gammel")


library(fusionchartsR)
df <- data.frame(label = c("Venezuela", "Saudi", "Canada", "Russia"), value = c(290, 260,180, 115))
df %>%
  fusionPlot(x = "label", y = "value", type = "doughnut2d") %>%
  fusionLegend(legendCaption = "LegendCaption", legendCaptionFontSize = "24") %>%
  fusionTheme(theme = "fusion")

#sankey graph

library(networkD3)
nodes = data.frame("name" = 
                     c("Node A", # Node 0
                       "Node B", # Node 1
                       "Node C", # Node 2
                       "Node D"))# Node 3
links = as.data.frame(matrix(c(
  0, 1, 10, # Each row represents a link. The first number
  0, 2, 20, # represents the node being conntected from. 
  1, 3, 30, # the second number represents the node connected to.
  2, 3, 40),# The third number is the value of the node
  byrow = TRUE, ncol = 3))
names(links) = c("source", "target", "value")
sankeyNetwork(Links = links, Nodes = nodes,
              Source = "source", Target = "target",
              Value = "value", NodeID = "name",
              fontSize= 12, nodeWidth = 30)

library(plotly)

fig <- plot_ly(
  type = "sankey",
  orientation = "h",
  
  node = list(
    label = c("A1", "A2", "B1", "B2", "C1", "C2"),
    color = c("blue", "blue", "blue", "blue", "blue", "blue"),
    pad = 15,
    thickness = 20,
    line = list(
      color = "black",
      width = 0.5
    )
  ),
  
  link = list(
    source = c(0,1,0,2,3,3),
    target = c(2,3,3,4,4,5),
    value =  c(8,4,2,8,4,2)
  )
)
fig <- fig %>% layout(
  title = "Basic Sankey Diagram",
  font = list(
    size = 10
  )
)

library(plotly)

fig <- plot_ly(
  type = "sankey",
  domain = list(
    x =  c(0,1),
    y =  c(0,1)
  ),
  orientation = "h",
  valueformat = ".0f",
  valuesuffix = "TWh"
)
fig <- fig %>% layout(
  title = "Energy forecast for 2050, UK - Department of Energy & Climate Change",
  font = list(
    size = 10
  ),
  xaxis = list(showgrid = F, zeroline = F),
  yaxis = list(showgrid = F, zeroline = F)
)
fig

library(plotly)
library(rjson)

json_file <- "https://raw.githubusercontent.com/plotly/plotly.js/master/test/image/mocks/sankey_energy.json"
json_data <- fromJSON(paste(readLines(json_file), collapse=""))

fig <- plot_ly(
  type = "sankey",
  domain = list(
    x =  c(0,1),
    y =  c(0,1)
  ),
  orientation = "h",
  valueformat = ".0f",
  valuesuffix = "TWh",
  
  node = list(
    label = json_data$data[[1]]$node$label,
    color = json_data$data[[1]]$node$color,
    pad = 15,
    thickness = 15,
    line = list(
      color = "black",
      width = 0.5
    )
  )
) 
fig <- fig %>% layout(
  title = "Energy forecast for 2050, UK - Department of Energy & Climate Change",
  font = list(
    size = 10
  ),
  xaxis = list(showgrid = F, zeroline = F),
  yaxis = list(showgrid = F, zeroline = F)
)

library(plotly)
library(rjson)

json_file <- "https://raw.githubusercontent.com/plotly/plotly.js/master/test/image/mocks/sankey_energy.json"
json_data <- fromJSON(paste(readLines(json_file), collapse=""))

fig <- plot_ly(
  type = "sankey",
  domain = list(
    x =  c(0,1),
    y =  c(0,1)
  ),
  orientation = "h",
  valueformat = ".0f",
  valuesuffix = "TWh",
  
  node = list(
    label = json_data$data[[1]]$node$label,
    color = json_data$data[[1]]$node$color,
    pad = 15,
    thickness = 15,
    line = list(
      color = "black",
      width = 0.5
    )
  ),
  
  link = list(
    source = json_data$data[[1]]$link$source,
    target = json_data$data[[1]]$link$target,
    value =  json_data$data[[1]]$link$value,
    label =  json_data$data[[1]]$link$label
  )
) 
fig <- fig %>% layout(
  title = "Energy forecast for 2050<br>Source: Department of Energy & Climate Change, Tom Counsell via <a href='https://bost.ocks.org/mike/sankey/'>Mike Bostock</a>",
  font = list(
    size = 10
  ),
  xaxis = list(showgrid = F, zeroline = F),
  yaxis = list(showgrid = F, zeroline = F)
)

fig

library(plotly)
library(rjson)

json_file <- "https://raw.githubusercontent.com/plotly/plotly.js/master/test/image/mocks/sankey_energy_dark.json"
json_data <- fromJSON(paste(readLines(json_file), collapse=""))

fig <- plot_ly(
  type = "sankey",
  domain = list(
    x =  c(0,1),
    y =  c(0,1)
  ),
  orientation = "h",
  valueformat = ".0f",
  valuesuffix = "TWh",
  
  node = list(
    label = json_data$data[[1]]$node$label,
    color = json_data$data[[1]]$node$color,
    pad = 15,
    thickness = 15,
    line = list(
      color = "black",
      width = 0.5
    )
  ),
  
  link = list(
    source = json_data$data[[1]]$link$source,
    target = json_data$data[[1]]$link$target,
    value =  json_data$data[[1]]$link$value,
    label =  json_data$data[[1]]$link$label
  )
)
fig <- fig %>% layout(
  title = "Energy forecast for 2050<br>Source: Department of Energy & Climate Change, Tom Counsell via <a href='https://bost.ocks.org/mike/sankey/'>Mike Bostock</a>",
  font = list(
    size = 10,
    color = 'white'
  ),
  xaxis = list(showgrid = F, zeroline = F, showticklabels = F),
  yaxis = list(showgrid = F, zeroline = F, showticklabels = F),
  plot_bgcolor = 'black',
  paper_bgcolor = 'black'
)

library(plotly)
fig <- plot_ly(
  type = "sankey",
  arrangement = "snap",
  node = list(
    label = c("A", "B", "C", "D", "E", "F"),
    x = c(0.2, 0.1, 0.5, 0.7, 0.3, 0.5),
    y = c(0.7, 0.5, 0.2, 0.4, 0.2, 0.3),
    pad = 10), # 10 Pixel
  link = list(
    source = c(0, 0, 1, 2, 5, 4, 3, 5),
    target = c(5, 3, 4, 3, 0, 2, 2, 3),
    value = c(1, 2, 1, 1, 1, 1, 1, 2)))
fig <- fig %>% layout(title = "Sankey with manually positioned node")

fig



#chart.js graph

install.packages("remotes")
remotes::install_github("JohnCoene/charter")
```

## Example

``` r
library(charter)

chart(cars, caes(speed, dist)) %>% 
  c_scatter()

remotes::install_github("allisonhorst/palmerpenguins")
data(penguins, package = 'palmerpenguins')

chart(data = penguins, caes(flipper_length_mm, body_mass_g)) %>% 
  c_scatter(caes(color = species, group = species)) %>% 
  c_colors( c("darkorange","darkorchid","darkcyan"))
```

#sigmajs graph

library(sigmajs)

# generate data
nodes <- sg_make_nodes()
edges <- sg_make_edges(nodes)

# visualise
sigmajs() %>%
  sg_nodes(nodes, id, label, size, color) %>%
  sg_edges(edges, id, source, target)

# from igraph 
data("lesmis_igraph")

layout <- igraph::layout_with_fr(lesmis_igraph)

sigmajs() %>%
  sg_from_igraph(lesmis_igraph, layout)
