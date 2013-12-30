#Machine Learning the Language of Chemistry As A Guide for Retrosynthesis




###Chemistry As A Language

Informally, there is a clear analogy between a chemist's understanding of a compound and a Chinese speaker's understanding of a sentence. In either case, the trained mind effortlessly identifies part-whole relationships, despite a lack of demarcations.  The analogy breaks down, however, since chemicals have no orientation, nor can their graphs be represented by simple lines as in sentences.

Despite the obvious differences, chemicals can be seen as conforming to generalization of language, where sentences are akin to simple polymers.  The two can be observed to obey similar part-whole statistics, as the following exercise demonstrates:

  1. Acquire from a database a sample of chemical compounds or (English) sentences.
  	a. Using NIH's [CIR database](http://cactus.nci.nih.gov/), we acquired 10000 random chemicals.
  	b. Using the [English Wikipedia](http://en.wikipedia.org), we acquired 10000 random sentences.  The spaces were removed, to make them similar to chemicals without demarcations.
  2. Construct a library of common subfragments.
    a. For chemicals, this is done by taking roughly 200 compounds, pairing them up, and computing the *most common subfragment*, as seen in Fig. 1
    
    ![Fig 1.](./pics/MCS.svg)
    
    Figure 1. Most Common Subfragment
    
    b. For language, this is done by taking roughly 200 sentences, and similarly pairing them up and finding the *largest common substring*.  To mimic the lack of orientation in chemistry, we ignore the order of sentences in this calculation.
  3. Compute the frequencies of the common fragments in the sample, and rank the most frequent as 1, the second most frequent as 2, etc.

The results of this exercise are shown in Fig. 2.  In both cases, the distributions can be fit to an *upper-truncated power law*, which may be explained by our small sample size [5].  A larger sample would exibit a proper power-law relationship.  Fits to both distributions are given in Fig. 3.

![Fig. 2](./pics/comparison.svg)

Figure 2. Rank vs. Frequency for chemical fragments and English sentence fragments

![Fig. 3](./pics/Fits-01.svg)

In the case of linguistics, the observed power-law distribution is known as *Zipf's Law* (1935).  As far as we know, this simple statistical observation has never been observed in chemistry before.  It immediately suggests that techniques for dealing with the analysis of language may fruitfully be applied to the analysis of chemical compounds.


![Eq 1.](./pics/tfidf.svg)

TF-IDF scores are commonly used to generate *word clouds* - Fig. 4 shows a word cloud for the Wikimedia Foundation's 2009-2010 annual report.  In a word cloud, the word's size is proportional to its TF-IDF score.

![Fig. 4](./pics/Wikimedia_Annual_Report_Word_Cloud.svg)
Figure 4. Word cloud for Wikimedia Foundation's 2009-2010 annual report 


TF-IDF naturally gives low weight to extremely common words like "a" and "the", as well as extremely uncommon words such as "sesquipedalian".  In chemistry, using the statistics we have computed, fragments like *methylene* will also get low weight.

### Ranking

In order to guide retrosynthesis, our algorithm identifies atoms as likely sites for retrosynthesis.  It *ranks* an atom `A` in molecule `M`, using a library `L` of submolecules with frequencies given by `F`, according to the following algorithm:

	def rank(A,M,L)
		submolecules <- Find all submolecules of M in library L
		entropy <- sum the TF-IDF scores of the submolecules for which A is a member
		return entropy 

![Fig. 5](./pics/alpha_cyclodextrin.svg)

Figure 5. α-cyclodextrin

![Fig. 6](./pics/sucrose.svg)

Figure 6. Sucrose

![Fig. 6](./pics/adeddu2.svg)

Figure 7. (HO)2-PO-S-C11-EG6-OH
## Conclusions




1. Jones, K. S. A Statistical Interpretation Of Term Specifity And Its Application In Retrieval. Journal of Documentation 28, 11–21 (1972).

2. Todd, M. H. Computer-aided organic synthesis. Chemical Society Reviews 34, 247–266 (2005).

3. Corey, E. J., Johnson, A. P. & Long, A. K. Computer-assisted synthetic analysis. Techniques for efficient long-range retrosynthetic searches applied to the Robinson annulation process. J. Org. Chem. 45, 2051–2057 (1980).

4. Samuel, A. L. Some studies in machine learning using the game of checkers. IBM J. Res. Dev. 3, 210–229 (1959).

5. Zipf, G. K. The psycho-biology of language. ix, (Houghton, Mifflin, 1935).

6. Burroughs, S. M. & Tebbens, S. F. Upper-Truncated Power Law Distributions. Fractals 09, 209–222 (2001).