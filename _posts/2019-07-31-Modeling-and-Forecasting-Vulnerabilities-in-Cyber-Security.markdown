---
layout: post
title:  "Modeling and Forecasting Vulnerabilities in Cyber-Security"
date:   2019-07-31
categories: 
---
## Introduction
As more and more things relay in information technology, the importance of vulnerabilities is growing rapidly. From Nuclear control systems, hydro power plants to your computer devices, every IT systems has been vulnerable at some point in its life cycle. A vulnerability is a weakness which can be exploited by an attacker to perform unauthorized actions in a computer system. In this project, I have studied some of the most important vulnerabilities.

I have collected the yearly and monthly data of each vulnerability from https://www.cvedetails.com/ starting from January 1999 to June 2019. 
Below is a representation of the yearly data.

```R
library(tidyverse)
library(scales)
library(cowplot)
library(forecast)
library(ggfortify)

Vuln=read.csv("C:/Users/paulina/Desktop/Vulnerabilities/Vulnerabilities Over Years.csv")

ggplot(data = Vuln, aes(x = Year), as.numeric = TRUE) +
  geom_line(aes(y = Vuln$DoS,colour = "Vuln$DoS"),size=1)+
  geom_line(aes(y = Vuln$Code.Execution,colour="Vuln$Code.Execution"),size=1)+
  geom_line(aes(y = Vuln$Overflow, colour="Vuln$Overflow"),size=1)+
  geom_line(aes(y = Vuln$Memory.Corruption, colour="Vuln$Memory.Corruption"),size=1)+
  geom_line(aes(y = Vuln$Sql.Injection, colour="Vuln$Sql.Injection"),size=1)+
  geom_line(aes(y = Vuln$XSS, colour="Vuln$XSS"),size=1)+
  geom_line(aes(y = Vuln$Directory.Traversal, colour="Vuln$Directory.Traversal"),size=1)+
  geom_line(aes(y = Vuln$Http.Response.Splitting, colour="Vuln$Http.Response.Splitting"),size=1)+
  geom_line(aes(y = Vuln$Bypass.something, colour="Vuln$Bypass.something"),size=1)+
  geom_line(aes(y = Vuln$Gain.Privileges, colour="Vuln$Gain.Privileges"),size=1)+
  geom_line(aes(y = Vuln$CSRF, colour="Vuln$CSRF"),size=1)+
  geom_line(aes(y = Vuln$File.Inclusion, colour="Vuln$File.Inclusion"),size=1)+
  ggtitle("Vulnerabilities Over Years")+ 
  scale_colour_manual("",   values=c("red","blue","orange","black","purple","yellow","green","brown","blue4","chartreuse4","darkmagenta","mediumvioletred","mediumorchid2"), 
breaks = c("Vuln$DoS", "Vuln$Code.Execution","Vuln$Overflow","Vuln$Memory.Corruption","Vuln$Sql.Injection","Vuln$XSS","Vuln$Directory.Traversal","Vuln$Http.Response.Splitting","Vuln$Bypass.something","Vuln$Gain.Information","Vuln$Gain.Privileges","Vuln$CSRF","Vuln$File.Inclusion"),
labels = c("DoS", "Code Execution", "Overflow","Memory Corruption","Sql Injection","XSS","Directory Traversal","Http Response Splitting", "Bypass something", "Gain Information","Gain Privileges","CSRF","File Inclusion"))+
 ylab("Number of Vulnerabilities")+
 theme(
    plot.title = element_text(color="black", size=14, face="bold.italic"),
    axis.title.x = element_text(color="black", size=14, face="bold"),
    axis.title.y = element_text(color="black", size=14, face="bold"))
```

![](../public/Vulnerabilities-Over-Years.png)

Figure 1. Visualization of Vulnerabilities over Years

In order to have a better forecast, the monthly data is used. This is because we don't have enough data if the study is conducted on an yearly basis.

```R

Total=read.csv("C:/Users/paulina/Desktop/Vulnerabilities/Monthly data Vulnerabilitiesb - Total.csv")
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

Below is the visualization of monthly data for some of the most important vulnerabilities. 

![](../public/DiffVulnerabilitiesOverMonths.png)

Figure 2. Visualization for some of the most important Vulnerabilities

As it can be seen from the graphical representation, the only similarity they have is their non-linear nature.


The number of Overflow vulnerabilities is very low between 1999-2002, then it starts to grow slowly and during 2018 it increases rapidly with a maximum value of 654 in June 2018. 


The number of Code Execution vulnerabilities is growing slowly from 1999 to 2003, then it increases reaching the maximum value of 379 on May 2005. After that it starts to decrease until 2013 then it starts to increase again. 


The number of Memory Corruption vulnerabilities is very low from 1999 to 2005, and then it starts to increase. It reachs the maximum value of 126 in July 2016. 


The maximum number of Sql Injection vulnerabilities is in December 2005, reaching 206. The data is frequently increasing-decreasing with two notable spikes on 2005 and 2009. 


At the start of data, the number of DoS vulnerabilities is low and we can observe an increase-decrase with random fluctuations. The number of vulnerabilities increases slowly reaching its highest point of 387 on July 2017 to start decreasing again.



The maximum number of Gain Privileges vulnerabilities is reached in September 2012 with a value of 107.


Based on the visualization, there is no seasonality on the six graphs mentioned above and the data behaves with random fluctuations and high spikes. 

## Methodology

The data is collected from CVE database, which is used in numerous cybersecurity products and services from around the world including U.S. National Vulnerability Database (NVD). Common Vulnerabilities and Exposures (CVE) website provides essential information for cybersecurity vulnerabilities such as, CVE ID, a description, a publish date, the level of importance (score), etc.
The monthly data of each vulnerability is from January 1999 to June 2019. There are 246 observations for every vulnerability type.

Transforming the data into monthly data for all the vulnerabilities from January 1999 to June 2019.
Furthermore, the data is analyzed to identify the trend, seasonality and cyclical components. Ggseasonplot and ggmonthplot are used to study the seasonality.

Modeling the data with methods like ARIMA (Auto Regressive Integrated Moving Average), ETS (Error, Trend, Seasonality) and ANN (Artificial Neural Networks). Errors like RMSE (Root Mean Square Error), MAPE (Mean Absolute Percentage Error) and MASE (Mean Absolute Scaled Error) have been taken into consideration to decide which model fitted better the real data.

Forecasting the monthly number of vulnerabilities from July 2019 to July 2020 with the method that better fitted the data. 

![](../public/Methodology.png)

Figure 3. The methodology of the project

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

In the image below, I visualized the monthly data for *all* the vulnerabilities from January 1999 to June 2019.

![](../public/Real-Data.png)

Figure 4. Visualization of Vulnerabilities over Months 

As it can be seen from the graphic results, in this time series the data nature is non-linear and there is no clear seasonality. The data appears with frequent random fluctuations. The number of vulnerabilities increases slowly from January 1999 to November 2002, and then it reaches a high spike in the end of 2002. From 2003 to 2004 it decreases and then it starts to increase with four high spikes until the 2007. From 2007 to 2012 we can see a decreasing trend of vulnerabilities. From 2012 to 2015 an increasing trend is observed, which includes two high spikes. From 2015 to 2017 we can see frequent random fluctuations, and then a high increase from January 2017 to May 2018. During 2019 the data starts to decrease hitting the lowest point for this year on February 2019. After that it starts to increase again during the last 3 months. The highest spike of vulnerabilities over months is reached on July 2018 with a value of 1665. 
We can observe a trend pattern on the increase and decrease of the number of vulnerabilities.

```R
tsTotal=ts(Total$Total,frequency=12, start=c(1999,1))
A=ggmonthplot(tsTotal,labels = month.abb,year.labels = TRUE,pch=19,ylab="Number of Vulnerabilities", main = "")
B=ggseasonplot(tsTotal, year.labels = TRUE, year.labels.left=TRUE, col=1:40, pch=19, main = "", xlab = "Month", ylab = "Number of Vulnerabilities")

plot_grid(A, B, labels = c("", ""), align = "v")
```

Below is the representation of the graphic results from ggseasonplot and ggmonthplot commands.

![](../public/ggmonthplot-ggseasonplot.png)

Figure 5. Visualization of the results from ggmonthplot and ggseasonplot

Ggmonthplot gives an average for every month, which is calculated from all the data. As it can be seen from the graphic results there is no seasonality and the highest number of vulnerabilities is reached in December, on the other side the lowest number of vulnerabilities is reached in November.

Ggseasonplot is used to show if there is the presence of seasonality. As it can be seen from the graphic representation, there is no seasonality and the number of vulnerabilities is very different from month to month. 

## Modeling

For this research, I studied the following time series methods: ARIMA (Auto Regressive Integrated Moving Average), ETS (Error, Trend, Seasonality) and ANN (Artificial Neural Networks).

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

The methods accuracy can be found below: 

```R
accuracy(fitArima)
                         ME     RMSE      MAE       MPE     MAPE      MASE         ACF1
      Training set 14.31946 212.7547 134.6948 -55.23432 77.65099 0.8578841 -0.00767389
```
```R
accuracy(fitANN)
                         ME     RMSE      MAE       MPE     MAPE      MASE        ACF1
      Training set -0.5757532 60.63429 42.95738 -64.44907 72.47471 0.2735997 0.00802777
```
```R
accuracy(fitEts)
                         ME     RMSE      MAE       MPE     MAPE      MASE       ACF1
      Training set 12.48149 214.8705 137.3688 -61.16628 83.69934 0.8749153 0.09734004
```

In this case the ANN model seems to be the most accurate model based on the test set RMSE, MAPE and MASE. The ANN model describes the non-linear nature of the data. 

```R
ggplot(data =Total,aes(x =Month))+
  geom_line(aes(y = Total,colour="Total"),alpha = 0.6, size = 0.72)+
  ylab("Number of Vulnerabilities")+xlab("Time")+
  geom_line(aes( y =  fitANN1,colour="fitANN1"), alpha = 0.6, size = 0.71)+
  ggtitle("Monthly Data of Vulnerabilities")+
  scale_x_date(labels = date_format("%Y-%m"), breaks='2 years')+
  scale_colour_manual("",
                      values=c("green","red"),
                      breaks = c("Total", "fitANN1"),
                      labels = c("Actual","Fitted ANN"))+
  theme(
    plot.title = element_text(color="black", size=12, face="bold.italic"),
    axis.title.x = element_text(color="black", size=10, face="bold"),
    axis.title.y = element_text(color="black", size=10, face="bold"),
    axis.text.x = element_text(angle=45,hjust=1))
```

![](../public/Fitted-Data.png)

Figure 6. Modeling the data with Artificial Neural Network (ANN)

Furthermore, as it can be seen from the graphic results the ANN fitted values are very close to the real data.

## Forecasting

Below are the forecasted values by the ANN model.

```R
f=forecast(fitANN,PI=TRUE,h=12)
f

 Point     Forecast   Lo 80     Hi 80    Lo 95     Hi 95
 247      1005.3793  928.0545 1082.7499 892.3804 1120.8312
 248       622.4810  550.6418  700.1276 507.7912  737.9177
 249       929.4657  848.4299 1008.0296 801.8744 1058.9968
 250      1027.2923  936.6664 1114.0036 894.7663 1180.8927
 251       741.8067  658.8352  851.3139 597.2214  910.0960
 252       893.0108  798.0413  968.7338 739.0178 1017.7492
 253       926.8484  823.9185 1009.8188 751.1406 1067.7841
 254       830.6525  686.2151  899.5199 629.0635  966.6916
 255       819.9568  717.8193  934.2144 673.5693  993.3874
 256      1296.7013 1093.0964 1388.1513 990.7073 1437.5853
 257       976.9696  758.7563 1059.7435 639.8099 1136.3516
 258       955.3288  801.0520 1085.3273 675.8726 1151.8166
 
autoplot(f,ylab="",ts.colour = 'red',facets = FALSE, conf.int = TRUE)
```
![](../public/Forecastes.png)

Figure 7. Visualization for predicted number of vulnerabilities at the time period 07/2019-07/2020

From the forecast graphic we can see that the forecasted data is in harmony with the previous data.
Doing a comparison on the number of real vulnerabilities and the forecasted number for July 2019, the difference between the values is small. Additionally, if a confidence interval of 95% is used, the real value of 1088 is included in the confidence interval.

:octocat: 
