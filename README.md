# co2-emissions-data-analysis
Once uploaded the repo, run the `Co2 emissions Analysis.ipynb` file
You will find a cell asking for the csv file 
```python
file_upload = files.upload()
```
You can download the file [here](https://drive.google.com/file/d/1bYWfWoPAaLSjiHQwQhHSYikSCqJYDGCM/view?usp=share_link "here")

## Handling missing values
 
You will find that the whole dataset have several missing values as shown in the figure below
![image](https://user-images.githubusercontent.com/50804224/200028164-d545e154-a953-4844-92e0-edee8b670f6d.png)
The graph shows white space for the values that are missing for every column, the table below show in numbers what is the total missing values and the representation of these missing values for total values for every column

|                      |iso_code   |country|year|co2        |consumption_co2|co2_growth_prct|co2_growth_abs|trade_co2  |co2_per_capita|consumption_co2_per_capita|share_global_co2|cumulative_co2|share_global_cumulative_co2|co2_per_gdp|consumption_co2_per_gdp|co2_per_unit_energy|coal_co2   |cement_co2|flaring_co2|gas_co2    |oil_co2    |other_industry_co2|cement_co2_per_capita|coal_co2_per_capita|flaring_co2_per_capita|gas_co2_per_capita|oil_co2_per_capita|other_co2_per_capita|trade_co2_share|share_global_cement_co2|share_global_coal_co2|share_global_flaring_co2|share_global_gas_co2|share_global_oil_co2|share_global_other_co2|cumulative_cement_co2|cumulative_coal_co2|cumulative_flaring_co2|cumulative_gas_co2|cumulative_oil_co2|cumulative_other_co2|share_global_cumulative_cement_co2|share_global_cumulative_coal_co2|share_global_cumulative_flaring_co2|share_global_cumulative_gas_co2|share_global_cumulative_oil_co2|share_global_cumulative_other_co2|total_ghg  |ghg_per_capita|methane    |methane_per_capita|nitrous_oxide|nitrous_oxide_per_capita|population |gdp        |primary_energy_consumption|energy_per_capita|energy_per_gdp|
|----------------------------|-----------|-------|----|-----------|---------------|---------------|--------------|-----------|--------------|--------------------------|----------------|--------------|---------------------------|-----------|-----------------------|-------------------|-----------|----------|-----------|-----------|-----------|------------------|---------------------|-------------------|----------------------|------------------|------------------|--------------------|---------------|-----------------------|---------------------|------------------------|--------------------|--------------------|----------------------|---------------------|-------------------|----------------------|------------------|------------------|--------------------|----------------------------------|--------------------------------|-----------------------------------|-------------------------------|-------------------------------|---------------------------------|-----------|--------------|-----------|------------------|-------------|------------------------|-----------|-----------|--------------------------|-----------------|--------------|
|Total missing values        |3256       |0      |0   |1255       |21228          |273            |1619          |21228      |1897          |21228                     |1255            |1255          |1255                       |9815       |21443                  |16063              |8016       |12956     |20822      |16359      |4665       |23205             |12986                |8344               |20823                 |16369             |5023              |23205               |21228          |12956                  |8016                 |20822                   |16359               |4665                |23205                 |12956                |8016               |20822                 |16359             |4665              |23205               |12956                             |8016                            |20822                              |16359                          |4665                           |23205                            |19996      |20049         |19993      |20047             |19993        |20047                   |2326       |11666      |16514                     |16523            |18401         |
|Total missing values in percentage|0.129185844|0      |0   |0.049793684|0.842247262    |0.010831614    |0.064235836   |0.842247262|0.075265831   |0.842247262               |0.049793684     |0.049793684   |0.049793684                |0.389422314|0.850777654            |0.637319473        |0.318044755|0.51404539|0.826138708|0.649063641|0.185089668|0.920687193       |0.515235677          |0.331058562        |0.826178384           |0.649460403       |0.199293763       |0.920687193         |0.842247262    |0.51404539             |0.318044755          |0.826138708             |0.649063641         |0.185089668         |0.920687193           |0.51404539           |0.318044755        |0.826138708           |0.649063641       |0.185089668       |0.920687193         |0.51404539                        |0.318044755                     |0.826138708                        |0.649063641                    |0.185089668                    |0.920687193                      |0.793366132|0.795468973   |0.793247104|0.795389621       |0.793247104  |0.795389621             |0.092286939|0.462863038|0.655213458               |0.655570544      |0.730082527   |


To see the total missing values of every column separeted by country, you will find this cell
```python
summary_val.to_csv('values_missing.csv', encoding='utf-8', index=False)
summary_per.to_csv('values_missing_percentage.csv', encoding='utf-8', index=False)
```
These two lines of code store:
1. A table with a sum of total values missing by country for all the columns stored in a .csv file called `values missing.csv` 
2. A table with a percentage of total values missing by country for all the columns stored in a .csv file called `values_missing_percentage.csv` 

### Deleting some data
The figure below show the countries that has more than 60% of missing values in total 
![image](https://user-images.githubusercontent.com/50804224/200085203-b8e62240-ac46-4dfd-af0c-15ca17263d51.png)

The figure above shows that these countries with huge amount of missing values are mainly located in Central America, Africa and Oceania. If this data is shown in numbers the next figure show the percentage of total missing values by country with more than 60%
![image](https://user-images.githubusercontent.com/50804224/200085255-18752e15-63c6-40b5-9024-c2d9dc4381a5.png)

#### Are these countries important to the whole world emissions?

[According to a research of our world in data](https://ourworldindata.org/co2-emissions "co2 emissions according to a research show in our world in data"), these countries not represent a meaningful impact on the total amount of emissions and other features related damaging the ozone layer, so that's why in the analysis this data is removed 

### Replacing missing values

The figure below shows the China example in scatter plots for all dataset characteristics impacting the global environment over the years
![image](https://user-images.githubusercontent.com/50804224/200086544-47a93f33-87b5-4642-8a58-c573eb03774f.png)
These plots show a meaningful characteristic for almost every single column in the dataset, there exist a **trend** this is why a function is built to replace the values missing in the dataset by an **interpolation** of the data for every column separated by **country**

The figure below show the China example with the missing values already filled following the approach already mentioned
![image](https://user-images.githubusercontent.com/50804224/200089362-2e1e34ec-ff91-404e-933f-bc0cc8788ef4.png)
