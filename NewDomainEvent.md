# Event: New Domain

New Domain notifications are sent when incoming data triggers a unique event. Characteristics for event types is that they should be quite rare and specific. The model event is the "first ever seen" event, where a notification is sent when a domain is seen for the first time on a server.

## Data


| #  |  Name          | Type            | Required | Description|
|:---| :------------- | :-------------  |:-------- | :------------- |
| 1  | Flags          | Integer         | yes      | Response Header flags |
| 2  | Timestamp      | Timestamp       |          | Event time of transmission |
| 5  | QClass         | Int16            | no      | Query Class |
| 3  | QName          | Bytestring       | yes     | The fully qualified domain name |
| 4  | QType          | Int16            | yes     | Query type |
| 8  | RdLength       | Int16            | yes     | Length of RDATA |
| 8  | Type           | Int16            |         |  |
| 11 | Version        | IP               |         |  |

Extensions for local use include information about the querying client, but these are not privacy safe and should be confined to the local system owner.

| # |  Name          | Type            | Required | Description|
|:--| :------------- | :-------------  |:---------|:---------------------------------------|
| 12 | Client        | IP              | no       | Pseaudonymized client IP address |
| 13 | Timestamp     | Datetime        | no       | Client query time |
| 14 | QHeader       | Int16           | no       | Request header flags |

