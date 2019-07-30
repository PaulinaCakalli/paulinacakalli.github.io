---
layout: post
title:  "Modeling and Forecasting Vulnerabilities on Cyber-Security"
date:   2019-07-30
categories: 
---
## Introduction
Vulnerabilities are very well known on Cyber-Security field. As more and more things relay in information technology, the importance of vulnerabilities is growing rapidly. From Nuclear control systems, hydro power plants to your computer devices, every IT systems has been vulnerable at some point in its life cycle. A vulnerability is a weakness which can be exploited by an attacker to perform unauthorized actions in a computer system. In this project, I have studied the most important vulnerabilities which are Overflow, Code Execution, Memory Corruption, Sql Injection, DoS, Gain Information, Gain Privileges, XSS, Directory Traversal, Http Response Splitting, Bypass Something, CSRF and File Inclusion. I have collected the monthly data of each vulnerability from https://www.cvedetails.com/ for the time period January 1999–June 2019. Common Vulnerabilities and Exposures (CVE) system provides information for cybersecurity vulnerabilities such as, CVE ID, a description, a publish date, the level of importance (score), etc. 

```R

library(tidyverse)
library(scales)
library(cowplot)
library(forecast)
library(ggfortify)

Total=read.csv("C:/Users/playbox/Desktop/Vulnerabilities/Monthly data Vulnerabilitiesb - Total.csv")
Total$Month=as.Date(Total$Month)
Total <- as.data.frame(Total)

# Overflow
A=ggplot(data =Total,aes(x =Month, y = Overflow, group=1))+
      geom_line(color = "darkblue", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
      scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
      ggtitle("Overflow ")+
      theme(
        plot.title = element_text(color="black", size=10, face="bold.italic"),
        axis.title.x = element_text(color="black", size=10, face="bold"),
        axis.title.y = element_text(color="black", size=10, face="bold"),
        axis.text.x = element_text(angle=45,hjust=1))
  
# Code Execution
B=ggplot(data =Total,aes(x =Month, y = Code.Execution,group=1))+
    geom_line(color = "darkred", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
    scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
    ggtitle("Code Execution")+
    theme(
      plot.title = element_text(color="black", size=10, face="bold.italic"),
      axis.title.x = element_text(color="black", size=10, face="bold"),
      axis.title.y = element_text(color="black", size=10, face="bold"),
      axis.text.x = element_text(angle=45,hjust=1))

# Memory Corruption
C=ggplot(data =Total,aes(x =Month, y = Memory.Corruption,group=1))+
    geom_line(color = "green4", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
    scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
    ggtitle("Memory Corruption")+
    theme(
      plot.title = element_text(color="black", size=10, face="bold.italic"),
      axis.title.x = element_text(color="black", size=10, face="bold"),
      axis.title.y = element_text(color="black", size=10, face="bold"),
      axis.text.x = element_text(angle=45,hjust=1))

# Sql Injection
D=ggplot(data =Total,aes(x =Month, y = Sql.Injection,group=1))+
    geom_line(color = "gold2", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
    scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
    ggtitle("Sql Injection")+
    theme(
      plot.title = element_text(color="black", size=10, face="bold.italic"),
      axis.title.x = element_text(color="black", size=10, face="bold"),
      axis.title.y = element_text(color="black", size=10, face="bold"),
      axis.text.x = element_text(angle=45,hjust=1))

# DoS
E=ggplot(data =Total,aes(x =Month, y = DoS,group=1))+
    geom_line(color = "mediumorchid4", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
    scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
    ggtitle("DoS ")+
    theme(
      plot.title = element_text(color="black", size=10, face="bold.italic"),
      axis.title.x = element_text(color="black", size=10, face="bold"),
      axis.title.y = element_text(color="black", size=10, face="bold"),
      axis.text.x = element_text(angle=45,hjust=1))
  
# Gain Privileges 
F=ggplot(data =Total,aes(x =Month, y = Gain.Privileges,group=1))+
    geom_line(color = "orangered", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
    scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
    ggtitle("Gain Privileges")+
    theme(
      plot.title = element_text(color="black", size=10, face="bold.italic"),
      axis.title.x = element_text(color="black", size=10, face="bold"),
      axis.title.y = element_text(color="black", size=10, face="bold"),
      axis.text.x = element_text(angle=45,hjust=1))

plot_grid(A, B, C, D, E, F, labels = c("", "","","","",""), align = "v")

```

Below is presented a visualization of monthly data for most important vulnerabilities using RStudio. 

![](../public/DiffVulnerabilitiesOverMonths.png)

Figure 1. Visualization of most important Vulnerabilities

As it can be seen from the graphic results they appear differently, but the meeting point is their non-linear behavior. The number of Overflow vulnerabilities is very low during the time period 1999-2002, then it starts to grow very slowly and during 2018 it increases rapidly with a max value of 654 in June.  The number of Code Execution vulnerabilities is growing slowly from 1999 to 2003, then it increases and in 2005 reaches a max value of 379 in May. After that it starts to decrease until the year 2013 where it start increases again. The number of Memory Corruption vulnerabilities is very low from 1999 to 2005, and then it starts to increase. The max value of 126 is signed in July 2016. The max number of 206 Sql Injection vulnerabilities is in December 2005, there are two high spikes on 2005 and 2009, and also the data behaves with frequently increase-decrease. The max number of 387 DoS vulnerabilities is in July 2017, the number of vulnerabilities is very low at the beginning and then from 2003-2006 it starts to increase-decrease with random fluctuations, after that it increases slowly with a high spike on July 2017 and then it decreases again. The max number of 107 Gain Privileges vulnerabilities is in September 2012, the number of vulnerabilities behaves with random fluctuations.

Based on the visualization, there is no seasonality on the six graphs mentioned above and the data behaves with random fluctuations and high spikes. Since there is a higher interest rate for the total number of all vulnerabilities in Information Security, on the previous step I have transformed the data into the monthly data of total vulnerabilities types.

## Methodology

The data is collected from CVE database, which is used in numerous cybersecurity products and services from around the world including U.S. National Vulnerability Database (NVD). The monthly data of each vulnerability is for the time period January 1999-June 2019. There are 246 observations for every vulnerability types.

In the second step, I have transformed the data into monthly data for all vulnerabilities for the time period January 1999-June 2019.
Then, the data is analyzed for the pattern of trend, seasonality and cyclic. Ggseasonplot and ggmonthplot are used to study the seasonality.

Modeling the data with the time series methods like ARIMA (Auto Regressive Integrated Moving Average), ETS (Error, Trend, Seasonality) and ANN (Artificial Neural Networks). Errors like RMSE (Root Mean Square Error), MAPE (Mean Absolute Percentage Error) and MASE (Mean Absolute Scaled Error) have been taken into consideration to decide which model fitted better the real data.

Forecasting the monthly number of vulnerabilities for the time period July 2019- July 2020 with the best time series method that fitted better the data. 

![](../public/Methodology.png)

Figure 2. The methodology of the project

## Analyzing

```R
ggplot(data =Total,aes(x =Month, y = Total,group=1))+
  geom_line(color = "red", alpha = 0.6, size = 0.72)+ ylab("Number of Vulnerabilities")+xlab("Time")+
  scale_x_date(labels = date_format("%Y-%m"), breaks='2 years')+
  ggtitle("Vulnerabilities Over Months")+
  theme(
    plot.title = element_text(color="black", size=12, face="bold.italic"),
    axis.title.x = element_text(color="black", size=10, face="bold"),
    axis.title.y = element_text(color="black", size=10, face="bold"),
    axis.text.x = element_text(angle=45,hjust=1))
```  
  
Below is given the visualization of monthly data vulnerabilities for the time period 01/1999-06/2019.

![](../public/Real-Data.png)
Figure 3. Visualization of Vulnerabilities over Months 

As it can be seen from the graphic results, in this time series the data behavior is non-linear and there is no clear seasonality. The data appears with frequently random fluctuations. The number of vulnerabilities increases slowly from 01/1999 to 11/2002, and then is a high spike on the end of 2002. From 2003 to 2004 it decreases and then a high spike is clearly seen, then it starts to increase with three high spikes until the 2007. From 2007 to 2012 we can see a decreasing trend of vulnerabilities. From 2012 to 2015 an increasing trend is available, which includes two high spikes. From 2015 to 2017 we can see frequently random fluctuations, and then a rapidly increase during the time period 01/2017-05/2018. During 2019 the data starts to decrease with a low spike on 02/2019 and it starts to increase again during the last 3 months. The highest spike of vulnerabilities over months is reached on 07/2018 with a value of 1665. As is described above the data appears with a lot of increase-decrease where the trend pattern is included, and high spikes.

```R
tsTotal=ts(Total$Total,frequency=12, start=c(1999,1))
A=ggmonthplot(tsTotal,labels = month.abb,year.labels = TRUE,pch=19,ylab="Number of Vulnerabilities", main = "")
B=ggseasonplot(tsTotal, year.labels = TRUE, year.labels.left=TRUE, col=1:40, pch=19, main = "", xlab = "Month", ylab = "Number of Vulnerabilities")

plot_grid(A, B, labels = c("", ""), align = "v")
```

Below is presented the graphic results from ggseasonplot and ggmonthplot commands.

![](../public/ggmonthplot-ggseasonplot.png)

Figure 4. Visualization of the results from ggmonthplot and ggseasonplot

Ggmonthplot gives an average for every month, which is calculated from all the data. As it can be seen from the graphic results there is no seasonality and the highest number of vulnerabilities is reached in December, from the other side the lowest number of vulnerabilities is reached in November.

Ggseasonplot is given to show if there is the presence of seasonality, but as it can be seen there is no seasonality and the number of vulnerabilities is very different from a year to the next. 

## Modeling

I have studied the time series methods like ARIMA (Auto Regressive Integrated Moving Average), ETS (Error, Trend, Seasonality) and ANN (Artificial Neural Networks).

```R
# ARIMA
fitArima=auto.arima(Total$Total)
fitArima1=fitted.values(fitArima)
```
```R
# ANN
fitANN=nnetar(Total$Total)
fitANN1=fitted.values(fitANN)
```
```R
# ETS
fitEts=ets(Total$Total)
fitEts1=fitted.values(fitEts)
```
