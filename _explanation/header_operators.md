---
title: 'Special operators'
layout: 'default'
description: 'Operators for loading resources and other tasks'
---


## Special operators

### 1\. The `#!` operator and `load_*` functions

The `#!` operator signals to the transpiler that the line is a header
line and it requires processing. These lines are considered as comments
by R, but the transpiler will pick them up.

#### 1.1. Use `load_script` to load any JavaScript library or another sketch R file

``` r
#! load_script("https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.0.0/p5.min.js")
#! load_script("other_sketch_R_file.R")
```

`load_script` supports CSS, JS and R files, online or local.

For the R files, additional transpiler options may be included at the
end, e.g. `#! load_script("abc.R", rules = basic_rules())`. See
`?compile_r` for the available options.

The package does not resolve circular referencing, e.g. file A and file
B source each other at the same time. Please avoid that\!

#### 1.2. Use `load_library` for shorthand of `load_script`

Instead of including the full link, simply call the library by name.

``` r
#! load_library("p5")
#! load_library("vegalite")
```

Currently, the following libraries are supported: `mathjs`, `p5`,
`chart`, `plotly`, `d3`, `vegalite` and `tensorflow`. When in doubt, one
can always look into the `src` function to see the full list.

#### 1.3. Use `load_data` to load tabular data (e.g. CSV) / JSON data file

``` r
#! load_data("my_file.json")
```

If the data file is named as `my_file.json`, then it will be available
in the variable `my_file_json`. The data variable is not supposed to be
modified (and is assigned the `const` tag). If one needs to change the
data, please proceed by making a copy.

The package handles CSV and JSON files by default and other file types
by using the `read_fun` option. Basically, any file that can be loaded
into R and converted to JSON is accepted. The use cases in mind are the
family of `read_*` functions provided by the `readr` package. See
`?compile_data` (or `?to_json`) for further detail.

### 2\. `declare()` / `let()`

`declare()` / `let()` are empty R functions that act as a place-holder
to facilitate conversion into JavaScript. If you want to assign a value
to a variable, you may proceed as:

``` r
declare (x)
x <- 3
# alternative
let (x = 3)
```

Note that `declare` and `let` are 100% interchangeable, e.g. `declare (x
= 3)` is valid. I prefer using `declare` for top-level variable
declaration and `let` for local use.

If one uses variables without declaring them, JavaScript will declare it
for you and place them in the global namespace.

### 3\. `%=>%` and `%+%`

`%=>%` maps to the arrow function `=>` in JavaScript.

`%+%` maps to `+` in JavaScript. One may think of `%+%` as the semantic
equivalent of `paste0`. The reason for creating this operator is that
JavaScript supports string addition, which has no equivalent binary
operator in R.

### 4\. `lambda`

The `lambda` function offers a convenient way to define anonymous
function, which works similar to `pryr::f`. For instance, `function(x,
y) { return(x + y) }` can be rewritten as `lambda(x, y, x + y)`.
