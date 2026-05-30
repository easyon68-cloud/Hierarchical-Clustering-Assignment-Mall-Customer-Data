# Hierarchical-Clustering-Assignment-Mall-Customer-Data
This assignment aims to utilize Hierarchical Clustering algorithms to analyze given datasets, extracting meaningful insights from their underlying structures.

Hierarchical Clustering - Mall Customer Segmentation
About the Project
This project applies Hierarchical Clustering on the Mall Customers dataset to group customers into segments based on their Annual Income and Spending Score. The goal is to find meaningful customer groups that can help the mall management make better business decisions.

Dataset
File: Mall_Customers.csv
Rows: 200
Columns: 5
ColumnDescriptionCustomerIDUnique ID for each customerGenderMale or FemaleAgeAge of the customerAnnual Income (k$)Annual income in thousandsSpending Score (1-100)Score assigned by the mall based on spending behavior

Libraries Used
pythonpandas
numpy
matplotlib
seaborn
scikit-learn
scipy
Install them using:
pip install pandas numpy matplotlib seaborn scikit-learn scipy

How to Run

Make sure Mall_Customers.csv is in the same folder as the script
Run the script:

python hierarchical_clustering.py

All plots and the output CSV will be saved in the same folder


Steps Followed
- Load and Explore the Data

Loaded the CSV using pandas
Checked the shape, data types, and null values
Printed basic statistics using .describe()

 - Exploratory Data Analysis (EDA)

Plotted histograms for Age, Income, and Spending Score
Scatter plot of Income vs Spending Score to see if clusters are visible
Boxplots to check for outliers
Bar chart for Gender distribution
Correlation heatmap

Observation: The scatter plot of Income vs Spending Score clearly shows 5 natural groups.
 - Feature Selection and Scaling

Selected Annual Income (k$) and Spending Score (1-100) as features
Applied StandardScaler to normalize the data
Scaling is important because hierarchical clustering uses Euclidean distance

 - Dendrogram

Built dendrograms using Ward, Complete, and Average linkage methods
The dendrogram helps decide how many clusters to use
Ward linkage gave the clearest separation

Observation: The largest gap in the Ward dendrogram appears when cutting at 5 clusters.
- Choosing the Number of Clusters

Used Silhouette Score to compare k = 2 to k = 8
Higher silhouette score = better-defined clusters

kSilhouette Score20.384230.461040.492650.5538 ✅60.538770.519880.4309
Best k = 5 (highest score)
- Applying Hierarchical Clustering

Used Ward linkage with k = 5
Applied fcluster to assign cluster labels
Plotted the result with 5 different colors

- Cluster Analysis

Computed average Age, Income, and Spending Score per cluster
Plotted bar charts to compare clusters

Cluster Summary:
ClusterCountAvg AgeAvg IncomeAvg SpendingCustomer Type13932.786.582.1High Income, High Spenders23241.089.415.6High Income, Low Spenders32125.325.180.0Low Income, High Spenders42345.226.320.9Low Income, Low Spenders58542.555.849.1Middle Income, Average Spenders
Step 8 - Save Output

Saved the dataset with cluster labels as mall_customers_with_clusters.csv


Output Files
FileDescriptioneda_distributions.pngHistograms for Age, Income, Spending Scoreeda_scatter.pngScatter plot of Income vs Spending Scoreeda_boxplots.pngBoxplots for all numeric featureseda_gender.pngGender distribution bar charteda_heatmap.pngCorrelation heatmapdendrogram_ward.pngDendrogram using Ward linkagedendrogram_complete.pngDendrogram using Complete linkagedendrogram_average.pngDendrogram using Average linkagesilhouette_scores.pngSilhouette score vs number of clustersfinal_clusters.pngFinal 5-cluster scatter plotcluster_profiles.pngBar charts of average features per clustermall_customers_with_clusters.csvDataset with cluster labels added

Conclusion
Hierarchical Clustering with Ward Linkage and k=5 successfully segmented the 200 mall customers into 5 distinct groups. The most valuable group for the mall is Cluster 1 (high income, high spending) which should be the main target for premium marketing. Cluster 2 (high income but low spending) is an opportunity group where targeted campaigns could increase engagement.
