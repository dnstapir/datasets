# Set: Previously seen

This set contains all domains previously seen on the local data collector. Lookups must be fast and the data structure must be appendable.

At TAPIR Edge, this set is implemented as a key-value store (PebbleDB) where existence of the record indicates that it is previously seen. If it doesn't exist, the query is for a **locally new domain**, and is sent to TAPIR Core as a New Domain event.

In TAPIR Core, the events from all TAPIR Edge instances are aggregated into one lookup table, where existence indicates that the domain is previously seen. If it does not exist, the query is for a **globally new domain**. The lookup table only maintains domains seen for a fixed time period, so "new" is relative to that time period - the domain may have been queried outside of the observation window. 

In all circumstances, well-known domains (and any wildcarded well-known domains) are never seen as new.
