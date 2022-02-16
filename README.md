# DS_202_hw4_choco

---
title: "homework_4"
author: "Isabel Wheeler"
date: "2/16/2022"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

```{r}
choco <- read.csv("https://ds202-at-isu.github.io/labs/data/choco.csv")
head(choco)
```

Question Set 1:
1.
```{r}
str(choco)
```
There are 1852 observations, so there are 1852 chocolate bars tested.

2.
```{r}
#Year is Review.Date
choco %>% ggplot(aes(x = as.factor(Review.Date))) + 
  geom_bar() + 
  labs(y = "Count", x = "Year") +
  ggtitle("Ratings vs. Year")
```

Question set 2:
1.
```{r}
ggplot(choco, aes(x = choco$Rating)) +
  geom_histogram() + 
  labs(y = "Count", x = "Rating") +
  ggtitle("Distribution of Ratings")
```
The distribution looks to be skewed slightly to the left and be centered around 3.5. When just looking at the histogram one might say that the rating of 5 is an outlier.

2.
```{r}
ggplot(data = choco, aes(x = Rating, y = factor(Cocoa.Pct))) +
  geom_point() +
  labs(y = "Cocoa Percentage", x = "Rating") +
  ggtitle("Cocoa Percentage vs. Ratings")
```
When looking at this plot there doesn't seem to be a relationship between cocoa percentage and rating, so I would say that rating doesn't depend on cocoa percentage. 

3.
```{r}
top3 <- dplyr::filter(choco, Company.Location %in% c("U.S.A.", "France", "Canada"))

ggplot(data = top3, mapping = aes(x = Company.Location, y = Rating)) + geom_boxplot()
```
When looking at these three box plots it seems that all three countries have about the same median and max when it comes to ratings. France has the smallest range and two outliers in the lower direction. USA has the same minimum as France and those lows are both outliers. Canada has the highest third quartile and USA has the lowest first quartile.

My own question:
How do the ratings differ out of the top three producing countries?
```{r}
company_factor <- as.factor(choco$Company)
head(summary(company_factor), 3)
#Soma, Bonnat, and Fresco have the most

company3 <- dplyr::filter(choco, Company %in% c("Soma", "Bonnat", "Fresco"))

ggplot(data = company3, mapping = aes(x = Company, y = Rating)) + 
  geom_boxplot()
```
