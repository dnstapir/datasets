# Set: Wellknown domains

Members of this set are high frequency domains generally seen as benign or harmless. Examples are www.google.com, facebook.com, etc. 

## THoughts on implementation

Seeing as this set is used to exclude data from analysis or other processing very early in the process, it is the single most sensitive dataset in terms of manipulation. Given that any wildcards used in this list would hide subdomains or hosts from view, the initial premise is that it is an exact match list. It also need not change rapidly, so one strategy is to provide the entire list in a signed binary blob, using a perfect hashing (fast), DAWG (space efficient) or similar data structure, possibly in combination. Probabilistic data structures can also be used, with the strict requirement of no false positives (Type I error). 

### Candidate data structures

- Perfect hash table
- Trie
- DAWG
- Reverse bloom filter

