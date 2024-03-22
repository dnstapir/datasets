```mermaid

%%{
  init: {
  "theme": "dark",
  "themeVariables": {
    "fontFamily": "monospace"
  }
}%%

flowchart LR
    A[DNS payload 
    <span style="font-size:11px;text-align:left;">rfc1035
    rfc6871</span>
] --- R(Resolver)
    B[DNS over UDP
    <span style="font-size:11px;">rfc1035
    </span>] --- R
    C[DNS over TCP
    <span style="font-size:11px;">rfc7766
    </span>] --- R
    D[DNS over TLS
    <span style="font-size:11px;">rfc7858
    </span>] --- R
    E[DNS over HTTPS
    <span style="font-size:11px;">rfc8484
    </span>] --- R
    F[DNS over QUIC
    <span style="font-size:11px;">rfc9250
    </span>] --- R
  R:::service --- T[DNStap data

    <span style="font-size:11px;">Server identity
    Server version
    Extra data
    Message type

    Message:
      Query type
      Socket family
      Socket protocol
      Query address
      Response address
      Query port
      Response port
      Query time_sec
      Query time_nsec

Query message:
DNS query payload
Query zone
Response time_sec
Response time_nsec

Response message:
DNS response payload

Policy list:
Policy event:
Policy type
Policy rule
Policy action
Policy match
Policy value
</span>]:::left
DTM --- Event["Event Notification

<span style='font-size:11px;'>Version
Timestamp (min)
Type: new_qname
Qname
Qtype
Qclass
Flags
Rdlength
Type: new_aggregate
See metadata</span>
"]:::left
T --- DTM(DTM):::service
DTM --- Hist["DNS Histogram
<span style='font-size:11px;'>
Timestamp (min)
Query name (labels0-9)
A_count
AAAA_count
MX_count
NS_count
Other_count
NonIN_count
OK_count
NX_count
Fail_count
Tag_Bitfield
Tag_String
V4Client_HLLbytes
V6Client_HLLbytes</span>
"]:::left

DTM --- Mini["Minimized DNS log

<span style='font-size:11px;'>Query name (labels 0-9)
QueryTime (ms)
ResponseTime (ms)
source_ipv4 (CryptoPAn)
dest_ipv4
source_ipv6_net (CryptoPAn)
source_ipv6_host (CryptoPAn)
dest_ipv6
source_port
dest_port
DNSprotocol

Query message
Response message</span>"]:::left
Mini --- L(Localise):::service 
L --- HL["DNS Histogram local

<span style='font-size:11px;'>Timestamp (min)
Query name (labels)

Uploaded histograms"]:::left
L --- QV["DNS Query Vectors
<span style='font-size:11px;'>
Starttime
Stoptime
Sequence of:
hash32(qname)

Dictionary:
Hash → qname, qname"
]:::left
HL --- AF(Aggregate Receiver)
QV --- AF
Hist --- AF
AF --- Gb(Globalise
<span style='font-size:11px;'>Intelligence Feed</span>)
Event --- Er(Event Receiver)
Er --- Gb
Gb --- Tem("TEM
<span style='font-size:11px;'>Event Nofication
(subset, new domain)"</span>)
Gb --- 3p(3rd Party
<span style='font-size:11px;'>Domain name list</span>)
Gb --- W("Web
<span style='font-size:11px;'>Histogram (categorized)
Domain name list"</span>)

classDef service fill:#295499,color:#000
classDef left text-align:left;

```
