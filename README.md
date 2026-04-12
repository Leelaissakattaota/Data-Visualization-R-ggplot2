# 📊 Data Visualization using ggplot2 & dplyr in R

![Language](https://img.shields.io/badge/Language-R-276DC3?style=flat-square&logo=r&logoColor=white)
![Library](https://img.shields.io/badge/Library-ggplot2-FF6B35?style=flat-square)
![Library](https://img.shields.io/badge/Library-dplyr-2E7D32?style=flat-square)
![Dataset](https://img.shields.io/badge/Dataset-Gapminder-0052CC?style=flat-square)
![IDE](https://img.shields.io/badge/IDE-RStudio-75AADB?style=flat-square&logo=rstudio&logoColor=white)
![Focus](https://img.shields.io/badge/Focus-Data%20Visualization-6A0DAD?style=flat-square)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen?style=flat-square)

---

## 📌 Project Overview

This project demonstrates **comprehensive data visualization techniques** 
using `ggplot2` and `dplyr` in R — applied to the famous **Gapminder dataset** 
covering global life expectancy, GDP per capita, and population data 
across 142 countries from 1952 to 2007.

It covers 5 chart types across 9 structured tasks — from basic scatterplots 
to multi-faceted visualizations showing global economic and health trends.

**Dataset:** Gapminder (142 countries, 12 years, 6 variables)  
**Language:** R  
**Libraries:** ggplot2 · dplyr · gapminder  

---

## 📂 Project Structure

```
Data-Visualization-R-ggplot2/
│
├── Data-visualization-using-ggplot2-and-dplyr-in-R.R  # Main R script (9 tasks)
├── Rplot.png          # Sample output — Scatterplot
├── Rplot03.png        # Sample output — Faceted plot
├── Rplot07.png        # Sample output — Bar/Boxplot
└── README.md
```

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| **R** | Core programming language |
| **RStudio** | Development environment |
| **ggplot2** | Grammar of Graphics visualization |
| **dplyr** | Data manipulation — filter, group_by, summarise, mutate |
| **gapminder** | Global development dataset |

---

## 📊 Gapminder Dataset

| Variable | Description |
|---|---|
| `country` | Country name (142 countries) |
| `continent` | Continent (5 continents) |
| `year` | Year (1952–2007, every 5 years) |
| `lifeExp` | Life expectancy at birth |
| `pop` | Population |
| `gdpPercap` | GDP per capita (USD) |

---

## 🚀 Project Workflow — 9 Tasks

---

### ✅ Task 1 — Import Packages & Explore Dataset
```r
library(gapminder); library(dplyr); library(ggplot2)
gapminder_1957 <- gapminder %>% filter(year == 1957)
```

---

### ✅ Task 2 — Scatterplots & Log Scales
```r
# Basic scatterplot
ggplot(gapminder_1957, aes(x = pop, y = lifeExp)) + geom_point()

# Log scale on x-axis
ggplot(gapminder_1957, aes(x = pop, y = lifeExp)) +
  geom_point() + scale_x_log10()

# Both axes on log scale
ggplot(gapminder_1957, aes(x = pop, y = gdpPercap)) +
  geom_point() + scale_x_log10() + scale_y_log10()
```

---

### ✅ Task 3 — Color & Size Aesthetics
```r
# Color by continent, size by GDP per capita
ggplot(gapminder_1957, aes(x = pop, y = lifeExp,
                            colour = continent, size = gdpPercap)) +
  geom_point() + scale_x_log10()
```

---

### ✅ Task 4 — Facetting (Multi-Panel Plots)
```r
# Facet by continent
ggplot(gapminder_1957, aes(x = pop, y = lifeExp)) +
  geom_point() + scale_x_log10() + facet_wrap(~continent)

# Facet by year — full gapminder dataset
ggplot(gapminder, aes(x = gdpPercap, y = lifeExp,
                       colour = continent, size = pop)) +
  geom_point() + scale_x_log10() + facet_wrap(~year)
```

---

### ✅ Task 5 — Summarized Scatterplots (dplyr + ggplot2)
```r
# Median life expectancy per year
by_year <- gapminder %>%
  group_by(year) %>%
  summarise(medianLifeExp = median(lifeExp))

# Median GDP per continent per year
by_year_continent <- gapminder %>%
  group_by(year, continent) %>%
  summarize(medianGdpPercap = median(gdpPercap))
```

---

### ✅ Task 6 — Line Plots (Trends Over Time)
```r
# Global median GDP trend
ggplot(by_year, aes(x = year, y = medianGdpPercap)) +
  geom_line() + expand_limits(y = 0)

# GDP trend by continent
ggplot(by_year_continent, aes(x = year, y = medianGdpPercap, color = continent)) +
  geom_line() + expand_limits(y = 0)
```

---

### ✅ Task 7 — Bar Plots
```r
# Median GDP by continent in 1957
ggplot(by_continent, aes(x = continent, y = medianGdpPercap)) +
  geom_col()

# GDP per capita — Oceania countries only
ggplot(oceania_1957, aes(x = country, y = gdpPercap)) +
  geom_col()
```

---

### ✅ Task 8 — Histograms
```r
# Population histogram (millions)
gapminder_1957 <- gapminder %>%
  filter(year == 1957) %>%
  mutate(pop_by_mil = pop / 1000000)

ggplot(gapminder_1957, aes(x = pop_by_mil)) +
  geom_histogram(bins = 30)

# Log scale histogram
ggplot(gapminder_1957, aes(x = pop)) +
  geom_histogram(bins = 30) + scale_x_log10()
```

---

### ✅ Task 9 — Boxplots with Labels
```r
# GDP per capita by continent — log scale + title
ggplot(gapminder_1957, aes(x = continent, y = gdpPercap)) +
  geom_boxplot() +
  scale_y_log10() +
  labs(title = "Comparing GDP per capita across continents")
```

---

## 📈 Visualizations Created

| # | Chart Type | Variables | Insight |
|---|---|---|---|
| 1 | Scatterplot | pop vs lifeExp | Basic relationship |
| 2 | Log Scatterplot | pop vs gdpPercap | Log-scale patterns |
| 3 | Colored Scatterplot | pop, lifeExp, continent, gdpPercap | Multi-dimensional view |
| 4 | Faceted Plot | gdpPercap, lifeExp by year | Global trends 1952–2007 |
| 5 | Trend Scatterplot | year vs medianLifeExp | Life expectancy over time |
| 6 | Line Plot | year vs medianGdpPercap by continent | Economic growth by region |
| 7 | Bar Chart | continent vs medianGdpPercap | Regional GDP comparison |
| 8 | Histogram | Population distribution | Pop spread in 1957 |
| 9 | Boxplot | continent vs gdpPercap | GDP inequality across continents |

---

## 🎓 Skills Demonstrated

- ggplot2 Grammar of Graphics — `aes()`, `geom_*()`, `scale_*()`, `facet_wrap()`
- dplyr data manipulation — `filter()`, `group_by()`, `summarise()`, `mutate()`
- 5 chart types — Scatterplot, Line, Bar, Histogram, Boxplot
- Log scale transformations — `scale_x_log10()`, `scale_y_log10()`
- Multi-aesthetic mapping — color, size, x, y simultaneously
- Facetting for multi-panel visualizations
- Data aggregation with `group_by()` + `summarise()`
- Custom labels with `labs(title = )`
- Global development data analysis with Gapminder

---

## 📜 Certifications

| Certification | Issuer | Platform |
|---|---|---|
| IBM Data Science Professional Certificate | IBM | Coursera |
| IBM Generative AI Professional Certificate | IBM | Coursera |
| IBM Agentic AI with RAG Certificate | IBM | Coursera |
| IBM RAG and Agentic AI Professional Certificate | IBM | Coursera |

---

## 🤝 Connect with Me

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Leela%20A-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/leela-a)
[![Gmail](https://img.shields.io/badge/Gmail-attotaleelaissak@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:attotaleelaissak@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-Leelaissakattaota-181717?style=flat-square&logo=github&logoColor=white)](https://github.com/Leelaissakattaota)
