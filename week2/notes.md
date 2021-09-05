<h1> Goals and Objectives </h1>

Explain what TF-IDF weighting is and why TF transformation and document length normalization are necessary for the design of an effective ranking function.
Explain what an inverted index is and how to construct it for a large set of text documents that do not fit into the memory.
Explain how variable-length encoding can be used to compress integers and how unary coding and gamma-coding work.
Explain how scoring of documents in response to a query can be done quickly by using an inverted index.
Explain Zipf’s law.

<h1> Guiding Questions </h1>

<h3> What are some different ways to place a document as a vector in the vector space? </h3>



<h3>  What is term frequency (TF)? </h3>

- In VSM, instead of using bit vectors when representing documents we will also incorporate the term occurence as well. However this introduces problems
where if a query contains an unimportant common word (Example: About, Of) unrelevant document that contains a lot of these world will be ranked higher. 
We can solve this by having a way on how to approximate if word is unimportant(IDF).


<h3> What is TF transformation? </h3>

- how to determine the value of word occurence in a document? (bit vector vs term frequency vector)

- motivation should not reward multiple terms so genereously which happens if we are using term frequency vectors (to bypss this issue querying "political campaign" ending up showing document with a lot of "food campaign" instead of some with political). Create function to represent term frequency properly without concerns of over compensating a word that occurs too many time.

- to capture the diminishing return from higher text frequency (avoid dominance of a word that occurs too many time, when we are using TF)

- we have several functions of TF so far   c(w,d) -> TF(w,d)   (where w= word, d=document, c= count of word in document, TF = function for word count term frequency)
- - bit vector (this will remove the value of word occurence completely)
- - full TF (this is vulnerable to words that appear too much in a document) 
- - log(1 + word_count)  (this is okay but we can do better?)
- - log(log(1+ word_count)) (better then before can we do better?)
- - BM25 =  (k+1)*word_count/(word_count+k) (industry standard, lower bound of bit vector when k is set to be 0, upper bound of full TF (fully linear, sensitive to occurence again), if K is very big)

<h3> What are the main ideas behind the retrieval function BM25? </h3>

- (k+1)*word_count/(word_count+k) 
- used to avoid the over dominance of a single term over others (diminishing returns)
- has upper bound of full TF vector
- has lower bound of bit vector
- robust and effective
- pretty good in most scenarios and it is very flexible since we can adjust the k parameter


<h3 > What is document frequency (DF)? </h3>

- total number of documents that contains a target word (See IDF) used in the IDF formula
- the maximum value of DF is the total number of documents in the collection set


<h3> What is inverse document frequency (IDF)? </h3>

- A function that is used to estimate if a word is a common unimportant word or not. This is done by calculating the log ratio of the number of documents to the number of documents that contains the word . The higher the occurence the lower the IDF value is. 
- The formula can be modelled as IDF(W) = log ( (M+1) / k)
- - W = is the word in question
- - M = total number of docs
- - k = number of documents that contains the word (minimum value of k is 0) - (DF)
- - note that M >= k  
- minimum value of IDF(W) = log( (M+1) + M ). (word exists in all document)
- maximum value of IDF(W) = log( (M+1) /1). (word only exists in one document)
- We use log instead of linear because we watned to be sensitive (if the occurence of the word is already around 50% we wanted to penalize this harsher then if it were 20%)

<h3> What is TF-IDF weighting? </h3>

- Formula of VSM where we dot product the TF and the IDF therefore incorporating the sense of word importanteness to our ranking formulae
- even with TF-IDF 


<h3> Why do we need to penalize long documents in text retrieval? </h3>

- the longer document, the higher the probability that it will match any type of query. That is why we wanna penalize documents that are really really long and doesn't contain a lot of content.
- a document is long because
- - it has more content (less penalization)
- - it uses more words (need to penalize)


<h3> What is pivoted document length normalization? </h3>

- average doc length as a "pivot" or standard.
- normalizer = 1 - b + d/(avdl) . where B is 0 <= B <= 1. d is how long it is away from the pivot. avdl is the pivot.
- if the length of the document is similar to the pivot we will give a value of 1. 
- - If it is shorter then the pivot the document ranking will be rewarded (dividided with value < 1).
- - If it is longer then the pivot the document ranking will be penalized (divided with value > 1)



<h3> What is the typical architecture of a text retrieval system? </h3>

Search engine system can contain 3 parts, indexer,scorer,feedback

- tokenizer = converts text to tokens
- - converts documents to document representation (index) which will be passed to the indexer
- - converts user queries to query representation which will be passed to scorer
- - performs normalization of lexical units and stemming = map similar words (programming and programmer --> "program" , computer and computation and compute --> computing)
- indexer = convert documents to data structure for fast search
- - works "offline" mode, can be done in a preprocessing (before user query)
- - use inverted index in most cases
- - can also use document index
- scorer = 
- - works "online" mode, needs user query to judge which document is best
- feedback =  (user judgment if a document matches uer query)
- - can be done "online"/"offline" depending on the use case (online if it requires real time feedback otherwise can be done with a async survey)





<h3> What is an inverted index? </h3>

have 2 data structures = "dictionary" and "postings"

<b> dictionary(lexicon) </b>
- create a hashtable, and for each term in the vocabulary 
- stores the global statsitics of the term in the document collection (IE: # of docs that contains the word, total frequency)

<b> postings </b>
- statistics for a term <> document_id combo
- it will store like the list of possitions that the term occured in the document, how frequently it occurs in that document and ETC2 


- use ram and use index
- emprical distirbution of index 
- ZIPF's law (rank * frequency^alpha = C where 0<=C<=1 and alpha approx= 1) 
- - a few words occur very frequently("a","of","we","about") but most words occur rarely
- - most frequent words in one corpus maybe rare in another




<h3> Why is it desirable to compress an inverted index? </h3>

- What we are comrpessing here is the "postings" table because it will be huge as it will be like the denormalized version of 
- save space 
- improve speed retrieval from disk (IO)


<h3> How can we create an inverted index when the collection of documents does not fit into the memory? </h3> 
 
Lesson 2.5
- distributed way, and store it in disk use merge sort to merge all the results
- also compress (compress integers)

TF Compression 
- ZIPf's law, words with small number of frequencies will be more then words with large number of frequencies.
- fewer bits for small integers at the cost of high bits for larger integers

DOC-ID Compression
- d'gap (store difference): d1, d2-d1, d3-d2
- Possible since we are processing documents sequentially

Integer compression methods
- Binary = equal length coding (works only in fixed length (int32, int64))

For variying length use these
- Unary = variable length, only useful when the integers are really small (1 = 1, 110 = 3, 11110 = 5 ). 0 is used as the sentinel and 1 for +1
- Gamma encoding = https://nlp.stanford.edu/IR-book/html/htmledition/gamma-codes-1.html . Prefix is unary coding of (1 + floor(log(x))) and suffix is the binary representaiton with the leading 1 removed (left most 1 removed). (The ones of the prefix also indicates the length of the suffix)
- 



<h3> How can we leverage an inverted index to score documents quickly?    </h3>

Lesson 2.6





<h1> Key Phrases and Concepts </h1>

Term frequency (TF)
Document frequency (DF) and inverse document frequency (IDF)
TF transformation
Pivoted length normalization
BM25
Inverted index and postings
Binary coding, unary coding, gamma-coding, and d-gap
Zipf’s law 



<h1> notes </h1>


Gamma Encoding

Prefix is unary
3 -- 10 1 
4 -- 110 00 
5 -- 110 01 
6 -- 110 10 
7 -- 110 11 (length is 110, meaning that there will be 2 suffix)
8 -- 1110 
9 -- 1110 001