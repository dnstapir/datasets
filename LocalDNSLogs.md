# Edge-local DNS logs

These logs are the remainder after Edge DNSTAP minimize (EDM) has removed queries marked for aggregation (or otherwise discarded). Currently the complete DNSTAP message with the IP address pseudonymised with CryptoPAn is stored locally at the Edge.

However, writing these logs is turned off by default as the local analysis engine is not fully implemented. Data will be tuned more closely to what is specifically needed as the local process evolves.


| #    | Name          | Type                  | Required       | Comment                                                            |
| :--  | :------------- | :-------------       | :------------- | :---------------------------------------------------------------   |
|1     |recordtype      |integer                |yes             |The type of DNSTAP record|
|2     |qtime           |Timestamp              |yes             |Query time|
|3     |label0          |Bytestring             |yes             |Top level domain name label (typically TLD, ccTLD or gTLD)|
|4     |label1          |Bytestring             |nullable        |Second domain name label|
|5     |label2          |Bytestring             |nullable        |Third domain name label|
|6     |label3          |Bytestring             |nullable        |Fourth domain name label|
|7     |label4          |Bytestring             |nullable        |Fifth domain name label|
|8     |label5          |Bytestring             |nullable        |Sixth domain name label|
|9     |label6          |Bytestring             |nullable        |Seventh domain name label|
|10    |label7          |Bytestring             |nullable        |Eighth domain name label|
|11    |label8          |Bytestring             |nullable        |Ninth domain name label|
|12    |label9          |list&lt;Bytestring&gt; |nullable        |Remaining domain name labels|
|13    |datagram        |Bytestring             |yes             |The DNSTAP datagram field (effectively the complete DNS packet)|
