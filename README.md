# SearchEngine-Project-Description

The goal of this project was to create a search engine using a MapReduce pipeline, a REST API, and serverside dynamic pages. Starting with an expansive list of wikipedia documents, I set out to create a program which given a text based query from a user would return the ten most relevant documents. To do this I calculated a relevancy score by using a MapReduce pipeline to calculate tf-idf. The four staged pipeline  finds the term frequency (tf) of the query across the set of documents and the inverse document frequency (idf) across all documents, each in a different stage of the pipeline. I strategically changed my key value pairs in each stage to allow for different analyses of the text. Using the tf's and idf's I found, the program makes 3 inverted indices which allow it to read the tf's for each term within a document and the idf's for a term across all documents within the same data structure. 

With the inverted indices' data, the program can calculate tf-idf for each term create a normalization for the terms in the query by sending the inverted indices to 3 separate index servers. A REST API reads the scores from these servers and deduces which were the top 10 scores among the 3 servers. If there are any tiebrakers the most important documents would be determined by a list of hardcoded pageranks for each wikipedia page. 

Then the REST API sends the page IDs to a frontend server which displays all the pages using Flask and HTML. The page ID is a primary key to a SQLite database which stores all the relevant information on each document, including the title, url, and brief description. By performing SQL queries on each of the 10 page IDs the program extracts the necessary data and displays it on the search results page. 

The search engine looks as follows: 

<img width="425" alt="image" src="https://github.com/omastey/SearchEngine-Project-Description/assets/67980312/c09bb2c5-64f0-4f3a-ab8e-d8fa1bc6ee15">


