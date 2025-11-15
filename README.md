# British Literary Prizes Explorer

**This is an interactive web application built with R Shiny to explore data on British literary prizes awarded from 1990 to 2022.**

**The data is loaded directly from the Post45 Data Collective's GitHub Repository.**

## 🚀 Core Features

-   The application is organized into three main tabs:

### 📊 1. Data Explorer

**Interactive Table:** Uses the DT package to display the full raw data. Users can sort, search, and paginate through the data.

**Filter Functions:**

**- Year Range:** Set a desired time period using a slider.

**- Prize Name:** Filter by one or more selected prizes.

**- Author:** Filter by one or more selected authors.

### 📈 2. Winners Over Time

**Line Chart:** Uses ggplot2 to generate a line chart showing the number of winners per year for selected prizes.

**Filter Functions:**

**- Year Range:** Set the period for analysis.

**- Prize Name:** Select the prizes to display on the chart (Defaults: Booker Prize, Women's Prize).

### 🏆 3. Top Winners

**Bar Chart:** Uses ggplot2 to create a horizontal bar chart showing the authors with the most prize wins, in descending order.

**Filter Functions:**

**- Year Range:** Set the period for calculating the rankings.

**- Prize Name:** Aggregate rankings for specific prizes or "All Prizes".

**- Show Top N:** Define the number of winners to display (e.g., Top 10, Top 20).

## 🔧 How the Code Works

**This app runs from a single app.R file, containing both the UI and Server logic.**

### 1. Load and Prepare Data

-   Reads data directly from the URL using readr::read_csv.

-   **(Important)** Uses dplyr::rename to change complex original column names (e.g., prize_name, prize_year, name) to simpler names for use within the app (e.g., Prize, Year, Author).

-   Prepares filter values (lists of authors, prizes) using unique().

### 2. UI (User Interface)

-   Applies the shinytheme("flatly") to improve the app's design.

-   Uses navbarPage to create the 3-tab structure.

-   Each tab uses sidebarLayout to place filters (inputs) on the left and results (outputs) on the right.

-   Input Widgets: sliderInput, selectizeInput, numericInput

-   Output Widgets: DT::dataTableOutput, plotOutput

### 3. Server (Logic)

-   Uses reactive() expressions (e.g., filtered_data_explore, filtered_data_time, filtered_data_top) to dynamically filter data based on user input.

-   These reactive blocks automatically re-run whenever a user changes a filter selection, updating the data.

-   Tab 1: DT::renderDataTable renders the reactive data into an interactive table.

-   Tab 2 & 3: renderPlot uses ggplot2 to redraw the visualizations (line chart, bar chart) based on the updated data.
