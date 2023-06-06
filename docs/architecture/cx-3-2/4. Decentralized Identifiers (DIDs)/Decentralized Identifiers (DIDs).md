# DID Document

This DID document adheres to the following standard:

 
* @context: An array of context URLs specifying the context for interpreting the DID document. In this case, it includes the W3C DID context and the ed25519-2020 cryptographic suite context.
  
* **id:** The unique identifier for the DID, represented as "did:web:example.com". The "web" method indicates that the DID is associated with a web-based identifier scheme, and "example.com" is the domain name.
* **verificationMethod:** An array of verification methods associated with the DID. Each verification method represents a cryptographic key or capability associated with the DID.
  * **id:** The identifier for the verification method, represented as "did:web:example.com:BPN123#key-0". It combines the DID with a specific key identifier.
    type: The type of the verification method, indicating it is a "JsonWebKey2020" type.
  * **publicKeyJwk:** The JSON Web Key (JWK) representing the public key associated with the verification method.
  * **kty:** The key type, specified as "JsonWebKey2020".
  * **crv:** The curve type of the key, in this case, "Ed25519".
  * **x:** The public key value, represented as "3534354354353".
This example showcases the standard structure of a DID document, including the context, identifier, and verification method, and demonstrates how to represent a specific verification method using a JSON Web Key.

## DID Document Structure
```json
{
  "@context": [
    "https://www.w3.org/ns/did/v1",
    "https://w3id.org/security/suites/ed25519-2020/v1"
  ],
  "id": "did:web:example.com:BPN123",
  "verificationMethod": [
    {
      "id": "did:web:example.com:BPN123#key-0",
      "type": "JsonWebKey2020",
      "publicKeyJwk": {
        "kty": "JsonWebKey2020",
        "crv": "Ed25519",
        "x": "3534354354353"
      }
    }
  ]
}
```


# DID  Methods
The following chapter discibes the supported DID Methods for Release 3.2 follwing the [W3C Standard](https://www.w3.org/TR/did-core/)
## did:web
The "did:web" method is a standard method for creating and managing Decentralized Identifiers (DIDs) within the consortium. This method is specifically designed for web-based identifiers, allowing organizations and individuals to leverage existing web infrastructure and technologies in the management of DIDs.

Key Features of the "did:web" Method:

Web-based Identifiers: The "did:web" method utilizes web domain names as the basis for creating DIDs. Organizations can register and control their DIDs using their existing domain names, making it easier to integrate DIDs into their web-based systems and applications.

Familiar Syntax: The "did:web" method follows a familiar syntax similar to standard web URLs, providing a recognizable and intuitive format for representing DIDs. For example, a DID using the "did:web" method could be represented as "did:web:example.com", where "example.com" is the registered domain name.

Web Infrastructure Integration: Leveraging the existing web infrastructure, organizations can utilize standard web protocols and tools for resolving and interacting with DIDs. This integration simplifies the implementation and adoption of DIDs within web-based systems, leveraging the security and scalability features already established on the web.

Flexibility and Interoperability: The "did:web" method promotes flexibility and interoperability by allowing organizations to choose their preferred web hosting and resolution mechanisms. Organizations can utilize existing web servers, DNS records, or dedicated DID resolvers to handle the resolution and retrieval of associated DID documents.

Wider Ecosystem Support: The "did:web" method benefits from the extensive support and tooling available for web technologies. Various libraries, frameworks, and services that support web development can be leveraged for creating, managing, and interacting with DIDs using the "did:web" method.

By adopting the "did:web" method as a standard within the consortium, organizations can harness the power of the web to enable decentralized identity management. This method provides a seamless integration of DIDs into existing web infrastructure, promoting interoperability and facilitating the adoption of decentralized identity solutions in web-based applications and systems.

the did:web methode follows the [W3C Standard](https://w3c-ccg.github.io/did-method-web/)

# DID Resolver

Resolving of did documents are covered by the [MiW](/docs/architecture/cx-3-2/2.%20Managed%20Identity%20Wallet/)

# DID Verification Methods

For Release Verification Method JsonWebSignature - ED25519

## Example 

```json

    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "https://example.com/issuer/123#ovsDKYBjFemIy8DVhc-w2LSi8CvXMw2AYDzHj04yxkc"
    }
  
```