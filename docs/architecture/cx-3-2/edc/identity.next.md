# 1. Introduction

This document provides a technical specification for how Tractus-X will support self-issued access tokens and verifiable
credentials in conjunction with `Managed Identity Wallets` (MIW) for core data-sharing operations.

### 2. Requirements

The following are the key requirements that inform this specification:

1. **Interoperability** - This specification will not require any implementation-specific or proprietary features. It
   must be possible for Relying Parties (RPs) to run on entirely different software infrastructures and still
   interoperate.
1. **Open Standards** - We will not re-invent the wheel. Existing standards will be used as much as possible.
1. **Open Source** - There must be an open source implementation of all components outlined in this specification.
1. **Business User Policies** - Business users must be able to easily author all required policies

A separate document will provide a technical design for implementing this specification in Tractus-X EDC.

# 3. Catena-X Identity

The `Dataspace Protocol Specifications` (DSP) are based on the concept that all participants have a stable identifier.
Software systems, or `participant agents`, act on behalf of participants to perform operations such as data sharing. In
this scheme, participant agent identities may be ephemeral since all operations such as signing `contract agreements`
are associated with the participant identity.

The fundamental stable identifier in Catena-X is the BPN. This specification will also make use of DIDs, which can be
employed to cryptographically verify a participant identity. These are related as follows:

```
BPN  ----- Can resolve to ----> DID
 ^                                |
 |                                |
 |----------Associated with--------                               
```

In this scheme it is possible for a participant to change its DID without altering its stable identifier. For example, a
participant may opt to change its hosting environment, resulting in a change to its DID such as the URL associated with
its DID in the case of `did:web` or its DID method. Since its BPN remains stable, existing signed contracts will not be
impacted.

# 4. Limitations

The following will be technical limitations of the first milestone:

1. Only [did:web](https://w3c-ccg.github.io/did-method-web/) will be supported, although it will be possible to
   accommodate other methods in the future.
2. Verifiable Presentations (VP) will only be transmitted as part of a client access token. A protocol for accessing VPs
   by a Relying Party will be supported in a future milestone. Since access tokens transmitted in HTTP headers are
   practically limited to 8K by most web infrastructure, size constraints will impact VP design.
3. The protocols described in this specification do not constitute a self-sovereign identity system (SSI) as key parts
   require hosted infrastructure.
4. Only one proof scheme for Verifiable Credentials will be
   supported - [JSON Web Signature 2020](https://www.w3.org/community/reports/credentials/CG-FINAL-lds-jws2020-20220721/).

> [OUTSTANDING] Define one supported **Verification Method**

# 5. Self-Issued Access Tokens

## 5.1. Self-Issued Token Format

The contents of the self-issued token must correspond
to [Open ID Connect Self-Issued Tokens](https://openid.net/specs/openid-connect-self-issued-v2-1_0.html#section-11)
and [JSON Web Token (JWT) Profile for OAuth 2.0 Access Tokens](https://datatracker.ietf.org/doc/html/rfc9068).
Namely:

- The `iss` and `sub` claims must be equal and set to the bearer's `web:did`.
- The `sub_jwk` claim is not used
- The `aud` set to the BPN of the provider
- The `client_id` set to the BPN of the consumer
- The `jti` claim that is used to mitigate against replay attacks
- The `vp` claim must contain at least one Verifiable Presentation that attests the BPN specified in the `client_id`.
- All VPs must be in the format specified by
  the [Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model/)

> In the future when VP subject-signed proofs are supported, the following parameters will be required:
> - All VPs must include a `domain` set to the BPN of the provider
> - All VPs must include a `challenge` as defined
    > in  [Verifiable Credentials Implementation Guidelines 1.0](https://www.w3.org/TR/vc-imp-guide/#presentations)
    > **Note these parameters are not required for this release**

> [OUTSTANDING] The `client_id` will not be set to the BPN. TBD what it will contain.

## 5.2. Self-Issued Token Validation

- If the `iss` and `sub` claims are equal, the RP must evaluate the token as a self-issued token.
- The `iss` claim must contain a `did:web` identifier
- The RP most resolve the `iss` DID and verify the token using the public key specified in the DID document.
- The RP must verify at least one VP is present in the `vp` claim that attests to the BPN specified in
  the `client_id` **using the key specified in the DID document**.
- The RP must evaluate the `domain` and `challenge` in each VP.

# 6. Verifiable Credentials and Presentations

## 6.1. Format

VCs will be in the following format specified by in the
[W3C VC Data Model example](https://www.w3.org/TR/vc-data-model/#example-usage-of-the-proof-property-on-a-verifiable-credential):
 
The follow is an example structure for VPs:

```json
{
  "@context": [
    "https://www.w3.org/2018/credentials/v1",
    "https://www.w3.org/2018/credentials/examples/v1"
  ],
  "id": "http://example.gov/credentials/3732",
  "type": [
    "VerifiableCredential",
    "..."
  ],
  "issuer": "https://example.edu",
  "issuanceDate": "2010-01-01T19:23:24Z",
  "credentialSubject": {
    "id": "did:example:ebfeb1f712ebc6f1c276e12ec21",
    "...": {}
  },
  "proof": {
    "type": "Ed25519Signature2020",
    "created": "2021-11-13T18:19:39Z",
    "verificationMethod": "https://example.edu/issuers/14#key-1",
    "proofPurpose": "assertionMethod",
    "proofValue": "z58DAdFfa9SkqZMVPxAQpic7ndSayn1PzZs6ZjWp1CktyGesjuTSwRdoWhAfGFCF5bppETSTojQCrfFPP2oumHKtz"
  }
}
```

The only supported proof type will
be [JSON Web Signature 2020](https://www.w3.org/community/reports/credentials/CG-FINAL-lds-jws2020-20220721/).

> In the future, support may be required
> for [Ed25519Signature2020](https://www.w3.org/community/reports/credentials/CG-FINAL-di-eddsa-2020-20220724/) (for
> example, if GAIA-X uses it).


## 6.2. Supported VPs and VC Types

The VC schemas will be defined in the [Product Core Schemas repository](https://github.com/catenax-ng/product-core-schemas/tree/main).

The following VCs will be required:

**Note this may be changed to only support the Summary VP** 

- **MembershipCredentialCX** - https://confluence.catena-x.net/display/CORE/Membership+Credential
- **BpnCredentialCX** - https://confluence.catena-x.net/display/CORE/BPN+Credential
- **DismantlerCredentialCX** - https://confluence.catena-x.net/display/CORE/Dismantler+Credential
- **UseCaseFrameworkConditionCX**
  - PCF - https://confluence.catena-x.net/display/CORE/PCF+Use+Case+Credential
  - Quality - https://confluence.catena-x.net/pages/viewpage.action?spaceKey=CORE&title=Quality+Use+Case+Credential
  - Resiliency - https://confluence.catena-x.net/display/CORE/Resiliency+Use+Case+Credential
  - Sustainability - https://confluence.catena-x.net/display/CORE/Sustainability+Use+Case+Credential
  - Trace - https://confluence.catena-x.net/display/CORE/Trace+Use+Case+Credential
  - Behavior Twin - https://confluence.catena-x.net/display/CORE/Behavior+Twin+Use+Case+Credential

### 6.2.3 Subject Signed Proofs

Subject-signed proofs will not be supported in this release. Instead, the self-issued token signature will be used as
proof. This requires the VC subject and token subject to be the same. In addition, a VC linking the BPN number to the
subject's DID must be present as a claim in the same authorization token.

## 6.3. Obtaining Verifiable Presentations

Access to MIW resources requires an access token obtained from an OAUth2 compatible endpoint using the client
credentials flow as explained in the [OAuth2 Specification](https://datatracker.ietf.org/doc/html/rfc6749#section-7).

Verifiable presentations can be obtained from a client-controlled endpoint termed a `wallet`. The wallet is responsible
for generating the VP, including its proof, for a particular `domain`.

### 6.3.1. MIR Verifiable Presentations Endpoints

The MIW will provide three endpoints that are relevant to the EDC:

#### Query Verifiable Credentials
`GET /api/credentials`

This endpoint will return available VCs matching a set of criteria that can be used to create VPs.


#### Create Verifiable Presentations
`POST /api/presentations`

This endpoint takes a list of VCs and generated a signed JWT containing VPs.

#### Verify Credentials
`POST /api/credentials/validations`

This endpoint will validate VPs.


## 6.3.1. Relying Party Endpoints for Obtaining Verifiable Presentations

This milestone will not support a protocol for RPs to obtain verifiable presentations from a client endpoint. In the
future [OpenID for Verifiable Presentations](https://openid.net/specs/openid-4-verifiable-presentations-1_0.html) should
be evaluated for suitability as this protocol.
 
# 7. DIDs

Only the `did:web` method will be supported. All DIDs will be resolved from the central MIW instance and therefore will be in the following format:

`did:web:[miw url]:[bpn as indentifier]`

The MIW will provide the following endpint for DID resolution:

`api/didDocuments/(identifier}`

DID documents will be in the following format:

```json
{
  "@context": [],
  "id": "did:web:miwurl:bpn",
  "verificationMethod": {
    "id": "did:web:miwurl:bpn",
    "type": "JsonWebKey2020",
    "publicKeyJwk": {
      "kty": "JsonWebKey2020",
      "crv": "Ed25519",
      "x": "..."
    }
  }
}
```

# 8. DSP Policy

DSP Policy will be used to advertise credential requirements in an interoperable way. Each policy must:

1. Be cryptographically tied to the BPN of the holder
2. A policy must be associated with the Json-ld type of its corresponding Verifiable Credential. This may be done out of
   band.
3. Policies will be simple [ODRL contraints](https://www.w3.org/TR/odrl-model/#constraint) consisting of a left operator
   that is a unique string key, an operand, and a right operator that may be an expression. The expression must be
   capable of being authored by business analysts and not be an executable expression. This is to ensure
   interoperability.

Specific supported policies will be defined in separate specifications.
