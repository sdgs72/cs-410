<h1> Guiding Questions </h1>

- What does a computer have to do in order to understand a natural language sentence?
1. Syntatic Analysis: Computers need to understand the syntatic category of a word (if a word is a noun/verb) (Part Of Speech Tagging)
2. Semantic Analysis: Computers need to understand the orders of a word (noun phrases)
3. Inference: Context and undestanding of the text also related to sentence ambiiguity) 

- What is ambiguity?
1. Given a sentence it can be inferred more than one way Example: A man saw a boy with a telescope. (Does this mean that the boy is using the telescope or the man is using a telescope to see the boy?) Other example: The trophy cannot fit inside the suitcase because it is to big)

- Why is natural language processing (NLP) difficult for computers?
1. It is hard to understand the context of a text. (word sense disintegratiion: Java could mean coffee or programming language depending on the context). 
2. Need the domain in order for NLP to work well.

- What is bag-of-words representation? Why do modern search engines use this simple representation of text?
1. Bag of words is where a document is parsed word by word and stored in a sort of hashtable where we will keep a counter of each word but we will lose the ordering of the document(and also lose word-phrase capabilities) however we will still retain the length and the number of occurences of each word in the document.

Bag-of-words representation is already good enough for most cases (chances are if you found a matching document it is accurate though not everytime but good enough). Since it is very hard to restrict searches in a certain domain automatically. And also because it scales well to other contexts


- What are the two modes of text information access? Which mode does a web search engine such as Google support?
1. Push - Users will receive notification about information (Example: movie recommendation). This however reuires the system to now information about the users.
2. Pull - Users will have to iniiate contact with the machine in order to get information (Pull have two different methods: Browsing and Querying). 
- - Querying - Requires keyword from the user. System will return a list of documents matching the keyword. Works well when the user knows what they are looking for 
- - Browsing - User navigates freely by following the UI structure of the document. Works well when the user doesn't know the exact keyword (or only know the rough keyword).

Google is categorized as "Pull" mode where users have to query in order to get (Netflix movie recommendation can be considered as "Push")

Another example is sightseeing. In SightSeeing while travelling if you know the address then you head directly to the location otherwise you would explore


- When is browsing more useful than querying to help a user find relevant information?
1. When the user doesn't know the exact keyword (or cannot enter the keyword)


- Why is a text retrieval task defined as a ranking task?
1. Algorithms to determine if a document is relevant to a query or not cannot be proven mathematically (empirical problem). So it is better if we let the user decide which document is right.
2. If we are using a document selection classified (where no "ranking" only true and false is outputed). The query can be either and it is hard to find the middle ground if we are not doing rankings
- - OverConstrained - No Document will be outputed
- - UnderConstrained - Too much document will be displayed confusing the user

Not all relevant documents are equally relevant


- What is a retrieval model?
1. A model where given a query, the model will return a colletion of documents.


- What are the two assumptions made by the Probability Ranking Principle?

The principle states that returning a ranked list of documents in descending order of probability that a document is relevant to the query is the optimal strategy under the following two assumptions.

1. The utility of a document is independent of the utility of another document. (The algorithm can score the document independently not as a group)

2. The users will browse the documents sequentially based on the rank.

However in reality this does not always hold (users can find a 2 document in a lower rank when combined to be stronger then 2 document in an upper rank. Users can also sometime scroll documents not in a sequential order). But in many cases it does work.


- How do we define the dimensions of the Vector Space Model(VSM)? What does “bag of words” representation mean?

VSM is a framework not an actual algorithm.

VSM contains 3 different components =  <b> Dimension, vector placament and similarity function</b>. Where we will rank the documents based on the grade given out by the similarity function.

In the simplest of form of VSM we can model the

Dimension - words in the vocabulary
 
Vector placement - Bit vector (0/1, absence/presence)

Similarity function - Dot product 

We will have 3 different components of the VSM.

The Vocabulary(V) = We will model each word in our list of vocabulary as 1 

The Query(Q) = Size of vector is the same as V, initialize with all Zeroes, for each word in Q that appears in V set that element to 1 (Bit vector).

The Document(Di) = similar to Q for each document.

VSM is like bag of words however we don't keep count of the # of occurences. In the simplest VSM the results will be returned in a sorted ranking where the highest value of the dot product between the Q and D (a single document) will be in the top of the result. However it doesn't put emphasis on the # of query word occurences in the document that can be misleading.


- What is the Vector Space Retrieval Model? How does it work?
1. See previous

- What does the retrieval function intuitively capture when we instantiate a vector space model with bag of words representation and bit representation for documents and queries?  

We will lose the ordering(phrasing of the words) and the number of occurence of a word as we will only value results with the highest dot product of the vectors that contain unique occurences. 



<h1> Key Concepts </h1>

- Part of speech tagging, syntactic analysis, semantic analysis, and ambiguity

- Bag of words representation

- Push, pull, querying, browsing

- Probability ranking principle

- Relevance

- Vector space model

- Dot product

- Bit vector representation  

