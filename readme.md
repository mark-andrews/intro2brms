# Software

Setting up your computer to use the `brms` R package is more work than normally required when using a new R package.
This is because `brms` relies on the external [Stan](https://mc-stan.org/) program, which in turns requires a C++ compiler and related tools.

The following guide is for Windows and Mac users.
If you are a Linux user, everything works on Linux too, but I won't provide instructions.


## Windows and Macs: Install latest version R and RStudio desktop

For both Macs and Windows, install the latest version of both R and RStudio Desktop.
Note that you must use RStudio Desktop. **RStudio Cloud will not work**.

As of early July 2023, the latest version of R is `4.3.1`, and the latest version of RStudio is `2023.06.0+421`.

You can find the installers for the latest version of R at https://cran.ma.imperial.ac.uk/ or https://www.stats.bris.ac.uk/R/ or at [any of these other mirrors](https://cran.r-project.org/mirrors.html).

## Windows only:  Install `Rtools43`

Rtools is for Windows only. It provides a C++ compiler and related tools. This toolchain is mostly used for compiling R packages from source code, which we will use below, but it is necessary for use with `brms`.

Go to https://cran.r-project.org/bin/windows/Rtools/rtools43/rtools.html and get the `Rtools43 installer`.

This is not a normal R package. The installer provides a normal Windows installer and this installs a new program on Windows, which is external to R and RStudio, named `rtools43`. Run the installer like you would run an Windows program installer, accepting the default options. This will take a few minutes to install and it installs a few gigabytes of code.

## Install RStan 2.26, compiling it from source

RStan is an R package. The version on CRAN is 2.21. That won't work. You must install 2.26, and compiling it from source, as follows:

```r
install.packages(c("rstan", "StanHeaders"), 
                 repos = c("https://mc-stan.org/r-packages/", getOption("repos")),
                 type = 'source')
```

To compile an R package from source on Windows, you need Rtools, but you will have that if you followed the previous step.

If you are using a Mac and encounter problems at this stage, you probably need to install Xcode Command Line tools, see e.g. https://www.makeuseof.com/install-xcode-command-line-tools/

The time taken to compile and install these R packages will be a lot longer than normally required to install R packages, but it should be 10 minutes or less depending on the power of your device.


## Install `tidyverse` and `brms`

Install both these packages as normal. If you get a pop-up asking *Do you want to install from sources the packages which need compilation?*, in this case, you can say *Yes* or *No*. It won't make a difference either way. But if you do say yes, it will take a bit longer.
```r
install.packages(c("tidyverse", "brms"))
```

## Test it

If the following works, then everything works. When you run the `brm` command, it should immediately state `Compiling Stan program...` and then after about one minute, you should get output saying something like `Chain 1: Iteration: 1 / 2000 ...`:

```r
library(tidyverse)
library(brms)

data_df <- tibble(x = rnorm(10))

M <- brm(x ~ 1, data = data_df)
```

## A possible fallback

[![Binder](https://notebooks.gesis.org/binder/badge_logo.svg)](https://notebooks.gesis.org/binder/v2/gh/mark-andrews/intro_bda_qub/HEAD?urlpath=rstudio)
