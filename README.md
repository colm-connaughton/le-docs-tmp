# Code repository for Leverage Efficiency paper

This project contains the python codes used to produce the data analyses and
figures in the [arxiv paper](https://arxiv.org/abs/1101.4548) on leverage efficiency. Fundamentally, the calculations involve calculating optimal leverage values for pairs of
assets, one considered "risky", the other considered "riskless".
Examples of risky assets include the SP500 index, Bitcoin, shares etc.
Examples of assets that are considered riskless include cash deposited with the
Federal Reserve, 10-year US Treasury Bonds, 10-year German Government Bonds.

# Data

Input data sets are times series containing the historical levels or returns for
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

# How to run the code

The code reads in data on a number of different assets, performs various optimal
leverage calculations on asset pairs and produces some numbers and plots for
each pair. It is structured as a pipeline with each pipeline stage performing
a distinct step in the analysis. A master python script called `workflow.py` runs
the entire pipeline from beginning to end. A config file is used to provide control over
the assets to be read in, the asset pairs to be analysed and the plots to be
produced. The config file can also be used to turn on and off individual
pipeline stages.

To run the code, run the following command in the terminal:

    python workflow.py config_default.yaml

The config file config_default contains only a single asset pair. A few other
config files are provided:

* To produce all of the results appearing in the paper run

    ```python workflow.py config_manuscript.yaml```

* To analyse all of the data for multiple asset pairs run

    ```python workflow.py config_run_all.yaml```

The latter can take a while since the variable window calculations are
slow - especially for the longer time series.

The config files are written in [yaml](https://kapeli.com/cheat_sheets/YAML.docset/Contents/Resources/Documents/index) format. Yaml is intended to be human-readable so
the config files should be fairly self-explanatory.

# Description of individual pipeline stages

The code is divided into several stages, each of which can be run independently
if you don't want to recalculate everything. Filenames for assets and pairs are
derived from the keys listed in the data tables above.

* `extract.py`

   Reads csv files containing historical asset time series data from the folder
   `data/1-source/` and converts them into a standard pandas dataframe format.
   These are then written in pickle format to the folder `data/2-intermediate/`.
   The standard dataframe has column names 'level' and/or 'return' and is indexed by a pandas `DateTimeIndex`. Missing values are interpolated so that the resulting dataframe has either daily or monthly frequency.

* `transform.py`

   Calculates the returns if only levels were provided. Converts annual rates of
   return (usually for interest rates) to daily or monthly returns. This stage reads
   the asset data from the pickles in the folder `data/2-intermediate/` and writes the final
   input data files into the folder `data/4-load/``

* `update.py`

   Not implemented yet. A future version of this will provide functionality to
   automatically update the time series with more recent data from online
   sources.

* `analysis.py`

   Performs all the calculations for the asset pairs specified in the config file.
   Asset time series are read from the folder `data/4-load/` and results of analyses
   for different pairs are written to the folder `data/5-analysis/`.

* `plots.py`

  Creates all the figures. Inputs are taken from the folder `data/5-analysis/`
  and pdf figures are written to the folder `data/6-figures/`.

# Details of project structure

![Structure of the code](/docs/project_structure.png)
