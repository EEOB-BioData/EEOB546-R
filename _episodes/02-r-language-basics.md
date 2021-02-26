---
title: "R Language Basics"
teaching: 30
exercises: 20
questions:
- "How to do simple calculations in R?"
- "How to assign values to variables and call functions?"
- "What are R's vectors, vector data types, and vectorization?"
- "How to install packages?"
- "How can I get help in R?"
- "What is an R Markdown file and how can I create one?"
objectives:
- "To understand variables and how to assign to them"
- "To be able to use mathematical and comparison operations"
- "To be able to call functions"
- "To be able to find and use packages"
- "To be able to read R help files for functions and special operators."
- "To be able to seek help from your peers."
- "To be able to create and use R Markdown files"
keypoints:
- "R has the usual arithmetic operators and mathematical functions."
- "Use `<-` to assign values to variables."
- "Use `ls()` to list the variables in a program."
- "Use `rm()` to delete objects in a program."
- "Use `install.packages()` to install packages (libraries)."
- "Use `library(packagename)`to make a package available for use"
- "Use `help()` to get online help in R."
---


<img src="../img/R.png" align="right" hspace="10">

## Introduction to R

R is a system for statistical computation and graphics. It provides, 
among other things, a programming language, high level graphics, 
interfaces to other languages and debugging facilities.  

As a programming language, R adopts syntax and grammar that differ from 
many other languages: objects in R are ‘vectors’, and functions are 
‘vectorized’ to operate on all elements of the object; R objects have 
‘copy-on-modify’ and ‘call-by-value’ semantics; common paradigms in other 
languages, such as the ‘for’ loop, are encountered less commonly in R.

Much of your time in R will be spent in the R interactive
console. This is where you will run all of your code, and can be a
useful environment to try out ideas before adding them to an R script
file. This console in RStudio is the same as the one you would get if
you typed in `R` in your command-line environment.

The first thing you will see in the R interactive session is a bunch
of information, followed by a ">" and a blinking cursor. In many ways
this is similar to the shell environment you learned about during the
unix lessons: it operates on the same idea of a "Read, evaluate,
print loop": you type in commands, R tries to execute them, and then
returns a result.

## Work flow within RStudio
There are three main ways one can work within RStudio.

1. Test and play within the interactive R console then copy code into
a .R file to run later.
   *  This works well when doing small tests and initially starting off.
   *  You can use the history panel to copy all the commands to the source file.
2. Start writing in an .R file and use RStudio's command / short cut
to push current line, selected lines or modified lines to the
interactive R console.
   * This works well if you are more advanced in writing R code; 
   * All your code is saved for later
   * You will be able to run the file you create from within RStudio
     or using R's `source()`  function.
3. Better yet, you can write your code in R markdown file. 
An [R Markdown file](http://rmarkdown.rstudio.com/) allows you to incorporate your
code in a narration that a reader needs to understand it, run it, and display your 
results. You can use multiple languages including R, Python, and SQL.  

> ## Tip: Creating an R Markdown document
>
> You can create a new R Markdown document in RStudio with the menu command 
> _File -> New File -> RMarkdown_. A new windows opens and asks you to enter 
> title, author, and default output format for your R Markdown document. After 
> you enter this information, a new R Markdown file opens in a new tab.  
> Notice that the file contains three types of content: 
> * An (optional) YAML header surrounded by ---s; 
> * R code chunks surrounded by ```s; 
> * text mixed with simple text formatting.  
>
> You can use the “Knit” button in the RStudio IDE to render the 
> file and preview the output with a single click or keyboard shortcut (⇧⌘K).
> Note that you can quickly insert chunks of code into your file with the keyboard 
> shortcut Ctrl + Alt + I (OS X: Cmd + Option + I) or the Add Chunk  command in the 
> editor toolbar. You can run the code in a chunk by pressing the green triangle on 
> the right. To run the current line, you can:  
> 1. click on the `Run` button above the editor panel, or  
> 2. select "Run Lines" from the "Code" menu, or  
> 3. hit Ctrl-Enter in Windows or Linux or Command-Enter on OS X.   
{: .callout}


## Using R as a calculator

The simplest thing you could do with R is do arithmetic:


~~~
1 + 100
~~~
{: .language-r}



~~~
[1] 101
~~~
{: .output}

And R will print out the answer, with a preceding "[1]". Don't worry about this
for now, we'll explain that later. For now think of it as indicating output.

Like bash, if you type in an incomplete command, R will wait for you to
complete it:


~~~
1 + 
~~~
{: .language-r}

Any time you hit return and the R session shows a "+" instead of a ">", it
means it's waiting for you to complete the command. If you want to cancel
a command you can simply hit "Esc" and RStudio will give you back the ">"
prompt.

> ## Tip: Cancelling commands
>
> If you're using R from the commandline instead of from within RStudio,
> you need to use `Ctrl+C` instead of `Esc` to cancel the command. This
> applies to Mac users as well!
>
> Cancelling a command isn't only useful for killing incomplete commands:
> you can also use it to tell R to stop running code (for example if its
> taking much longer than you expect), or to get rid of the code you're
> currently writing.
>
{: .callout}

When using R as a calculator, the order of operations is the same as you
would have learned back in school.

From highest to lowest precedence:

 * Parentheses: `(`, `)`
 * Exponents: `^` or `**`
 * Divide: `/`
 * Multiply: `*`
 * Add: `+`
 * Subtract: `-`


~~~
3 + 5 * 2
~~~
{: .language-r}



~~~
[1] 13
~~~
{: .output}

Use parentheses to group operations in order to force the order of
evaluation if it differs from the default, or to make clear what you
intend.


~~~
(3 + 5) * 2
~~~
{: .language-r}



~~~
[1] 16
~~~
{: .output}

This can get unwieldy when not needed, but  clarifies your intentions.
Remember that others may later read your code.  


~~~
(3 + (5 * (2 ^ 2))) # hard to read
3 + 5 * 2 ^ 2       # clear, if you remember the rules
3 + 5 * (2 ^ 2)     # if you forget some rules, this might help
~~~
{: .language-r}

The text after each line of code is called a
"comment". Anything that follows after the hash (or octothorpe) symbol
`#` is ignored by R when it executes code.

Really small or large numbers get a scientific notation:


~~~
2/10000
~~~
{: .language-r}



~~~
[1] 2e-04
~~~
{: .output}

Which is shorthand for "multiplied by `10^XX`". So `2e-4`
is shorthand for `2 * 10^(-4)`.

You can write numbers in scientific notation too:


~~~
5e3  # Note the lack of minus here
~~~
{: .language-r}



~~~
[1] 5000
~~~
{: .output}

## Mathematical functions

R has many built in mathematical functions. To call a function,
we simply type its name, followed by  open and closing parentheses.
Anything we type inside the parentheses is called the function's
arguments:


~~~
# trigonometry functions
sin(1)  
~~~
{: .language-r}



~~~
[1] 0.841471
~~~
{: .output}



~~~
# natural logarithm
log(1)  
~~~
{: .language-r}



~~~
[1] 0
~~~
{: .output}



~~~
# base-10 logarithm
log10(10) 
~~~
{: .language-r}



~~~
[1] 1
~~~
{: .output}



~~~
# natural exponential function
exp(0.5) # e^(1/2)
~~~
{: .language-r}



~~~
[1] 1.648721
~~~
{: .output}

Don't worry about trying to remember every function in R. You
can simply look them up on Google, or if you can remember the
start of the function's name, use the tab completion in RStudio.

This is one advantage that RStudio has over R on its own, it
has auto-completion abilities that allow you to more easily
look up functions, their arguments, and the values that they
take.

Typing a `?` before the name of a command will open the help page
for that command. As well as providing a detailed description of
the command and how it works, scrolling to the bottom of the
help page will usually show a collection of code examples which
illustrate command usage. We'll go through an example later.

## Comparing things

We can also do comparison in R:


~~~
# equality (note two equals signs, read as "is equal to")
1 == 1  
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}



~~~
# inequality (read as "is not equal to")
1 != 2  
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}



~~~
# less than
1 <  2  
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}



~~~
# less than or equal to
1 <= 1  
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}



~~~
# greater than
1 > 0  
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}



~~~
# greater than or equal to
1 >= -9 
~~~
{: .language-r}



~~~
[1] TRUE
~~~
{: .output}


> ## Tip: Comparing Numbers
>
>
> Further reading: [http://floating-point-gui.de/](http://floating-point-gui.de/)
>
{: .callout}


## Variables and assignment

We can store values in variables using the assignment operator `<-`, like this:


~~~
x <- 1/40
~~~
{: .language-r}

Notice that assignment does not print a value. Instead, we stored it for later
in something called a **variable**. `x` now contains the **value** `0.025`:


~~~
x
~~~
{: .language-r}



~~~
[1] 0.025
~~~
{: .output}

More precisely, the stored value is a *decimal approximation* of
this fraction called a [floating point number](http://en.wikipedia.org/wiki/Floating_point).

Look for the `Environment` tab in one of the panes of RStudio, and you will see that `x` and its value
have appeared. Our variable `x` can be used in place of a number in any calculation that expects a number:


~~~
log(x)
~~~
{: .language-r}



~~~
[1] -3.688879
~~~
{: .output}

Notice also that variables can be reassigned:


~~~
x <- 100
~~~
{: .language-r}

`x` used to contain the value 0.025 and and now it has the value 100.

Assignment values can contain the variable being assigned to:


~~~
x <- x + 1 #notice how RStudio updates its description of x on the top right tab
~~~
{: .language-r}

The right hand side of the assignment can be any valid R expression.
The right hand side is *fully evaluated* before the assignment occurs.

> ## Tip: A shortcut for assignment operator
>
> IN RStudio, you can create the <- assignment operator in one keystroke 
> using `Option -` (that's a dash) on OS X or `Alt -` on Windows/Linux.
>
{: .callout}

It is also possible to use the `=` operator for assignment:


~~~
x = 1/40
~~~
{: .language-r}

But this is much less common among R users. So the recommendation is to use `<-`.

> ## Tip: Naming variables
> Variable names can contain letters, numbers, underscores and periods. They
> cannot start with a number nor contain spaces at all. Different people use
> different conventions for long variable names, these include
>
>  * periods.between.words
>  * underscores\_between_words
>  * camelCaseToSeparateWords
>
> What you use is up to you, but **be consistent**.
>
{: .callout}

> ## Warning: Naming variables
> Notice, that R does not use a special symbol to distinguish between variable
> and simple text. Instead, the text is placed in double quotes "text".
> If R complains that the object *text* does not exist, you probably forgot to 
> use the quotes!
>
{: .callout}


## Vectorization

One final thing to be aware of is that R is *vectorized*, meaning that
variables and functions can have vectors as values. For example


~~~
1:5
~~~
{: .language-r}



~~~
[1] 1 2 3 4 5
~~~
{: .output}



~~~
2^(1:5)
~~~
{: .language-r}



~~~
[1]  2  4  8 16 32
~~~
{: .output}



~~~
x <- 1:5
2^x
~~~
{: .language-r}



~~~
[1]  2  4  8 16 32
~~~
{: .output}

This is incredibly powerful; we will discuss this further in an
upcoming lesson.


## Managing your environment

There are a few useful commands you can use to interact with the R session.

`ls` will list all of the variables and functions stored in the global environment
(your working R session):


~~~
ls() # to list files use list.files() function
~~~
{: .language-r}



~~~
[1] "args"    "dest_md" "op"      "src_rmd" "x"      
~~~
{: .output}

> ## Tip: hidden objects
>
> Like in the shell, `ls` will hide any variables or functions starting
> with a "." by default. To list all objects, type `ls(all.names=TRUE)`
> instead
>
{: .callout}

Note here that we didn't given any arguments to `ls`, but we still
needed to give the parentheses to tell R to call the function.

If we type `ls` by itself, R will print out the source code for that function!


~~~
ls
~~~
{: .language-r}



~~~
function (name, pos = -1L, envir = as.environment(pos), all.names = FALSE, 
    pattern, sorted = TRUE) 
{
    if (!missing(name)) {
        pos <- tryCatch(name, error = function(e) e)
        if (inherits(pos, "error")) {
            name <- substitute(name)
            if (!is.character(name)) 
                name <- deparse(name)
            warning(gettextf("%s converted to character string", 
                sQuote(name)), domain = NA)
            pos <- name
        }
    }
    all.names <- .Internal(ls(envir, all.names, sorted))
    if (!missing(pattern)) {
        if ((ll <- length(grep("[", pattern, fixed = TRUE))) && 
            ll != length(grep("]", pattern, fixed = TRUE))) {
            if (pattern == "[") {
                pattern <- "\\["
                warning("replaced regular expression pattern '[' by  '\\\\['")
            }
            else if (length(grep("[^\\\\]\\[<-", pattern))) {
                pattern <- sub("\\[<-", "\\\\\\[<-", pattern)
                warning("replaced '[<-' by '\\\\[<-' in regular expression pattern")
            }
        }
        grep(pattern, all.names, value = TRUE)
    }
    else all.names
}
<bytecode: 0x7fb3bbf28b58>
<environment: namespace:base>
~~~
{: .output}

You can use `rm` to delete objects you no longer need:


~~~
rm(x)
~~~
{: .language-r}

If you have lots of things in your environment and want to delete all of them,
you can pass the results of `ls` to the `rm` function:


~~~
rm(list = ls())
~~~
{: .language-r}

In this case we've combined the two. Like the order of operations, anything
inside the innermost parentheses is evaluated first, and so on.

In this case we've specified that the results of `ls` should be used for the
`list` argument in `rm`. When assigning values to arguments by name, you *must*
use the `=` operator!!

If instead we use `<-`, there will be unintended side effects, or you may get an error message:


~~~
rm(list <- ls())
~~~
{: .language-r}



~~~
Error in rm(list <- ls()): ... must contain names or character strings
~~~
{: .error}

> ## Tip: Warnings vs. Errors
>
> Pay attention when R does something unexpected! Errors, like above,
> are thrown when R cannot proceed with a calculation. Warnings on the
> other hand usually mean that the function has run, but it probably
> hasn't worked as expected.
>
> In both cases, the message that R prints out usually give you clues
> how to fix a problem.
>
{: .callout}

## R Packages

It is possible to add functions to R by writing a package, or by
obtaining a package written by someone else. There
are over 7,000 packages available on CRAN (the comprehensive R archive
network). R and RStudio have functionality for managing packages:

* You can see what packages are installed by typing
  `installed.packages()`
* You can install packages by typing `install.packages("packagename")`,
  where `packagename` is the package name, in quotes.
* You can update installed packages by typing `update.packages()`
* You can remove a package with `remove.packages("packagename")`
* You can make a package available for use with `library(packagename)`

## Writing your own code

Good coding style is like using correct punctuation. You can manage without it, 
but it sure makes things easier to read. As with styles of punctuation, there 
are many possible variations. [Google’s R style guide](https://google.github.io/styleguide/Rguide.xml) 
is a good place to start. The [formatR](https://cran.r-project.org/web/packages/formatR/index.html) 
package, by Yihui Xie, makes it easier to clean up poorly formatted code. 
Make sure to read the notes on the [wiki](https://github.com/yihui/formatR/wiki) 
before using it.

## Looking for help

### Reading Help files

R, and every package, provide help files for functions. To search for help use:


~~~
?function_name
help(function_name)
~~~
{: .language-r}

This will load up a help page in RStudio (or as plain text in R by itself).

Note that each help page is broken down into several sections, including
Description, Usage, Arguments, Examples, etc.

### Special Operators

To seek help on special operators, use quotes:


~~~
?"+"
~~~
{: .language-r}

### Getting help on packages

Many packages come with "vignettes": tutorials and extended example documentation.
Without any arguments, `vignette()` will list all vignettes for all installed packages;
`vignette(package="package-name")` will list all available vignettes for
`package-name`, and `vignette("vignette-name")` will open the specified vignette.

If a package doesn't have any vignettes, you can usually find help by typing
`help("package-name")`.

### When you kind of remember the function

If you're not sure what package a function is in, or how it's specifically spelled you can do a fuzzy search:


~~~
??function_name
~~~
{: .language-r}

### When you have no idea where to begin

If you don't know what function or package you need to use
[CRAN Task Views](http://cran.at.r-project.org/web/views)
is a specially maintained list of packages grouped into
fields. This can be a good starting point.

### When your code doesn't work: seeking help from your peers

If you're having trouble using a function, 9 times out of 10,
the answers you are seeking have already been answered on
[Stack Overflow](http://stackoverflow.com/). You can search using
the `[r]` tag.

If you can't find the answer, there are two useful functions to
help you ask a question from your peers:


~~~
?dput
~~~
{: .language-r}

Will dump the data you're working with into a format so that it can
be copy and pasted by anyone else into their R session.


~~~
sessionInfo()
~~~
{: .language-r}



~~~
R version 4.0.4 (2021-02-15)
Platform: x86_64-apple-darwin17.0 (64-bit)
Running under: macOS Catalina 10.15.7

Matrix products: default
BLAS:   /Library/Frameworks/R.framework/Versions/4.0/Resources/lib/libRblas.dylib
LAPACK: /Library/Frameworks/R.framework/Versions/4.0/Resources/lib/libRlapack.dylib

locale:
[1] en_US.UTF-8/en_US.UTF-8/en_US.UTF-8/C/en_US.UTF-8/en_US.UTF-8

attached base packages:
[1] stats     graphics  grDevices utils     datasets  methods   base     

other attached packages:
[1] knitr_1.31

loaded via a namespace (and not attached):
[1] compiler_4.0.4 magrittr_2.0.1 tools_4.0.4    stringi_1.5.3  stringr_1.4.0 
[6] xfun_0.21      evaluate_0.14 
~~~
{: .output}

Will print out your current version of R, as well as any packages you
have loaded.

## Vocabulary

As with any language, it's important to work on your R vocabulary.  Here is a 
[good place to start](http://adv-r.had.co.nz/Vocabulary.html)

> ## Challenge 1
>
> Which of the following are valid R variable names?
> 
> ~~~
> min_height
> max.height
> _age
> .mass
> MaxLength
> min-length
> 2widths
> celsius2kelvin
> ~~~
> {: .language-r}
>
> > ## Solution to challenge 1
> >
> > The following can be used as R variables:
> > 
> > ~~~
> > min_height
> > max.height
> > MaxLength
> > celsius2kelvin
> > ~~~
> > {: .language-r}
> >
> > The following creates a hidden variable:
> > 
> > ~~~
> > .mass
> > ~~~
> > {: .language-r}
> >
> > The following will not be able to be used to create a variable
> > 
> > ~~~
> > _age
> > min-length
> > 2widths
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

> ## Challenge 2
>
> What will be the value of each  variable  after each
> statement in the following program?
>
> 
> ~~~
> mass <- 47.5
> age <- 122
> mass <- mass * 2.3
> age <- age - 20
> ~~~
> {: .language-r}
>
> > ## Solution to challenge 2
> >
> > 
> > ~~~
> > mass <- 47.5
> > ~~~
> > {: .language-r}
> > This will give a value of 47.5 for the variable mass
> >
> > 
> > ~~~
> > age <- 122
> > ~~~
> > {: .language-r}
> > This will give a value of 122 for the variable age
> >
> > 
> > ~~~
> > mass <- mass * 2.3
> > ~~~
> > {: .language-r}
> > This will multiply the existing value of 47.5 by 2.3 to give a new value of
> > 109.25 to the variable mass.
> >
> > 
> > ~~~
> > age <- age - 20
> > ~~~
> > {: .language-r}
> > This will subtract 20 from the existing value of 122 to give a new value
> > of 102 to the variable age.
> {: .solution}
{: .challenge}


> ## Challenge 3
>
> Run the code from the previous challenge, and write a command to
> compare mass to age. Is mass larger than age?
>
> > ## Solution to challenge 3
> >
> > One way of answering this question in R is to use the `>` to set up the following:
> > 
> > ~~~
> > mass > age
> > ~~~
> > {: .language-r}
> > 
> > 
> > 
> > ~~~
> > [1] TRUE
> > ~~~
> > {: .output}
> > This should yield a boolean value of TRUE since 109.25 is greater than 102.
> {: .solution}
{: .challenge}


> ## Challenge 4
>
> Clean up your working environment by deleting the mass and age
> variables.
>
> > ## Solution to challenge 4
> >
> > We can use the `rm` command to accomplish this task
> > 
> > ~~~
> > rm(age, mass)
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

> ## Challenge 5
>
> Install packages in the `tidyverse` collection
>
> > ## Solution to challenge 5
> >
> > We can use the `install.packages()` command to install the required packages.
> > 
> > ~~~
> > install.packages("tidyverse")
> > ~~~
> > {: .language-r}
> {: .solution}
{: .challenge}

> ## Challenge 6
> Use help to find a function (and its associated parameters) that you could
> use to load data from a csv file in which columns are delimited with "\t"
> (tab) and the decimal point is a "." (period). This check for decimal
> separator is important, especially if you are working with international
> colleagues, because different countries have different conventions for the
> decimal point (i.e. comma vs period).
> hint: use `??csv` to lookup csv related functions.
{: .challenge}
