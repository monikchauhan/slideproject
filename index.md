---
title       : Farenheit to Celsius Converter
subtitle    : Devolping Data Products Project
author      : Monika Chauhan
job         : Study-Study
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap,shiny}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Introduction   

The FtoC shinyApp accepts temperature in Farenheit from the user and returns equivalent Celsius degress.   

The default temperature is 32F.  

The user can either enter the temperature manually or use the step up or down by 5degrees.






--- .class #id 

## ui.R for the User interaction

```r
library(shiny)
shinyUI(pageWithSidebar(
  # Application title
  headerPanel("Farenheit to Celsius Prediction"),
  
  sidebarPanel(
  numericInput('faren', 'Farenheit Degrees F',32,min=0,max=500,step=5),
  submitButton('Submit')
    ),
  
mainPanel(
  h3('Equivalent Degree Celsius'),
  h4('You entered'),
  verbatimTextOutput("inputValue"),
  h4('which predicts'),
  verbatimTextOutput("prediction")
  )
  
  
 ))
```

<!--html_preserve--><div class="container-fluid">
<div class="row">
<div class="col-sm-12">
<h1>Farenheit to Celsius Prediction</h1>
</div>
</div>
<div class="row">
<div class="col-sm-4">
<form class="well">
<div class="form-group shiny-input-container">
<label for="faren">Farenheit Degrees F</label>
<input id="faren" type="number" class="form-control" value="32" min="0" max="500" step="5"/>
</div>
<div>
<button type="submit" class="btn btn-primary">Submit</button>
</div>
</form>
</div>
<div class="col-sm-8">
<h3>Equivalent Degree Celsius</h3>
<h4>You entered</h4>
<pre id="inputValue" class="shiny-text-output"></pre>
<h4>which predicts</h4>
<pre id="prediction" class="shiny-text-output"></pre>
</div>
</div>
</div><!--/html_preserve-->

---

## server.R for server side processing

```r
library(shiny)
f2c<-function(faren) (faren-32)*5/9

shinyServer(
  function(input,output){
    output$inputValue<- renderPrint({input$faren})
    output$prediction<- renderPrint({f2c(input$faren)})
    
    
  }
  )
```

---

## Running FtoC

```r
faren<-32 #default value, otherwise it assumes the value inputted by the user
faren<-(faren-32)*5/9
faren
```

```
## [1] 0
```
---



