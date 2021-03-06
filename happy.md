 ---
  title: "NBA 2014-2015球季 各隊分析"
  output: html_document
  ---
  
  
```{r echo=T}
  #install.packages("SportsAnalytics")
  library(SportsAnalytics)
  NBA1415<-fetch_NBAPlayerStatistics("14-15")
```
## **各隊最辛苦的球員**
  
  ---各隊上場分鐘數最多的球員---

```{r echo=T}
  MaxPlayed<-aggregate(TotalMinutesPlayed~Team,NBA1415,max)
  #tapply(NBA1415$TotalPoints,NBA1415$Team,max)
  NBA1415MaxPlayed<-merge(NBA1415,MaxPlayed)
  output<-NBA1415MaxPlayed[order(NBA1415MaxPlayed$TotalMinutesPlayed,decreasing = T),c("Team","Name","TotalMinutesPlayed")]
  library(knitr)
  kable(output, digits=2)
```
  
## **各隊得分王**
  
  ---**各隊得分最多的球員**---
  
```{r echo=T}
  MaxPoint<-aggregate(TotalPoints~Team,NBA1415,max)
  
  NBA1415MaxPoint<-merge(NBA1415,MaxPoint)
  output<-NBA1415MaxPoint[order(NBA1415MaxPoint$TotalPoints,decreasing = T),c("Team","Name","TotalPoints")]
  library(knitr)
kable(output, digits=2)
```
 
## **各隊最有效率球員**
 
  ---**各隊總得分/出戰分鐘數 最高的球員**---
  
```{r echo=T}
  EFFMax<-aggregate(TotalPoints/TotalMinutesPlayed~Name,NBA1415,max)
  NBA1415EFFMax<-merge(NBA1415,EFFMax)
  FinalEFFMax<-aggregate(TotalPoints/TotalMinutesPlayed~Team,NBA1415EFFMax,max)
  NBA1415FinalEFFMax<-merge(NBA1415EFFMax,FinalEFFMax)
  output<-NBA1415FinalEFFMax[order(NBA1415FinalEFFMax$`TotalPoints/TotalMinutesPlayed`,decreasing = T),c("Team","Name","TotalPoints/TotalMinutesPlayed")]
  library(knitr)
  kable(output, digits=2)
```
  
  
## **各隊三分球出手最準的球員**
  
---**各隊三分球命中/出手三分球 最高的球員**---
  
```{r echo=T}
  Shoter<-aggregate(ThreesMade/ThreesAttempted~Name,NBA1415,max)
  NBA1415Shoter<-merge(NBA1415,Shoter)
  FinalShoter<-aggregate(ThreesMade/ThreesAttempted~Team,NBA1415Shoter,max)
  NBA1415FinalShoter<-merge(NBA1415Shoter,FinalShoter)
  output<-NBA1415FinalShoter[order(NBA1415FinalShoter$`ThreesMade/ThreesAttempted`,decreasing = T),c("Team","Name","ThreesMade/ThreesAttempted")]
  library(knitr)
  kable(output, digits=2)
```