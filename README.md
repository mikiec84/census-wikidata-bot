# census-wikidata-bot

![Census-bot-logo](https://raw.githubusercontent.com/CommerceDataService/census-wikidata-bot/master/images/census_wiki_bot.jpg)

This project contains code for a bot which interacts with [Wikidata](https://www.wikidata.org/wiki/Wikidata:Main_Page) and [Wikipedia](https://en.wikipedia.org/wiki/Main_Page) using the pywikibot library.  This bot is designed to use Census data specifically and push it to the Wiki if a page exists for the requested subject matter.

## Setup
In order to set up this bot to run, a wikidata account with a bot flag approval is necessary.  This bot uses python 3.5 and the main library for interaction with the Wikidata API is [Pywikibot](https://www.mediawiki.org/wiki/Manual:Pywikibot).

#### user-config.py
This is the configuration file for the bot.  In the this file, insert your user account in the following line:<br>
`usernames['sitename']['en'] = u'ExampleBot'`

The `mylang` and `family` parameters will also need to be set accordingly.  Please refer to the documentation for Pywikibot for additional information regarding this (as well as logging in).

#### Environment Variables
You will need to define an environment variable with the name `CENSUS` and a value of your Census API key in order for the bot to use your API key in order to interact with the Census API's.  In order to obtain a Census API key, refer to the following [here] (http://api.census.gov/data/key_signup.html).

#### Data Configuration files
This bot application consists of various data configuration files to support the test and production instances of the bot.  

## Scope
This bot is set up to use a configuration file

Currently, this bot is only set up to use a static file containing U.S. state population values for 2015.  The bot will use these values to search and see if a page exists for that state.  If a single result is found, it will access the page and check if the population statement is present.  If so, it will check the claims.  If there is a claim with no `point in time` value, it will be deleted.  Subsequently, it will check for any entries referring to a `2015` point in time.  If it finds any it will check them for completeness.  if anything is off, it will delete that entry and make a new complete entry.  If no population statement is present or if no 2015 entry for population is present it will add that to the page.  Currently, there is a page for Arizona, Oregon, California, and Virginia on the test site which this bot will find.

## Future Scope
Going forward, there will be changes to the functionality of this bot and the range of data that it accesses and inserts into Wikidata.  This page will be periodically accordingly.


#### data files
There are two data files in the `/data` directory of the project.  These contain the necessary information for the bot to know how to communicate with the Census API's, what to get from the API to write to Wikidata, and how to write it.  There is a set structure to these files and you may add JSON objects to them in order for the bot to operate on additional Census API's or additional values for an existing API call.  Since property keys differ between the [test wikidata site] (https://test.wikidata.org/) and the main site, there are separate files for each.

Lastly, for testing purposes, there is a `mode` argument for the `addPopValues.py` file.  This is required and will determine whether the bot runs under test or production mode (including which data file it should use).

## Running Bot
Once setup has been completed, the bot can be run by executing the `addPopValues.py` file.

#### Modes of execution
- Test, Production, Debug

##Logging
You may follow logs of the actions that occurred for execution of a bot by looking at the logs in the `/logs` directory.  Log filenames are prefaced with `censusbot-log`+ the `YYYYMMDD` value.
