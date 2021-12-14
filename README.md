# GDELT Dataset Builder for Critical Social Science

The main notebook in this repo (`gdelt-databuilder.ipynb`) uses scala/Spark to _load and filter_ [1] data from _our live updating delta lake GDELT_ [2] _storage infrastructure_ [3], but relies on Python `koalas` [4] for data wrangling.

----
1. [github.com/aamend/spark-gdelt](https://github.com/aamend/spark-gdelt) – package for easy loading of GDELT data in Spark environments
2. [GDELT](https://github.com/gdelt/gdelt.github.io) — database
3. [github.com/lamastex/spark-gdelt-examples](https://github.com/lamastex/spark-gdelt-examples) — data infrastructure and scala code
4. [github.com/databricks/koalas](https://github.com/databricks/koalas) – it's genius! 🐨
