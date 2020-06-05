# Code repository for Leverage Efficiency paper

This project contains the python codes used to generate the results in the [arxiv paper](https://arxiv.org/abs/1101.4548) on leverage efficiency. Fundamentally,the calculations involve calculating optimal leverage values for pairs of
assets, one considered "risky", the other considered "riskless".
Examples of risky assets include the SP500 index, Bitcoin, shares etc.
Examples of assets that are considered riskless include cash deposited with the
Federal Reserve, 10-year US Treasury Bonds, 10-year German Government Bonds.

# How to run the code

    python workflow.py config_default.yaml

# Data sets

Input data sets are times eries containing the historical levels or returns for
various assets.
A number of publicly available data sets are provided in the folder data/1-source.
Instructions on how to add new data sources are in the wiki.
Each asset is assigned a key code string which is use to refer to it both in
the code and in the config files that control the code.
The keys for the data sets provided with the repository and a brief description
of the corresponding data set is here:

## "Risky" assets

key | data set | Source
--- | --- | ---
SP500 | SP500 real time price index | https://finance.yahoo.com/quote/%5ESPX/history?p=%5ESPX
SP500TR | SP500 Total Return index (accounting for dividends) | https://finance.yahoo.com/quote/%5ESP500TR/history/
BTC | Bitcoin | https://finance.yahoo.com/quote/BTC-USD/history?p=BTC-USD and https://www.coindesk.com/price/bitcoin
BRK | Berkshire Hathaway shares | https://finance.yahoo.com/quote/BRK-A/history?p=BRK-A
MAD | Madoff ponzi scheme | http://lml.org.uk/wp-content/uploads/2019/12/madoff.csv
DAX | DAX performance index | https://finance.yahoo.com/quote/%5EGDAXI/history?p=%5EGDAXI

## "Riskless" assets
key | data set | Source
--- | --- | ---
FED | Federal Reserve overnight rates | https://fred.stlouisfed.org/series/FEDFUNDS and https://t.co/FDm5p3P828?amp=1
DGS10 | 10-year US Treasury bonds | https://fred.stlouisfed.org/series/DGS10
IRDE | Immediate Rates: Less than 24 Hours: Call Money/Interbank Rate for Germany | https://fred.stlouisfed.org/series/IRSTCI01DEM156N

# Description of individual pipeline stages

The code is divided into several stages, each of which can be run independently
if you don't want to recalculate everything:

* extract.py
* transform.py
* update.py
* analysis.py
* plots.py

# Details of project structure

![Structure of the code](/docs/project_structure.png)
