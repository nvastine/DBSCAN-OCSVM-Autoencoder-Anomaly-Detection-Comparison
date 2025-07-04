# DBSCAN, OCSVM, Autoencoder Anomaly Detection Comparison
This project compared three anomaly detection methods on unlabeled, time-series NYC Taxi reporting: unsupervised density-based clustering (DBSCAN), semi-supervised one class classification support vector machine (OCSVM), and an autoencoder method based on a threshold reconstruction loss. 


![Data Exploration](Images/Exploratory_Data_Analysis.png)

The models are assessed on two datasets: an hourly-aggregate binning taxi volume per hour, and a daily-aggregate binning taxi volume per day. Further feature engineering was performed to retain time-series context including rolling averages, rate of change, and cyclic encoding of time features. 

![Feature Engineering](Images/Feature_Engineering.png)

Models were tuned to achieve a qualitatively justified 10-15% anomaly rate, and visually evaluated using taxi volume vs. time plots and PCA/t-SNE visualizations. 

All three models performed similarly on the simpler daily-aggregated data. OCSVM was easier to interpret on hourly-aggregated data than the other methods. OCSVM labeled hourly-aggregated data anomalies grouped by day (ie entire days of hourly data was marked as anomalous more often than individual hours), while DBSCAN and the autoencoder appeared to mark anomalies primarily in high variance commute windows (ie harder to predict taxi volume at 8 AM due to higher variance). The differences in model performance was explained by evaluating feature importance using the resulting anomaly labels in a Random Forest classifier. The models had similar feature importance in daily-aggregates which explained their similar results. However, DBSCAN and the autoencoder used count more heavily than OCSVM in hourly-aggregates, perhaps explaining the hourly variation. OCSVM instead relied on daily rolling average and rate of change in the hourly-aggregates, explaining its ability to label entire days as anomalies in the hourly-aggregated data. Of the tested methods, all three appeared suitable on the simpler day-aggregated data. OCSVM seemed most robust on the more complex hour-aggregated data. 

![OCSVM Anomalies](Images/OCSVM_Anomalies.png)

Future work may consider other features from the dataset to differentiate anomalies, evaluate the methods on labeled anomaly data for easier comparison, and compare algorithm performance to long short-term memory (LSTM) recurrent neural networks (RNN) designed for time-series data.
