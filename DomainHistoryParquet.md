# Parquet: Domain History

A datastore that retains all domains seen (similar to passive DNS systems) and classification information related to those domains. Statistics are retained only insofar that they were relevant for classification. In essence the data is write-only, and, as it is the source of truth various lists such as Wellknown Domains, Suspect Domains, etc, modification of entries must be tracked and authorized carefully.

## Data

Domains

DomainTrie

Labels

<table>
  <tr>
    <th>Name</th>
    <th>Type</th>
    <th>Comment</th>
  </tr>
  <tr>
    <td>label0</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label1</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label2</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label3</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label4</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label5</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label6</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label7</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label8</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>label9</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
  <tr>
    <td>labelrest</td>        
    <td>bytestring</td>           
    <td>Domain name label</td>
  </tr>
</table>
