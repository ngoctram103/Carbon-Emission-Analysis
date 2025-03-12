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

# 3. Research
### Câu 1: Which products contribute the most to carbon emissions?
```sql
SELECT product_name, ROUND(AVG(carbon_footprint_pcf),2) AS avg_pcf
FROM product_emissions
GROUP BY product_name
ORDER BY avg_pcf DESC
LIMIT 10
```
#### Kết quả
| product_name                                                                                                                       | avg_pcf    | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00 | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00 | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00 | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00 | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00  | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00  | 
| TCDE                                                                                                                               | 99075.00   | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00   | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00   | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00   | 
### Câu 2: What are the industry groups of these products?
```sql
SELECT pe.product_name, ig.industry_group, ROUND(AVG(carbon_footprint_pcf),2) AS avg_pcf
FROM product_emissions pe
JOIN industry_groups ig ON pe.industry_group_id=ig.id
GROUP BY product_name
ORDER BY avg_pcf DESC
LIMIT 10
```
#### Kết quả
| product_name                                                                                                                       | industry_group                     | avg_pcf    | 
| ---------------------------------------------------------------------------------------------------------------------------------: | ---------------------------------: | ---------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3718044.00 | 
| Wind Turbine G132 5 Megawats                                                                                                       | Electrical Equipment and Machinery | 3276187.00 | 
| Wind Turbine G114 2 Megawats                                                                                                       | Electrical Equipment and Machinery | 1532608.00 | 
| Wind Turbine G90 2 Megawats                                                                                                        | Electrical Equipment and Machinery | 1251625.00 | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | Automobiles & Components           | 191687.00  | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | Materials                          | 167000.00  | 
| TCDE                                                                                                                               | Materials                          | 99075.00   | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | Automobiles & Components           | 91000.00   | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | Automobiles & Components           | 85000.00   | 
| Mercedes-Benz SL (SL 350)                                                                                                          | Automobiles & Components           | 72000.00   | 

### Câu 3: What are the industries with the highest contribution to carbon emissions?
```sql
SELECT ig.industry_group, ROUND(AVG(carbon_footprint_pcf),2) AS avg_pcf
FROM product_emissions pe
JOIN industry_groups ig ON pe.industry_group_id=ig.id
GROUP BY industry_group
ORDER BY avg_pcf DESC
LIMIT 10
```
#### Kết quả
| industry_group                                   | avg_pcf   | 
| -----------------------------------------------: | --------: | 
| Electrical Equipment and Machinery               | 891050.73 | 
| Automobiles & Components                         | 35373.48  | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 24162.00  | 
| Capital Goods                                    | 7391.77   | 
| Materials                                        | 3208.86   | 
| "Mining - Iron, Aluminum, Other Metals"          | 2727.00   | 
| Energy                                           | 2154.80   | 
| Chemicals                                        | 1949.03   | 
| Media                                            | 1534.47   | 
| Software & Services                              | 1368.94   | 
### Câu 4:What are the companies with the highest contribution to carbon emissions?
```sql
SELECT c.company_name, ROUND(AVG(pe.carbon_footprint_pcf),2) AS avg_pcf
FROM product_emissions pe
JOIN companies c ON pe.company_id=c.id
GROUP BY company_name
ORDER BY avg_pcf DESC
LIMIT 10
```
#### Kết quả
| company_name                           | avg_pcf    | 
| -------------------------------------: | ---------: | 
| "Gamesa Corporación Tecnológica, S.A." | 2444616.00 | 
| "Hino Motors, Ltd."                    | 191687.00  | 
| Arcelor Mittal                         | 83503.50   | 
| Weg S/A                                | 53551.67   | 
| Daimler AG                             | 43089.19   | 
| General Motors Company                 | 34251.75   | 
| Volkswagen AG                          | 26238.40   | 
| Waters Corporation                     | 24162.00   | 
| "Daikin Industries, Ltd."              | 17600.00   | 
| CJ Cheiljedang                         | 15802.83   | 
### Câu 5:What are the countries with the highest contribution to carbon emissions?
```sql
SELECT co.country_name, ROUND(AVG(pe.carbon_footprint_pcf),2) AS avg_pcf
FROM product_emissions pe
JOIN countries co ON pe.country_id=co.id
GROUP BY country_name
ORDER BY avg_pcf DESC
LIMIT 10
```
#### Kết quả
| country_name | avg_pcf   | 
| -----------: | --------: | 
| Spain        | 699009.29 | 
| Luxembourg   | 83503.50  | 
| Germany      | 33600.37  | 
| Brazil       | 9407.61   | 
| South Korea  | 5665.61   | 
| Japan        | 4600.26   | 
| Netherlands  | 2011.91   | 
| India        | 1535.88   | 
| USA          | 1332.60   | 
| South Africa | 1119.27   | 
### Câu 6: What is the trend of carbon footprints (PCFs) over the years?
```sql
SELECT year, ROUND(SUM(avg_pcf),2) AS sum_pcf_by_year
FROM (
  	SELECT year, product_name, AVG(carbon_footprint_pcf)AS avg_pcf
  	FROM product_emissions
  	GROUP BY year, product_name) AS non_dup_product
GROUP BY year
ORDER BY year
LIMIT 10
```
#### Kết quả
| year | sum_pcf_by_year | 
| ---: | --------------: | 
| 2013 | 496005.50       | 
| 2014 | 548213.50       | 
| 2015 | 10810407.00     | 
| 2016 | 1608962.17      | 
| 2017 | 224799.67       | 
### Câu 7: Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?
```sql
WITH raw_data AS (
	SELECT 	ndp.year,
			ig.industry_group,
			ROUND(SUM(ndp.avg_pcf),2) AS sum_pcf_by_year
	FROM (
  		SELECT year, product_name, industry_group_id, AVG(carbon_footprint_pcf)AS avg_pcf
  		FROM product_emissions pe
	  	GROUP BY year, product_name, industry_group_id) AS ndp
  	JOIN industry_groups ig ON ndp.industry_group_id=ig.id
	GROUP BY year, industry_group)
SELECT 	raw_data.industry_group,
		SUM(last_y.sum_pcf_by_year - raw_data.sum_pcf_by_year) AS delta
FROM raw_data
LEFT JOIN raw_data last_y ON raw_data.year - 1=last_y.year AND raw_data.industry_group = last_y.industry_group
GROUP BY industry_group
HAVING delta IS NOT NULL
ORDER BY delta
```
#### Kết quả
| industry_group                                   | delta       | 
| -----------------------------------------------: | ----------: | 
| Automobiles & Components                         | -1274644.00 | 
| Capital Goods                                    | -34826.00   | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | -7944.00    | 
| Software & Services                              | -687.00     | 
| Consumer Durables & Apparel                      | -263.00     | 
| Telecommunication Services                       | -131.00     | 
| Retailing                                        | 0.00        | 
| Food & Staples Retailing                         | 771.00      | 
| "Food, Beverage & Tobacco"                       | 1075.50     | 
| Commercial & Professional Services               | 2489.00     | 
| Media                                            | 7837.00     | 
| Technology Hardware & Equipment                  | 42404.33    | 
| Materials                                        | 82503.00    | 
