# Wikipedia_PageRank
Compute Page Rank using  Hadoop and Map Reduce on AWS clusters.

* In the first step we will be calculating the total number of articles present in the input files. For this we create a map and reduce task. The mapper will emit the article name as the key and  "1" in the value. In the reducer phase we will iterate through all the article names and get the summation of the total number of article names present and write it to a file named as num_nodes.

*	Now for calculating the page rank we will be taking 8 iterations. For the first iteration we are creating a different set of mapper and reducer so that the input file can be modified and we calculate the page rank based on the initial page rank.
We generate the output from the mapper phase in the following format:
```html
<outlink> <ArticleName> \t pagerank \t Total_number_of_outlinks_for_article
<ArticleName>  <!_A_>
```

The above pageRank is calculated by taking the **1\N**

* So we emit two set of items for each article in the mapper phase.
* In the reducer for the first iteration after the sort and shuffle phase, we get an article  along with all its inlinks and the set of     outlinks for the article.

  The input will be of this form :
  ```html
   <article> <!Outlinks> <inlink \t pagerank \t total_number_outlinks> <inlink \t pagerank \t total_number_outlinks>
  ```
* In the reducer we will calculate the page rank by the formula given. 
Then emit the following from the reducer:
  
```html
<Article><pagerank><list of outlinks>
```

Here the article will be the key and other will form the value and gets written in the file names as iter1.
* We have modified the output so that it is in the same format as the input that the mapper expects so that we can run it 8 number of times.


