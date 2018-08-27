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

### Search results

Additionally, the results of searching for entity-bearing queries with Google Custom Search Engine (CSE) (Sect. 4.2 of the paper) are contained under 2 compressed directories (`freq_{5_to_9,10+}.tar.gz`), shared in this [link](link) **TODO** . Once decompressed:

  - A file `cse_results-freq_10+/<type>/query_<i>.json` contains the JSON response after searching for the actual entity-bearing query that results from instantiating the `(i+1)`-th type-level query pattern with the most prominent entity of that type. (Such a pattern is the one in the `(i+1)`-th row of `data/1-refiners_acquisition/3-type_level_query_patterns/<type>.tsv`.)
  - Analogously, a file `cse_results-freq_5_to_9/<type>/query_<i>.json` contains the JSON responses for less frequent type-level refiners. Specifically, it contains the response for the `(i+1)`-th type-level query pattern, considering *only* the patterns with frequency in the range `[5..9]` (i.e., the pattern in the `(i + N_<type> + 1)`-th row of `data/1-refiners_acquisition/3-type_level_query_patterns/<type>.tsv`, with `N_<type>` being the number of query patterns for `<type>` with frequency larger than 9).

Each JSON file is in this format:

```
{
    "1_type": <type>,
    "2_tl_q": <type-level query pattern>,
    "3_ae_q": <actual entity-bearing query>,
    "4_f": <frequency of type-level query pattern>,
    "5_results": {
        "items": <list of top-10 search results>,
        ...
    }
}
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
