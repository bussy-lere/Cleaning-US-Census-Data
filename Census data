import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import codecademylib3_seaborn
import glob

us_census = glob.glob("states*.csv")

df_list = []
for filename in us_census:
  data = pd.read_csv(filename)
  df_list.append(data)                                  
us_census = pd.concat(df_list)

us_census['Income'] = us_census['Income'].replace('[\$]', '', regex=True)
us_census['Income'] = pd.to_numeric(us_census['Income'])

split_gender = us_census['GenderPop'].str.split('_', expand=True)

us_census['Men'] = split_gender[0].str.split('(\d+)', expand = True)[1]

us_census['Women'] = split_gender[1].str.split('(\d+)', expand = True)[1]

us_census.Women = pd.to_numeric(us_census.Women)

us_census.Men = pd.to_numeric(us_census.Men)

difference = us_census.TotalPop - us_census.Men

us_census.Women = us_census.Women.fillna(value = difference)
                                        
# finding duplicates
duplicates = us_census.duplicated()
print(duplicates.value_counts())
# dropping duplicates
us_census = us_census.drop_duplicates()
duplicates = us_census.duplicated()
print(duplicates.count())
#Plotting the scatterplot
plt.scatter(us_census.Women, us_census.Income)
plt.show()



countries = ['Hispanic', 'White', 'Black', 'Native', 'Asian', 'Pacific']


# print(us_census.dtypes)
for country in countries:
  us_census[country] = us_census[country].replace('[\%]', '', regex = True)
  us_census[country] = pd.to_numeric(us_census[country])
  us_census[country] = us_census[country].fillna(value = us_census[country].mean())
  plt.hist(us_census[country], bins = 10)
  plt.show()
print(us_census.head())
