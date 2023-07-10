# Overwiew SSI Agent Lib

## Introduction

The *SSI Agent Lib* provides core functionalities and abstractions commonly required when implementing a digital wallet or any service leveraging self-sovereign identities (SSI).

## System Scope and Context

![System Scope](./SystemScope.png)

The SSI Lib is intended for use by the Catena-X Managed Identity Wallet (MIW), the Eclipse Dataspace Connector (EDC), and third-party self-hosted wallets. While the SSI Lib provides did:web DID resolution capabilities, it also supports external DID resolution (e.g., Uniresolver).

## Solution Strategy

The library adopts a stateless design with no data persistency. It offers segregated interfaces, allowing usage of both internal features and external components. 
## Features

The lib provides the following main features:

| Feature                          | Description                                                                                          |
| -------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Create DID                       | Create a DID of type `did:web`.                                                                      |
| Parse DID                        | Parse a DID of type `did:web` and return the URL of the respective DID document.                     |
| Generate DID document            | Return a valid DID document for a given DID.                                                         |
| Resolve DID document             | Resolve the DID document of a given DID of type `did:web`.                                           |
| Issue Verifiable Credential      | Issue a verifiable credential with a JSON-LD document as payload.                                    |
| Issue Verifiable Presentation    | Issue a verifiable presentation for a given set of verifiable credentials as a JSON Web Token (JWT). |
| Verify Verifiable Presentation   | Verify the issuer's signature of a given JWT representing a  verifiable presentation.                |
| Validate Verifiable Presentation | Validated the expiry date and audience of given JWT representing a verifiable presentation.          |
| Generate a key pair              | Generates a key pair (consisting of a private and public key) using `Ed25519` algorithm.             |
