# Multientity Recommender
A recommender for 1000 most popular movies, books, and TV shows using GPT-Embeddings of their 30 most important keywords. This repository is meant to serve as a proof-of-concept. 

## Executive Summary
The method used here is to encode movies, books, TV shows as GPT Embeddings using the GPT Embeddings API to create a Word2Vec style recommender. Then we would convert the query into a GPT Embedding as well and find the closest movies in the new recommender space. This method is very similar to our current methodology of performing recommendations using Word2Vec. 


## Implementation: GPT-ADA Embeddings for Free Text Search
* This method leverages the GPT ADA Embeddings to create a Multientity Word2Vec style Recommender model. This is cached and stored. When a free text query is passed, it is turned into an embedding with the GPT-ADA API. The nearest neighbours to the query in the cached Recommender Model are returned. 

* Since all these approaches require the utilization of a paid API, we have decided to experiment only with 3000 entities from the IMDB and Goodreads datasets for books, movies, and TV shows. Here, encoding means - going from movie entity —>  text that would be the input to a subsequent GPT Embedding call. 

## Wins
* The machinery fits very well with our current implementation of recommendations. We can simply cache and store a GPTRecommender to immediately unlock Free text search. We can do any of the filtering/pools that we currently do with ease. 
* The query is very lightweight since the only on-the-fly computation is the generation of the GPT embedding for the free text prompt and then a recommendation call - both fulfilled in a few milliseconds.
* This provides proof-of-concept to create a multi-entity recommender with cross-vertical recommenders. Recommendations across books and movies and TV shows seem reasonabky consistent and are very promising to take it further. 
## Shortcomings
* Text encoding is the biggest open research question with this methodology. It turns out, giving just the movie title does not guarantee the embedding contains all the relevant information about the movie. It could place an overemphasis on the text itself. For eg: A query like “I want a feel-good sunshine type of movie” returns movies with “sun” or “warmth” explicitly in their title. 
* While overview and genre in GPT Encoding returned reasonably sound results, it did have some blindspots - it was not able to retrieve certain queries with great accuracy.  E.g “Movies with LGBT themes” gave surprising results like La La Land. It would bode well to invest in more prompt engineering to truly capture the nuances of semantics for mood elicitation for recommendations. 
* It does not understand semantics of logical operators such as and, or, not and only considers text similarity. So the query “movies about wizard boys but not Harry Potter” emphatically returns all Harry Potter movies. 
