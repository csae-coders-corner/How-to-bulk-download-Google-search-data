
![CC Graphics 2024_DownloadData](https://github.com/csae-coders-corner/How-to-bulk-download-Google-search-data/assets/148211163/f1c0608d-c4c6-430d-a33c-bf567946209a)

# How-to-bulk-download-Google-search-data
Google Trends is a great data source, but unfortunately, their API only lets you compare 5 search terms at once. In addition, it scales search intensity to be relative to the other search terms, making it complicated and tedious if you want to download a large number of searches at once. Luckily, there is a great R package called ‘GTrendsR’ that helps you to return search intensity for a larger number of terms across a range of dates and regions. In this R code, I show you how to combine GTrendsR with an additional loop so that you can bulk download search terms into a csv file.

First create a file with the terms you want to search for and save it with a .csv extension. Just include all words, each on its own row.

Next find the correct country code and fill this in, along with the dates you are interested in. This code would be if searching for search intensity in England, Scotland and Wales. The code is:

```
installed.packages("readr","gtrendsR")

library(readr)

library(gtrendsR)
```

### Load your keywords list (.csv file)

```
kwlist = readLines("variables.csv")

The for loop downloads the data for every single keyword in your list


resultslist <- list() 

for (keywords in kwlist){

**Choose countries**

  country=c('GB-ENG', 'GB-SCT', 'GB-WLS')

**Define time period**

  time=("2015-01-01 2019-09-30")

  channel='web'

**Obtain google data**

trends = gtrends(keywords, gprop =channel,geo=country, time = time )

resultslist[[keywords]] <- trends$interest_over_time

}

**Generate output data frame**

output <- as.data.frame(do.call("rbind", resultslist)) 

**Download the data frame "output" as a .csv file**

write.csv(output,"output.csv")
```

**Katherine Stapleton, DPhil Candidate in Economics, Lincoln College, Oxford, 29 October 2019**

