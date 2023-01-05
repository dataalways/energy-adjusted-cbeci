# Adjusting the Cambridge Bitcoin Electricity Consumption Index for US Energy Prices


| Source | Date | Latest Reading |
|:------------------------------------|:---------------------------------------------|:---------------------------------------------|
| [Cambridge Bitcoin Electricity Consumption Index (CBECI)](https://ccaf.io/cbeci/index) | 2023-01-04 | 93.8 TWh per year |
| CBECI Adjusted for Electricity Prices | 2023-01-04 | 83.5 TWh per year |


--- 

Last data updates:
- Cambridge Bitcoin Electricity Consumption Index: Jan 4, 2022
- US Energy Information Administration: Jan 4, 2022 (data to October 2022)

---

The Cambridge Bitcoin Electricity Consumption Index is the gold standard of models for tracking the power utilization of the Bitcoin Network, but it is not without flaws. One of these flaws is the model's assumption of constant global electricity prices ($0.05 per kWh). In the current energy shortage, the world is faced with rapidly rising electricity prices and the model must be adjusted.

![rising_electricity_prices]

The attached Jupyter Notebook leverages data available from the US Energy Information Administration and the availability of CBECI data for various energy price assumptions to model the expected network power usage over time for the given price data. 

The data finds that although average US industrial electricity prices discounted by 27% to best-match the historic $0.05 per kWh assumption from Cambridge, has historically lined up well with the data, the values in 2022 differ dramatically, suggesting that the CBECI is currently overestimating the electricity demand that the network can support by as much as 20%.

![adjusted_cbeci]


## Usage

If the latest dataset is stale, you should update both the CBECI and EIA data. 

To update the CBECI data:
- Run the Jupyter Notebook titled `generate-cambridge-data.ipynb`
- The data will be automatically downloaded and saved into the `datasets` directory.

To update the EIA data: 
- Go to the following link to access [EIA data](https://www.eia.gov/electricity/data/browser/#/topic/7?agg=0,1&geo=g&endsec=2&linechart=ELEC.PRICE.US-IND.M&columnchart=ELEC.PRICE.US-IND.M&map=ELEC.PRICE.US-IND.M&freq=M&start=201001&ctype=map&ltype=pin&rtype=s&pin=&rse=0&maptype=0)
- Scroll down and ensure that the slider near the top of the table has the latest date selected
- Hit the `DOWNLOAD` dropdown and select `Table (CSV)` 
- Copy the downloaded .csv file into the datasets folder replacing the stale dataset previously contained.
- Run the `energy-adjusted-cbeci.ipynb` or test scripts to generate new figures

## Limitations

- The CBECI data is only available at $0.01 increments, therefore energy price data in between these increments had to be linearly interpolated.
- The US Energy Information Administration data postings are generally a couple months delayed, so for recent estimates this script forward fills energy prices (assumes them to have not changed since the last data point), which makes the last couple months of data unstable and may also lose seasonal variations.


[rising_electricity_prices]: ./tmp-figures/electricity-rates.png
[adjusted_cbeci]: ./tmp-figures/cbeci-adjusted-recent.png