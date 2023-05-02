---
title: "Intersectionality and Dialogue"
author: "Kesia Otieno"
date: "`r format(Sys.time(), '%d %B, %Y')`" 
output: 
  prettydoc::html_pretty:
    toc: true
    theme: architect
    highlight: github 
bibliography: practicum_bibliography.bib
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(fig.align = 'center',out.width = '100%', echo = TRUE)
```

```{r data, include = FALSE}
library(readr)
library(dplyr)
library(ggplot2)
library(tidyverse)
library(knitr)
library(tidytext)
library("data.table")
library("bibtex")
library(readxl) 
```

# Introduction 

## Background

  The world now is saturated with media content. It is not new that we've seen a movement of pointing out the lack of racial and ethnic representation in film. Not only has it been a topic of representation but representation that does not come from stereotypes or have negative societal impacts on entire racial groups [@Gray2016-fz]. It has been noted by scholars that the foundation of American cinema was built on the use of racial stereotypes [@DVN/KERZQY_2018]. While I am interested in these topics, I wanted this paper to pivot toward the intersections of identity within film. From the discussion of racial and ethnic diversity in film, there is also the topic of intersectionality and the importance of not only including meaningful representation of race but also gender [@sutherland2017here], sexuality, disability, age, class, etc [@Smith2007-xc]. This paper seeks to gain some insight into and/or general analysis of the intersection of race and gender-related to dialogue in film.

## Emergence of DuVernay Test & Importance 

  There has been talk of a new test dubbed the [**DuVernay Test**](https://www.vox.com/2016/2/1/10888212/duvernay-test-movie-diversity) which inspects the presence of racially diverse characters in films [@massie_2016]. Its origins come from the Bechdel Test which requires a story where two women have a conversation about something other than a man [@rossbechdel]. The three metrics for the DuVernay Test are speaking parts, complex characters, and names. Complex characters are two racial minority characters that are not in a relationship and have complex lives that are not directly tied in relation to white characters [@massie_2016]. The "names" metric is to ensure the characters have names and roles. The metric speaking parts refer to the characters having dialogue that is not about a supporting white character. Some film examples that pass the DuVernay Test are Black Panther(2018), Parasite(2019), Selma (2014), Crazy Rich Asians(2018) [@massie_2016] . The data set I used did not provide a variable for complex characters, however, it did provide Character Names and Extracted Word Dialogue of the characters. Although this data analysis does not use the DuVernay Test I believe it is important to keep in mind for future analysis on the topic.

## Purpose

  Through this information on Gender, Race, and Script Dialogue, my research question is "Does the combination of gender and race have a significant impact on the amount of words spoken by a character?" As we've seen from test like DuVernay, speaking parts can potentially be indicative of representation. Since the amount of speaking parts could be central to representation in film, hypothetically, a characters race and gender could influence it. The null hypothesis here is that there is no significant change in medians of the intersection of gender and race and speaking parts. The alternative hypothesis is that there is a significant change (whether that be increase or decrease) in the medians between of the intersection of gender and race and speaking parts.

        H0: There is no relationship between the interesction of Gender+Race and Polygraph Word Count.

        H1: There is a relationship between the interesction of Gender+Race and Polygraph Word Count.
        
                    α = .05

The chosen significance level is an alpha of 0.05. 

# Methods 

## Collecting Data

  The data set is from Harvard's [**Racial lines**](file:///C:/Users/kesia/Downloads/Racial_Lines_2018%20(2).pdf) data set. The [**Racial lines**](file:///C:/Users/kesia/Downloads/Racial_Lines_2018%20(2).pdf) data set originates from a previous data set of screenplays with 780 films on gender and dialogue conducted by Hannah Anderson and Matt Daniel at the Pudding [@Anderson2016-pd]. The [**Racial lines**](file:///C:/Users/kesia/Downloads/Racial_Lines_2018%20(2).pdf) data set took the data set from The Pudding and incorporated the variable of Race [@DVN/KERZQY_2018]. As Noted in the section below I removed several variables that were not necessary for the data analysis I was conducting.I then used the wilcox.test() function to generate test statistics to use in my analysis.

```{r, include = FALSE}
library(readxl)
actors <- read_excel("actors.xlsx", col_types = c("numeric", 
    "text", "text", "text", "text", "text", 
    "numeric", "numeric"), na = "NA")
View(actors)
```

```{r Renaming Gender, include = FALSE}
actors[actors$GENDER == "f", "GENDER"] <- "Women"
actors[actors$GENDER == "m", "GENDER"] <- "Men" 
```

```{r Renaming Character Race, include = FALSE}
actors[actors$CHARACTER_RACE == "b", "CHARACTER_RACE"] <- "Black" 
actors[actors$CHARACTER_RACE == "a", "CHARACTER_RACE"] <- "East Asian"
actors[actors$CHARACTER_RACE == "i", "CHARACTER_RACE"] <- "Indigenous"
actors[actors$CHARACTER_RACE == "l", "CHARACTER_RACE"] <- "Latinx"
actors[actors$CHARACTER_RACE == "n", "CHARACTER_RACE"] <- "Near Eastern"
actors[actors$CHARACTER_RACE == "s", "CHARACTER_RACE"] <- "South Asian"
actors[actors$CHARACTER_RACE == "w", "CHARACTER_RACE"] <- "White"
```

```{r Removing Unnecessary Columns, include = FALSE}
actors2 <- subset(actors, select = -c(SCRIPT_ID,CHARACTER_NAME,ACTOR_NAME,ACTOR_RACE)) 
```

```{r Adding New Gender+Race Column, include= FALSE}
actorsFINAL <- actors2 %>% unite("Gender_Race", CHARACTER_RACE:GENDER, remove = FALSE) 
actorsFINAL$Gender_Race <- factor(actorsFINAL$Gender_Race, levels=c('Black_Women', 'Black_Men', 'East Asian_Women', 'East Asian_Men', 'Indigenous_Women','Indigenous_Men',"Latinx_Women", 'Latinx_Men','Near Eastern_Women','Near Eastern_Men', 'South Asian_Women', 'South Asian_Men','White_Women', 'White_Men'))
```

```{r, echo = FALSE}
ggplot(actorsFINAL, aes(x = Gender_Race, y = POLYGRAPH_.WORDS, color = Gender_Race)) + geom_boxplot() + coord_flip() + scale_y_log10() + labs(title = "Race+Gender Relation with Polygraph Words", x = "Race+Gender", y = "Polygraph words")

```
 

## Purpose For Plots & Test   

### Mann Whitney U Test 

  I used the Shapiro-Wilk Test and generated a histogram for each unique Race+Gender category I intended to use. Both methods illustrated that my individualized data sets did not have a normal distribution. Due to my data nor having a normal distribution I sought out a Non-Parametric Analysis to compare outcomes between two independent variables. I opted for a non-directional or two-tailed U-test as the possible directionality was not something I wanted to be specified.  

```{r - Create Data Set - Actors & Polygraph, include = FALSE }
actors_polygraph <- subset(actorsFINAL, select = -c(GENDER,AGE,CHARACTER_RACE))
```
  
```{r Filtering out White Actors- , echo = FALSE}
actors_polygraph_graph <- actors_polygraph[actors_polygraph$Gender_Race != "White_Men",] 
actors_polygraph_graph2 <- actors_polygraph_graph[actors_polygraph_graph$Gender_Race != "White_Women",] 
```

```{r, echo=FALSE}
ggplot(actors_polygraph_graph2, aes(y = POLYGRAPH_.WORDS, color = Gender_Race)) + geom_histogram(bins = 13) + scale_y_log10() + facet_wrap(~ Gender_Race) +labs(title = "Race+Gender & Polygraph Words Distribution", x = "Count", y = "Polygraph Word") 

# Important Note ! Please note I removed the Grid Histogram Plots of White_Women and White_Men because there n values were so high you could not view the counts for any other race+gender group. Additionally, there is no visualization of Near Eastern Characters because there was no observations of Near Eastern Women characters.
```

### Pie Chart - Still Pending...

  While it is true Pie Charts are not the best tool for proper data visualization it does come in handy when providing legible visualization. The Pie Chart was used to show the reader the percentage of each demographic present in the data set and compare to the U.S. Census data to represent how certain groups are over represented.

### Box Plot

  The Box Plot used in the "Collecting Data" section was utilized to provide a summary of the distribution of the Polygraph words and to highlight any outliers.

## Modeling Data 

For Modeling the Data I utilized several r packages:

-   ggplot2
-   dplyr
-   tidyverse
-   knitr
-   tidytext
-   readr
-   data.table
-   bibtex
-   readxl

# Results 

```{r Mann-Whitney-Wilcoxon Test- Black Characters, echo = FALSE}

BlackWomen <- actors_polygraph %>% filter(Gender_Race == "Black_Women")  
BlackMen <- actors_polygraph %>% filter(Gender_Race == "Black_Men") 

BW_Words <- c(BlackWomen$POLYGRAPH_.WORDS) 
BM_Words <- c(BlackMen$POLYGRAPH_.WORDS) 

length(BW_Words) <- length(BM_Words)

Black_Characters <- data.frame(BW_Words,BM_Words) 

wilcox.test(BW_Words, BM_Words, data=Black_Characters)

```

```{r Mann-Whitney-Wilcoxon Test- East Asian Characters, echo = FALSE}

EastAsian_Women <- actors_polygraph %>% filter(Gender_Race == "East Asian_Women")  
EastAsian_Men <- actors_polygraph %>% filter(Gender_Race == "East Asian_Men") 

EAW_Words <- c(EastAsian_Women$POLYGRAPH_.WORDS) 
EAM_Words <- c(EastAsian_Men$POLYGRAPH_.WORDS) 

length(EAW_Words) <- length(EAM_Words)

EastAsian_Characters <- data.frame(EAW_Words,EAM_Words) 

wilcox.test(EAW_Words, EAM_Words, data=EastAsian_Characters)

```

```{r Mann-Whitney-Wilcoxon Test- Indigenous Characters, echo = FALSE}

IndigenousWomen <- actors_polygraph %>% filter(Gender_Race == "Indigenous_Women")

IndigenousMen <- actors_polygraph %>% filter(Gender_Race == "Indigenous_Men") 

IW_Words <- c(IndigenousWomen$POLYGRAPH_.WORDS) 
IM_Words <- c(IndigenousMen$POLYGRAPH_.WORDS) 

length(IW_Words) <- length(IM_Words)

Indigenous_Characters <- data.frame(IW_Words,IM_Words) 

wilcox.test(IW_Words, IM_Words, data = Indigenous_Characters)

```

```{r Mann-Whitney-Wilcoxon Test- Latinx Characters, echo = FALSE}

LatinxWomen <- actors_polygraph %>% filter(Gender_Race == "Latinx_Women")  
LatinxMen <- actors_polygraph %>% filter(Gender_Race == "Latinx_Men") 

LW_Words <- c(LatinxWomen$POLYGRAPH_.WORDS) 
LM_Words <- c(LatinxMen$POLYGRAPH_.WORDS) 

length(LW_Words) <- length(LM_Words)

Latinx_Characters <- data.frame(LW_Words,LM_Words) 

wilcox.test(LW_Words, LM_Words, data=Latinx_Characters)

```

```{r Mann-Whitney-Wilcoxon Test- South Asian Characters, echo = FALSE}

SouthAsian_Women <- actors_polygraph %>% filter(Gender_Race == "South Asian_Women")  
SouthAsian_Men <- actors_polygraph %>% filter(Gender_Race == "South Asian_Men") 

SAW_Words <- c(SouthAsian_Women$POLYGRAPH_.WORDS) 
SAM_Words <- c(SouthAsian_Men$POLYGRAPH_.WORDS) 

length(SAW_Words) <- length(SAM_Words)

SouthAsian_Characters <- data.frame(SAW_Words,SAM_Words) 

wilcox.test(SAW_Words, SAM_Words, data=SouthAsian_Characters, exact = FALSE)

``` 

```{r Mann-Whitney-Wilcoxon Test- White Characters, echo = FALSE}

White_Women <- actors_polygraph %>% filter(Gender_Race == "White_Women")  
White_Men <- actors_polygraph %>% filter(Gender_Race == "White_Men") 

WW_Words <- c(White_Women$POLYGRAPH_.WORDS) 
WM_Words <- c(White_Men$POLYGRAPH_.WORDS) 

length(WW_Words) <- length(WM_Words)

White_Characters <- data.frame(WW_Words,WM_Words) 

wilcox.test(WW_Words, WM_Words, data = White_Characters)

# Mann-Whitney-Wilcoxon Test- White Characters

``` 


```{r Table of U Test Statistic, echo = FALSE}

library(readxl)
Utest <- read_excel("Utest.xlsx", col_types = c("text", 
    "numeric", "text"))
View(Utest)

"Table 1.1 p-Value calculated for Race+Gender using the Mann-Whitney U Test"

kable(Utest)


```

  With this table we can observe that we failed to reject the null hypothesis in all cases except for the comparison between Latinx Women and Latinx Men. In the case of Latinx characters, the p-value was less than out set alpha level so we reject the null hypothesis.

# Discussion 

## Limitations  

  There were several limitations to this data analysis: 

### Dataset 

  The data set is a bit outdated as it spans from 1974 - 2014 [@Anderson2016-pd]. Additionally, there were several missing values that could have contributed to the extreme skewness of the data set when separated into segment populations (Race & Gender). Additionally, please note that there was no comparison between Near Eastern Women characters and Near Eastern Men characters because amongst 780 films there was not one observation of a Near Eastern Woman character.  

**Sample Bias**: As this data orginated from **The Pudding** then was transformed by **Racial Lines**, then further transformed by me it is important to note this sample is not fully representative of all Hollywood films. [@DVN/KERZQY_2018]

### Movie Context 

  I mainly stuck to just analyzing the numbers and not making large claims because of how variant movies could be. There is always the chance a character speaks very few words but it is essential if not central to the plot of the movie. Some examples, John Wick:4. Additionally, this paper does not account for the reception of viewers of the films. There is also the possibility that there is a film filled with representation that is negative such as several stereotypes. An example of this is the film *The Birth of a Nation* whose character is regarded as Black, however, the actor was a white man in Black face in the movie is based on stereotypes and regards the Klu Klux Klan in a positive light [@Erigha2015-jb}. 

### Beginner Statistician 

  I think it is only fair to the audience to disclose that I am not a statistician! I have just begun to learn statistics so my analysis may not be as in-depth and analytical as it could be but I hope you got some type of insight.


# Conclusion 

  With new concepts such as The DuVernay Test up and coming it will be interesting to see if speaking parts could possibly increase or decrease positive representation in film for minorities. Additionally, although probably rather very difficult and time consuming, I hope to see more intersectionality analysis when determining representation in film. 
  
# Bibliography 
