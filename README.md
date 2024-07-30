# readme-crypto-price-chart

A minimal implementation for periodically updated live crypto price charts embedded directly in your README. The prices are sourced from CoinGecko's free public APIs and automatically updated using GitHub workflows.

## Chart Data
<!-- CHART_START -->
*Chart will be dynamically inserted here.*
<!-- CHART_END -->

## How to Set Up

To set up this project:

1. **Create a Workflow**: Add a `main.yml` file in the `.github/workflows` directory of your repository.

2. **Ensure Write Permissions**: Make sure your repository has the necessary permissions to update the README file.

3. **Customize Your Setup**:
   - You can modify settings in the `main.yml` file

### Yaml Configuration (`main.yml`)

Inside the `main.yml` file, you can the set configurations

```yaml
  on:
  schedule:
    - cron: '* * * * *' # Runs every minute, modify to change frequency

  jobs:
    update-readme:
      steps:
      - name: Fetch OHLCV data
        env: 
          TITLE: WETH/USDC #Specify the title of the chart
          CHAIN: eth #Specify the chain - eth/bsc/polygon_pos/avax/movr/cro/one/boba/ftm/bch, check entire list: https://api.geckoterminal.com/api/v2/networks
          POOL: '0x88e6a0c2ddd26feeb64f039a2c41296fcb3f5640' #Specify the pool address - currently WETH/USDC pool
          TIMEFRAME: day #Specify the timeframe - day/hour/minute
          AGGREGATE: 1 #Specify the aggregate options - day: [1], hour: [1, 4, 12] minute: [1, 5, 15]
          LIMIT: 365 #Specify the limit - 100 to 1000, changing may need some modification to code below to fit the data
```

## How It Works

1. **Data Fetching**: The script fetches the latest crypto prices from CoinGecko's API.

2. **Data Processing**: It formats the data and inserts it into the README between the `<!-- CHART_START -->` and `<!-- CHART_END -->` tags.

## Chart Data
```markdown
<!-- CHART_START -->
*Chart will be dynamically inserted here.*
<!-- CHART_END -->
```

3. **Automated Updates**: Using GitHub Actions, the script runs on a defined schedule (e.g., daily) to ensure the data remains current.

## Customization

- **Frequency**: Adjust the cron schedule in the workflow file to change how often the data updates.
- **API Data**: Modify the script to fetch different data points or crypto pools as needed.

## Contributions

Contributions are welcome! Please submit issues or pull requests with any improvements, new features, or bug fixes.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

