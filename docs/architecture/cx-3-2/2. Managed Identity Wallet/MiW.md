# Managed Identity Wallet

To align the identity, authentication and data exchange of participants with the open and decentralized concepts within GAIA-X, especially self-sovereign identities, every legal entity associated to a BPNL number should have the possibility to also get a W3C compliant DID (Decentralized Identifier). Due to the lack of production-ready SSI infrastructure and slow adoption on the market, this is in a first step achieved by providing a managed wallet (also called "Custodian") with a private/public key pair and related DID for a legal entity along with the onboarding. This wallet can then be used via the Managed Identity Wallet API by other services or applications such as the Self Description or the EDC to issue and retrieve verifiable credentials and create verifiable presentations on behalf of a certain legal entity as part of governance processes and use cases. 

# EDC used Endpoints

## Get Credential

For Fetching an Credential the EDC can use the credentialendpoint
and define the Credential Type he wants to have. The Summary Credential 
can only be one time in a User Wallet.

"/api/credentials?type=['SummaryCredential']"

## Create Presentation

"/api/presentations?withAudience=['Audience1','Audience2']+asJwt=true"

## Validate Presentation

The Enpoint is called with the presentation in the body

"/api/presentations/validation?withDateValidation=true"

# Single Instance View 

![MIW Single Instance View](images/SingleInstanceDomainView.png)

# Summary VC

Summary VC Schema Documentation
Introduction
The Summary VC is a temporary credential designed to consolidate a set of individual Catena-X Verifiable Credentials (VCs) into a compact form. It serves the purpose of fitting within HTTP header limits, making it easier to transmit and process the credentials efficiently. This document provides the specifications for the Summary VC schema, outlining its structure and key properties.

Summary VC Example
Here is an example of a Summary VC in JSON-LD format:

```json
{
  "@context": [
    "https://w3id.org/2023/tractusx/credentials/summary/v1"
  ],
  "id": "<credential uid>",
  "type": [
    "VerifiableCredential",
    "SummaryCredential"
  ],
  "issuer": "<did:web:issuer>",
  "issuanceDate": "2023-06-02T12:00:00Z",
  "expirationDate": "2022-06-16T18:56:59Z",
  "credentialSubject": {
    "id": "<did:web:subject>",
    "holderIdentifier": "<BPN>",
    "type": "SummaryCredential",
    "items": [
      "MembershipCredential",
      "DismantlerCredential",
      "PcfCredential",
      "SustainabilityCredential",
      "QualityCredential",
      "TraceabilityCredential",
      "BehaviorTwinCredential",
      "BpnCredential"
    ],
    "contracTemplates": "https://public.catena-x.org/contracts/"
  }
}
```

## Summary VC Schema Specification
The Summary VC schema is based on the JSON-LD format and consists of the following properties:

- @context (array of strings): Specifies the context in which the Summary VC is interpreted. In this case, it references the Catena-X Summary VC schema version 1 context.

- id (string): Represents the unique identifier for the Summary VC.

- type (array of strings): Indicates the type of the credential. It includes "VerifiableCredential" and "SummaryCredential" to identify the Summary VC.

- issuer (string): Represents the decentralized identifier (DID) of the entity issuing the Summary VC.

- issuanceDate (string): Specifies the date and time when the Summary VC was issued, following the ISO 8601 format (e.g., "2023-06-02T12:00:00Z").

- expirationDate (string): Represents the date and time when the Summary VC will expire, following the ISO 8601 format.

- credentialSubject (object): Contains information about the subject of the Summary VC.

- id (string): Represents the decentralized identifier (DID) of the subject entity associated with the Summary VC.

- holderIdentifier (string): Provides an identifier (e.g., BPN) for the holder of the Summary VC.

- type (string): Specifies the type of the credential subject, which is "SummaryCredential" in this case.

- items (array of strings): Lists the types of individual Catena-X VCs included in the summary. Each item is represented by a string value corresponding to the type of the VC.

- contracTemplates (string): Indicates the URL pointing to the contract templates associated with the Summary VC.

Conclusion
The Summary VC schema defines a structure for consolidating multiple Catena-X VCs into a concise format suitable for transmission within HTTP headers. It allows for efficient processing and sharing of credentials while adhering to the limitations imposed by header size restrictions. The example provided demonstrates the key properties and their roles within the schema.