# GDELT Dataset Builder for Critical Social Science

The main notebook in this repo (`gdelt-databuilder.ipynb`) uses scala/Spark to _load and filter_ [1] data from a _live updating delta lake GDELT_ [2] _storage infrastructure_ [3], and relies on Python `koalas` [4] for data wrangling.

The method assumes that `gdelt_databuilder.ipynb` is run in a Databricks [5] environment where deltalake storage of GDELT [1; 3] 

----
1. [github.com/aamend/spark-gdelt](https://github.com/aamend/spark-gdelt) – package for easy loading of GDELT data in Spark environments
2. [GDELT](https://github.com/gdelt/gdelt.github.io) — database
3. [github.com/lamastex/spark-gdelt-examples](https://github.com/lamastex/spark-gdelt-examples) — data infrastructure and scala code
4. [github.com/databricks/koalas](https://github.com/databricks/koalas) – it's genius! 🐨
5. [Databricks](https://github.com/databricks) – notebook environment for scala and python (and others) 
