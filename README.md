# Account Takeover Classification

This repository contains a machine learning pipeline designed to classify whether an attempted login is fraudulent or legitimate, using factors such as time and location.

## Dataset

The dataset used for this project is the **Risk-Based Assessment** dataset, which can be found [here](https://riskbasedauthentication.org/analysis/largescale/#-data-set).  
Due to its large size, the dataset could not be uploaded to this repository. Please download the dataset and place it in the same directory as the project files for proper functionality.

## Feature Encoding

The following techniques were employed to preprocess and encode features:

- **Timestamp Conversion**: Timestamps are transformed into cyclical features using sine and cosine values for both the day of the year and the hour of the day.
- **IP Address Encoding**: IP addresses are encoded as four separate numerical values, following the approach outlined in the paper *"Encoding IP Address as a Feature for Network Intrusion Detection"* by Enchun Shao. You can access the paper [here](https://hammer.purdue.edu/articles/thesis/Encoding_IP_Address_as_a_Feature_for_Network_Intrusion_Detection/11307287?file=20040305).
- **Dropped Features**: Features such as round-trip time, cities, and regions are dropped due to excessive missing values.
- **One-Hot Encoding**: Categorical features like country and device type are one-hot encoded.
- **OS and Browser Factorization**: Instead of splitting operating system (OS) and browser names/versions into multiple features—which introduced excessive noise—these are factorized as single combined features.
- **User Agent**: User agent strings are factorized for simplicity.

## Target

The target variable is **"Is Account Takeover"**, which is either `True` (T) or `False` (F).  

Due to the rarity of account takeover events in the dataset (only 141 rows out of 31,269,264, or approximately 0.00045%), the following considerations were made:
- A **stratified train/test split** ensures that the rare target is appropriately distributed across training and testing sets.
- The evaluation metric used is **ROC-AUC**, which is well-suited for imbalanced datasets.

## Future Improvements

To enhance the model's accuracy and usability, the following improvements could be explored:

1. **Latitudinal and Longitudinal Features**: Incorporating latitude and longitude as feature columns, potentially inferred from IP addresses or obtained using a dataset with more comprehensive city and region data.
2. **Better Target Distribution**: Acquiring a dataset with a higher proportion of account takeover events for more effective training.
3. **Expanded Dataset Availability**: Publicly available datasets for risk-based authentication (RBA) are limited. Collaborations or synthetic data generation may help overcome this limitation.

---

This project demonstrates the potential for machine learning models to combat account takeover fraud effectively, despite the challenges posed by imbalanced datasets and feature sparsity.
