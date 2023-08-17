# Event: New domain

Whenever a new domain is seen in the query stream, this is sent as an event to the Core system. A domain is seen as new if it does not exist in the global _Wellknown domains_ set or the local _Previously seen_ set.

## Data

The main dataset is related only to the query data and response. This data is not directly connected to any given client. However, the query itself may be unique to a given client, which in the context of other queries could be used to correlate data to a specific user, but given that the _New domain_ event is taken out of this context and the encoding of the personal data is known only to the domain owner, this data is privacy safe. Also, there is no exact timing data included in the main data as arrival time to the analysis platform is sufficient, which mitigates using event time for correlation. 


'Name        Type            Description'
---
'''
name        bytestring      The full domain
type        int16           Query type
class       int16           Query Class
flags       int16           Header flags
ttl         int32           Resource record time-to-live
rdlength    int16           Length of RDATA
rdata       bytestring      Resource record
nsname      bytestring      Name of responding authoritative server
nsip        ip              Address of responding authoritative server
'''

Extensions for local use include information about the querying client, but these are not privacy safe and should be confined to the local system owner.

Name        Type            Description
---
client      ip              Pseaudonymized client IP address
timestamp   datetime        Client query time
qheader     int16           Request header flags


## Source

There are multiple strategies for creating this dataset. The straightforward approach is to collect the information from the resolver northbound query stream. One consequence of using this method is that it disconnects the query from the issuing client. For centralized analysis, this is advantageous, as it makes the data privacy safe, but from a system owner perspective it denies the possibility for mitigation if the query is identified as malicious.

This suggests a two-pronged approach. The event is generated from the northbound query stream directly. The correlation to the southbound client is done separately and the local event including the client is generated.


## Implementation thoughts

Since lookups must be very fast, finding domains that can be quickly ignored is first priority. For resolvers that use, for instance, pre-fetching of expiring cache entries, identifying these and discarding them without further lookups is desireable. 

The constraints for the concept of _New domain_ is that false negatives - that is, seen domains being reported again - is less problematic than false positives - domains not seen discarded as seen. An inverse bloom filter satisfies this criteria but is not easily updated with new entries. This suggests a multi-tiered approach.

Since parts of the already known domains are bootstrapped from a list, it is also possible to use a tiered approach within this space, such as using a DAWG for the long-term static entries and a Trie or hash table for the dynamic entries. See _Wellknown domains_ for a longer discussion.
