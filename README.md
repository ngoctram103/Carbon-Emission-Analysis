# 1. Introduction
## What is the project about?
![cover](https://raw.githubusercontent.com/ngoctram103/cover/bb7385936f58a4ff66d94953f309b73849232879/cover.jpg "cover")

Photo by Chris LeBoutillier (unsplash.com)

This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.
## Data Source: Where Our Data Comes From
Our dataset is compiled from publicly available data from nature.com and encompasses the product carbon footprints (PCF) for various companies. PCFs represent the greenhouse gas emissions associated with specific products, quantified in CO2 (carbon dioxide equivalent)
## Data Structure
The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.

![Diagram](https://raw.githubusercontent.com/ngoctram103/cover/refs/heads/main/Database%20diagram.png "Diagram")
# 2. Tables description
## Table 'product_emissions'
### Câu lệnh lấy 3 dòng của bảng 'product_emissions'
```sql
SELECT *
FROM product_emissions
LIMIT 3
```
### Kết quả
| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 
## Table 'industry_groups'
### Câu lệnh lấy 3 dòng của bảng 'industry_groups'
```sql
SELECT *
FROM industry_groups
LIMIT 3
```
### Kết quả
| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 
## Table 'companies'
### Câu lệnh lấy 3 dòng của bảng 'companies'
```sql
SELECT *
FROM companies
LIMIT 3
```
### Kết quả
| id | company_name               | 
| -: | -------------------------: | 
| 1  | "Autodesk, Inc."           | 
| 2  | "Casio Computer Co., Ltd." | 
| 3  | "Cisco Systems, Inc."      | 
## Table 'countries'
### Câu lệnh lấy 3 dòng của bảng 'countries'
```sql
SELECT *
FROM countries
LIMIT 3
```
### Kết quả
| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 
