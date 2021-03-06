# Coinbase historic candlestick scraper

This is a simple data collection script for getting historical candle stick data from coinbase pro's public api.

It collects all the candlestick data for **every** currency that is listed in coinbase products.

This script respects their public api rate limits requests to 3 a second. 
It is probably not a good idea to constantly run it to collect to get market data. 
It is recommended to run it every few hours or daily to collect the candlestick data.

## Pre-requisites

The following is needed to run this script:

* Python (3.9.1)
* Mongo DB (4.4.3)

## Setup

The script can be installed locally with setup tools and doing the following:

```bash
> python setup.py sdist
> python setup.py install --user
```

## Default configuration

The default configuration:

* **host**: localhost
* **port**: 27017
* **database_name**: coinbase-pro
* **collection_suffix**: historical-candlestick-data

You can override these settings with a dotfile called `.cb-candlesticks.ini` in the user's home directory.

```ini
[mongo_db]
host=<host>
port=<port>
database=<database>
collection_suffix=<collection-suffix>
```

## Run

The script is fairly straight forward to run.

```
$ cb-candlesticks -h
usage: historic_candle_stick_data.py [-h] -g {1m,5m,15m,1hr,6h,1d} [-s START] [-e END]

Gets the historical candlestick data from coinbase

optional arguments:
  -h, --help            show this help message and exit
  -g {1m,5m,15m,1hr,6h,1d}, --granularity {1m,5m,15m,1hr,6h,1d}
                        the granularity of the candle sticks to collect
  -s START, --start START
                        start time in the format Y-m-d
  -e END, --end END     snd time in the format Y-m-d
```

## Usage

### Example 1

The application has a preset time period if just given a granularity data. You must specify the `-g` option.

```
$ cb-candlesticks -g 1m
```

The preset time periods are based on what **roughly** makes sense for a given granularity level. 

### Example 2

You can specify a date and time to scrap results against. 
The string format is quite simple Y-m-d e.g. 14<sup>th</sup> Feb 2021 is `2021-02-14`  

```
$ cb-candlesticks -g 1m -s 2021-02-13 -e 2021-02-14
```

**WARNING**: If you set a very small granularity, and a large date range this script may take quite a while to complete.

## changelog

### Feb 27th 2020

* Now looks for `dotfile` file in the users `$HOME` directory.
* Installable from setup tools (I've only tested this on Linux).
* Fixed the enums being incorrect for certain time periods which broke the time/granularity mappings.

### Feb 14th 2020

* Initial data collection script, README.md

## TODO 

* Proper logging
* Error handling
* Quiet mode

# LICENSE

The code is distributed under the WTFPL license.

<a href="http://www.wtfpl.net/download/wtfpl-badge-1/" rel="attachment wp-att-49"><img alt="wtfpl-badge-1" src="http://www.wtfpl.net/wp-content/uploads/2012/12/wtfpl-badge-1.png" width="88" height="31"></a>
