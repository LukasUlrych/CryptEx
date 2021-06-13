# CryptEx
## Python based app for cryptocurrency trading - WINDOWS 10 only (sorry mac/linux users)

With CryptEx you:
 - have all crypto accounts accessible through one simple interface
   - no need to have multiple tabs open constantly
   - no need to navigate through various websites
 - can create market, limit, stop & trail orders
   - stop and trail orders supported even for exchanges without native implementation
   - open orders are tracked to see how close they are to execution
 - can keep track of your current and past positions
   - by grouping oders into positions you can follow your trading/investing performance
 - can keep track of all your crypto assets

Based on ccxt library (https://github.com/ccxt/ccxt) for most of API calls, CryptEx provides user with clean (almost spartan) looking GUI. You can use CryptEx with or without direct acces to your accounts via API. If you chose to use it without API keys, you will still be able to see your positions across various exchanges but all inputs will need to be manual. With API keys all your existing positions (if given exchange allows it) will be downloaded into CryptEx automatically.

## Updating to new version
Download latest release from https://github.com/LukasUlrych/CryptEx/releases/ and unpack the zip file. Now, before you delete the old version, it is absolutely vital that you copy folder **Data** (it can be found in folder **Auxilliary**) and store it somewhere safe, since it contains all your data. After tripple checking that you've really stored correct folder **Data**, you can delete the old version, unzip the new one and replace new folder Data with your old one.

## Getting started
Download latest release from https://github.com/LukasUlrych/CryptEx/releases/, unpack the zip file and start CryptEx.exe. If you are uncertain about that, you can check with https://www.virustotal.com/gui/ (or any antivirus of your choice) for any malware or viruses. There aren't any :)

### Welcome screen
When you first run CryptEx, this is what will welcome you. Not much I admit.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/initial_screen.png?raw=true)

### Adding new exchanges
In the right panel click **Show settings -> Exchanges -> Add new exchange**

From the dropdown menu choose the exchange you want to add (in my instance it was Binance). If you want to add your API keys, this is the time. You need to log to your exchange account and generate it there. If you mess it up, don't worry, you can always create new one. Keep in mind, that some exchanges may have different naming conventions (**API key** is almost always the same, but **secret** here may be called something else there, as well as **password**, or it may be totally omitted, in which case API key is all you need).

Let me just say here, that I, nor anyone else (discounting the possibility that your computer gets hacked), have no way of seeing your API keys. CryptEx is run only locally on your pc. If you're unsure how to create API keys (or what it is in the first palce), just google it :) It is nothing shady.

The date setting box labeled **History reach** is there so you can determine how far into the past should CryptEx search for your closed orders. In most cases exchanges allow to go somewhere between 6 months and 5 years back. It varies.

If you're not sure if you want to add your API keys, that's ok, you don't have to.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/add_exchange.png?raw=true)

### Adding new pair
Having an exchange is only half the battle, now you need to download specific pairs you want to follow. If you have added your API keys in the step before, and clicked **Yes** when prompted about downloading your history, you probably already have some pairs imported. If not, well then ..

In the right panel click **Show settings -> Pairs -> Add new pair**

From the dropdown menus you first choose exchange (Binance here), then quote currency (USDT) and then base currency (BTC). This setup will download BTC/USDT pair from Binance.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/add_pair.png?raw=true)

### Changing graph
Now that you have added your first pair, you can see the chart by clicking **exchange - quote - base** in the top left menu. If promted, set the desired timeframe in the top menu of the chart frame.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/first_plot.png?raw=true)

The smaller graph below the main one is the RSI indicator - currently this cannot be changed, maybe in the future.

### Watchlist
For quick acces you can pin current pair to watchlist by clicking **Add current** in left panel. Clicking **Remove current** removes it from watchlist. The **Change** column in watchlist refers to yesterday's closing price.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/watchlist.png?raw=true)

### New welcome screen
Now that you have added your first exchange and pair, you can finally set your welcome screen the way you want.

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

So, if price of BTC goes to 45k and then falls, sell order triggers at 45k * 0.95 = 42,750. 
If 40k is the top, sell order triggers at 40k * 0.95 = 38k. 
If 40k is not even reached, I've set a stop price, which triggers sell order at 35k (this can omitted by clicking **None**). 
If you want to start **Trail order** immediately, click **Start now**. 
Next to **Trail** there is dropdown menu with Rel and % as choices - ingnore it, it doesn't do anything yet.

Again, keep in mind, that trail orders are also being checked locally, so CryptEx needs to be up and running for them to trigger.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/trail_order.png?raw=true)

### Canceling open orders
By double clicking the order in **Open orders** table the same window opens up, but with the extra **Cancel** button.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/cancel_order.png?raw=true)

### Switching frames
Depending on how adventurous you are, you might have stumbled upon it yourself, but let us assume you haven't. By clicking Tab key or clicking mouse wheel you get to the second main frame of CryptEx.

Here you can see
- Echange status - whether you should it expect to work or not
- Un-indexed closed orders (we'll get to what it means)
- Your open positions
- Your closed positions
- All your open orders
 
![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/tables_frame.png?raw=true)

### Turn closed orders into positions
If you already have some closed orders you can group them into closed and open positions. For this purpose there is the **Index** column - orders with the same index form one position. Whether the position is open or closed is determined automatically. 

In the picture below you can see some fake orders I created.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/closed_as_frame.png?raw=true)

And here you can see how it translates into positions - the orders with index 1 form a closed position (everything was sold). The order with index 2 is an open position.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/existing_positions.png?raw=true)

### Changing indices
By double clicking any closed order in the **Closed orders** table you can open a customization window where you can set indices (or change pretty much anything) for your closed orders.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/customize_closed_orders.png?raw=true)

### Adding custom closed orders
If you've not added your API keys you still may use this functionality by creating fake closed orders. Right click the **Closed orders** table and select **Add custom order**. By clicking **Delete this order** you may delete the order you have right-clicked on.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/add_custom_closed_order.png?raw=true)

This demonstration is just one way of how you can use the index functionality. Feel free to experiment and find the use that best suits you.

### Updating data after exchange addition
If you have added your API keys later or you trade through some other means and want to synchronize your data with CryptEx go to **Show settings -> Update exchange data** pick your exchange and let it sync. Depending on how many pairs you've been trading and how far into the past the exchange allows to reach, this will probably take some time.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/update_exchange_data.png?raw=true)

### Creating price alerts
By clicking **Create alert** in the right frame you open yet another window where you can customize your alert. Unfortunately, the alert (when triggered) so far only opens a new window, so you need to be in front of your computer to see it.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/first_alert.png?raw=true)

After creatiing your first alert, this is what it will look like.

![](https://github.com/LukasUlrych/CryptEx/blob/main/Images/first_alert_set.png?raw=true)

## Exchange specific things
Although ccxt supports more than 100 exchanges I do not have the means nor the willpower to test CryptEx on all of them. Always be aware of the fact, that you are using this software of your own volition and that I am not responsible in any way for any possible financial (or any other) harm that this usage might cause you. Be aware that trading cryptocurrencies bears an inherent risk and that you alone are responsible for the choices you make.

Tested exchanges: **Binance, Kraken, KuCoin, Bittrex, Coinbase Pro, AscendEx, Huobi Pro, Poloniex**
- these I use or have used in the past, so everything should work fine here

Support for price websockets (real-time price updates): **Binance, Kraken, KuCoin, Bittrex, Coinbase Pro, AscendEx, Huobi Pro, HitBTC**
- other exchanges use price updates via API calls (way slower so stop and trail orders will be delayed)

Support for margin trading: **Kraken** - but use at your own peril (work in progress)

# FAQ (really a work in progress)
1. Something doesn't work as it used to
  - restart the application (wait at least 20 seconds)

2. I have inserted my API keys but I can't see my private data (wallet info, closed orders etc.)
  - First, make sure you've inserted correct value to correct field. Most exchanges have **Key** and **Secret** named the same but some may not. Also, if given exchange doesn't show you any **Password** value for API keys, just leave it empty.
  - If that doesn't help, try to sync your clock following e.g. this guide https://www.groovypost.com/howto/synchronize-clock-windows-10-with-internet-atomic-time/ This is a known issue with Binance that I have no way of correcting from my end. Sorry.

If something isn't working properly or you have some ideas for improvement, please don't be shy and let me know. Either here on github by opening a new issue or via email on mypython36 et gmail.com

# Contributions
CryptEx is my hobby project, so I work on it in my spare time. In no way do I make this app public in order to get rich from it, it just feels like someone other than me might find it useful.

If you have found CryptEx useful and feel like manifesting this gratitude in some way, here's all the info you need :)

BTC: 35Hhzgmc4qxF6T7TmWQG213cSPowzPVfaD

ETH: 0xAe6Cbd122adcB339F9869686a39f95030643c0DE

LTC: LgJjYzXTqciDqndGetGyhdRfBP6RQ6GSwe

XRP: rpdPWZTLkN3ZjkNwbwPTShT55Y6qcTNPpR

DASH: XcB1oaTsHvUuXBxbiM2mJdoESdZVCCTprN

ALIAS (public address): SZ9r4M1KVhiztDm76yEpbRXgmwWCxLNBKN

ALIAS (stealth address): smYmruQX3H1SwaKkQmHQJcitwg7WDS2zsoj51fVFNbuTY9hvw2AyLdHjdZzxzLGbhYq3YCkvrGcNLRDYCGVnNhNCh59So4gwG3uBAC
