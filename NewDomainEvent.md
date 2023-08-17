# Event: New domain

Whenever a new domain is seen in the query stream, this is sent as an event to the Core system. A domain is seen as new if it does not exist in the global _Wellknown domains_ set or the local _Previously seen_ set.

## Data

The main dataset is related only to the query data and response. This data is not directly connected to any given client. However, the query itself may be unique to a given client, which in the context of other queries could be used to correlate data to a specific user, but given that the _New domain_ event is taken out of this context and the encoding of the personal data is known only to the domain owner, this data is privacy safe. Also, there is no exact timing data included in the main data as arrival time to the analysis platform is sufficient, which mitigates using event time for correlation. 

<table>
  <tr>
    <th>Name</th>        
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>name</td>        
    <td>bytestring</td>      
    <td>The full domain</td>
  </tr>
  <tr>
    <td>type</td>        
    <td>int16</td>           
    <td>Query type</td>
  </tr>
  <tr>
    <td>class</td>       
    <td>int16</td>           
    <td>Query Class</td>
  </tr>
  <tr>
    <td>flags</td>       
    <td>int16</td>           
    <td>Header flags</td>
  </tr>
  <tr>
    <td>ttl</td>         
    <td>int32</td>           
    <td>Resource record time-to-live</td>
  </tr>
  <tr>
    <td>rdlength</td>    
    <td>int16</td>           
    <td>Length of RDATA</td>
  </tr>
  <tr>
    <td>rdata</td>       
    <td>bytestring</td>      
    <td>Resource record</td>
  </tr>
  <tr>
    <td>nsname</td>      
    <td>bytestring</td>      
    <td>Name of responding authoritative server</td>
  </tr>
  <tr>
    <td>nsip</td>        
    <td>ip</td>              
    <td>Address of responding authoritative server</td>
  </tr>
</table>

Extensions for local use include information about the querying client, but these are not privacy safe and should be confined to the local system owner.


<table>
  <tr>
    <th>Name</th>        
    <th>Type</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>client</td>
    <td>ip</td>              
    <td>Pseaudonymized client IP address</td>
  </tr>
  <tr>
    <td>timestamp</td>   
    <td>datetime</td>        
    <td>Client query time</td>
  </tr>
  <tr>
    <td>qheader</td>     
    <td>int16</td>           
    <td>Request header flags</td>
  </tr>
</table>


## Source

There are multiple strategies for creating this dataset. The straightforward approach is to collect the information from the resolver northbound query stream. One consequence of using this method is that it disconnects the query from the issuing client. For centralized analysis, this is advantageous, as it makes the data privacy safe, but from a system owner perspective it denies the possibility for mitigation if the query is identified as malicious.

This suggests a two-pronged approach. The event is generated from the northbound query stream directly. The correlation to the southbound client is done separately and the local event including the client is generated.


## Implementation thoughts

Since lookups must be very fast, finding domains that can be quickly ignored is first priority. For resolvers that use, for instance, pre-fetching of expiring cache entries, identifying these and discarding them without further lookups is desireable. 

The constraints for the concept of _New domain_ is that false negatives - that is, seen domains being reported again - is less problematic than false positives - domains not seen discarded as seen. An inverse bloom filter satisfies this criteria but is not easily updated with new entries. This suggests a multi-tiered approach.

Since parts of the already known domains are bootstrapped from a list, it is also possible to use a tiered approach within this space, such as using a DAWG for the long-term static entries and a Trie or hash table for the dynamic entries. See _Wellknown domains_ for a longer discussion.
