---
title       : "rtweet: Collecting Twitter data"
subtitle    : Intro and tutorial
author      : Michael W. Kearney
institution : Center for Research Methods & Data Analysis
framework   : revealjs        # {io2012, html5slides, shower, dzslides, ...}
revealjs:
  theme: simple
  transition: linear
  center: "true"
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
url: {lib: "."}
knit        : slidify::knit2slides
---

<style>
@import url('https://fonts.googleapis.com/css?family=Inconsolata');
h2 {
line-height: 1.5em !important;
}
h4, h5 {
color: #222 !important;
font-weight: 400 !important;
}
code {
font-family: Inconsolata !important;
font-size: 20pt !important;
line-height: 1.5em !important;
}
</style>

## rtweet: Collecting Twitter Data
#### Michael W. Kearney
##### Center for Research Methods & Data Analysis
##### University of Kansas

--- 

<section>

## Twitter APIs
- Limited (lots of money) use
    - **Firehose** API (firehose.twitter.com)
- Publicly available
    - **REST** API (api.twitter.com)
    - **Stream** API (stream.twitter.com)

---

## REST API
- Archived collection of tweets and users data
- Search queries extend 7-10 days max

---

## Stream API
- Three different ways to access the stream API

---

## Sample
1. Randomly samples about 5% (I think) of tweets

```r
rt <- stream_tweets(q = "")
```

---
## Filter
2. Streams all tweets using keyword filter(s)

```r
rt <- stream_tweets(q = "yolo,rstats")
```

---

## Tracking
3. Streams all tweets from and mentioning users

```r
rt <- stream_tweets(q = "hillaryclinton,realdonaldtrump")
```

</section>

---

<section>

## Firehose for free I
1. Firehose via `search_tweets()`

```r
search_firehose <- paste0(letters, collapse = " OR ")
search_firehose
```

```
## [1] "a OR b OR c OR d OR e OR f OR g OR h OR i OR j OR k OR l OR m OR n OR o OR p OR q OR r OR s OR t OR u OR v OR w OR x OR y OR z"
```

```r
rt <- stream_tweets(q = search_firehose)
```

---

## Firehose for free II
2. Firehose via `stream_tweets()`

```r
stream_firehose <- paste0(letters, collapse = ",")
stream_firehose
```

```
## [1] "a,b,c,d,e,f,g,h,i,j,k,l,m,n,o,p,q,r,s,t,u,v,w,x,y,z"
```

```r
rt <- stream_tweets(q = stream_firehose)
```

</section>

--- 

## search_tweets() args
- **q**: Search query with boolean syntax
- **include_rts**: Filter out retweets
- **type**: Search for `"popular"`, `"recent"`, `"mixed"`

```r
rt <- search_tweets(q = "rstats OR statistics OR \"data science\"",
    include_rts = FALSE, type = "recent")
```

--- 

## stream_tweets() args
- **q**: Stream query to use any of 3 methods
- **timeout**: Length of time for stream (in seconds)
- **file_name**: Name to save file. If NULL (default) a tmp file is created and deleted
- **parse**: Locial indicating whether to parse into tidy data frame

```r
rt <- stream_tweets(q = "rstats,statistics,hadley",
    timeout = 60 * 10, file_name = "rstats.json", parse = TRUE)
```

--- 

## The end
- That's it!
