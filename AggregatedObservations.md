# Observation: Aggregated

Observations made in TAPIR Core are summarised into 32 defined meta-tags signifying some significant event or combination of events. These meta-tags are used by Edge Policy Manager for policy decisions. All relevant meta-tags are set in the message, and time-to-live signifies how long the data can be trusted by POP, after which it can be deleted. 

The implication of TTL is that messages need to be sent periodically to sustain a given policy action by POP. The TTL is effectively the time between actions in TAPIR Core to reaffirm the premise for the observation. This can vary, depending on the source data, but will always be the shortest TTL for the composition of meta-tags.  

There exists a formal "delete" message, if there is a need to (forcibly) remove an entry before the TTL time has expired. The TTL expiration acts as a safeguard should the "delete" message somehow fails. 


| #  |  Name                | Type           | Required | Description|
|:---| :------------------- | :------------- |:-------- | :------------- |
| 1  | SrcName              | Bytestring     | yes      | Source of the message data |
| 2  | MsgType              | Bytestring     | yes      | Type of message, e.g. "observation" | 
| 3  | ListType             | Bytestring     | yes      | Category of data, e.g. "greylist" |
| 4  | Added                | List of Struct | no       | Domains to be added for policy calculations. Can be an empty list |
| 5  | Added.Name           | Bytestring     | no       | Domain name the entry relates to |
| 6  | Added.TimeAdded      | Timestamp      | no       | Time the event was triggered, i.e. source detection time |
| 7  | Added.TTL            | Int32          | no       | Record time-to-live |
| 8  | Added.TagMask        | Int32          | no       | Aggregated meta-tags |
| 9  | Deleted              | List of Struct | no       | Domains to be deleted. Can be an empty list |
| 10 | Deleted.Name         | Bytestring     | no       | Name of responding authoritative server |
| 11 | Deleted.TimeDeleted  | Timestamp      | no       | Time the event was triggered at source |
| 12 | Msg                  | Bytestring     | no       | Arbitrary message. Can be an empty string |
| 13 | TimeStamp            | Timestamp      | yes      | Time of message transmission |
| 14 | Creator              | Bytestring     | yes      | Creator of the message |

