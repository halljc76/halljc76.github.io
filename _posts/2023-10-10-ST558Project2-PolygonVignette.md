## Leveraging the `polygon` Stock API to Analyze Apple Stock Data

For this blog post, I will chronicle my experiences leveraging the `httr` package
in `R` to query stock ticker data from the `polygon` API, a free API available at
[polygon.io](polygon.io).

The vignette created to accompany this blog post can be found [here](https://halljc76.github.io/polygonVignette), and contains a much more thorough explanation of the packages, functions, and analysis. I highly encourage the reader to check it out, as it demonstrates how `R` can interface with online resources to perform data analysis, rather than solely relying on in-house or locally stored alternatives!

The sections of this blog post detail my experiences in creating this vignette!

### What Was Done

The vignette defines functions that leverage **three** endpoints -- two 
*Market Data Endpoints* (Aggregates and Grouped Daily, per Polygon's website), 
and a *Reference Data Endpoint* on the tickers of which Polygon keeps track.

Each endpoint received its own individual function, as well as a common function
not presented in the vignette that I defined to process any query results from
JSON to `R` data frames, allowing the `tidyverse` family to take over any data analysis.

Once functions were defined, I retrieved historical data from Apple stock over the past two years -- this was the timeframe allowed by the **basic** plan of the API, and unfortunately meant that, in order to go back into the past, small lapses of data were included in the resulting API calls. To do this, however, I had to write a loop that performed multiple API calls, all while staying within the *5* calls/minute afforded to me by the API. (This proved... more tedious than I would like to admit!) To decide on Apple stock (and to test out the quality of the data returned by the API), I used the reference endpoint function to query $1000$ stocks that could be returned to me by the API (again, at a free level), and compared the exchanges on which these were traded via contingency tables.

Having data, I plotted the different series of stock prices -- *open* and *close*, as well as *high* and *low*. Data were gathered at minute and daily intervals, the former to attempt to capture a more complete picture of the movement of the stock, and the latter to create plots that, due to the sheer number of original data points in the per-minute dataset, were aesthetically viable and comprehensible. 

### What Went Right... and What Went Wrong?

I begin the reflection on this project by addressing the 'elephant in the post' -- this API was rather limiting on what was available to users at a free tier. Not wanting to do sports or disease APIs (as were the examples in the project description), and instead wanting to appear 'original,' I went hunting for an API; the Polygon website was incredibly professional and, as obtaining an **authentication** was easy enough, I proceeded with it for the duration of the project.

Not having **any** categorical data on the per-minute or per-day stock price data was rather alarming (i.e., no 'indices' on how intense trading was during that time, no reference to historical data or news headlines that might be of interest) meant that, with the exception of the aforementioned contingency table data, I would have to create my own to achieve numerical summaries at levels of categorical data. Making my own variable, `higher`, representing whether a stock price finished the day higher than when it opened, proved to be *invaluable*, as it reinforced the notion that one could not accurately declare whether the stock would increase or decrease on any given day without context and further, more sophisticated analysis. Moreover, it reinforced that the practice of 'day trading,' while becoming more popular in the past few years, is incredibly difficult.

While the data retrieved from the API was *somewhat* difficult to work with, in the sense of completing required types of visualizations for the project, the API nevertheless returned data that made it possible! Additionally, having experience converting from a JSON object via the `jsonlite` package and querying an API through `httr` (having actually designed my *own* API through the `plumber` package before) was great! All in all, while I might choose a different API in the future, or if I were asked to do this project again, the experience with the Polygon API was rather seamless and is a product I would recommend to anyone looking for experience with visualizing stock data!

### Links

Vignette: [link](https://halljc76.github.io/polygonVignette)

GitHub Repository: [link](https://github.com/halljc76/polygonVignette)
