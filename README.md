# Datasets
Datasets generated within the data collection and analysis systems

## Events

Events are sent for analysis as they happen

- [New Domain Event](NewDomainEvent.md)
- [Suspect Domain Event](SuspectDomainEvent.md)

## Reports

Reports are collections of data that are sent for analysis at timed intervals

- [Histogram](HistogramReport.md)

## Vectors

Vectors are encoded sequences of queries

- [Query Vector](QueryVector.md)

## Sets

Sets are, in essence, lookup tables

- [Wellknown Domains](WellknownDomainsSet.md)
- [Previously Seen](PreviouslySeenSet.md)

## Transformations

Transformations is the process that transforms one dataset into a different dataset, typically for the purpose of feature extraction, aggregation and/or privacy enhancement.

- [Pseudonymization](PseudonymizationTransform.md)

## Filters

Filters primarily serve to minimize data by removing uninteresting data or noise. These filters act on the collected data and are different from filters acting on the DNS query-response process.

- [IngressMinimization](IngressMinimizationFilter.md)
