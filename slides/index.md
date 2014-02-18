---
title       : Reliability and Reproducibility in R and Dependency Versioning
subtitle    : DLL Hell in R
author      : Jeroen Ooms
job         : UCLA
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
---

<!-- 
library(slidify)
library(slidifyLibraries)
-->

## CRAN packages

![total count](totalcount.png)

> - Who uses R packages?
> - Who has created R packages?
> - Exponential growth
> - 5000 pkgs on CRAN as of Nov 2013
> - More on BioConductor, Github, etc.

---

## What is a dependency?

```no-highlight
Package: dplyr
Type: Package
Title: dplyr: a grammar of data manipulation
Version: 0.1.1
Author: Hadley Wickham <h.wickham@gmail.com>, Romain Francois <romain@r-enthusiasts.com>
Maintainer: Hadley Wickham <h.wickham@gmail.com>
Description: A fast, consistent tool for working with data frame like objects, both in
  memory and out of memory.
URL: https://github.com/hadley/dplyr
Depends: R (>= 3.0.2)
Imports: assertthat, utils, methods, Rcpp
Suggests: hflights, RSQLite, RSQLite.extfuns, RMySQL, RPostgreSQL, data.table, 
  bigrquery, testthat, Lahman, knitr, microbenchmark, ggplot2, mgcv
```

---

## Depencency Types:

> - Dependencies between packages: `Depends`, `Imports`, `Suggests`, `Enhances`, `LinkingTo`.
> - R, Sweave, knitr script depends on package: `library(ggplot2)`
> - System/application embedded R functionality.

## Dependency Relations

> - Depends
> - Reverse Depends
> - Dependency Network (directed graph)
> - Indirect Dependencies (transitivity)

---

## Reverse Dependency Count

![reverse count](reversecount.png)

> - Some popular packages on CRAN
> - 370 packages depend on MASS (Aug 2012)
> - Counting recursive dependencies yields a different list (what would be on top?)

---

## Depenency Conflicts

> - DLL Hell (&reg; Microsoft)
> - R is in the same phase as Windows 98
> - All dependency relationships are unversioned
> - This assumes package versions are interchangable.
> - They are not.
> - Result: everything constantly breaks due to changes in dependencies.

---

## CRAN Policy

<q> For a package update, please check that any packages depending on this one still pass R CMD check: it is especially expected that you will have checked your own packages. A listing of the reverse dependencies of the current version can be found on the CRAN web page for the package.</q>

---

## Policy Implications

> - Package author responsible
> - Basically forbids any breaking changes / refactoring / cleanup
> - Result: popular packages get stuck
> - Does not solve the actual problem
