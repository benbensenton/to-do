# to-do

- streamplotter module, probably back to pyqt graph as module in jupyterlab (https://gist.github.com/iverasp/9349dffa42aeffb32e48a0868edfa32d ,                                                                                                                  https://pyqtgraph.readthedocs.io/en/latest/ ,                                                                                                                                      https://github.com/bokeh/bokeh/blob/2.4.0/examples/app/ohlc/main.py ,
                                                                             https://www.numpyninja.com/post/hdf5-file-format-with-pandas)
        - since pyqt as app not flexible enough
        - bokeh is pretty and convienent but not fast enough   
        - matplotlib to slow
        - plotly no streaming
        - hadoop/pyspark/zeromq/dask/vaex/ray/modin/pyarrow/pystore currently overkill 
        - https://github.com/ray-project/ray





- minute download function integration in bs app           ✓ done
        - return value check
              . no return value check for empty or error csv, handle it in hdf5 writer?  --> we dont need to keep processing the 24 slices for symbol url that returns a empty                   list, pop it from queue, break loop, continue with new symbol, what are the error cases: either limit reached(should not occure due to implementation) or                         empty/nonsense data-API error etc(filter it out by checking the http response for a specific string)
        - no immediate hdf5 writting option, since additional computation needed (e.g. timestamp as index)
        - implement slice selection 
              . as if else statement to select slice tuple
              . gui implementation as selection, box appears if intraday function is selected
              . this running month 'year1slice1', last 3 month (year1slice1,year1slice2,year1slice3), last year (), all () 

- symbol search query + implementation in app --> gives symbol masterfile but not suvivorship biased free (they dont serve data on delisted companys) wich needs to be maintained 
        - ticker symbol list generator script              ✓ done
        - allow 2 types of input, either user typed string also as list to process for every entry, and as internally generated whole string posibility when a certain leading             symbol is in string, e.g. @all, when found run the generator function, write out that string list to csv
        - make a processed list(write out as csv after every sucess), when app crashes or something needs to restart, compare @all.csv with processed.csv, load unique and                 continue
        - its a pasting field, same as for symbol, does it support dot notation? xxx.FRA / xxx.LON  --> is it all capital?
        - returns json or csv, use json? or append csv and later parse once (US Mutual Fund 5 Letter code, .FRA notation, others 7 Position Letter/Number combis
        - Build by country, exchange, ticker
        - sql bc hdf5 to unstructured or as df in hdf5 all with indexing
        - 4 letter search string with letters 26^4 combination in length 1-4 places = 475254 combinations, free account 5 request/min 500r/d = 100 min/d, 950days ≈ 2.5years
         paid account: 75 request/min / unlimited request/day: 24*60*75= 108000 requests/day  ≈ 4.5 days @ 24h uptime ⇒ free tier aws? (unnecessary overhead, but good practice,          docker etc, the limiting factor is now return answer delay ⇒ async requests, multiprocess easyer? , every thread appends creates 1 file or all threads appending to 1            file
        - symbolist is made unique and sorted by country,exchange, type(equity, etf usw), symbol    Order-structure: Symbol_Master -->USA-->NYSE-->EQUITY-->Minute_Intraday--> A
     - only needed once a year maybe                                                                                                  GER   NASDAQ ETF      Daily              AA
                                                                                                                                      JP    ...    ...                        AAA
                                                                                                                                      ...
- expand hdf5 writer for minute intraday and symbol_master write capabilitys


- query hdf5 --> has it the right capabilities?
        - saved columns need to be data_columns otherwise select does not work
        - e.g. finding the .max() value of all symbols in all US stocks
               path_to_tables = 
               with pd.HDFStore("store.h5") as store:
                   for path_to_table in path_to_tables:
                        store.select("path_to_table", where=['Volume.max()'])
                        # pd.read_hdf("store_tl.h5", "path_to_table", where=['Volume.max()'])   // probably functions dont work?  


- kalmann on historic as initial start with streamplotter


- additional data sources
        - options, future, etc




- multiple linear regression:
    - https://notebook.community/afarouky/become-datascience-master/linear-regression-tutorial/(Multiple)-Linear-Regression-tutrial
    - statsmodels OLS : https://www.statsmodels.org/stable/generated/statsmodels.regression.linear_model.OLS.html

- Evolution trategies in lieu of Reinforced learning:
    - https://openai.com/blog/evolution-strategies/

- Lo papers @ sloan:
   - https://alo.mit.edu/?s=spectral+factor+models&topic=&first-year=1986&second-year=2020&post_type=research-page
   - https://alo.mit.edu/?s=&topic=&first-year=2000&second-year=2021&post_type=research-page

- IEX crumbling quotes:
   - https://iextrading.com/docs/The%20Evolution%20of%20the%20Crumbling%20Quote%20Signal.pdf

- Oreley hilpisch, Python for Finance Notebooks:
  - https://base.pqp.io/base/ju/get_iframe 



- when time, Rebuild the whole bs app from Qt(fkng horendous docu, very time consuming, maybe together with a real exe) into some other framework
