# 1. Introduction: The Summary VC

The Summary VC (S-VC) is a temporary credential designed to roll-up a number of other Tractus-X VCs into a compact form
that will fit within HTTP header limits. This document specifies the Summary VC schema.

The following is an example Summary VC:

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

A Json-Ld context defining Summary VC terms is [here](./summary.vc.context.v1.json)

# 2. Verifiable Credential Properties

## 2.1. Credential Subject and Credential Holder

The credential subject and credential holder must be the same as described by
the [Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model/#subject-is-the-holder).

- The mandatory `id` property of the `credentialSubject` object must be set to the subject's DID (`did:web`).
- The mandatory `holderIdentifier` property of the `credentialSubject` object must be set to the subject's BPN.

## 2.2 Summary Items

The mandatory `items` property defined by the `https://w3id.org/2023/tractusx/credentials/summary/v1` context contains a
set of string identifiers indicating the credential types held by the subject.

Valid items are:

- cx-active-member
- cx-dismantler
- cx-pcf
- cx-sustainability
- cx-quality
- cx-traceability
- cx-behavior-twin
- cx-bpn

## 2.3 Mandatory Properties

If mandatory properties are not present, the VC should be interpreted as invalid.

# 3. Issues

The following are outstanding questions and issues that need to be resolved. There is
a [proposed context](./summary.vc.context.modified.v1.json) that resolves these issues.

## 3.1. Clear Properties

- What are `credentialSubject#type` and `credentialSubject#name` used for?

## 3.2 Consistent Naming

- The `credentialSubject#items` property is too ambiguous and should be something
  like `credentialSubject#hasCredentials`
- The `credentialSubject#contract-template` property uses hyphens and should be consistent with W3C camelCase
- The `credentialSubject#items-template` property uses hyphens and should be consistent with W3C camelCase

## 3.3 Referencing Credential Types

Credentials referenced in the [Summary Items property](#22-summary-items) should correspond to credential types, not
hyphenated strings, e.g.`DismantlerCredential` instead of `cx-dismantler`. Note that actual types will not be used as
that would require term definitions in the VC context.

The proposed valid property values are:

- MembershipCredentialCX
- DismantlerCredential
- PcfCredential
- SustainabilityCredential
- QualityCredential
- TraceabilityCredential
- BehaviorTwinCredential
- BpnCredential

## 3.4 Use of IRIs

The `credentialSubject#contract-template` property should be an IRI instead of text. There it should be defined as
type `@id`:

```json
{
  "contractTemplate": {
    "@id": "summary:contractTemplate",
    "@type": "@id"
  }
}
```
