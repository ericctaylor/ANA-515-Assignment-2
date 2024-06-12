# ANA-515-Assignment-2

---
title: "New Voter Registration"
author: "Eric Carrieri Taylor"
date: "2024-06-12"
output:
  html_document: default
  pdf_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

### Section 1: Description of the Data

The dataset under analysis is focused on the registration of new voters across various jurisdictions in the United States. It measures the number of new registered voters each month from different jurisdictions, providing insights into voter registration trends over time. This data was collected to answer research questions related to electoral engagement, the impact of policy changes on voter registration, and demographic shifts in voter registration patterns.

### Section 2: Reading the Data into R

```{r}
# Load necessary packages
library(readr)

# Read the data into R
data <- read_csv("/Users/erictaylor/Downloads/New Voter Registration.csv")
```

### Section 3: Cleaning the Data

```{r}
# Load necessary packages
library(dplyr)

# Clean the data
# Rename columns for consistency and convert date columns to proper Date format
data <- data %>%
  rename(Jurisdiction = Jurisdiction,
         Year = Year,
         Month = Month,
         New_Registered_Voters = `New registered voters`)

# Convert Month to numeric, handling non-numeric values
# First, identify non-numeric values in the Month column
non_numeric_months <- data$Month[!grepl("^\\d+$", data$Month)]

# Print non-numeric values for inspection
print(non_numeric_months)

# Replace non-numeric months with NA
data$Month[!grepl("^\\d+$", data$Month)] <- NA

# Now convert Month to numeric
data$Month <- as.numeric(data$Month)

# Print the first few rows to verify
head(data)

```

### Section 4: Characteristics of the Data

This dataframe has `r nrow(data)` rows and `r ncol(data)` columns. The names of the columns and a brief description of each are in the table below:

```{r}
# Load necessary package for displaying table
library(knitr)

# Column names and descriptions
column_descriptions <- data.frame(
  Column_Name = c("Jurisdiction", "Year", "Month", "New_Registered_Voters"),
  Description = c("The region where the data was collected", 
                  "The year of data collection", 
                  "The month of data collection", 
                  "The number of new registered voters")
)

# Display the table
kable(column_descriptions, col.names = c("Column Name", "Description"))
```

### Section 5: Summary Statistics

```{r}
# Calculate summary statistics for selected columns
# Using summary functions to get min, max, mean, and number of missing values

# For column 'Year'
year_min <- min(data$Year, na.rm = TRUE)
year_max <- max(data$Year, na.rm = TRUE)
year_mean <- mean(data$Year, na.rm = TRUE)
year_missing <- sum(is.na(data$Year))

# For column 'Month'
month_min <- min(data$Month, na.rm = TRUE)
month_max <- max(data$Month, na.rm = TRUE)
month_mean <- mean(data$Month, na.rm = TRUE)
month_missing <- sum(is.na(data$Month))

# For column 'New_Registered_Voters'
new_reg_voters_min <- min(data$New_Registered_Voters, na.rm = TRUE)
new_reg_voters_max <- max(data$New_Registered_Voters, na.rm = TRUE)
new_reg_voters_mean <- mean(data$New_Registered_Voters, na.rm = TRUE)
new_reg_voters_missing <- sum(is.na(data$New_Registered_Voters))

# Output the results
list(
  Year = list(min = year_min, max = year_max, mean = year_mean, missing = year_missing),
  Month = list(min = month_min, max = month_max, mean = month_mean, missing = month_missing),
  New_Registered_Voters = list(min = new_reg_voters_min, max = new_reg_voters_max, mean = new_reg_voters_mean, missing = new_reg_voters_missing)
)


```
