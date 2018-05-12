HEROES-OF-PYMOLI

OBSERVED TREND 1: There is a 81% Male Population of Players which creates the overall increase in Item sales, which was a total of $1867.68.

OBSERVED TREND 2: Within the Player population, the age group that caused this huge spike in purchse counts were between 16 and 25 year olds. Taking the bigger count at 39% is mostly 21-25 year age groups.

OBSERVED TREND 3: As we dive into more detail regarding the players, there are some top spenders amonst the group that are purchasing more than 2 or 3 games at a total purchase value $9+. These games that are hot ticket items are: Betrayal, Whisper of Grieving Widows and Arcane Gem.

```python
# Dependencies
import pandas as pd
import json
```


```python
#Name of json file
json_file = "purchase_data.json"
```


```python
#Read json file
with open(json_file, 'r') as datafile:
    datastore = json.load(datafile)

```


```python
#Convert list into DataFrames
df_gamers = pd.DataFrame(datastore)
df_gamers.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>SN</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>38</td>
      <td>Male</td>
      <td>165</td>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
      <td>Aelalis34</td>
    </tr>
    <tr>
      <th>1</th>
      <td>21</td>
      <td>Male</td>
      <td>119</td>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
      <td>Eolo46</td>
    </tr>
    <tr>
      <th>2</th>
      <td>34</td>
      <td>Male</td>
      <td>174</td>
      <td>Primitive Blade</td>
      <td>2.46</td>
      <td>Assastnya25</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>1.36</td>
      <td>Pheusrical25</td>
    </tr>
    <tr>
      <th>4</th>
      <td>23</td>
      <td>Male</td>
      <td>63</td>
      <td>Stormfury Mace</td>
      <td>1.27</td>
      <td>Aela59</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Print List of columns in DataFrame
df_gamers.columns
```




    Index(['Age', 'Gender', 'Item ID', 'Item Name', 'Price', 'SN'], dtype='object')




```python
###PLayer Count
#total number of Players
total_num_players = df_gamers["SN"].count()
total_num_players

total_df = pd.DataFrame({
    "Total Number of Players": [total_num_players]
})
total_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Number of Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>780</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Selecting specific Column information for review and calculations.
reduced_column_A = df_gamers.loc[:, ["Item Name","Price"]]
reduced_column_A.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Bone Crushing Silver Skewer</td>
      <td>3.37</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Stormbringer, Dark Blade of Ending Misery</td>
      <td>2.32</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Primitive Blade</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Final Critic</td>
      <td>1.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Stormfury Mace</td>
      <td>1.27</td>
    </tr>
  </tbody>
</table>
</div>




```python
###Purchasing Analysis (Total)

#Calculations of Unique Items, No. Purchases, Avg of Purchases and Total Revenue
#into new DataFrame with column formatting
unique_items = len(reduced_column_A["Item Name"].unique())
unique_items

#caluculation og Average Prices
avg_price = reduced_column_A["Price"].mean()
avg_price

#calculation of total number of Purchases
num_purchases_df = reduced_column_A["Item Name"].count()
num_purchases_df

#calculations of total Price
total_price = reduced_column_A["Price"].sum()
total_price

#create a new DataFrame to hold all calculations
purchasing_df = pd.DataFrame({
    "Number of Unique Items": [unique_items],
    "Average Purchase Price": [avg_price],
    "Total Number of Purchases": [num_purchases_df],
    "Total Revenue": [total_price]
})  

#format columns
purchasing_df["Average Purchase Price"] = purchasing_df["Average Purchase Price"].map("${:.2f}".format)
purchasing_df["Total Revenue"] = purchasing_df["Total Revenue"].map("${:.2f}".format)
purchasing_df

purchasing_df[["Number of Unique Items","Average Purchase Price","Total Number of Purchases","Total Revenue"]].head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Purchase Price</th>
      <th>Total Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>179</td>
      <td>$2.93</td>
      <td>780</td>
      <td>$2286.33</td>
    </tr>
  </tbody>
</table>
</div>




```python
###Gender Demographics

#Grouping the DataFrame by "Gender"
gender_group = df_gamers.groupby("Gender")
gender_group["Gender"].count()

#create new DataFrame for Item Name counts
gender_overall = pd.DataFrame(gender_group["Item Name"].count())
gender_overall.head()

#rename column
gender_overall = gender_overall.rename(
    columns={"Item Name": "Total Count"})
gender_overall.head()

#reset Index
gender_overall = gender_overall.reset_index()
gender_overall.head()

#calculations for Gender Percentage
total_gen_players = df_gamers["Gender"].count()
total_gen_players

count_per_gender = gender_group["Gender"].count()
count_per_gender

#create new DataFrame of Gender Percentage
gender_percent = pd.DataFrame((count_per_gender/total_gen_players)*100)
gender_percent.head()

gender_percent = gender_percent.rename(
    columns={"Gender": "Percentage of Players"})
gender_percent.head()

gender_percent = gender_percent.reset_index()
gender_percent.head()

#merge DataFrames into one by Gender
gender_overall = gender_overall.merge(gender_percent, on="Gender")

#format columns
gender_overall = gender_overall[["Gender","Percentage of Players","Total Count"]]
gender_overall.head()

gender_overall["Percentage of Players"] = gender_overall["Percentage of Players"].map("{:.2f}".format)
gender_overall.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Gender</th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Female</td>
      <td>17.44</td>
      <td>136</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Male</td>
      <td>81.15</td>
      <td>633</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Other / Non-Disclosed</td>
      <td>1.41</td>
      <td>11</td>
    </tr>
  </tbody>
</table>
</div>




```python
###Purchasing Analysis (Gender)

#create a new Data Frame for calculations
purch_group = pd.DataFrame(df_gamers)
purch_group.head()

#Calculations for Total Price Purchase
gen_purch_total = purch_group.groupby(["Gender"]).sum()["Price"]


#Calculations for Average Count
gen_avg_count = purch_group.groupby(["Gender"]).mean()["Price"]


#Calculations for Total Gender count
gen_counts = purch_group.groupby(["Gender"]).count()["Price"]



# Calculate Normalized Purchasing
gen_norm_total_purchase = gen_total_purchase["Price"].sum()
gen_norm_total_purchase

gen_norm_count = gen_purchase_count["Gender"].count()
gen_norm_count

normalized_total = gender_purchase_total / gen_norm_count
normalized_total

# Convert to DataFrame

gender_summary = pd.DataFrame({"Purchase Count": gen_counts,
                                 "Average Purchase Price": gen_avg_count,
                                 "Total Purchase Value": gen_purch_total,
                              "Normalized Totals": normalized_total
                              })

#Format columns
gender_summary["Average Purchase Price"] = gender_summary["Average Purchase Price"].map("${:,.2f}".format)
gender_summary["Total Purchase Value"] = gender_summary["Total Purchase Value"].map("${:,.2f}".format)
gender_summary["Normalized Totals"] = gender_summary["Normalized Totals"].map("${:,.2f}".format)
gender_summary = gender_summary.loc[:, ["Purchase Count", "Average Purchase Price", "Total Purchase Value", "Normalized Totals"]]
gender_summary
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Female</th>
      <td>136</td>
      <td>$2.82</td>
      <td>$382.91</td>
      <td>$2.82</td>
    </tr>
    <tr>
      <th>Male</th>
      <td>633</td>
      <td>$2.95</td>
      <td>$1,867.68</td>
      <td>$2.95</td>
    </tr>
    <tr>
      <th>Other / Non-Disclosed</th>
      <td>11</td>
      <td>$3.25</td>
      <td>$35.74</td>
      <td>$3.25</td>
    </tr>
  </tbody>
</table>
</div>




```python
###Age Demographics

#create table grouped by bins
# Create the bins in which Data will be held over 4 years

#create new DataFrame to support Bins and groups
BIN_df = pd.DataFrame(df_gamers)
BIN_df

#create table grouped by bins
# Create the bins in which Data will be held over 4 years
bins = [0, 10, 15, 20, 25, 30, 35, 40, 100]
age_ranges = ['<10', '11-15', '16-20', '21-25', '26-30', '31-35', '36-40', '40+']

#create groups to have placed into age_range groups by Age
BIN_df['Age Range'] = pd.cut(BIN_df["Age"], bins, labels=age_ranges)
BIN_df

#Group by Age Range
age_group = BIN_df.groupby("Age Range").count()
age_group["Age"].count()

#create a new DataFrame to store groups
age_overall = pd.DataFrame(age_group["Age"])
age_overall.head()

#rename column as Total Count
age_overall = age_overall.rename(
    columns={"Age": "Total Count"})
age_overall

#reset the Index
age_overall = age_overall.reset_index()
age_overall

#Calculations of Group Precent by Age
total_age_players = BIN_df["Age"].count()
total_age_players

count_per_age = age_group["Age"].count()
count_per_age

age_group_percent = pd.DataFrame((age_group["Age"]/total_age_players)*100)
age_group_percent.head()

#rename column within DataFrame
age_group_percent = age_group_percent.rename(
    columns={"Age": "Percentage of Players"})
age_group_percent

age_group_percent = age_group_percent.reset_index()
age_group_percent

#Merge the Datasets into one by Age Range
age_overall = age_overall.merge(age_group_percent, on="Age Range")

#rearrange columns
age_overall = age_overall[["Age Range","Percentage of Players","Total Count"]]
age_overall.head()

#format column
age_overall["Percentage of Players"] = age_overall["Percentage of Players"].map("{:.2f}".format)
age_overall




```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Age Range</th>
      <th>Percentage of Players</th>
      <th>Total Count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>&lt;10</td>
      <td>4.10</td>
      <td>32</td>
    </tr>
    <tr>
      <th>1</th>
      <td>11-15</td>
      <td>10.00</td>
      <td>78</td>
    </tr>
    <tr>
      <th>2</th>
      <td>16-20</td>
      <td>23.59</td>
      <td>184</td>
    </tr>
    <tr>
      <th>3</th>
      <td>21-25</td>
      <td>39.10</td>
      <td>305</td>
    </tr>
    <tr>
      <th>4</th>
      <td>26-30</td>
      <td>9.74</td>
      <td>76</td>
    </tr>
    <tr>
      <th>5</th>
      <td>31-35</td>
      <td>7.44</td>
      <td>58</td>
    </tr>
    <tr>
      <th>6</th>
      <td>36-40</td>
      <td>5.64</td>
      <td>44</td>
    </tr>
    <tr>
      <th>7</th>
      <td>40+</td>
      <td>0.38</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python
BIN_df.groupby("Age Range").sum()["Price"]
```




    Age Range
    <10       96.62
    11-15    224.15
    16-20    528.74
    21-25    902.61
    26-30    219.82
    31-35    178.26
    36-40    127.49
    40+        8.64
    Name: Price, dtype: float64




```python
###Purchasing Analysis by Age

#Calculations for Total Price Purchase
age_total_purchase = BIN_df.groupby(["Age Range"]).sum()["Price"]


#Calculations for Average Count
age_avg_overall = BIN_df.groupby(["Age Range"]).mean()["Price"]


#Calculations for Total Purchase count
age_purchase_count = BIN_df.groupby(["Age Range"]).count()["Price"]



# Calculate Normalized Purchasing
age_normalized_total = age_total_purchase / age_purchase_count
age_normalized_total

# Convert to DataFrame

age_summary = pd.DataFrame({"Purchase Count": age_purchase_count,
                                 "Average Purchase Price": age_avg_overall,
                                 "Total Purchase Value": age_total_purchase,
                              "Normalized Totals": age_normalized_total
                              })

#Format columns
age_summary["Average Purchase Price"] = age_summary["Average Purchase Price"].map("${:,.2f}".format)
age_summary["Total Purchase Value"] = age_summary["Total Purchase Value"].map("${:,.2f}".format)
age_summary["Normalized Totals"] = age_summary["Normalized Totals"].map("${:,.2f}".format)
age_summary = age_summary.loc[:, ["Purchase Count", "Average Purchase Price", "Total Purchase Value", "Normalized Totals"]]
age_summary


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Normalized Totals</th>
    </tr>
    <tr>
      <th>Age Range</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>&lt;10</th>
      <td>32</td>
      <td>$3.02</td>
      <td>$96.62</td>
      <td>$3.02</td>
    </tr>
    <tr>
      <th>11-15</th>
      <td>78</td>
      <td>$2.87</td>
      <td>$224.15</td>
      <td>$2.87</td>
    </tr>
    <tr>
      <th>16-20</th>
      <td>184</td>
      <td>$2.87</td>
      <td>$528.74</td>
      <td>$2.87</td>
    </tr>
    <tr>
      <th>21-25</th>
      <td>305</td>
      <td>$2.96</td>
      <td>$902.61</td>
      <td>$2.96</td>
    </tr>
    <tr>
      <th>26-30</th>
      <td>76</td>
      <td>$2.89</td>
      <td>$219.82</td>
      <td>$2.89</td>
    </tr>
    <tr>
      <th>31-35</th>
      <td>58</td>
      <td>$3.07</td>
      <td>$178.26</td>
      <td>$3.07</td>
    </tr>
    <tr>
      <th>36-40</th>
      <td>44</td>
      <td>$2.90</td>
      <td>$127.49</td>
      <td>$2.90</td>
    </tr>
    <tr>
      <th>40+</th>
      <td>3</td>
      <td>$2.88</td>
      <td>$8.64</td>
      <td>$2.88</td>
    </tr>
  </tbody>
</table>
</div>




```python
###Top Spenders

#group by SN
SN_group = df_gamers.groupby("SN")
SN_group

#Total Price Purchase by SN
top_spend_total_purch = SN_group["Price"].sum()
top_spend_total_purch.head()

#Average Purchase by SN
top_spend_avg_purch = SN_group["Price"].mean()
top_spend_avg_purch.head()

#Total Purchase Count by SN
top_spend_purch_count = SN_group["Price"].count()
top_spend_purch_count.head()

#consolidate all tables
top_spend_summary = pd.DataFrame({"Purchase Count": top_spend_purch_count,
                                 "Average Purchase Price": top_spend_avg_purch,
                                 "Total Purchase Value": top_spend_total_purch})

#format columns and sort them by Total Purchase Value
top_spend_summary["Average Purchase Price"] = top_spend_summary["Average Purchase Price"].map("${:.2f}".format)
top_spend_summary
top_spend_summary["Total Purchase Value"] = top_spend_summary["Total Purchase Value"].map("${:.2f}".format)
top_spend_summary
top_spend_summary = top_spend_summary[["Purchase Count", "Average Purchase Price", "Total Purchase Value"]]
top_spend_summary.sort_values(by=["Total Purchase Value"], ascending=False).head()


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Qarwen67</th>
      <td>4</td>
      <td>$2.49</td>
      <td>$9.97</td>
    </tr>
    <tr>
      <th>Sondim43</th>
      <td>3</td>
      <td>$3.13</td>
      <td>$9.38</td>
    </tr>
    <tr>
      <th>Tillyrin30</th>
      <td>3</td>
      <td>$3.06</td>
      <td>$9.19</td>
    </tr>
    <tr>
      <th>Lisistaya47</th>
      <td>3</td>
      <td>$3.06</td>
      <td>$9.19</td>
    </tr>
    <tr>
      <th>Tyisriphos58</th>
      <td>2</td>
      <td>$4.59</td>
      <td>$9.18</td>
    </tr>
  </tbody>
</table>
</div>




```python
###Popular Items

#Group multiple columns for overall count
grouped_items = df_gamers.groupby(['Item ID', 'Item Name'])
grouped_items.count()

#Total Price Purchase by Item ID and Item Name
item_total_purch = grouped_items["Price"].sum()
item_total_purch.head()

#Average Price Purchase by Item ID and Item Name
item_avg_purch = grouped_items["Price"].mean()
item_avg_purch.head()

#Total Purchase Count by Item ID and Item Name
item_purch_count = grouped_items["Price"].count()
item_purch_count.head()

#create a new DataFrame with all above variables
item_summary = pd.DataFrame({"Purchase Count": item_purch_count,
                                 "Item Price": item_avg_purch,
                                 "Total Purchase Value": item_total_purch})

#format columns and sort by Purchase Count
item_summary["Item Price"] = item_summary["Item Price"].map("${:.2f}".format)
item_summary
item_summary["Total Purchase Value"] = item_summary["Total Purchase Value"].map("${:.2f}".format)
item_summary
item_summary = item_summary[["Purchase Count", "Item Price", "Total Purchase Value"]]
item_summary.sort_values(by=["Purchase Count"], ascending=False).head()


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>39</th>
      <th>Betrayal, Whisper of Grieving Widows</th>
      <td>11</td>
      <td>$2.35</td>
      <td>$25.85</td>
    </tr>
    <tr>
      <th>84</th>
      <th>Arcane Gem</th>
      <td>11</td>
      <td>$2.23</td>
      <td>$24.53</td>
    </tr>
    <tr>
      <th>31</th>
      <th>Trickster</th>
      <td>9</td>
      <td>$2.07</td>
      <td>$18.63</td>
    </tr>
    <tr>
      <th>175</th>
      <th>Woeful Adamantite Claymore</th>
      <td>9</td>
      <td>$1.24</td>
      <td>$11.16</td>
    </tr>
    <tr>
      <th>13</th>
      <th>Serenity</th>
      <td>9</td>
      <td>$1.49</td>
      <td>$13.41</td>
    </tr>
  </tbody>
</table>
</div>




```python
###Most Profitable Items

#Use same DataFrame from above to create same output of table information
item_summary = pd.DataFrame({"Purchase Count": item_purch_count,
                                 "Item Price": item_avg_purch,
                                 "Total Purchase Value": item_total_purch})

#Format columns and sort by Total Purchase Value
item_summary["Item Price"] = item_summary["Item Price"].map("${:.2f}".format)
item_summary
item_summary["Total Purchase Value"] = item_summary["Total Purchase Value"].map("${:.2f}".format)
item_summary
item_summary = item_summary[["Purchase Count", "Item Price", "Total Purchase Value"]]
item_summary.sort_values(by=["Total Purchase Value"], ascending=False).head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>170</th>
      <th>Shadowsteel</th>
      <td>5</td>
      <td>$1.98</td>
      <td>$9.90</td>
    </tr>
    <tr>
      <th>21</th>
      <th>Souleater</th>
      <td>3</td>
      <td>$3.27</td>
      <td>$9.81</td>
    </tr>
    <tr>
      <th>37</th>
      <th>Shadow Strike, Glory of Ending Hope</th>
      <td>5</td>
      <td>$1.93</td>
      <td>$9.65</td>
    </tr>
    <tr>
      <th>127</th>
      <th>Heartseeker, Reaver of Souls</th>
      <td>3</td>
      <td>$3.21</td>
      <td>$9.63</td>
    </tr>
    <tr>
      <th>120</th>
      <th>Agatha</th>
      <td>5</td>
      <td>$1.91</td>
      <td>$9.55</td>
    </tr>
  </tbody>
</table>
</div>


