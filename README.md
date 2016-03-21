# PRIS
R code to visualize nuclear power reactors constructed till summer 2015

#change the working directory
#Load all relevant packages for this exercise!
setwd("/Users/Fabian/Desktop/Visualization")
library(ggmap)
library(ggplot2)
library(googleVis)
#get the csv file
re <- read.csv("re.csv")
#take a look at the first couple rows of the csv file
head(re)
#create new column with $Latitude and $Logitude columns merged and separated by ":"
re$reac <- paste(round(re$Latitude, 3), round(re$Longitude, 3), sep = ":")
head(re)
#Change order, so reac is in first place:
reac <- re[, c(22, 1:22)]
head(reac)

#parsimonious data, I.E. LESS INFO
reac$Tip <- as.character(paste("ID =", reac$Reactor.Unit, "<BR>", "Type =", reac$Type, "<BR>", "Supplier =", reac$Reactor.Supplier, "<BR>", "Capacity (MW)=", reac$Reference.Unit.Power..MW., "<BR>"))

replot <- gvisMap(reac, locationvar = "reac", tipvar = "Tip", options = list(enableScrollWheel = TRUE, height = 800, mapType = c("terrain", "satellite"), useMapTypeControl = TRUE))
plot(replot)
