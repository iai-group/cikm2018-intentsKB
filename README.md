# IntentsKB: A Knowledge Base of Entity-Oriented Search Intents

This repository provides resources developed within the following paper:

> D. Garigliotti and K. Balog. IntentsKB: A Knowledge Base of Entity-Oriented Search Intents. In CIKM'18, October 2018.

These resources allow to reproduce the results presented in the paper.


## 1. Refiners Acquisition

Data obtained in the *refiners acquisition* pipeline stage (Sect. 5.1 of the paper) are placed under the directory `data/1-refiners_acquisition/`. 

 - A tab-separated file `1-top_entities_per_type/<type>/entity_pageviews.tsv` contains the top 1,000- most popular entities of the Freebase type `<type>` . Each row in the file is in the format:

```
<entity>	<pageviews>
```

 - After decompressing `2-API_query_suggestions.tar.gz` (into a directory of 1.3 GB of size), a JSON file `2-API_query_suggestions/<type>/<i>.json` contains the API query suggestions obtained for the `(i+1)`-th entity in the entities file of the type `<type>` (`i` >= 0). The content is of the shape:

```
{
    "<i>": <list of API query suggestions>
}
```

 - A tab-separated file `3-type_level_query_patterns/<type>.tsv` contains the type-level query patterns for type `<type>`, decreasingly sorted by frequency (total number of API query suggestions for entities in `<type>`). Each row in the file is in the format:

```
<type-level query pattern>	<frequency>
```


## 2. Refiners Categorization

Intent categories predicted in the *refiners categorization* pipeline stage (Sect. 5.2 of the paper) are contained in the tab-separated file `data/2-refiners_categorization/predictions.tsv`. Each row in the file is of the shape: 

```
<type>	<refiner>	<category>

```


## 3. Intents Discovery

Entity-oriented search intents discovered in the *intents discovery* pipeline stage (Sect. 5.3 of the paper) are stored in the tab-separated file `data/3-intents_discovery/clustering.tsv`. Each row in the file is in the format: 

```
<type>	<category>	<cluster ID>	<cluster label>	<refiner>	<similarity>
```


## 4. IntentsKB Knowledge Base


The final knowledge base (Sect. 5.4 of the paper) is stored in the tab-separated file `intentsKB/quadruples.tsv`, which contains rows each of the shape as follows (Sect. 3 of the paper):

```
<intent ID>	<predicate>	<object>	<confidence>
```

Here, `<object>` is `-` for the predicate `isAProfile` (each meaning a quadruple that only states the confidence of the intent profile; cf. Eq. (1) of the paper).


## Contact

Should you have any questions, please contact Darío Garigliotti at dario.garigliotti[AT]uis.no (with [AT] replaced by @).
