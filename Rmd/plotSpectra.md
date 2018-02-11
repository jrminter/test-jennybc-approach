---
title: "Plot MSA Spectra"
author: "John Minter"
date: "Created: 2018-02-01 Last Modified: 2018-02-11"
output:
  html_document:
    keep_md: true
    variant: github_md
---



## Load a spectrum

First we get our exemplar **.msa** format spectrum file. I had included
the file in the `rEDS` package. We will suppress the messages where R
has loaded the required packages by using the optional `quietly` 
variable.


```r
library(rEDS, quietly=TRUE)
fi <- system.file("extdata", "Benitoite.msa", package = "rEDS")
print(fi)
#> [1] "/Library/Frameworks/R.framework/Versions/3.4/Resources/library/rEDS/extdata/Benitoite.msa"
```

Next, we create a Spectrum object using the `SingleMSA` function.
You can get the help page by typing `??rEDS::singleMSA` into the
R console.


```r
spc <- singleMSA(fi, probecur=2.5)
```

and now we can plot the spectrum.


```r
plot(spc, maxEnergy=10000, doLog=TRUE)
```

![](plotSpectra_files/figure-html/unnamed-chunk-3-1.png)<!-- -->

We can also create a ggplot with a linear intensity scale. You can
get the help page by typing `??rEDS::ggplotSpectrumLinY` into the 
R console.


```r
plt <- ggplotSpectrumLinY(fi, "Benitoite", 0.2, 7.0, 1.0, 2.5)
print(plt)
```

![](plotSpectra_files/figure-html/unnamed-chunk-4-1.png)<!-- -->

next we will make a plot with a logarithmic intensity


```r
plt <-ggplotSpectrumLogY(fi, "Benitoite", 0.2, 7.0, 1.0, 2.5)
print(plt)
```

![](plotSpectra_files/figure-html/unnamed-chunk-5-1.png)<!-- -->
