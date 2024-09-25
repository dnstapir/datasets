# Transform: Pseudonymization

Pseudonymization acts on the client IP addresses (or similar direct identifiers) in order to obscure the identity of the client. The process produces a one to one mapping between the identifyer and a pseudonym key using an encryption key. Since the process is reversible and maintains a consistent map between the two, it is not anonymization and should not be seen as such.

TAPIR Edge implements this using CryptoPAn for client addresses stored locally. These are never transmitted outside the Edge system. 
