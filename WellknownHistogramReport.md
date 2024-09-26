# Report: Wellknown Domain Histogram

Most wellknown domains are mostly uninteresting from an analysis perspective, yet the number of clients and queries are interesting for the understanding of a DNS queries baseline, making it possible to relate interesting events and changes to the overall state of the DNS environment. 

| #   | Name                | Spark type                     | Comment                                     |
|:----|:--------------------|:------------------------------ |:----------------------------------------    |
| 1   | Date                | DatetimeType()                 | Date of histogram                           |
| 2   | Creator             | StringType()                   | The resolver which is created the histogram |
| 3   | Label0              | StringType()                   | Top level label of domain name              |
| 4   | Label1              | StringType()                   | Second label of domain name                 |
| 5   | Label2              | StringType()                   | Third label of domain name                  |
| 6   | Label3              | StringType()                   | Fourth label of domain name                 |
| 7   | Label4              | StringType()                   | Fifth label of domain name                  |
| 8   | Label5              | StringType()                   | Sixth label of domain name                  |
| 9   | Label6              | StringType()                   | Seventh label of domain name                |
| 10  | Label7              | StringType()                   | Eighth label of domain name                 |
| 11  | Label8              | StringType()                   | Ninth label of domain name                  |    
| 12  | Label9              | StringType()                   | Tenth label of domain name                  |
| 13  | Hour                | ByteType()                     | hour of the day when the query was sent     |
| 14  | Minute              | ByteType()                     | minute of the day when the query was sent   |                              
| 15  | Tagstring           | StringType()                   | General representation of tag string, <br/> attributes related to the domain name   |
| 16  | Fqdn                | StringType()                   | Fully qualified domain name                 |                              
| 17  | RFqdn              | StringType()                    | Reversed fully qualified domain name        |
| 18  | IdnFqdn            | StringType()                    | Internationalized domain name               |
| 19  | ACount              | DecimalType(20,0)              | Count of A queries                          |
| 20  | AAAACount           | DecimalType(20,0)              | Count of AAAA queries                       |
| 21  | MXCount             | DecimalType(20,0)              | Count of MX queries                         |
| 22  | NSCount             | DecimalType(20,0)              | Count of NS queries                         |
| 23  | OtherTypeCount      | DecimalType(20,0)              | Count of other query types                  |
| 24  | NonINCount          | DecimalType(20,0)              | Count of non-IN query class                 |
| 25  | OKCount             | DecimalType(20,0)              | Count of successful queries                 |
| 26  | NXCount             | DecimalType(20,0)              | Count of NXDOMAIN queries                   |
| 27  | FailCount           | DecimalType(20,0)              | Count of failed queries                     |
| 28  | OtherRcodeCount     | DecimalType(20,0)              | Count of other return codes                 |
| 29  | Deltas              | ArrayType(IntegerType())       | Time deltas between values                  |
| 30  | OKPerClient         | ArrayType(IntegerType())       | Count of successful queries per client      |
| 31  | NXPerClient         | ArrayType(IntegerType())       | Count of NXDOMAIN queries per client        |
| 32  | FailPerClient       | ArrayType(IntegerType())       | Count of failed queries per client          |
| 33  | OtherRcodePerClient | ArrayType(IntegerType())       | Count of other return codes per client      |
| 34  | OtherTypePerClient  | ArrayType(IntegerType())       | Count of other types per client             |
| 35  | NonINPerClient      | ArrayType(IntegerType())       | Count of non-IN queries per client          |
| 36  | v4Clients           | ArrayType(IntegerType())       | Count of v4 clients                         |
| 37  | v6Clients           | ArrayType(IntegerType())       | Count of v6 clients                         |
| 38  | v4ClientsHLL        | BinaryType()                   | Hyper Log Log sketch of IPv4 clients        |
| 39  | v6ClientsHLL        | BinaryType()                   | Hyper Log Log sketch of IPv6 clients        |
| 40  | v4ClientsCount      | IntegerType()                  | Total count of v4 clients                   |
| 41  | v6ClientsCount      | IntegerType()                  | Total count of v6 clients                   |
