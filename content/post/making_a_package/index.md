---
title: "Making an R package"
author: "Pierrette Lo"
date: 2020-09-08
categories: ["R"]
tags: ["devtools", "usethis", "packages"]
summary: Quick-start guide to building an R package
---
 
## Overview

This is my quick-start guide to creating a package. See "References" section below for more/better information.

This package is in a private repo on my work org, so I can't share the actual package. It is called {BeatAMLTools}, and the two functions in it are `get_data()` and `clean_headers()`.

### Create package

Make sure {devtools} is installed and loaded.

Create package template in RStudio using `New Project > New Directory > R Package`

This will create the `DESCRIPTION` and `NAMESPACE` files and `R` and `man` folders

### Add content

Write the function and save it as an R script in the `R` folder (can overwrite `hello.R` file that is created as part of the package template).

With cursor inside function, do `Ctrl+Shift+Alt+R` to insert a roxygen skeleton. 

Fill in title, description, params, return, examples.

### Documentation

Go to `DESCRIPTION` and fill in overall package info (don't insert "_PACKAGE" as instructed in another tutorial).

Include license = GPL-3 (I think, since this uses code from packages that are GPL-2? See https://kbroman.org/pkg_primer/pages/licenses.html).

Update documentation (add `function.Rd` file to `man` folder) by typing `document()` in console.

Preview documentation using `help("function_name")`.

### Dependencies

Functions from other packages should be called as `package::function()` in the R script - don't use `library()`. 

Add dependencies to `DESCRIPTION`. You should almost always use `type = "Imports"`. However, with RMariaDB as an "Import", my `get_data()` function would not work in other scripts without loading `library(RMariaDB)`. When I changed it to "Depends:" in `DESCRIPTION`, it then loaded RMariaDB without needing `library()`. I had to edit `DESCRIPTION` manually; `type = "Depends"` just gave a warning without actually doing it.

Dependencies can be added to `DESCRIPTION` by typing manually, or use command `use_package("package")`.

### Build & check package

Use `build()` in console to build package.

Then go to Build menu > Install and Restart.

Package should work!

`?function` should bring up the documentation.

Check package using Build > Check Package.

Then upload `R`, `man`, `DESCRIPTION`, and `NAMESPACE` to GitHub.

README should include installation instructions:

>Installation:
>
>Because this is a private repo, you will first need to generate a GitHub personal access token [here](https://github.com/settings/tokens).
>
>You can then install the package using `devtools::install_github("ohsu-heme/BeatAMLTools", auth_token = " ")`.


When using the package, be sure to include `library(BeatAMLTools)` instead of just `BeatAMLTools::` to be sure the latest build is loaded. 

### Adding a function to an already-built package

1. Update `DESCRIPTION` version and other info if needed
2. Add new script to `R` folder for new function (e.g. `clean_headers.R`)
3. In console, run `document()` and then `help("function_name")` to check
4. Update "depends" manually in `DESCRIPTION`, or use `use_package("package")` to add
5. Build, Install/Restart, and Check package
6. Push changed files to GitHub

### REFERENCES

* https://hilaryparker.com/2014/04/29/writing-an-r-package-from-scratch/
* http://tinyheero.github.io/jekyll/update/2015/07/26/making-your-first-R-package.html
* https://github.com/jstaf/r-package-devel
* https://kbroman.org/pkg_primer/
* http://r-pkgs.had.co.nz/
