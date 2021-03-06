---
title: "Plot Penepma Spectra"
author: "John Minter"
date: "Created: 2018-02-01 Last Modified: 2018-02-13"
output:
  html_document:
    keep_md: true
    variant: github_md
---



Our objective is to convert an output spectrum from a Monte Carlo
simulation using PENEPMA into a R dataframe for analysis and other
processing.


## Load a spectrum

First we load the libraries we will need ans get our exemplar file.


```r
library(rEDS)
library(pander)
library(ggplot2)
spcPath <- system.file("extdata", "pe-spect-01.dat", package = "rEDS")
spcPath
#> [1] "/Library/Frameworks/R.framework/Versions/3.4/Resources/library/rEDS/extdata/pe-spect-01.dat"
```

Then want to create an R dataframe using the `penepmaSpcToDF` function.
To see the help page for the function, type this in the R console:

```
??rEDS::penepmaSpcToDF
```

Now we create the dataframe. Let's also print out the column names of
the dataframe.


```r
df <- penepmaSpcToDF(spcPath)
rownames(df) <- c()
print(names(df))
#> [1] "keV" "pd"  "unc"
```


Now we are ready to plot the spectrum. There is a very large dynamic
range for both the **probability density** and the **uncertainty**.
Penepma sets a lower limit for data at **1.0e-35**. Missing values are
set to zero. We want to remove values from the dataframe that are
below a useful limit. We do this below and plot a copy of the 
dataframe that is limited to the useful values.


```r
plt <- ggplot(df, aes(x = keV, y = pd)) +
       geom_line() + 
       scale_x_continuous(breaks = seq(from = 0, to = 15, by = 1),
                          limits = c(0,15)) +
       scale_y_log10(limits = c(1.0,1.0e+6)) +
       xlab(label="X-ray energy [keV]") +
       ylab(label="probability density") +
       # (1/(eV*sr*electron)") +
       ggtitle('PENEPMA simulation of Corning EagleXG glass at 15 kV') +
       theme(axis.text=element_text(size=12),
             axis.title=element_text(size=12),
             # center the title
             plot.title = element_text(hjust = 0.5))
       
print(plt)
```

![](plotPenepma_files/figure-html/unnamed-chunk-3-1.png)<!-- -->
