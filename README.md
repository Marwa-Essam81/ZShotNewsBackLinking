Ths is the  source code for the paper: **Zero-Shot Reranking with Encoder Models for News Background Linking**

# ZeroShotRerankingNBL

This is the source code for the paper with the title: Zero-Shot Reranking with Dense Encoder Models for News Background Linking. 

The code is written using both **Java (version "14.0.1")** and **Python (Python 3.8).**

**Required Data: **
- You need to download first the Washington Post collection file: **https://trec.nist.gov/data/wapost/**. The dataset is publicly available but you need to sign first an organizational aggrement form. Make Sure you request V3 of this collection. If you want to use this code without this dataset, then create some sample news articles in a collection file. An example of how an article's JSON object is formatted is given in the file: **NewsArticleFormat.txt**.
- For preprocessing the news articles, you need the stop words : **StopWordsSEO.txt** file provided in this repository. 

**1) Indexing the data:**
* Export the archive **Java.zip** archive.
* Create a maven project using the exported directory. This directory contains the **<Pom.xml>** file that defines the required dependencies for this project.
* Compile your project 
* To create an inverted index for the data, run **<indexer.class>**. The indexer class will first split the dataset file into multiple files for a quick indexing process, then it will call multiple threads to start indexing.

**2) Create a SQL database for the data:** 
* Use a local SQL engine such as SQLPro to create a database **"WPostDB"**.
* Import the provided file : **WPostDB.sql** into your created database to create the required tables.
* Run **<Database.class>** from within your maven project to insert the news articles from the dataset into the created database.


**3) Retrieve the Candidate Background Links:**
* Run <BackgroundLinking.class>. You will need the provided file **Queries.txt ** that contains the unique ids for the query articles.

**4) Rerank the candidate background links:**
* Export the archive **Python.zip** provided in this repository
* The file **<requirements.txt>** has the required python packages used in this work.
* For each of the Transfromer models that we compare in this paper, you will find a python file that implements the following:
	- Encoding the query articles and save its encodings on desk.
	- Encoding the candidate background links and save its encodings on desk.

* Kindly note that we preferred to encode the query and candidates first then load the encodings from the encoding files during the matching process for efficiency purposes. This way, one can choose to run the encoding methods either on a CPU or a GPU.
* Note that the file PromCSEModel.py is taken from the Open license PromCSE model respository : https://github.com/YJiangcm/PromCSE/tree/master (file promcse/models.py) but renamed for clarity

* The encoding process for each model varies given the model's required input length as shown in the paper. However, there are common methods that are used by all models (such as matching a candidate article's encoding to the query passages encoding). The file **<utils.py>** has these common methods. 

* The file **<ResultsIntegration.py>** contains the methods that calculate the integration between the lexical and the semantic relevance signals generated by the SBert Model as described in the paper. Export first the lexical and the semantic scores as shown in the encoder class **<SBertEncoder.py>**. Then, call the integration method required from **<ResultsIntegration.py>**. An example of calling the SumOfScores intergation function is shown in the file.




