# GDELT Dataset Builder for Critical Social Science

The main notebook in this repo (`gdelt-databuilder.ipynb`) uses scala/Spark to _load and filter_ [1] data from a _live updating delta lake GDELT_ [2] _storage infrastructure_ [3], and relies on Python `koalas` [4] for data wrangling.

The method assumes that `gdelt_databuilder.ipynb` is run in a Databricks [5] environment where deltalake storage of GDELT [1; 3] is mounted.

##### Resources
>1. [github.com/aamend/spark-gdelt](https://github.com/aamend/spark-gdelt) – package for easy loading of GDELT data in Spark environments
>2. [GDELT](https://github.com/gdelt/gdelt.github.io) — database
>3. [github.com/lamastex/spark-gdelt-examples](https://github.com/lamastex/spark-gdelt-examples) — data infrastructure and scala code
>4. [github.com/databricks/koalas](https://github.com/databricks/koalas) – it's genius! 🐨
>5. [Databricks](https://github.com/databricks) – notebook environment for scala and python (and others) 

### Background

GDELT is a huge and growing database which starts from the notion of `events`. These events are identified in news media globally, in over 100 languages, in print, broadcast, and web formats. The registered events are tagged with themes, people, organisations, emotions, etc., and all such elements are put together in GDELT's _Global Knowledge Graph_ (GKG), which is a real-time `graph` interlinking all of the event data. Some of the data go as far back as 1979.

>"The GDELT Project is a realtime open data global graph over human society as seen through the eyes of the world's news media, reaching deeply into local events, reaction, discourse, and emotions of the most remote corners of the world in near-realtime and making all of this available as an open data firehose to enable research over human society" [gdeltproject.org](https://www.gdeltproject.org/)

GDELT, in other words, is a very ambitious project, and also highly complex. [All the codebooks and documentation](https://github.com/lamastex/spark-gdelt-examples/tree/master/gdelt-docs) are quite intimidating. Aside from the events and GKG data, the GDELT project also offers [other datasets](https://www.gdeltproject.org/data.html#rawdatafiles).

This notebook offers a method to drill down fast to applications of GDELT that I feel may be interesting from the perspective of critical social science analyses that can be useful in their own right, but maybe mainly as some form of 'mainstream'/'ground truth' baseline to contrast with analyses of processes and behaviours in social media.

### Building the dataset

These are the general steps performed in `gdelt-databuilder.ipynb`, with more details described in the actual notebook:

1. We start from GDELT's [GKG 1.0](https://www.gdeltproject.org/data.html#rawdatafiles) and select a timeframe to analyse. This example uses `start_date = "2020-01-01 00:00:00"` and `end_date = "2020-12-31 00:00:00"`.

2. Choose a set of searchstrings to get data, based on searching the news article URLs, about the topic(s) we are interested in. This example uses `%covid%`, `%vaccine%` or `%vaxx%`.

3. See which GDELT coded themes are the most common in data matching our searchstrings, and broaden the search in the GKG based on these. In this example we got around 1.9M articles based on the URL searches, with 11.8M articles added through matching theme codes. Removing duplicates across the two sets of data, we ended up with 12.2M articles about our topic(s).

4. Based on the `eventIds` found in our current dataset, we connect to GDELT's [Event Database 1.0](https://www.gdeltproject.org/data.html#rawdatafiles) and join in the extended event data from there. This means that we are enriching the data we already have with more columns about the events identified through the GKG.

5. A set of datawrangling steps with `koalas` leads up to an ordered and useful dataframe.
