# Set: Wellknown domains

Members of this set are high frequency domains generally seen as benign or harmless. Examples are `www.google.com`, `www.facebook.com`, etc. 

## Data

This data is primarily used for filtering data, but it also aims to constitute the best approximation to a _known good_ classification. 

|  Name          | Type            | Description    |
| :------------- | :-------------  | :------------- |
|name            |bytestring       |The full domain |
|match_exact     |boolean          |Exact(1) or subtree match(0)|

category?
ttl?

## Source

THere are multiple parameters that define a wellknown, non-malicious domain name. A primary indicator is that it is queried and resolves uniformly across both time and space by large groups of clients. Unfortunately, this may be true for large endemic malware such as Conficker and can be artificially achieved by botnets set to game the system. 

Historically, the Alexa Top Million list has been used for this purpose and sometimes served as an exclusion filter for malicious domain names, resulting in there being a number of high-ranked malicious domains listed. There was also an assumption that the entire SOA of a listed domain was "safe". 

A long sliding window does 



## Implementation thoughts

Seeing as this set is used to exclude data from analysis or other processing very early in the process, it is the single most sensitive dataset in terms of manipulation. Given that any wildcards used in this list would hide subdomains or hosts from view, the initial premise is that it is an exact match list. It also need not change rapidly, so one strategy is to provide the entire list in a signed binary blob, using a perfect hashing (fast), DAWG (space efficient) or similar data structure, possibly in combination. Probabilistic data structures can also be used, with the strict requirement of no false positives (Type I error). 

### Candidate data structures

- Perfect hash table
- Trie
- DAWG
- Reverse bloom filter

