# Filter: Ingress Minimization

The bulk volume of DNS queries are to wellknown domains (such as www.google.com) and most of these are useful neither for analysis nor logging purposes. The [Ingress Minimization](#filter-ingress-minimization) filter removes these entries before they are sent to the query database. For the purpose of statistics, queries and clients are counted, generating the [Wellknown Domain Histogram](WellknownHistogramReport.md) dataset.
