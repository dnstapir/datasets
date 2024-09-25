# Event: New Domain

New Domain notifications are sent when incoming data triggers a unique event. Characteristics for event types is that they should be quite rare and specific. The model event is the "first ever seen" event, where a notification is sent when a domain is seen for the first time on a server.

## Data


| #  |  Name          | Type            | Required | Description|
|:---| :------------- | :-------------  |:-------- | :------------- |
| 1  | Event          | Integer         | yes      | Type of event |
| 2  | Sendtime       | Timestamp       | no       | Event time of transmission |
| 3  | Name           | Bytestring       | yes     | The fully qualified domain name |
| 4  | Type           | Int16            | yes     | Query type |
| 5  | Class          | Int16            | no      | Query Class |
| 6  | RFlags         | Int16            | yes     | Response Header flags |
| 7  | TTL            | Int32            | no      | Resource record time-to-live |
| 8  | RdLength       | Int16            | yes     | Length of RDATA |
| 9  | RData          | Bytestring       | no      | Response data resource record |
| 10 | NSName         | Bytestring       | no      | Name of responding authoritative server |
| 11 | NSIP           | IP               | no      | IPv4 or IPv6 address of responding authoritative server |

Extensions for local use include information about the querying client, but these are not privacy safe and should be confined to the local system owner.

| # |  Name          | Type            | Required | Description|
|:--| :------------- | :-------------  |:---------|:---------------------------------------|
| 12 | Client        | IP              | no       | Pseaudonymized client IP address |
| 13 | Timestamp     | Datetime        | no       | Client query time |
| 14 | QHeader       | Int16           | no       | Request header flags |

