# Cryptocurrencies

## Overview

Accountability Accounting, a prominent investment bank, is interested in offering a new cryptocurrency investment portfolio for its customers. In this analysis, a report will be created that includes what cryptocurrencies are on the trading market and how they could be grouped to create a classification system for this new investment. The data will need to be processed to fit the machine learning models. Since there is no known output for what to look for, unsupervised learning will be used. A clustering algorithm will be used to group the cryptocurrencies, and data visualizations will be used to share the findings.

## Results

Steps for analysis:
- Preprocessing the Data for PCA
- Reducing Data Dimensions Using PCA
- Clustering Cryptocurrencies Using K-means
- Visualizing Cryptocurrencies Results

### Preprocessing the data

- Read data into a DataFrame
- Drop the "IsTrading" column
- Remove the rows that have at least one null value
- Create a new DataFrame that only holds the names of the cryptocurrencies
- Use the get_dummies() method to create variables for the two text features, "Algorithm" and "ProofType" and store the results in a new DataFrame
```
# Use get_dummies() to create variables for text features.
X = pd.get_dummies(crypto_df, columns=['Algorithm', 'ProofType'])
X.head()
```
- Then, use the StandardScaler fit_transform() function to standardize the features from the new DataFrame
```
# Standardize the data with StandardScaler().
crypto_scaled = StandardScaler().fit_transform(X)
print(crypto_scaled[0:5])
```
### Reduce the data dimensions using PCA (Principal Component Analysis) algorithm

- Apply PCA to reduce the dimensions to three principal components
```
# Using PCA to reduce dimension to three principal components.
pca = PCA(n_components= 3)
crypto_pca = pca.fit_transform(crypto_scaled)
crypto_pca
```
- Create a new DataFrame and use the same index as the previous DataFrame and columns named "PC 1", "PC 2", and "PC 3"
```
# Create a DataFrame with the three principal components.
pcs_df = pd.DataFrame(data = crypto_pca, columns= ['pc1', 'pc2', 'pc3'],index= crypto_df.index)
pcs_df.head(10)
```

![image](https://user-images.githubusercontent.com/67409852/150661880-96770021-f96f-43fc-8f12-88db49193062.png)

### Clustering Cryptocurrencies Using K-means

- Using the previous DataFrame, create an elbow curve using hvPlot to find the best value for K

```

```
![image](https://user-images.githubusercontent.com/67409852/150661913-f25255bf-8562-46f8-b9aa-9f9d9673bf3f.png)

- Run the K-means algorithm to make predictions of the K clusters for the cryptocurrencies’ data
- Create a new DataFrame by concatenating the crypto_df and pcs_df DataFrames on the same columns
- Add another column named "Class" that will hold the predictions



![image](https://user-images.githubusercontent.com/67409852/150661955-dbaec1c0-d1d7-4a3c-a597-26ecaccdfce3.png)

![image](https://user-images.githubusercontent.com/67409852/150661993-5607220f-0327-4396-ac37-df036bee1f75.png)

![image](https://user-images.githubusercontent.com/67409852/150662058-adb818c3-de07-466a-be0b-cab118ca8f25.png)

![image](https://user-images.githubusercontent.com/67409852/150662026-4ab727c7-6856-42d2-99d7-62f99bff543b.png)

## Summary
