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

Total=read.csv("C:/Users/playbox/Desktop/Vulnerabilities/Monthly data Vulnerabilities.csv")
Total$Month=as.Date(Total$Month)
Total <- as.data.frame(Total)

# Overflow
A=ggplot(data =Total,aes(x =Month, y = Overflow, group=1))+
  geom_line(color = "darkblue", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
  theme( axis.text.x = element_text(angle=45,hjust=1))+
  scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
  ggtitle("Overflow ")+
  theme(
  plot.title = element_text(color="black", size=10, face="bold.italic"),
  axis.title.x = element_text(color="black", size=10, face="bold"),
  axis.title.y = element_text(color="black", size=10, face="bold"))
  
# Code Execution
B=ggplot(data =Total,aes(x =Month, y = Code.Execution,group=1))+
  geom_line(color = "darkred", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
  theme( axis.text.x = element_text(angle=45,hjust=1))+
  scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
  ggtitle("Code Execution")+
  theme(
  plot.title = element_text(color="black", size=10, face="bold.italic"),
  axis.title.x = element_text(color="black", size=10, face="bold"),
  axis.title.y = element_text(color="black", size=10, face="bold"))

# Memory Corruption
C=ggplot(data =Total,aes(x =Month, y = Memory.Corruption,group=1))+
  geom_line(color = "green4", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
  theme( axis.text.x = element_text(angle=45,hjust=1))+
  scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
  ggtitle("Memory Corruption")+
  theme(
  plot.title = element_text(color="black", size=10, face="bold.italic"),
  axis.title.x = element_text(color="black", size=10, face="bold"),
  axis.title.y = element_text(color="black", size=10, face="bold"))

# Sql Injection
D=ggplot(data =Total,aes(x =Month, y = Sql.Injection,group=1))+
  geom_line(color = "gold2", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
  theme( axis.text.x = element_text(angle=45,hjust=1))+
  scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
  ggtitle("Sql Injection")+
  theme(
  plot.title = element_text(color="black", size=10, face="bold.italic"),
  axis.title.x = element_text(color="black", size=10, face="bold"),
  axis.title.y = element_text(color="black", size=10, face="bold"))

# DoS
E=ggplot(data =Total,aes(x =Month, y = DoS,group=1))+
  geom_line(color = "mediumorchid4", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
  theme( axis.text.x = element_text(angle=45,hjust=1))+
  scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
  ggtitle("DoS ")+
  theme(
  plot.title = element_text(color="black", size=10, face="bold.italic"),
  axis.title.x = element_text(color="black", size=10, face="bold"),
  axis.title.y = element_text(color="black", size=10, face="bold"))
  
# Gain Privileges 
F=ggplot(data =Total,aes(x =Month, y = Gain.Privileges,group=1))+
  geom_line(color = "orangered", alpha = 0.6, size = 0.6)+ ylab("Number of Vuln.")+xlab("Time")+
  theme( axis.text.x = element_text(angle=45,hjust=1))+
  scale_x_date(labels = date_format("%Y-%m"), breaks='3 years')+
  ggtitle("Gain Privileges")+
  theme(
  plot.title = element_text(color="black", size=10, face="bold.italic"),
  axis.title.x = element_text(color="black", size=10, face="bold"),
  axis.title.y = element_text(color="black", size=10, face="bold"))

plot_grid(A, B, C, D, E, F, labels = c("", "","","","",""), align = "v")

```

Below is presented a visualization of monthly data for most important vulnerabilities using RStudio. 

![](../public/DiffVulnerabilitiesOverMonths.png)
