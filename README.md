# Confoederatio Ludens Image Corpus

This is a dataset created for the [Confoederatio Ludens](https://chludens.ch/) research project, which investigates video game design, development and culture in Switzerland from 1968-2000. The images are screenshots from video games relevant to the research project and acquired through MobyGames screenshots and YouTube stills.

## Setup
I like working with [Miniconda](https://docs.anaconda.com/free/miniconda/) and [Jupyter Notebooks](https://jupyter.org/). If that speaks to you as well, the setup is easy.

### 1. Follow the [Miniconda installation guide](https://docs.anaconda.com/miniconda/miniconda-install)

```bash
conda deactivate
conda create --your_env_name python=3.9
conda activate your_env_name
pip install notebook
```

### 2. Navigate into this repository

```bash
jupyter notebook
```

### 3. Produce Wikidata query

The scraper scripts work with the resulting csv of a Wikidata SPARQL query. The query file is in the repository and the original query is accessible via [here](https://query.wikidata.org/index.html#SELECT%20DISTINCT%20%3Fitem%0A%20%20%28GROUP_CONCAT%28DISTINCT%20%3FitemLabel%20%3B%20separator%3D%27%2C%27%29%20as%20%3Flabel%29%0A%20%20%28GROUP_CONCAT%28DISTINCT%20YEAR%28%3FpublicationDate%29%20%3B%20separator%3D%27%2C%27%29%20as%20%3Fdate%29%0A%20%20%28GROUP_CONCAT%28DISTINCT%20%3FplatformLabel%20%3B%20separator%3D%27%2C%27%29%20as%20%3Fplatforms%29%0A%20%20%28GROUP_CONCAT%28DISTINCT%20%3FcountryOfOriginLabel%20%3B%20separator%3D%27%2C%27%29%20as%20%3Fcountry_of_origin%29%0A%20%20%28GROUP_CONCAT%28DISTINCT%20%3FmobygamesID%20%3B%20separator%3D%27%2C%27%29%20as%20%3Fmobygames_id%29%0A%20%20%28GROUP_CONCAT%28DISTINCT%20%3FdescribedAtURLLabel%20%3B%20separator%3D%27%2C%27%29%20as%20%3Fyoutube_url%29%0AWHERE%20%7B%0A%20%20%3Fitem%20wdt%3AP31%20wd%3AQ7889%20%3B%0A%20%20%20%20%20%20%20%20wdt%3AP577%20%3FpublicationDate.%0A%0A%20%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP943%20%7C%20wdt%3AP3080%20%7C%20wdt%3AP86%20%7C%20wdt%3AP57%20%7C%20wdt%3AP50%20%7C%20wdt%3AP287%20%7C%20wdt%3AP162%20%7C%20wdt%3AP767%20%3Fstaff%20.%0A%20%20%20%20%3Fstaff%20wdt%3AP27%20wd%3AQ39%20.%0A%20%20%7D%0A%20%20UNION%0A%20%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP123%20%7C%20wdt%3AP178%20%3Fcompany%20.%0A%20%20%20%20%3Fcompany%20wdt%3AP17%20wd%3AQ39%20.%0A%20%20%7D%0A%20%20UNION%0A%20%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP495%20wd%3AQ39%20.%0A%20%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP400%20%3Fplatform%20.%0A%20%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP11688%20%3FmobygamesID%20.%0A%20%20%7D%0A%20%20%0A%20%20OPTIONAL%20%7B%0A%20%20%20%20%3Fitem%20wdt%3AP973%20%3FdescribedAtURL%20.%0A%20%20%20%20FILTER%28contains%28str%28%3FdescribedAtURL%29%2C%27youtube%27%29%29%20.%0A%20%20%7D%0A%20%20%0A%20%20FILTER%20%28%3FpublicationDate%20%3C%20%222000-01-01T00%3A00%3A00Z%22%5E%5Exsd%3AdateTime%29%0A%20%20%0A%20%20SERVICE%20wikibase%3Alabel%20%7B%0A%20%20%20%20bd%3AserviceParam%20wikibase%3Alanguage%20%22en%22%20.%0A%20%20%20%20%0A%20%20%20%20%3Fitem%20rdfs%3Alabel%20%3FitemLabel%20.%0A%20%20%20%20%3Fplatform%20rdfs%3Alabel%20%3FplatformLabel%20.%0A%20%20%20%20%3FcountryOfOrigin%20rdfs%3Alabel%20%3FcountryOfOriginLabel%20.%0A%20%20%20%20%3FdescribedAtURL%20rdfs%3Alabel%20%3FdescribedAtURLLabel%20.%0A%20%20%7D%0A%7D%0AGROUP%20BY%20%3Fitem%0AORDER%20BY%20ASC%28%20%3Fdate%20%29).

## Files

- 10_Scrape_Mobygames.ipynb: Download and prepare MobyGames screenshots
- 20_Scrape_Youtube.ipynb: Download, generate and prepare YouTube stills
- 50_Create_Random_Sample.ipynb: Generate a random sample
- 60_Explore.ipynb: Basic setup to explore the dataset through image clustering

## Legal
- MobyGames screenshots as well as YouTube stills are (c) by their respective creators
- Dataset created by Adrian Demleitner, 2024, licensed under [CC-BY-4.0](LICENSE-CCBY)
