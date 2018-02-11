# Example analyses 

At the 2017 RStudio Conference, Jenny Bryan cited the advantage of
keeping the markdown files knit from .Rmd files and uploading them
to the repository **instead of** .html files. By choosing the
`github_md` variant of markdown, Jenny claimed the rendering was
more helpful for those who visit the repository. Here I test that
idea. I set this up with two of the vignettes from my `rEDS`
package. **I think Jenny is correct!**

## An example YAML block:

I ended up using a YAML block as shown below:

```
---
title: "Plot Penepma Spectra"
author: "John Minter"
date: "Created: 2018-02-01 Last Modified: 2018-02-13"
output:
  html_document:
    keep_md: true
    variant: github_md
---

```

## Links to example analyses 

[Plotting EDS spectra](Rmd/plotSpectra.md)

[Plotting PENEPMA spectra](Rmd/plotPenepma.md)

