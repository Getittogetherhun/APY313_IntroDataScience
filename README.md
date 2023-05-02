title: "Intersectionality and Dialogue"
author: "Kesia Otieno"

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

  The data set is from Harvard's [**Racial lines**](file:///C:/Users/kesia/Downloads/Racial_Lines_2018%20(2).pdf) data set. The [**Racial lines**](file:///C:/Users/kesia/Downloads/Racial_Lines_2018%20(2).pdf) data set originates from a previous data set of screenplays with 780 films on gender and dialogue conducted by Hannah Anderson and Matt Daniel at the Pudding [@Anderson2016-pd]. The [**Racial lines**](file:///C:/Users/kesia/Downloads/Racial_Lines_2018%20(2).pdf) data set took the data set from The Pudding and incorporated the variable of Race [@DVN/KERZQY_2018]. As Noted in the section below I removed several variables that were not necessary for the data analysis I was conducting.I then used the wilcox.test() function to generate test statistics to use in my analysis

## Purpose For Plots & Test   

### Mann Whitney U Test 

  I used the Shapiro-Wilk Test and generated a histogram for each unique Race+Gender category I intended to use. Both methods illustrated that my individualized data sets did not have a normal distribution. Due to my data nor having a normal distribution I sought out a Non-Parametric Analysis to compare outcomes between two independent variables. I opted for a non-directional or two-tailed U-test as the possible directionality was not something I wanted to be specified.  


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

Anderson, Hanah, and Matt Daniels. 2016. Film Dialogue: The Largest Ever Analysis of Film Dialogue. The Pudding.
Erigha, Maryann. 2015. “Race, Gender, Hollywood: Representation in Cultural Production and Digital Media’s Potential for Change.” Sociol. Compass 9 (1): 78–89.
Gray, J R A T. 2016. Diversity in Hollywood: Failure of Inclusion Plagues the Entire Industry. Variety Magazine. New York City: Variety. Web.
Massie, Victoria M. 2016. “Want to Measure a Film’s Diversity? Try "the Duvernay Test.".” Vox. Vox. https://www.vox.com/2016/2/1/10888212/duvernay-test-movie-diversity.
Ross, Shawna. n.d. “A Bechdel Test for# MLA16.”
Smith, Stacy L, Marc Choueti, and Katherine Pieper. 2007. Inequality in 900 Popular Films: Examining Portrayals of Gender, Race/Ethnicity, LGBT, and Disability from 2007-2016.
Sutherland, Jean-Anne, and Kathryn M Feltey. 2017. “Here’s Looking at Her: An Intersectional Analysis of Women, Power and Feminism in Film.” Journal of Gender Studies 26 (6): 618–31.
Svaikovsky, Victoria, Anne Meisner, Eve Kraicer, and Matthew Sims. 2018. “Racial Lines.” Harvard Dataverse. https://doi.org/10.7910/DVN/KERZQY.
