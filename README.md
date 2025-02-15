## reactablefmtr <a href='https://kcuilla.github.io/reactablefmtr/index.html'><img src="man/figures/reactablefmtr_hex_logo.png" align="right" width="150" height="185"/>

<!-- badges: start -->
[![CRAN Status](https://www.r-pkg.org/badges/version/reactablefmtr?color=blue)](https://cran.r-project.org/package=reactablefmtr?color=blue)
[![CRAN Downloads](https://cranlogs.r-pkg.org/badges/grand-total/reactablefmtr?color=brightgreen)](https://cranlogs.r-pkg.org/badges/grand-total/reactablefmtr?color=brightgreen)
<!-- badges: end -->

The {reactablefmtr} package simplifies and enhances the styling and formatting of tables built with the {reactable} **R** package. The {reactablefmtr} package provides many conditional formatters that are highly customizable and easy to use.

* **Conditionally format tables** with [color scales](https://kcuilla.github.io/reactablefmtr/articles/color_scales.html), [color tiles](https://kcuilla.github.io/reactablefmtr/articles/color_tiles.html), and [data bars](https://kcuilla.github.io/reactablefmtr/articles/data_bars.html). Assign icons from [Font Awesome](https://fontawesome.com/icons?d=gallery&p=2) with [icon assign](https://kcuilla.github.io/reactablefmtr/articles/icon_assign.html) and [icon sets](https://kcuilla.github.io/reactablefmtr/articles/icon_sets.html).
  
* **Custom table themes** that can [easily](https://kcuilla.github.io/reactablefmtr/articles/themes.html) be applied to any {reactablefmtr} or {reactable} table.
  
* **Embed images** directly from the web into your [table](https://kcuilla.github.io/reactablefmtr/articles/embed_img.html).
  
* **Save tables** as static PNG files or as interactive HTML files.

The {reactablefmtr} package was built using a combination of **R**, **CSS**, and **HTML** in order to allow any level of **R** user to build highly customizable and stylish tables without having to learn additional programming languages.

For more examples, check out the [vignettes](https://kcuilla.github.io/reactablefmtr/articles/). To stay up to date with the latest upgrades to the development version, be sure to follow the package [news](https://kcuilla.github.io/reactablefmtr/news/index.html).

## Installation

The {reactablefmtr} package is available from CRAN and can be installed with:

```{r}
install.packages("reactablefmtr")
```

Or install the development version of {reactablefmtr} with:

```{r}
remotes::install_github("kcuilla/reactablefmtr")
```

## Examples

### Data Bars

Use `data_bars()` to assign horizontal bars to each row. There are many ways to [customize](https://kcuilla.github.io/reactablefmtr/reference/data_bars.html) the look of `data_bars()`, including the alignment of the bars, the position of the text labels, and the option to add icons and images to the bars. See the [tutorial](https://kcuilla.github.io/reactablefmtr/articles/data_bars.html) for customization examples. 


<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/data_bars_animated_demo.gif" align="center" />

### Sparklines

Use `react_sparkline()` to create sparklines or `react_sparkbar()` to create sparkline bar charts. The sparklines are highly customizable and interactive. As you hover over each data point, the value will appear. The sparklines are imported from the [{dataui}](https://timelyportfolio.github.io/dataui/index.html) package, so this package will need to be downloaded from GitHub in order to use this feature.
   
<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/sparklinesgif1.gif" algin="center"/>
<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/sparklinesgif2.gif" algin="center"/>

### Color Scales

Use `color_scales()` to assign conditional colors to cells based on their relative values. The color of the text in the cells automatically adjusts based on the shade of the cell color, allowing the use of dark-colored palettes. See the [tutorial](https://kcuilla.github.io/reactablefmtr/articles/color_scales.html) for more examples.

```{r}
library(reactablefmtr)
library(tidyverse)
library(gapminder)
 
population_data <- gapminder %>% 
  filter(continent == "Americas") %>%
  mutate(country = as.character(country),
         year = paste0("'", str_sub(year, 3, 4))) %>% 
  select(country, year, lifeExp) %>%
  pivot_wider(names_from = year, values_from = lifeExp) 

reactable(
  population_data,
  pagination = FALSE,
  showSortIcon = FALSE,
  defaultSorted = "'52",
  defaultSortOrder = "desc",
  defaultColDef = colDef(
    maxWidth = 45,
    style = color_scales(population_data, show_text = FALSE, span = TRUE)
  ),
  columns = list(
    country = colDef(
      maxWidth = 160
    )
  )
) %>% 
  add_title("Average Life Expectancy") %>% 
  add_source("Data sourced from the {gapminder} package") 
```

<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/colorscales_heatmap2.gif" align="center"/>


### Icon Sets

Use `icon_sets()` to conditionally assign icons to values from the [Font Awesome](https://fontawesome.com/icons?d=gallery&p=2) library based on their relative values. Any number of icons and/or colors can be applied to values within each column. Customization options such as number formatting and positioning of icons are also available. See the [tutorial](https://kcuilla.github.io/reactablefmtr/articles/icon_sets.html) for more options.


<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/MPGbyCarTypeICONS.png" algin="center"/>
  
 
### Icon Assign

Use `icon_assign()` to assign icons to values from the [Font Awesome](https://fontawesome.com/icons?d=gallery&p=2) library. Multiple customization options are available, such as bucketing values and the option to show/hide values next to the icons. See the [tutorial](https://kcuilla.github.io/reactablefmtr/articles/icon_assign.html) for more options.

<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/5E26F646-AE47-4044-B01D-6BEBF28DD08B.jpeg" align="center" />


## Custom Themes

Within {reactablefmtr}, there are 24+ custom table themes. The themes include [bootstrap](https://bootswatch.com/) themes, themes inspired by news/sports sites such as The New York Times, FiveThirtyEight, and ESPN, as well as other custom themes that can only be found within {reactablefmtr}. The themes can be applied easily to tables by simply referencing the theme name. Additional customization options, such as changing the font size, font color, etc. are also [available](https://kcuilla.github.io/reactablefmtr/articles/themes.html).

An example of the fivethirtyeight() theme:

<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/78A671F4-6705-4EE9-9B49-D29934FFE019.jpeg" align="center" />


## Add a Title, Subtitle, and Source

Titles and subtitles can be easily placed above any {reactablefmtr} or {reactable} table with `add_title()` and `add_subtitle()`. Also have the option to include a source below a table with `add_source()`. Additional customization options such as changing the alignment, font size, font family, font style, and font color are available within each formatter.

```{r}
reactable(iris[10:29, ]) %>%
  add_title("This is a title") %>% 
  add_subtitle("This is a subtitle") %>% 
  add_source("This is a source")
```

<img src="https://raw.githubusercontent.com/kcuilla/reactablefmtr/main/man/figures/README_add_title.png" align="center" />


## Create Data Visualizations

Who says {reactablefmtr} can just be used to make tables? You can create data visualizations like the one shown below. [Source code](https://github.com/kcuilla/Tidy-Tuesday/blob/main/2021_26/park_spending.R) 

<img src="https://raw.githubusercontent.com/kcuilla/Tidy-Tuesday/main/2021_26/park_spending_per_resident.png" align = "center" />


## Save Static or Interactive Tables

{reactablefmtr} or {reactable} tables can be saved directly to a file as a static PNG image or as an interactive HTML file with `save_reactable()`.

Save as a PNG file:

```{r}
save_reactable(table_name, "table.png")
```

Save as an HTML file:

```{r}
save_reactable(table_name, "table.html")
```

If custom CSS styling is applied to the table within an R Markdown document:

```{r}
save_reactable("table_name.Rmd", "table.png")
```

If you prefer to use a pipe:

```{r}
table_name %>%
save_reactable("table.png")
```


## Acknowledgments & Contributions

* A huge thank you to Greg Lin for creating the amazing [{reactable}](https://glin.github.io/reactable/index.html) package! Without Greg, {reactablefmtr} simply would not exist! 

* Thank you to June Chao for contributing to the span option in `color_scales()` and `color_tiles()`!

* Thank you to Kent Russell for putting together the wonderful [{dataui}](https://timelyportfolio.github.io/dataui/index.html) package and suggesting integrating the code with {reactablefmtr} to allow interactive sparkline customization in reactable tables.

