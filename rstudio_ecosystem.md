---
title: The RStudio Ecosystem
author: by Stuart Hertzog
date: March&ndash;May 2018
output:
  html_document:
    df_print: paged
  pdf_document: default
  word_document: default
---

# RStudio\_Ecosystem

  
    $\(document\).ready\(function\(\) {  
      $items = $\('div\#TOC li'\);  
      $items.each\(function\(idx\) {  
        num\_ul = $\(this\).parentsUntil\('\#TOC'\).length;  
        $\(this\).css\({'text-indent': num\_ul \* 10, 'padding-left': 0}\);  
      }\);  
  
    }\);  


![](.gitbook/assets/rstudio_full_logo.png)

**The RStudio IDE is the flagship of a comprehensive RStudio ecosystem.**

## R Notebooks

[R Notebooks](https://rmarkdown.rstudio.com/r_notebooks.html) are the most basic type of [RMarkdown](rstudio_ecosystem.md#rmarkdown) document. They are the RStudio equivalent to [Jupyter Notebooks](https://jupyter.org/). As described by [RStudio](https://rmarkdown.rstudio.com/r_notebooks.html):

> An R Notebook is an R Markdown document with chunks that can be executed independently and interactively, with output visible immediately beneath the input.

**Any R Markdown document can be used as a Notebook, and all R Notebooks can be rendered to other R Markdown document types**.

### Creating An R Notebook File

**The RStudio menu item** _**File -&gt; New File -&gt; R Notebook**_ creates a new [RStudio Notebook](https://rmarkdown.rstudio.com/r_notebooks.html) containing instructions on how to use an R Notebook.

```text
---
title: "R Notebook"
output:
  html_notebook
---

This is an [R Markdown](http://rmarkdown.rstudio.com) Notebook. When you execute code within the notebook, the results appear beneath the code. 

Try executing this chunk by clicking the *Run* button within the chunk or by placing your cursor inside it and pressing *Cmd+Shift+Enter*. 

```
{r}
plot(cars)
```

Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing *Cmd+Option+I*.

When you save the notebook, an HTML file containing the code and output will be saved alongside it (click the *Preview* button or press *Cmd+Shift+K* to preview the HTML file). 

The preview shows you a rendered HTML copy of the contents of the editor. Consequently, unlike *Knit*, *Preview* does not run any R code chunks. Instead, the output of the chunk when it was last run in the editor is displayed.
```

For more information see [RStudio Notebook](https://rmarkdown.rstudio.com/r_notebooks.html).

### R Notebook HTML files

**An** [**R Notebook HTML file**](https://rmarkdown.rstudio.com/r_notebook_format.html) **is a special type of** [**R Notebook**](rstudio_ecosystem.md#r-notebook).

It is an HTML file that uses the `.nb.html` extension and it enables:

* **the source .Rmd document** and
* **chunk outputs** to be recovered.

The `html_notebook` output format is specified in the YAML metadata:

```text
title: "my_document_title"
output:
    html_notebook
```

With the `_yaml` file written this way, the command `rmarkdown::render()` will create an `.nb.html` R Notebook HTML Format file.

For more information, see [Details of the R Notebook HTML Format](https://rmarkdown.rstudio.com/r_notebook_format.html).

**Note**: The [RStudio instructions](https://rmarkdown.rstudio.com/r_notebook_format.html#generating-r-notebooks-with-custom-output) show an incorrect `YAML` header. You must use the `_yaml` format shown above or RStudio will throw an error and not compile.

## RMarkdown

> R Markdown documents are fully reproducible. They use a productive notebook interface to weave together narrative text and code to produce elegantly-formatted output from multiple languages including R, Python, and SQL.  
> --- [_RStudio RMarkdown_](https://rmarkdown.rstudio.com/)

[**RMarkdown documents**](https://rmarkdown.rstudio.com/) **are the default RStudio document**. They are plain-text files with the `.Rmd` extension and can be used to generate many different types of output. The main ones are:

* [HTML documents](https://rmarkdown.rstudio.com/html_document_format.html) -- `.html`
* [PDF Documents](https://rmarkdown.rstudio.com/pdf_document_format.html) -- `.pdf`
* [Word Documents](https://rmarkdown.rstudio.com/word_document_format.html) -- `.docx`

In addition to the standard output formats \(above\), RMarkdown documents can generate output in many other formats, via the [pandoc](rstudio_ecosystem.md#pandoc) conversion engine.

[Beamer](https://rmarkdown.rstudio.com/beamer_presentation_format.html), [HTML5 slides](https://rmarkdown.rstudio.com/ioslides_presentation_format.html), [Tufte-style handouts](https://rmarkdown.rstudio.com/tufte_handout_format.html), [books](https://bookdown.org/yihui/bookdown/), [dashboards](https://rmarkdown.rstudio.com/flexdashboard/), [interactive documents](https://rmarkdown.rstudio.com/authoring_shiny.html), [scientific articles](https://github.com/rstudio/rticles), and [websites](https://rmarkdown.rstudio.com/rmarkdown_websites.html).

[**RStudio maintains a gallery of examples**](https://rmarkdown.rstudio.com/gallery.html) of the many uses of RMarkdown.

### knitr

> RMarkdown uses the [knitr](https://yihui.name/knitr/) report generation package to output to the different file formats.

**The** `knitr` **package enables integration of R code into** [**LaTeX**](https://en.wikipedia.org/wiki/LaTeX)**,** [**LyX**](https://en.wikipedia.org/wiki/LyX)**,** [**HTML**](https://en.wikipedia.org/wiki/HTML)**,** [**Markdown**](https://en.wikipedia.org/wiki/Markdown)**,** [**AsciiDoc**](https://en.wikipedia.org/wiki/AsciiDoc)**, and** [**reStructuredText**](https://en.wikipedia.org/wiki/ReStructuredText) **documents**. It can execute code chunks in a variety of languages via [knitr Language Engines](https://rmarkdown.rstudio.com/authoring_knitr_engines.html), including for:

* R
* Python
* SQL
* Bash
* Rcpp
* Stan
* JavaScript
* CSS

**To process a code chunk using an alternate language engine** simply use the name of the engine in place of `{r}` in the chunk declaration, for example:

```text
```{bash, eval = FALSE}
cat flights1.csv flights2.csv flights3.csv > flights.csv
```
```

#### Code Chunk Options

**RMarkdown code chunk processing can be controlled** by including [_Chunk Options_](https://rmarkdown.rstudio.com/lesson-3.html) in the _Chunk Declaration_, for example:

`{r, include = FALSE`} prevents code and results from appearing.  
R Markdown still runs the code and the results can be used by other chunks.  
`{r, eval = FALSE`} prevents to code from running but it still appears. `{r, echo = FALSE`} prevents code but not the results from appearing.  
This is a useful way to embed figures.  
`{r, message = FALSE`} prevents messages generated by code from appearing.  
`{r, warning = FALSE`} prevents warnings generated by code from appearing.  
`{r, fig.cap = "..."`} adds a caption to graphical results.

The [R Markdown Reference Guide \(.pdf\)](https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf) has a list of useful options. [Yihui's `knitr` options](https://yihui.name/knitr/options/) has full documentation of all `knitr` code processing controls.

### pandoc

The RStudio installation includes [pandoc](http://pandoc.org/), which is used for conversion between RMarkdown and [the various output formats](https://rmarkdown.rstudio.com/formats.html). You may have to [install pandoc on your system](http://pandoc.org/installing.html) for conversion to take place, especially for `.pdf` output, which goes through an intermediate `LaTeX` stage.

`pandoc` can also be run from the commond line if it is installed separately. This is explained in detail in the [pandoc manual](http://pandoc.org/MANUAL.html).

## Shiny

> [Shiny](http://shiny.rstudio.com/) is an R package that makes it easy to build interactive web apps straight from R. You can host standalone apps on a webpage or embed them in [R Markdown](http://rmarkdown.rstudio.com/) documents or build [dashboards](http://rstudio.github.io/shinydashboard/). You can also extend your Shiny apps with [CSS themes](http://rstudio.github.io/shinythemes/), [htmlwidgets](http://www.htmlwidgets.org/), and JavaScript [actions](https://github.com/daattali/shinyjs/blob/master/README.md).  
>  --- [_RStudio Shiny_](http://shiny.rstudio.com/)

[**RStudio's Shiny**](http://shiny.rstudio.com/) **is a Web application framework for R that takes static** [**RMarkdown documents**](rstudio_ecosystem.md#rmarkdown) **and** [**Web sites**](https://rmarkdown.rstudio.com/html_document_format.html) **to the next level**.

There is no limit to building online documentation, interactive tutorials, and statistical data interfaces with these powerful R packages:

* [`htmlwidgets`](http://www.htmlwidgets.org/) enables JavaScript visualisations and interactive components to be incorporated into [R Markdown documents](rstudio_ecosystem.md#rmarkdown) and Shiny web applications, as shown in this [showcase](http://www.htmlwidgets.org/showcase_leaflet.html) and this [gallery](http://www.htmlwidgets.org/)
* [`crosstalk`](http://rstudio.github.io/crosstalk/) wires widgets together, including linked brushing between widgets and client side filtering
* [`shinydashboard`](http://rstudio.github.io/shinydashboard/) makes it easy to create all kinds of Web dashboards, as shown in [these examples](http://rstudio.github.io/shinydashboard/examples.html)

and others:

* [`intrval`](https://github.com/psolymos/intrval) can be used to build for example, a [Web slider](http://peter.solymos.org/code/2018/03/08/shiny-slider-examples-with-the-intrval-r-package.html)

We will explore [building Shiny apps](http://shiny.rstudio.com/) in a future Tutorial.

### Shiny Server

[Shiny Server](https://www.rstudio.com/products/shiny/shiny-server/) makes your [Shiny Web apps](http://shiny.rstudio.com/) accessible on a local network, an Enterprise server, or on the Internet. There are two flavours of server:

* [Shiny Server Open Source](https://www.rstudio.com/products/shiny/download-server/) and 
* [Shiny Server Pro](https://www.rstudio.com/products/rstudio-server-pro/)

Documentation is available for:

* [Installing Shiny Server Open Source](https://www.rstudio.com/products/shiny/download-server/)
* [Shiny Server Pro Admin Guide](http://docs.rstudio.com/shiny-server/)
* [shinyapps.io User Guide](http://docs.rstudio.com/shinyapps.io/index.html)

Shiny Apps can be available to an Intranet or to the Internet via:

* [An Enterprise Server](https://www.rstudio.com/products/rstudio-server-pro/)
* [RStudio Connect](https://www.rstudio.com/products/connect/)
* [shinyapps.io](https://www.rstudio.com/products/shinyapps/)

The difference between the latter two is [explained here](https://support.rstudio.com/hc/en-us/articles/217240558-What-is-the-difference-between-shinyapps-io-and-Shiny-Server-Pro-).

## bookdown

![](.gitbook/assets/bookdown_logo.png)

> [`bookdown`](https://github.com/rstudio/bookdown) is an open-source R package that makes it really easy to creates online books and technical documents using [RMarkdown](rstudio_ecosystem.md#rmarkdown).

`bookdown` **books open a new avenue for Web-enabled book publishing**.

They are essentially **responsive RMarkdown Web sites**, complete with content navigation, plus the ability to display and process computer code using a wide range of programming languages, including interactive [Shiny dashboards](http://rstudio.github.io/shinydashboard/examples.html) and [Web apps](http://shiny.rstudio.com/gallery/).

`bookdown` **has added a few important missing features** related to writing books, such as figure and table caption numbering and cross-references, and the ability to embed [HTML widgets](https://www.rstudio.com/products/shinyapps/) or [Shiny apps](http://shiny.rstudio.com/gallery/).

**Developed and maintained by RStudio software engineer** [**Yihui Xie**](http://yihui.name), `bookdown` books can be published on [bookdown.org](https://bookdown.org/), a free service provided by [RStudio Inc](https://www.rstudio.com/about/). Books are available for download, and the author holds full copyright.

[![](https://bookdown.org/yihui/bookdown/images/cover.jpg)](https://bookdown.org/)

**Fully-documented** in --- of course! --- a [`bookdown` book called _bookdown_](https://bookdown.org/yihui/bookdown/), the `bookdown` package uses many of the same conventions as [other RMarkdown document types](rstudio_ecosystem.md#rmarkdown), so conversion of any RStudio project to an online book is relatively straightforward.

[A Minimal Book Example](https://github.com/rstudio/bookdown-demo) can be cloned from GitHub. It can also be downloaded as a [`.zip` file](https://github.com/rstudio/bookdown-demo/archive/master.zip) if you are [not familiar with GitHub](http://rogerdudler.github.io/git-guide/).

### `bookdown` Installation

[Installation](https://bookdown.org/home/getting-started.html) requires the [devtools](https://www.rstudio.com/products/rpackages/devtools/) R package to be first installed, after which `bookdown` can be installed from [its GitHub repository](https://github.com/rstudio/bookdown):

\`\`\`{r eval = FALSE} install.packages\("devtools"\) devtools::install\_github\("rstudio/bookdown"\)

```text
### `tinytex`

**PDF output requires some version of the [LaTeX](https://www.latex-project.org/) typesetting system** to be installed. LaTeX is not a stand-alone typesetting program in itself, but document preparation software that runs on top of Donald E. Knuth's [TeX typesetting system](https://en.wikipedia.org/wiki/TeX).

**[TeX distributions](https://www.latex-project.org/get/#tex-distributions) usually bundle together all the parts needed** for a working TeX system. [LaTeX](https://www.latex-project.org/) and many of the packages built on it form an important component of any modern TeX distribution.

**As this is a large package consisting of many gigabytes of files** that users may not wish to install, [Yihui Xie wrote `tinytex`](https://yihui.name/tinytex/), a lightweight, cross-platform, portable, and easy-to-maintain LaTeX distribution based on [TeX Live](https://en.wikipedia.org/wiki/TeX_Live).

#### `tinytex` Installation

Installation of `tinytex` is accomplished with:

```{r, eval = FALSE}
install.packages(c('tinytex', 'rmarkdown'))
tinytex::install_tinytex()
```

 [**PDF output**](https://rmarkdown.rstudio.com/pdf_document_format.html) **\(including** [**Beamer slides**](https://rmarkdown.rstudio.com/beamer_presentation_format.html)**\) requires a full TeX installation.**

## blogdown

![](.gitbook/assets/blogdown.png)

> Just as [WordPress](https://wordpress.com/) changed the Web by bringing blogging to the masses, [blogdown](https://bookdown.org/yihui/blogdown/) has opened a path for the more computer-savvy to create quick-loading, static blog sites using [RMarkdown](rstudio_ecosystem.md#rmarkdown).

Not content with authoring [`bookdown`](rstudio_ecosystem.md#bookdown), RStudio developer [Yihui Xie](http://yihui.name) took the next logical step by writing the [`blogdown` R package](https://bookdown.org/yihui/blogdown/).

**Based on the** [**Hugo website framework**](https://gohugo.io/)**,** `blogdown` **lets you write posts in RStudio as RMarkdown.Rmd files These are automatically converted to blog posts for uploading to a hosting service, including** [**GitHub pages**](https://pages.github.com/).

### Learning `blogdown`

It is advisable to first read Yihui Xie and Alison Presmanes Hill's `bookdown` book [Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/) to become familiar with `bookdown` concepts and the [Hugo framework](https://gohugo.io/) before you embark on creating your first blog site.

**These links offer practical Setup hints and guidance:**

#### blogdown Setup

* [Up and running with blogdown \| Alison Presmanes Hill](https://alison.rbind.io/post/up-and-running-with-blogdown/)
* [Getting Started With Blogdown \| Borasky Research Journal](https://www.znmeb.mobi/2017/05/12/getting-started-with-blogdown/)
* [R Blogdown Setup in GitHub \(2\) \| Tales of R](https://aurora-mareviv.github.io/talesofr/2018/02/r-blogdown-setup-in-github-2/)
* [A Technical Introduction to Yihui's personal website ](https://support.rbind.io/2017/04/25/yihui-website/#fnref:For-two-reasons)
* [A not-so-technical introduction to Daijiang's personal website](https://support.rbind.io/2017/04/28/daijiang-website/#fnref:frankly-I-cloned)

#### blogdown Links

* [blogdown: Creating Websites with R Markdown](https://bookdown.org/yihui/blogdown/)
* [Announcing blogdown - Yihui Xie, RStudio 2017-09-11](https://blog.rstudio.com/2017/09/11/announcing-blogdown/)
* [GitHub - rstudio/blogdown: Create Blogs and Websites with R Markdown](https://github.com/rstudio/blogdown)
* [GitHub - rbind/blogdown-demo: A minimal website example using blogdown](https://github.com/rbind/blogdown-demo)
* [Twitter hashtag \#blogdown](https://twitter.com/hashtag/blogdown)

### Hugo Themes

`blogdown` **uses** [**Hugo themes**](https://gohugo.io/themes/) **to style the look and feel of its blogs**. The default theme for `blogdown` is [_hugo-lithium_](https://github.com/yihui/hugo-lithium), a minimal theme that offers several options, detailed in [Section 2.4.1](https://bookdown.org/yihui/blogdown/themes.html#the-default-theme) of the `blogdown` book. The base theme can be modified to suit your taste, or it can be replaced by another theme.

**The** [**Hugo web site**](https://gohugo.io/) **showcases many** [**user-contributed themes**](https://themes.gohugo.io). These can be examined online and downloaded for use as-is or as a starting point for themeing.

#### Hugo Links

* [Hugo](https://gohugo.io/) --- world's fastest \(?\) framework for building websites
* [Hugo Setup Guide](https://gohugo.io/getting-started/installing/) --- applies to `blogdown` blog sites
* [Hugo Themeing](https://gohugo.io/themes/) --- how to choose and fine-tune a blog
* [Contributed Hugo Themes](https://themes.gohugo.io) -- hundreds of excellent Hugo themes
* [Converting Old Wordpress Posts To Hugo](https://riinu.netlify.com/2018/02/converting-old-wordpress-posts-to-hugo/) --- goodbye WordPress!

### `blogdown` Blogs

A list of R-related `blogdown` blogs is kept at [rbind on Github](https://github.com/rbind). R-blogs made with `blogdown` can be viewed [here](https://github.com/search?q=org%3Arbind+blogdown).

An interesting and uncluttered example is [Simply Statistics](https://simplystatistics.org/), a statistics blog by Rafa Irizarry, Roger Peng, and Jeff Leek.

## RStudio Products

![](.gitbook/assets/rstudio_full_logo%20%281%29.png)

**Some RStudio products are open-source and free for student and personal use**. Others are priced for professional or Enterprise deployment.

### Software

* [R Notebooks](https://rmarkdown.rstudio.com/r_notebooks.html) --- equivalent to [Jupyter Notebooks](https://jupyter.org/)
* [RMarkdown](https://rmarkdown.rstudio.com/) --- creates `.Rmd` files using [Pandoc Markdown](https://rmarkdown.rstudio.com/authoring_pandoc_markdown.html) 
* [R Packages](https://www.rstudio.com/products/rpackages/) --- available on [CRAN](https://cran.r-project.org/) and [GitHub](https://github.com/rstudio)
* [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop) --- the RStudio IDE, also on [GitHub](https://github.com/rstudio)
* [RStudio Server](https://www.rstudio.com/products/rstudio/#Server) --- free for personal and local Network use
* [Shiny](https://www.rstudio.com/products/shiny/) --- build interactive Web pages and  [JavaScript](https://www.javascript.com) apps
* [Shiny Server](https://www.rstudio.com/products/shiny/shiny-server2/) --- free for local network and Web access behind a firewall

### Cloud Services

* [RStudio Server Pro](https://www.rstudio.com/products/rstudio-server-pro/) -- enhanced admin, Enterprise security and pricing
* [RStudio Connect](https://www.rstudio.com/products/connect/) -- team management, Enterprise security and pricing
* [RStudio Cloud \(in alpha\)](https://rstudio.cloud/) --- Do, Share, Teach, and Learn Data Science
* [Shiny Server Pro](https://www.rstudio.com/products/shiny-server-pro/) -- share Shiny apps, Enterprise security and pricing
* [shinyapps.io](https://www.rstudio.com/products/shinyapps/) -- deploy Shiny apps, enhanced security, scalable
* [Bookdown Book Publishing](https://bookdown.org/) --- free for `bookdown` static page books

### Resources

* [RStudio Cheat Sheets](https://www.rstudio.com/resources/cheatsheets/) --- PDF format
* [RStudio Community](https://community.rstudio.com/) --- register for full Forum access
* [RStudio Documentation](https://support.rstudio.com/hc/en-us/categories/200035113-Documentation) --- Help articles for all RStudio products
* [RStudio Server&gt; Getting Started](https://support.rstudio.com/hc/en-us/articles/234653607-Getting-Started-with-RStudio-Server) --- lists many links for setup and use
* [RStudio Server Pro Admin. Guide](http://docs.rstudio.com/ide/server-pro/) --- web-accessible User Manual

 \[Part 1 - RStudio IDE\]\(RStudio.html\)   \|  \[Part 2 - Fundamentals of R\]\(R\_Programming.html\) 

