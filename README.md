# OKX Automated Grid Trading Bot

This is a Python-based automated trading program designed specifically for the OKB-USDT trading pair on the OKX exchange. The program employs a grid trading strategy, aiming to capture market volatility by dynamically adjusting the grid and position size, and includes a built-in risk management mechanism.

## Core Functions

* **Automated Grid Trading**: Executes grid buy/sell strategies for the OKB-USDT trading pair.

* **Dynamic Grid Adjustment**: Automatically adjusts the grid size based on market volatility (GRID_PARAMS in `config.py`).

* **Risk Management**:

* Maximum Drawdown Limit (MAX_DRAWDOWN)

* Daily Loss Limit (DAILY_LOSS_LIMIT)

* Maximum Position Size Limit (MAX_POSITION_RATIO)

* **Web User Interface**: Provides a simple web interface (via `web_server.py`) for real-time monitoring of trading status, account information, orders, and configuration adjustments.

* **State Persistence**: Saves transaction state to a JSON file in the `data/` directory for recovery after restart.

* **Push Notifications**: Sends important event and error notifications (`PUSHPLUS_TOKEN`) via PushPlus.

* **Logging**: Detailed runtime logs are recorded in the `trading_system.log` file.

## Environment Requirements

* Python 3.8+

* See the `requirements.txt` file for dependencies.

* **Minimum Server Configuration Recommendations**:

* CPU: 1 core or more (2 cores recommended)

* Memory: 512MB or more (1GB or 2GB recommended)

* Disk Space: 500MB available space

* Operating System: Windows, Linux, or macOS

* Network: Must be able to access the OKX API and PushPlus (if notifications are enabled)

* Network Recommendation: Low-latency networks are recommended, such as those in Japan.

## Installation Steps

1. **Clone the repository**:

``bash

git clone https://github.com/tingxifa/okx-grid-bot

cd okx-grid-bot

```

2. **Create and activate the virtual environment**:

* **Windows**:

``bash

python -m venv .venv

.\.venv\Scripts\activate

```

* **Linux / macOS**:

``bash

python3 -m venv .venv

source .venv/bin/activate

```

3. **Install dependencies**:

``bash

pip install -r requirements.txt

```

## Configuration

1. **Create the `.env` file**:

Create a file named `.env` in the project root directory.

2. **Configure Environment Variables**:

Add the following necessary environment variables to your `.env` file and fill in your information:

``dotenv

# OKX API (Required)

OKX_API_KEY=YOUR_OKX_API_KEY

OKX_SECRET_KEY=YOUR_OKX_SECRET_KEY

OKX_PASSPHRASE=YOUR_OKX_PASSPHRASE

# PushPlus Token (Optional, used for push notifications)

PUSHPLUS_TOKEN=YOUR_PUSHPLUS_TOKEN

# Initial Settings (Optional, affects first run and statistics)

# If not set, INITIAL_PRINCIPAL and INITIAL_BASE_PRICE default to 0

INITIAL_PRINCIPAL=1000.0 # Your initial total assets (USDT)

INITIAL_BASE_PRICE=600.0 # Your appropriate initial benchmark price (used to determine direction on initial launch)

``` **Important:** Ensure your OKX API Key has spot trading permissions, but **do not** enable withdrawal permissions.

3. **Adjust Trading Parameters (Optional)**:

You can modify the parameters in the `config.py` file according to your strategy needs, for example:

* `BASE_SYMBOL` : 'OKB' # Base currency

* `QUOTE_SYMBOL` : 'USDT' # Pricing currency

* `INITIAL_GRID`: Initial grid size (%)

* `MIN_TRADE_AMOUNT`: Minimum trade amount (USDT)

* `MAX_POSITION_RATIO`, `MIN_POSITION_RATIO`: Maximum/minimum position sizing

* Risk parameters (`MAX_DRAWDOWN`, `DAILY_LOSS_LIMIT`)

* Volatility to grid correspondence (`GRID_PARAMS['volatility_threshold']`)

## Running

Run the main program in the root directory of the project in the activated virtual environment:

```bash python` main.py

```

After the program starts, it will connect to the exchange, initialize its state, and execute trading logic.

## Docker Deployment

Before deployment, please configure the environment variables in the `.env` file according to the instructions above.

``bash

# Pull the code

# (Skip if you have already completed the above steps)

git clone https://github.com/tingxifa/okx-grid-bot

cd okx-grid-bot

# Deploy the image

docker-compose up -d

```

*If you need to customize the port, please modify the port mapping in `docker-compose.yml`.*

## Web Interface

After the program starts, a web server will run automatically. You can access the following address through a browser to monitor and manage the trading bot:

`http://127.0.0.1:58080`

*Note: The port number (58080) is defined in `web_server.py`. If you cannot access it, please check this file. *

The web interface allows you to view your current status, account balance, positions, pending orders, and historical records, and may offer some manual operation or configuration adjustment functions.

## Logs

The program's runtime logs will be output to the console and simultaneously recorded in the `trading_system.log` file in the project root directory.

## Precautions

* **Trading Risks**: All trading decisions are executed automatically by the program, but the market inherently carries risks. Please ensure you understand the strategy principles and potential risks, and bear the consequences of your trades yourself. It is not recommended to invest large sums of money without fully understanding and testing.

* **API Key Security**: Keep your API Key and Secret safe and do not disclose them to others.

* **Configuration Appropriateness**: Ensure that the configurations in `config.py` and `.env` meet your expectations and risk tolerance.

## Contributions

Pull Requests or Issues are welcome to improve the project.

## Acknowledgements

This project is adapted from the [GridBNB-USDT](https://github.com/EBOLABOY/GridBNB-USDT) project. Special thanks to [@EBOLABOY](https://github.com/EBOLABOY) for providing this excellent open-source project.
