# My-Firstrandomnumberplotting
This an assigment for the products development course in Coursera
What is Shiny?

Shiny is a web application framework for R.
Shiny allows you to create a graphical interface so that users can interact with your visualizations, models, and algorithms without needed to know R themselves.
Using Shiny, the time to create simple, yet powerful, web-based interactive data products in R is minimized.
Shiny is made by the fine folks at R Studio.
Some Mild Prerequisites

Shiny doesn't really require it, but as with all web programming, a little knowledge of HTML, CSS and Javascript is very helpful.

HTML gives a web page structure and sectioning as well as markup instructions
CSS gives the style
Javscript for interactivity
Shiny uses Bootstrap (no relation to the statistics bootstrap) style, which (to me) seems to look nice and renders well on mobile platforms.

Availible Tutorials

If you're interested in learning more about HTML, CSS, and Javascript we recommend any one of the following resources:

Mozilla Developer Network Tutorials
HTML & CSS from Khan Academy
Tutorials from Free Code Camp
Getting Started

Make sure you have the latest release of R installed
If on Windows, make sure that you have Rtools installed
install.packages("shiny")
library(shiny)
Great tutorial at http://shiny.rstudio.com/tutorial/
Basically, this lecture is walking through that tutorial offering some of our insights
A Shiny project

A shiny project is a directory containing at least two files:

ui.R (for user interface) controls how your app looks.
server.R that controls what your app does.
Apps with Plots

Allowing users to manipulate data and to see the results of their manipulations as a plot can be very useful. Shiny provides the plotOutput() function for ui.R and the renderPlot() function for sever.R for taking user input and creating plots.

Plot App: ui.R Part 1

library(shiny)
shinyUI(fluidPage(
  titlePanel("Plot Random Numbers"),
  sidebarLayout(
    sidebarPanel(
      numericInput("numeric", "How Many Random Numbers Should be Plotted?", 
                   value = 1000, min = 1, max = 1000, step = 1),
      sliderInput("sliderX", "Pick Minimum and Maximum X Values",
                  -100, 100, value = c(-50, 50)),
# ...
Plot App: ui.R Part 2

# ...
      sliderInput("sliderY", "Pick Minimum and Maximum Y Values",
                  -100, 100, value = c(-50, 50)),
      checkboxInput("show_xlab", "Show/Hide X Axis Label", value = TRUE),
      checkboxInput("show_ylab", "Show/Hide Y Axis Label", value = TRUE),
      checkboxInput("show_title", "Show/Hide Title")
    ),
    mainPanel(
      h3("Graph of Random Points"),
      plotOutput("plot1")
    )
  )
))
Plot App: server.R Part 1

library(shiny)
shinyServer(function(input, output) {
  output$plot1 <- renderPlot({
    set.seed(2016-05-25)
    number_of_points <- input$numeric
    minX <- input$sliderX[1]
    maxX <- input$sliderX[2]
    minY <- input$sliderY[1]
    maxY <- input$sliderY[2]
# ...
Plot App: server.R Part 2

# ...
    dataX <- runif(number_of_points, minX, maxX)
    dataY <- runif(number_of_points, minY, maxY)
    xlab <- ifelse(input$show_xlab, "X Axis", "")
    ylab <- ifelse(input$show_ylab, "Y Axis", "")
    main <- ifelse(input$show_title, "Title", "")
    plot(dataX, dataY, xlab = xlab, ylab = ylab, main = main,
         xlim = c(-100, 100), ylim = c(-100, 100))
  })
})

https://derderi123456.shinyapps.io/My-Firstrandomnumberplottting/
