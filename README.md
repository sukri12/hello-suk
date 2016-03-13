# hello-suk
Spatial Autoregression model
setwd("C://R/SARIMA_example") # 

require(astsa) # 
require(tseries)

x <- read.csv("tights.csv", header = FALSE, sep=";") # 
y <- ts(x, start=c(2012, 1), end=c(2014, 4), frequency=12) # 

adf.test(y, k=6)

plot(y)

acf2(y, 26)

forc <- sarima.for(y,12,2,1,2,0,1,1,12)

library(zoo)
m <- merge(as.zoo(y),as.zoo(forc$pred), suffixes = c("fact", ""))
write.zoo(m, file = "forc.csv", index.name = "Index", row.names = FALSE, col.names = NULL, sep = ";")

model <- sarima(y,2,1,2,0,1,1,12)
