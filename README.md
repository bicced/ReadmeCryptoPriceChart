# readme-crypto-price-chart

A minimal implementation for live crypto price charts embedded directly in your README. The prices are sourced from CoinGecko's free public APIs and periodically updated using GitHub workflows. The chart is constructed using mermaid.js

<!-- CHART_START -->
*Chart will be dynamically inserted here.*
<!-- CHART_END -->

## How to Set Up

To set up this project:

1. **Create a Workflow**: Add a `main.yml` file in the `.github/workflows` directory of your repository.

2. **Ensure Write Permissions**: Make sure your repository has the necessary permissions to update the README file. Under the repository's - Settings > Actions > General > Workflow permissions

3. **Customize Your Setup**:
   - You can modify settings in the `main.yml` file

### Yaml Configuration (`main.yml`)

Inside the `main.yml` file, you can the set configurations

```yaml
  on:
  schedule:
    - cron: '0 0 */1 * *' # Runs once every day

  jobs:
    update-readme:
      steps:
      - name: Fetch Chart data
        env: 
          TITLE: WETH/USDC # Title of the chart
          CHAIN: eth # Chain - eth/bsc/polygon_pos/avax/movr/cro/one/boba/ftm/bch, check entire list: https://api.geckoterminal.com/api/v2/networks
          POOL: '0x88e6a0c2ddd26feeb64f039a2c41296fcb3f5640' # Pool pair address
          TIMEFRAME: day # Timeframe - day/hour/minute
          AGGREGATE: 1 # Aggregate options - day: [1], hour: [1, 4, 12] minute: [1, 5, 15]
          LIMIT: 365 # Limit - 100 to 1000, changing this may require modification to code below to fit the data
```

## How It Works

1. **Data Fetching**: The script fetches the latest crypto prices from CoinGecko's API.

2. **Data Processing**: It formats the data and inserts it into the README between the `<!-- CHART_START -->` and `<!-- CHART_END -->` tags.

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

