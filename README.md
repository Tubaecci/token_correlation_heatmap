# Crypto Token Correlation Heatmap

This project analyzes and visualizes the correlation between multiple cryptocurrency tokens using historical price data from the CoinGecko Pro API.

## Features

- Fetch historical price data for any set of tokens
- Calculate log returns and token volatility
- Generate a correlation heatmap for selected tokens
- Save and load processed data for fast analysis

## Project Structure

```
token_heatmap/
├── Database/                # Saved data files (e.g., joblib)
├── Notebooks/               # Jupyter notebooks for data processing and analysis
│   ├── 01_data.ipynb        # Data fetching and preparation
│   └── token_correlation.ipynb # Correlation and visualization
├── token_heatmap/           # Source code and .env file
│   └── .env                 # API key for CoinGecko Pro
├── requirements.txt         # Python dependencies
```

## Setup

1. **Clone the repository**

2. **Install dependencies**
   ```
   pip install -r requirements.txt
   ```

3. **Add your CoinGecko Pro API key**
   - Create a `.env` file in the `token_heatmap` folder:
     ```
     GECKO_API=your_api_key_here
     ```

## Usage

1. **Fetch and save token price data**
   - Run `01_data.ipynb` to fetch historical prices for your chosen tokens and save the DataFrame.

2. **Analyze correlations**
   - Open `token_correlation.ipynb` to load the saved data, calculate log returns, volatility, and plot the correlation heatmap.

## Example

```python
# Fetch prices for Bitcoin, Ethereum, and Solana
token_ids = ["bitcoin", "ethereum", "solana"]
api_key = os.getenv("GECKO_API")
df_prices = fetch_token_prices(token_ids, api_key=api_key)
```

```python
# Plot correlation heatmap
corr = df_prices.pct_change().apply(lambda x: np.log1p(x)).corr()
sns.heatmap(corr, annot=True, cmap='coolwarm', vmin=-1, vmax=1)
plt.title("Token Correlation Heatmap")
plt.show()
```

## Requirements

- Python 3.8+
- requests
- pandas
- numpy
- matplotlib
- seaborn
- python-dotenv
- joblib

## License

MIT License

---

**Note:** Keep your `.env` file private and do not commit it to version control.
