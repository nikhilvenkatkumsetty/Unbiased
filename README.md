![PyPI - Python Version](https://img.shields.io/pypi/pyversions/Py) 
[![flask](https://img.shields.io/badge/flask-v1.1.1-blue)](https://github.com/topics/flask) 
[![python](https://img.shields.io/badge/website-up-brightgreen)](https://github.com/topics/python)
[![Open Source? Yes!](https://badgen.net/badge/Open%20Source%20%3F/Yes%21/blue?icon=github)](https://github.com/Naereen/badges/) 
[![contributions welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg?style=flat)](https://github.com/pratikwatwani/Unbiased/issues) 
[![GitHub issues](https://img.shields.io/github/issues/Naereen/StrapDown.js.svg)](https://GitHub.com/Naereen/StrapDown.js/issues/)

<p align="center">
  <kbd>
    <img src="https://github.com/pratikwatwani/Event-Based-Influence-on-Wikipedia/blob/master/assets/logo.png" width="250" height="200" margin-right=500px>
  </kbd>
</p>

# <h1 align="center">UNBIASED</br>Spatio Temporal Event Based Influence on Wikipedia Edits</h1>

### <h2 align="center"><kbd>[Presentation](https://docs.google.com/presentation/d/1CPY6hL6gpJWHJdGLeQp7smaeLmAUaLXKfNtiZ5eszwU/edit?usp=sharing)</kbd>&nbsp;&nbsp;&nbsp;<kbd>[Demo](https://www.unbiaswiki.me)</kbd></h2>

## Motivation🚀 
Every day there are thousands of notable transactions over the globe; protests, market dips, terrorist attacks, etc. 

The question is, **Do global events lead to influence in edits of Wikipedia articles?**

**UNBIASED** is a tool to serve moderators and researchers to leverage open data to understand and further research patterns in Wikipedia edits contribution. 

## Data🪣
| Type | Source                                               | Size    | Update Frequency | Location   |
|------|------------------------------------------------------|---------|------------------|------------|
|  <img src="https://github.com/pratikwatwani/Event-Based-Influence-on-Wikipedia/blob/master/assets/structured%20data.png" width="80" margin-right="80">    | GDELT, Global Database of Events, Language, and Tone |   **6+ TB**  |    15 minutes    |  Public S3 |
|  <img src="https://github.com/pratikwatwani/Event-Based-Influence-on-Wikipedia/blob/master/assets/unstructured%20data.png" width="80" height='90' margin-right="80">     | Wikipedia Metadata                                   | **~500 GB** |      Varies      | Private S3 |          


**GDELT:**    

<img align ='left' src="https://maelfabien.github.io/assets/images/header.jpg" width="300">
The GDELT Project monitors the world's broadcast, print, and web news from nearly every corner of every country in over 100 languages and identifies the people, locations, organizations, themes, sources, emotions, counts, quotes, images and events driving our global society every second of every day, creating a free open platform for computing on the entire world.<br><br><br><br>



**Wikipedia Metadata:**    
<img align ='left' src="https://www.bunkered.co.uk/uploads/site/_articleBodyImage/Wikipedia-logo-1024x576.jpg" width="300"></img>  

Historical and Current dump of English Wikipedia consisting metadata including edits, commits, messages, userids', timestamp of each edit on the wikipedia article. <br> <br> <br><br> <br> <br>       

## Pipeline Architecture🔗
<kbd><img align='center' src="https://github.com/pratikwatwani/Event-Based-Influence-on-Wikipedia/blob/master/assets/pipeline.png"></kbd><br/>

## Architectural Components🗜️
| Entity  | Purpose          | Type                                             |
|---------|------------------|--------------------------------------------------|
| AWS S3  | Raw Data Storage | -                                                |
| AWS EC2 | Spark Cluster    | Master - 1 x m5a.large<br>Worker - 5 x m5a.large |
| AWS EC2 | TimescaleDB      | 1 x m5.xlarge                                    |
| AWS EC2 | Web App          | 1 x t3.large                                     |
| AWS EC2 | Airflow Scheduler| 1 x t3.large                                     |
| AWS EC2 | Decompressor     | 1 x t3.large                                     |


## Challenges🤕
### Data
1. Splitting, keyword generation and binning. 
2. Fuzzy pattern matching. 
3. Data Modeling 
4. Query processing optimization.

### Architectural 
1. Database parameter optimization.
2. PySpark tuning.

## UI🖥
<p align="center"><kbd><img src="https://github.com/pratikwatwani/Event-Based-Influence-on-Wikipedia/blob/master/assets/UI/UI%201.png" width ="900px" height="400px"></kbd></p></br>
----
<p align="center"><kbd><img src="https://github.com/pratikwatwani/Event-Based-Influence-on-Wikipedia/blob/master/assets/UI/UI%202.png" width ="900px" height="400px"></kbd></p></br>
----
<p align="center"><kbd><img src="https://github.com/pratikwatwani/Event-Based-Influence-on-Wikipedia/blob/master/assets/UI/UI%203.png" width ="900px" height="400px"></kbd></p></br>

## Directory Structure🗂️
```bash
/
│
├── assets
│     ├── logo.png
│     ├── pipeline.png
│     ├── dataingestion
│     └── dataingestion
│
├──  src
│     │ 
│     ├── dataingestion
│     │     ├── scraper.py
│     │     ├── scraperModules
│     │     │      ├── __init__.py 
│     │     │      ├── linkGenerator.py
│     │     │      ├── fileWriter.py
│     │     ├── lists
│     │     │      ├── current_urls.txt
│     │     │      └── historic_urls.txt
│     │     └── runScrapper.sh
│     │
│     ├── decompressor  
│     │     └── decompressor.sh
│     │
│     ├── processor
│     │     ├── dbWriter.py
│     │     ├── wikiScraper.py
│     │     ├── gdeltProc.py
│     │     ├── gdeltModules
│     │     │      ├── __init__.py
│     │     │      ├── eventsProcessor.py
│     │     │      ├── geographiesProcessor.py
│     │     │      ├── mentionsProcessor.py
│     │     │      └── typeCaster.py
│     │     ├── wikiModules
│     │     │      ├── __init__.py
│     │     │      ├── metaProcessor.py
│     │     │      └── tableProcessor.py
│     │     ├── gdelt_run.sh
│     │     └── wiki_run.sh
│     │
│     ├── frontend
│     │     ├── __init__.py
│     │     ├── application.py
│     │     ├── appModules
│     │     │      ├── __init__.py
│     │     │      ├── dbConnection.py
│     │     │      └── dataFetch.py
│     │     ├── requirements.txt
│     │     ├── queries
│     │     │      ├── articleQuery.sql
│     │     │      └── scoreQuery.sql
│     │     └── assets
│     │            ├── layout.css
│     │            ├── main.css
│     │            └── logo.png
│     │
│     └── airflow
│           └── dag.py
│
├── License.md
├── README.md
├── config.ini
└── .gitignore
```

## Instructions📝

## Optimizations⚙️
1. Unpigz
2. Data Modeling
3. Query optimization
4. Database parameters
5. Serializing
6. Oversubscription
7. Partitioning
8. Spark-Submit 

## License🔑

This project is licensed under the AGPL-3.0 License - see the [LICENSE.md](LICENSE.md) file for details     


<h6>&copy; All product names, logos, and brands are property of their respective owners.</h6>
