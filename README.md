# CryptEx
## Python based engine for cryptocurrency trading - WINDOWS 10 only (sorry mac/linux users)

CryptEx allows you to:
 - create orders (market, limit, stop, trail) on various exchanges in one simple interface
 - keep track of your current and past positions
 - keep track of all your crypto assets
 - set alerts based on price crossing or price closing events

Based on ccxt library (https://github.com/ccxt/ccxt) for most of API calls, CryptEx provides user with clean (almost spartan) looking GUI. You can use CryptEx with or without direct acces to your accounts via API. If you chose to use it without API keys, you will still be able to see your positions across various exchanges but all inputs these will need to be manual. With API keys all your existing positions (if given exchange allows it) will be downloaded into CryptEx automatically.

## Updating to new version
Download latest release from https://github.com/LukasUlrych/CryptEx/releases/ and unpack the zip file. Now, before you delete the old version, it is absolutely vital that you copy folder **Data** (it can be found in folder **Auxilliary**) and store it somewhere safe, since it contains all your data. After tripple checking that you've really stored correct folder **Data**, you can delete the old version, unzip the new one and replace new folder Data with your old one.

## Getting started
Download latest release from https://github.com/LukasUlrych/CryptEx/releases/, unpack the zip file and start CryptEx.exe. If you are uncertain about that, you can check with https://www.virustotal.com/gui/ (or any antivirus of your choice) for any malware or viruses. There shouldn't be any :)

### Welcome screen
When you first run CryptEx, this is what will welcome you. Not much I admit.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/initial_screen.png?raw=true)

### Adding new exchanges
In the right panel click **Show settings -> Exchanges -> Add new exchange**

From the dropdown menu choose the exchange you want to add (in my instance it was Binance). If you want to add your API keys, this is the time. You need to log to your exchange account and generate it there. If you mess it up, don't worry, you can always create new one. Keep in mind, that some exchanges may have different naming conventions (**API key** is almost always the same, but **secret** here may be called something else there, as well as **password**, or it may be totally omitted, in which case API key is all you need).

Let me just say here, that I, nor anyone else (discounting the possibility that your computer gets hacked), have no way of seeing your API keys. CryptEx is run only locally on your pc.

The date setting box labeled **History reach** is there so you can determine how far into the past should CryptEx search for your closed orders. In most cases exchanges allow to go somewhere between 6 months and 5 years back. It varies.

If you're not sure if you want to add your API keys, that's ok, you don't have to.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/add_exchange.png?raw=true)

### Adding new pair
Having an exchange is only half the battle, now you need to download specific pairs you want to follow. If you have added your API keys in the step before, and clicked **Yes** when prompted about downloading your history, you probably already have some pairs imported. If not, well then ..

In the right panel click **Show settings -> Pairs -> Add new pair**

From the dropdown menus you first choose exchange (Binance here), then quote currency (USDT) and then base currency (BTC).

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/add_pair.png?raw=true)

### Changing graph
Now that you have added your first pair, you can see the chart by clicking **exchange - quote - base** in the top left menu. If promted, set the desired timeframe in the top menu of the chart frame.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/first_plot.png?raw=true)

### Watchlist
For quick acces you can pin current pair to watchlist by clicking **Add current** in left panel. Clicking **Remove current** removes it from watchlist. The **Change** column in watchlist refers to yesterday's closing price.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/watchlist.png?raw=true)

### New welcome screen
Now that you have added your first exchange and pair, you can finally set your welcome screen to something less ugly.

In the right panel click **Show settings -> Application -> Set initial graph** and take your pick.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/init_plot_settings.png?raw=true)

### Creating orders
This part is for you only if you have added API keys. In the right panel click **Create spot order** (there is a **Margin** button above, but that doesn't work yet). This opens a new window where you can see your current balances and last price changes (bid, ask). These labels are also 'clickable', for easier use.

#### Limit order
Should be pretty straightforward :) (the same goes for **Market** order type)

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/limit_order.png?raw=true)

#### Stop order
In CryptEx Stop order works as stop-market order, meaning that if the price crosses given **Stop price** level, a **Market** order (buy or sell) will be triggered. In the example below I am trying to sell 0.1 BTC for 40k, but setting my stop at 35k. Keep in mind, that stop orders are being checked locally, so CryptEx needs to be up and running for them to trigger.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/stop_order.png?raw=true)

### Trail order
In my implementation **Trail** order works like this:

I want to sell my 0.1 BTC at 40k but ideally above, with the possibility that it will go higher. So I set my **Trail** order at 40k with **Trail** equal to 5 - this means that once price touches 40k, trail order triggers and starts recording highest achieved price (starting from 40k). Once price falls further then 5% (**Trail**), market sell order gets triggered.

So, if price of BTC goes to 45k and then falls, sell order triggers at 45k * 0.95 = 42,750
If 40k is the top, sell order triggers at 40k * 0.95 = 38k
If 40k is not even reached, I've set a stop price, which triggers sell order at 35k (this can omitted by clicking **None**)
If you want to start **Trail order** immediately, click **Start now**
Next to **Trail** there is dropdown menu with Rel and % as choices - ingnore it, it doesn't do anything yet.

Again, keep in mind, that trail orders are also being checked locally, so CryptEx needs to be up and running for them to trigger.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/trail_order.png?raw=true)

### Switching frames
Depending on how adventurous you are, you might have stumbled upon it yourself, but let us assume you haven't. By clicking Tab key or clicking mouse wheel you get to the second main frame of CryptEx.

Here you can see
- Echange status - whether you should it expect to work or not
- Un-indexed closed orders (we'll get to what it means)
- Your open positions
- Your closed positions
- All your open orders
 
![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/tables_frame.png?raw=true)

### Closed orders into positions
If you already have some closed orders

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/closed_as_frame.png?raw=true)

## Exchange specific things
Although ccxt supports more than 100 exchanges I do not have the means nor the willpower to test CryptEx on all of them. Always be aware of the fact, that you are using this software of your own volition and that I am not responsible in any way for any possible harm that this usage might cause you.

Tested exchanges: **Binance, Kraken, KuCoin, Bittrex, Coinbase Pro, AscendEx, Huobi Pro, Poloniex**
- these I use or have used in the past, so everything should work fine here

Support for price websockets (real-time price updates): **Binance, Kraken, KuCoin, Bittrex, Coinbase Pro, AscendEx, Huobi Pro, HitBTC**
- other exchanges use price updates via API calls (way slower so stop and trail orders will be delayed)

Support for margin trading: **Kraken** - but use at your own peril (work in progress)

# FAQ (really a work in progress)
1. Something doesn't work as it used to - restart the application (wait at least 20 seconds)
2. I have inserted my API keys but I can't see my private data (wallet info, closed orders etc.)
- First, make sure you've inserted correct value to correct field. Most exchanges have **Key** and **Secret** named the same but some may not. Also, if given exchange doesn't show you any **Password** value for API keys, just leave it empty.
- If that doesn't help, try to sync your clock following e.g. this guide https://www.groovypost.com/howto/synchronize-clock-windows-10-with-internet-atomic-time/ This is a known issue with Binance that I have no way of correcting from my end. Sorry.
