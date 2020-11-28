## Senate Insider Trading Investigation

**Quick Look:** Both Senators and House Representatives are required to disclose financial stock transactions. Some articles came out around this time pointing out suspicious trading activity by a few politicians. A friend and I took the database of XML/PDFs for the Senate data (2013-2017) and created a database using scraping techniques + mechanical turk for difficult to parse entries. Combining with financial data, we were able to investigate suspicious trades on our own. We were able to identify the same instances from the news data. Critically, however, we failed to find evidence that these trades were suspicious in their relative size or even profitability. 

### Technology Used
- Python
- Amazon Mechanical Turk (First Time)

### Description

A series of articles had come out in the news around 2016/2017 about the trading activity of members of congress. Elected representatives using non-public information for personal gain in office is not the kind of representation I think Americans deserve. As a quant researcher focusing on equity strategies I felt like I had the right skillset to comb through this dataset and check if anything looked suspcious. For this project I collaborated with another quant researcher. 

### Data

Some of this data was well structured (XML files). However, especially for looking at the data for the House, we quickly ran into an annoying amount of handwritten documents. For these handwritten documents, we used the Amazon mechanical turk API where we could pay a per-task fee for people to manually transcribe it (OCR was too difficult on tabular data). We ended up focusing on the Senate due to these sorts of data quality issues.

Even for the well structured data we often ran into issues. One example here is that although a field may be populated, each Senator had their own conventions on how they entered it. For example, even for the same stock senators might enter in "Apple", "AAPL", "Apple (AAPL)", "Apple Inc.", etc. Since we need to map this to financial data we need to have consistent IDs across each of these assets. This took some manual correcting and fuzzy matching. 

Finally, for market data we used yahoo finance to grab the time series of returns over the life of the trades.

### Analysis

First, a few senators make up the bulk of the trading activity. We were interested in both average profitability (are Senators savvy traders?) as well as suspicious trade identification (was this an unusually timed trade?).

In order to make claims about the trading behavior we needed to make some rough approximations about when politicians were entering/exiting trades. Often there would be partial liquidations that needed to be handled. 

Our results were surprising on both fronts. For aggregated trading behavior, we failed to see the strong outperformance over the market that we expected to see. However, not all senators were included in this due to data issues and we worried about selection bias in the senators that chose to report transparently vs. in more difficult to analyze documents (handwritten).

For single suspicious trades, we looked at the 5, 30, 60 day periods after every transaction to see if there was a significant change in stock price. For example, if a senator bought a biotech stock that then appreciated 20% afterwards that is highly suspicious. Conditioning on these sorts of trades flagged some of the trades that we saw in news articles. Here though, we found that on average individual senators were equally making/losing these large amounts. We expected to see that individuals on certain committees were consistently notching in big returns. For the members that did trade, there were many instances where they sold when they should have bought (or vice versa). As a result, we couldn't point to any smoking gun here.

We held off on further research at this point to focus on other projects.

### Update

In the time since we looked at this there have been various other projects doing similar things. 

This <a href="https://www.nber.org/papers/w26975?utm_campaign=ntwh&utm_medium=email&utm_source=ntwg24&mod=article_inline"> paper </a> takes a much more rigorous approach and finds results consistent with ours that these politicians in this sample do not appear to be making unusual profits through trading. 

Additionally other sources of cleaned data for doing this now exist in easier to access ways, for example <a href="https://senatestockwatcher.com/"> Senate Stock Watcher </a> and <a href="https://sec.report/"> SEC Report </a>.
