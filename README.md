# SSMC - Semantic Similarity Measure Clustering
SSMC is a Python executable script designed to measure semantic similarity between a set of objects annotated by ontology terms. 
As is, the tool is intended for a very limited applicability using specific IC-based pairwise and groupwise semantic similarity measures. It currently supports the BMA and simGIC groupwise measures, the Resnik pairwise measure, and the Resnik, Sanchéz and Seco information content (IC) measures. Aditionaly, SSMC can cluster objects through their similarity scores using Spectral Clustering. 

## Functionalities

- ### Semantic similarity using multiple ontologies
SSMC uses the owlready2 module which can reason simultaneously over different ontogies without excessive time expenditure. It leverages this feature to recognize annotations from different sources and calculate semantic similarity using multiple ontologies. 

- ### Negative annotations
SSMC recognizes negative annotations (those often identified in annotation files by the NOT qualifier) and stores them separately from conventional (positive) annotations. SSMC also boasts an alternative polar implementation for BMA and simGIC that accepts negative annotations. 

- ### Semantic clustering
SSMC can model object semantic similarity scores into an affinity matrix, and use it as a precomputed input for distance-based clustering approaches. As only similarity scores are necessary, clustering functionality extends to the previous features.


## Installing and using SSMC
The script itself can be extracted and used as a runnable through CLI. SSMC requires the following python modules: collections, itertools, json, logging, math, matplotlib, numpy, owlready2, pandas, seaborn, sklearn, statistics, sys.

###  How to setup a run
SSMC accepts as input a JSON file with a series of mandatory (and optional) user defined configurations. An example has been provided in Configuration.json in the Example folder. It requires:
- __Object_Data__ - The path to a tab separated (tsv) file containing objects ids and their corresponding annotations. If there are multiple object annotation files, paths should be separated by a ";". All annotations must be identified by a valid IRI and must be separated by a ";" sign. If the file contains negative annotations, then each positive and negative anotation IRI must be prefixed by either a "+" and a "-" sign respectively. 
- __Ontologies__ - The path or paths to valid ontology files containing the terms used for object annotations and (optional but recomended) their term IRI prefixes. Supported ontology formats in owlready2 include RDF/XML and OWL/XML. 
- __Similarity Settings__ - Contains the ids of the semantic measures to be used (check table below). Measure arguments include a pairwise measure and an IC measure. Unecessary arguments will be safely ignored.

| Measure Name    | Type| SSMC ID  | Polar Version ID |
| ------------- |:-------------:|:-------------:|:-------------:|
|simGIC	|Groupwise| simGIC	| polGIC |
|BMA	|Groupwise|BMA	| polBMA| 
| Resnik  |Pairwise| Resnik1995	| - |
|Resnik  |IC|Resnik1995| -|
| Sanchéz  |IC|Sanchez2011| -|
| Seco  |IC|Seco2004| -|

- __Queries__ - Each query must have a path to its file (a tsv file containing object id pairs), a SSM_ID with semantic measure IDs (if multiple, separated by a "," sign), a Results path for the output. It may also contain optional information for the clustering approach, including the intended K number of clusters, the Score(s) used to cluster and the Cluster Path.

Once the configurations are finished, run through CLI using the JSON as the only argument.

### Test Run
The folder "Example" contains the necessary files for a test run (includes also the expected results files), provided you already have the Gene Ontology (GO) owl.  



## Authors
- __David Carriço__
- __Cátia Pesquita__

## Acknowledgments
This project has been funded by Portuguese FCT through the LASIGE Research Unit (UID/CEC/00408/2019), and by the SMILAX project - Semantic Mining with Linked Data (PTDC/EEI_ESS/4633/2014)
