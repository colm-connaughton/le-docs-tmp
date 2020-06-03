# Code repository for Leverage Efficiency paper

This project contains the python codes used to generate the results in the [arxiv paper](https://arxiv.org/abs/1101.4548) on leverage efficiency. Fundamentally,the calculations involve calculating optimal leverage values for pairs of
assets, one considered "risky", the other considered "riskless". 
Examples of risky assets include the SP500 index, Bitcoin, shares etc. 
Examples of assets that are considered riskless include cash deposited with the
Federal Reserve, 10-year US Treasury Bonds, 10-year German Government Bonds.

# How to run the code

python workflow.py config_default.yaml

# Data sets

Input data sets are timeseries containing the historical levels or returns for
various assets.
A number of data sets are provided in the folder data/1-source.
Instructions on how to add new data sources are in the wiki.
Each asset is assigned a key code string which is use to refer to it both in 
the code and in the config files that control the code. 
The keys for the data sets provided with the repository and a brief description
of the corresponding data set is here:

# Description of individual pipeline stages
