# WebApp Ativos Brazil

[This](https://gabrielmelo.shinyapps.io/shiny_webapp_finances/) is a Shiny web application that allows you to analyze stock data for Brazilian assets. The application retrieves data from Yahoo Finance and provides interactive charts for the selected asset.

## Dependencies

The following packages are required to run the application:

- shiny
- quantmod
- readxl

Make sure to install these packages before running the application.

## Installation

1. Clone the repository or download the code files.

2. Ensure that the required dependencies are installed.

3. Run the following code in R to launch the application:

4. You can edit using your own list of assets or portfolio that you want to track. Simply create your own list in an excel file such as [YahooTickersBrazil](YahooTickersBrazil.xlsx).

```R
library(shiny)
library(quantmod)
library(readxl)
source("server.R")

# Load the stock ticker data
YahooTickersBrazil <- read_excel("YahooTickersBrazil.xlsx")

# Define the user interface (UI)
ui <- fluidPage(
  titlePanel("WebApp Ativos Brasil"),
  sidebarLayout(
    sidebarPanel(
      helpText("Selecione o ativo que deseja analisar. A informação será coletada do Yahoo Finanças."),
      selectInput("symb", 
                  label = "Symbol", 
                  choices = unique(YahooTickersBrazil$Symbol),
                  selected = "PETR4.SA"),
      
      dateRangeInput("dates",
                     "Date range",
                     start = "2020-01-01",
                     end = as.character(Sys.Date())),
      HTML("
        <h6>Autor: <a href='https://github.com/melogabriel' target='_blank'>github.com/melogabriel</a></h6>
        <h6>e-mail: <a href='mailto:gabriel-melo@outlook.com'>gabriel-melo@outlook.com</a></h6>
      ")
    ),
    
    mainPanel(plotOutput("plot"))
  )
)

# Run the app
shinyApp(ui, server)
```

## Usage

If you want to follow this list of Brazilian assets, you can go to (https://gabrielmelo.shinyapps.io/shiny_webapp_finances/) and use my app.

- Select the desired asset from the dropdown list.
- Specify the date range for the data.
- The application will retrieve the stock data and display an interactive chart.

![](webapp_ativos_brazil.gif)

## About this project 

This project was developed as part of the Data Science course of the Master's Degree in Administration at the Postgraduate Programme in Administration at the Fluminense Federal University (PPGAd-UFF).

Feel free to contact the author for any questions or feedback.
