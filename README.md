# Carbon-Emission-Analysis

`SELECT product_name, SUM(carbon_footprint_pcf)
FROM product_emissions
GROUP BY product_name
ORDER BY SUM(carbon_footprint_pcf) DESC
LIMIT 1`
