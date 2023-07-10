# Structure and Formats

The following is an example of a verifiable credential that demonstrates the structure and formats used:

```json
{
    "id": "UUID",
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/businessPartnerData"
    ],
    "type": ["VerifiableCredential", "MembershipCredentialCX"],
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",
    "issuer": "did", // operating environment
    "credentialSubject": {
        "type": "MembershipCredential",
        "holderIdentifier": "bpn",
        "memberOf": "Catena-X",
        "status": "Active",
        "startTime": "2021-06-16T18:56:59Z"
    }
}
```

This verifiable credential includes the following information:

* **id:** A unique identifier for the credential (UUID).
* **@context:** An array of context URLs specifying the context for interpreting the credential.
* **type:** An array indicating the type of the credential, including "VerifiableCredential" and "MembershipCredentialCX".
* **issuanceDate:** The date and time when the credential was issued (in UTC format).
* **expirationDate:** The date and time when the credential expires (in UTC format).
* **issuer:** The issuer of the credential, identified by a decentralized identifier (did) associated with the operating environment.
* **credentialSubject:** An object containing information about the subject of the credential.
* **type:** The type of the credential subject, which is "MembershipCredential".
* **holderIdentifier:** A unique identifier for the holder of the credential (in this case, "bpn").
* **memberOf:** The organization or group the holder is a member of (in this case, "Catena-X").









**status:** The status of the credential, indicating it is currently "Active".
startTime: The date and time when the membership started (in UTC format).

This example showcases the structure and key attributes of a verifiable credential, demonstrating how it can be used to represent membership credentials within the Catena-X ecosystem.