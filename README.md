# CryptEx
## A python based engine for cryptocurrency trading

CryptEx allows you to:
 - create orders (market, limit, stop, trail) with the possibility of setting a follow-up order
 - set alerts based on price crossing a certain threshold (EMA, SMA) or price closing above or below certain threshold
 - keep track of your current and past positions
 - keep track of all your crypto assets

Based on ccxt library (https://github.com/ccxt/ccxt) for most of API calls, CryptEx provides user with clean (almost spartan) looking graphical user interface.

## Getting started
Download latest release from https://github.com/LukasUlrych/CryptEx/releases/, unpack the zip and start CryptEx.exe. If you are uncertain about that, you can check with https://www.virustotal.com/gui/ for any malware or viruses, There shouldn't be any :)

### Adding new exchange
In the right panel click **Show settings -> Exchanges settings -> Add exchange**
Here you choose the exchagne you are looking for from the dropdown menu. If you wish so, you can also add your API keys here. The app will work without them, but you won't be able to to create orders, see your closed positions or your balances.

### Deleting exchange
In top menu click **Settings -> Manage exchanges -> Delete exchange** and choose which one. Done You can check via https://www.virustotal.com/gui/ for any malware or viruses, There shouldn't be any :)

### Add new pair
In top menu click **Show settings -> Pairs settings -> Add pair**
Here you choose on which exchange and the pair itself. If you provided API keys, your closed orders will download automatically, however, some exchanges do not provide complete history via API, so keep that in mind.

### Delete pair
In top menu click **Show settings -> Pairs settings -> Delete pair**
Here you choose exchange and the pair itself. Done

### Changing graph
In top menu click **Exchanges**, choose exchange and pair and voila. For quick acces you can pin current pair to watchlist by clicking **Add current** in left panel. Clicking **Remove current** removes it from watchlist.

### Stop order
Market and Limit orders are (hopefully) pretty straightforward. In CryptEx Stop order works as stop-market order, meaning that if the price crosses given stop price level, a market order (buy or sell) will be triggered.

### Trail order
Setting stop price here works the same as with Stop order. Price here reffers to a level, when Trail order will get active. Trail (always in %) states by how much the price of asset needs to change for the order to trigger.

### Note
Keep in mind, that since a lot of exchanges do not support Stop and Trail orders, these are handled within the application itself so it needs to be running constantly if you wish to use these order types.

Example: Let's say, that current price of BTC is 1100$.
You want to buy it lower, somewhere below 1000$ ideally, but you want to give it some space to breathe.
So you create a Trail order with Price = 950 and Trail = 5.
This menas, than once price of BTC falls to 950, the order gets activated, but will not be triggered, until BTC rises by 5%.
So if it falls to 900$ and then shoots up, the order will trigger a market buy at 900 * 1.05 = 945.

You don't have to set Price if you don't want to. All you need to do is click **Start now** check button on the right side of the order window an the Trail order will be activcated immediately.

## Exchange specific things
Although ccxt supports more than 100 exchanges I do not have the means nor the willpower to test CryptEx on all of them. Always be aware of the fact, that you are using this software of your own volition and that I am not responsible in any way for any possible harm that this usage might cause you.

Tested exchanges: **Binance, Kraken, KuCoin, Bittrex, Coinbase Pro, BitMax (AscendEx), Poloniex**
Support for websockets (real-time price updates): **Binance, Kraken, KuCoin, Bittrex, Coinbase Pro, BitMax (AscendEx), Poloniex, HitBTC**
- other exchanges use price updates via API calls (way slower)
Support for margin trading: **Kraken**

## Kinks
Mouse-wheel click allows you to transition between the two main frames of the app. I will change it in the futrue to something more intuitive.

When looking at closed orders table for given pair, you will notice **Index** column. This one is interactive by double-clicking and it serves the purpose of grouping orders into opan or closed positions. So if you bought 100 BTC in 5 buys and sold it all in 2 sells, you give all those orders the same index (numbers only). This position will then show on the other frame as closed with some basic info.

If you have only bought something so far, the procedure is the same. Jut index orders you want to have groupped together with the same index.
