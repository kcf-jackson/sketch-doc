---
title: Features
---

## Load JavaScript libraries

### Load a JavaScript source

Load any JavaScript resource using the `#!` operator and the
`load_script` function. It supports both online and local resources.

#### A full example

    #! load_script("https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.0.0/p5.min.js")

    cp <- c("#184A45FF", "#B0B8B4FF")  # color palette

    setup <- function() {
        createCanvas(450, 450)         # width x height 
    }

    draw <- function() {
        background(color(cp[0]))       # Index starts with 0 in JavaScript
        declare (s, d, offset)         # Declare local variables before use
        
        # Set up variables to draw dots
        s <- 0:8                  
        d <- 40 / sqrt(s + 1)          # Diameter
        offset <- cumsum(c(0, d[0:7])) + d / 2
        for (i in s) {            
            angle <- 2 * pi * frameCount / 360 * (i + 1)   # `frameCount` is provided by p5.js
            x <- 225 + offset[i] * cos(angle)
            y <- 225 + offset[i] * sin(angle)
            
            fill(color(cp[1]))         # Fill colors
            stroke(color(cp[1]))       # Border colors
            circle(x, y, d[i])         # Draw the dot on screen
        }
    }

<!--html_preserve-->
<iframe height="500px" src="sketch_temp/sketch_1.html" style="border: none; display: block;" width="500px">
</iframe>
<!--/html_preserve-->

### Load a JavaScript library

For convenience, a selection of libraries can be loaded by the names
directly rather than by links. At the time of writing, it supports
`mathjs`, `p5.js`, `chart.js`, `plotly.js`, `d3.js`, `vegalite.js` and
`tensorflow.js`. Simply use `load_library` in place of `load_script`,
e.g. use `#! load_library("p5")` for the first line above.

Manipulate the DOM
------------------

### Using the browser API directly

The browser object `document` is available for use. One may think of it
as a library and call it using `::` operator.

    textbox <- document::createElement("div")
    textbox$innerText <- "Hello World"

    body <- document::querySelector("body")
    body$appendChild(textbox)

### Using the `dom` module

The `dom` module provides a few functions for the most used
functionalities.

    #! load_library("dom")
    textbox <- dom("div", list(innerText = "Hello World"))
    print_dom(textbox, "body")

R-like data structure
---------------------

### R list

    # constructor
    data0 <- list(x = 1:3, y = list(z = 4:6))
    length(data0)

    # extract and extract2
    data0[0]
    data0['x']
    data0[0:1]
    data0[c('x', 'y')]

    data0[[0]]
    data0[['x']]
    data0[[c('y', 'z')]]


    # extractAssign
    data0 <- list(x = 1:3, y = 4, z = 5)
    length(data0)

    data0[0] <- 999
    data0['y'] <- 999
    data0['z'] <- list(z = 999)
    data0['a'] <- list(z = c(9, 9, 9))
    data0[0:1] <- c(99, -99)
    data0[2:3] <- 999
    data0[c('x', 'y')] <- list(z = 999)     
    data0[c('z', 'a')] <- list(a = 99, b = -99)


    # extractAssign2
    data0 <- list(x = 1:3, y = list(z = 4:6), z = 6)
    length(data0)

    data0[[0]] <- 99
    data0[['z']] <- -99
    data0[['a']] <- 99

    data0[[c(1,0)]] <- 99
    data0[[c('y', 'z')]] <- -99

### R array (including vector and matrix)

    # Vector
    # constructor
    x <- 1:10

    # extract (No extract2)
    x[0]
    x[0:2]
    x[]

    # extractAssign
    x[0] <-  99
    x[1:2] <- c(-99, -99)
    x[3:5] <- 1
    x[] <- -1

    # Matrix
    # constructor
    y <- matrix(99, 2, 2)
    y <- matrix(1:4, 2, 2, FALSE)
    y <- matrix(1:4, 2, 2, TRUE)
    y <- matrix(c('a','b','c','d'), 2, 2)
    y <- matrix(1:6, 2, 3)
    y <- matrix(1:6, 3, 2)

    # extract (No extract2)
    y <- matrix(1:6, 2, 3)
    y[0, 0]
    y[0, 0:1]
    y[c(0,1), c(0)]
    y[0:1, 0:1]
    y[0, ]
    y[0:1, ]
    y[, 0:1]

    # extractAssign
    y <- matrix(1:4, 2, 2)
    y[0,0] <- 99
    y[1, 0:1] <- matrix(c(11,-11), 1, 2)
    y[1, 0:1] <- c(99,-99)

    y[0, 0:1] <- -11
    y[0:1,0:1] <- matrix(4:1, 2, 2)

    y[0, ] <- matrix(c(-99,99), 1, 2)
    y[0, ] <- c(-99,99)
    y[, 0] <- matrix(c(-11,11), 2, 1)
    y[, 0] <- c(-11,11)

    y[0:3] <- 4:1
    y[0:1, 0:1] <- 4:1

    # Array
    # constructor
    x <- array(99, c(2,3,4))
    x <- array(1:8, c(2,2,2))
    x <- array(c('a', 'b', 'c', 'd'), c(2, 2))
    x <- array(c('a', 'b', 'c', 'd'), c(2, 2, 1))
    x <- array(c('a', 'b', 'c', 'd'), c(1, 2, 2))

    # extract (No extract2)
    y <- array(1:4, c(2,2))
    y[0,0]
    y[0, 0:1]

    y <- array(1:8, c(2,2,2))
    y[0, 0, 0:1]
    y[0:1, 0, 0]
    y[, 0, 0]
    y[0, , 0]

    # extractAssign
    # 2 dimenions
    y <- array(1:4, c(2,2))
    y[0, 0] <- 99
    y[0, 0:1] <- c(11, -11)
    y[1, 0:1] <- -22
    y[1, ] <- c(11, -11)
    y[0:1, 0:1] <- matrix(4:1, 2, 2)
    # y[] <- matrix(5:8, 2, 2) # Not supported

    # 3 dimenions
    y <- array(1:8, c(2,2,2))
    y[0, 0, 0] <- 99
    y[1, 0, 0:1] <- c(-11,11)
    y[1, 0:1, 0] <- 22
    y[0, 0:1, 0:1] <- matrix(11:14, 2, 2)
    y[0, 0:1, 0:1] <- 91:94
    y[0:1, , 0] <- matrix(21:24, 2, 2)

### R dataframe

    # constructor
    df0 <- data.frame(x = 1:3, y = 4:6)

    # extract
    df0[0]
    df0['y']
    df0[1]
    df0[c(1)]
    df0[c('y')]

    df0[0, 1]
    df0[0, 'x']
    df0[0:1, 'x']
    df0[0:2, 'x']
    df0[0:2, 0]

    # extract2
    df0[['x']]
    df0[[0]]
    df0[['y']]
    df0[[1]]
    # df0[[0, 'x']] # Not supported

    # extractAssign (no extract2Assign)
    # one argument
    df0 <- data.frame(x = 1:3, y = 4:6)
    df0['x'] <- 1
    df0['y'] <- 7:9
    df0[0] <- 2
    df0[1] <- 97:99
    df0[c('x','y')] <- 99
    df0[c('x','y')] <- matrix(7:12, 3, 2)

    # two arguments
    df0 <- data.frame(x = 1:3, y = 4:6)

    df0[1, 'x'] <- 7
    df0[0:1, 'x'] <- 99
    df0[0:1, 'y'] <- c(7, 77)
    df0[0, c('x', 'y')] <- 22
    df0[0, c('x', 'y')] <- c(77, 88)
    df0[0:1, c('x', 'y')] <- 10
    df0[0:1, c('x', 'y')] <- matrix(-1:-4, 2, 2)

Supports basic Object-Oriented Programming (OOP)
------------------------------------------------

    #! load_library("p5")

    # Define a 'ball' object
    ball <- function(x, y, r) {
        self$x <- x
        self$y <- y
        self$r <- r
        self$draw <- function() {
            circle(self$x, self$y, self$r)
        }
    }

    # Initialise an array of 'ball' objects
    balls <- map(1:10, function(i) {
        return(ball$new(i * 20, i * 20, i * 2))
    })

    # Main
    setup <- function() {
        createCanvas(300, 300)
        map(balls, function(ball) { ball$draw() })
    }

Load any structured data
------------------------

### Load any tabular data

`sketch` supports CSV by default and allows custom functions via the
`read_fun` argument. The argument is created mainly to support the wide
range of data input functions from the `readr` package. The data is
stored in a constant variable named after the file name but with “.”
replaced by "\_" (as “.” has special meaning in JavaScript).

    #! load_data("./mtcars.csv")
    mtcars_csv$show()

    #! load_data("./mtcars.tsv", read_fun = readr::read_tsv, as_data_frame = TRUE)
    mtcars_tsv$show()

### Load any JSON file

    #! load_data("./mtcars.json")
    names <- Object::keys
    print <- console::log

    mtcars_json
    print(names(mtcars_json))

Integrate with V8 and Shiny
---------------------------

Deploy with ease
----------------

### Embed an app in an R Markdown document

### Deploy as a JavaScript file

Organise code by modules
------------------------

Customisable and Extensible
---------------------------

    #! load_library("tensorflow")

This is useful using R like a JavaScript macro system. In fact, it is
also useful as a R macro system.

<!-- ## Learn and Share easily (to come) -->
<!-- ## Auto-completion (to come) -->
<!-- ## Online editor (to come) -->
