# Web-Search-Engine
### An inverted index for a set of webpages

Suppose we are given a set of webpages W. For our purposes, each webpage w ∈ W will be considered to be a sequence of words w1, w2, . . . wk. Another way of representing the webpage could be to maintain a list of words along with the position(s) of the words in the webpage.
      
The small connector words like “is”, “the”, “of”, “for” have not been stored. Words like this are referred to as stop words and are generally removed since they are very frequent and normally contain no information about the content of the webpage.

In mathematical notation we would say that given a webpage w = w1, w2, . . . , wk, the index of w is \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `{(u : i1(u), . . . i(u)) : wij (u) = u, 1 ≤ j ≤ }`.
    
An index is used to find the location of a particular string (word) in a specific document or webpage, but when we move to a collection of webpages, we need to first figure out which of the web pages contain the string. For this we store an inverted index. Let us try to define an inverted index formally.

### A scoring function for search term relevance
Given a word w and a webpage p, the relevance score is defined as \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `relevancew(p) = tf w(p) ∗ idf w(p)`

#### Term Frequency
It is the total number of occurrence of a word w in a webpage p, denoted by fw(p). It is normalized by the total number of words
in webpage p, denoted by |W(p)|. \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `tfw(p) = fw(p) / |W(p)|`

#### Inverse document frequency
It is the logarithm of the total number of webpages, denoted by N divide by the logarithm of the number of webpages
nw(p) that contain the word w. It is defined as \
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; `idfw(p) = log N / nw(p)`

### Compound Searches

#### OR queries
Given a search query q1 . . . qk, any page that contains any of the words q1 to qk is a valid answer. The relevance score of a page p
is computed as \
 `relevanceq1...qk (p) = Xk i=1 relevanceqi (p),`\
and pages are returned in decreasing order of relevance. Note that if some qi does not occur in page p the relevanceqi
(p) = 0.

#### AND queries
Given a search query q1 . . . qk, any page that contains all of the words q1 to qk is a valid answer. The relevance score of a page
p is computed as \
`relevanceq1...qk (p) = Xk i=1 relevanceqi (p),`\
and pages are returned in decreasing order of relevance.

#### Phrase queries
Given a search query q1 . . . qk, any page that contains q1 in position , q2 in position +1 and so on till qk in position +k−1
is said to contain the phrase q1 . . . qk at the position . Suppose in a webpage p having |W(p)| words, the phrase q1 . . . qk occurs m times then the relevance score of page p for this phrase is \
`relevanceq1...qk (p) = tfq1...qk (p) ∗ idfq1...qk (p) = m |W(p)| − (k − 1) ∗ m ∗ log N /nw(p)`
