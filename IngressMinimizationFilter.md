# Filter: Ingress Minimization

The bulk volume of DNS queries are to wellknown domains (such as www.google.com) and most of these are useful neither for analysis nor logging purposes. The [Ingress Minimization](#filter-ingress-minimization) filter removes these entries before they are sent to the query database. For the purpose of statistics, queries and clients are counted, generating the [Wellknown Domain Histogram](WellknownHistogramReport.md) dataset.

This filter is currently generated from lists such as Tranco or OpenPageRank, which are compiled into a DAWG and downloaded by Edge DNSTAP Minimiser. The process for generating the file can be found here: 

[Generate DAWG](DAWG_howto.md)

and a (small) example file file can be hound here:

[wellknown.dawg](wellknown.dawg)
