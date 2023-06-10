# 1. Introduction: Tractus-X Verifiable Credentials

The document provides guidelines for defining Tractus-X Verifiable Credentials (VC) based on
the [Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model/).

## 1.2. Goals

The goal of these guidelines are to provide a baseline for VC interoperability across Tractus-X projects regardless of
technology platform. These guidelines are intended to ensure that:

- It is possible to process and verify VCs using independent software stacks
- All TX VCs have consistent schemas and Json-Ld contexts
- All VC Json-Ld contexts are correctly defined and allow for proper Json-Ld processing
- Consistent naming standards are used for all VC definitions
- A consistent versioning scheme is adopted for all VCs
- A consistent Json-Ld context resolution scheme is used for all VCs

# 2. The Tractus-X Namespace

All VCs must be defined in the `Tractus-X namespace`

# 3. Defining Verifiable Credentials

All TX verifiable credentials must conform to
the [Verifiable Credentials Data Model v1.1](https://www.w3.org/TR/vc-data-model/).

> Note that the URL scheme adopted by this specification is the one in use by the W3C, which supports the ability to
> version context definitions.

## 3.1. The Master VC Context

A master Json-Ld 1.1 context is defined that contains common terms. VCs may have their own contexts that define terms
and reference the master context. This allows VC definitions to be evolved and versioned independently. The master
context should be referenced as:

`https://w3id.org/tractusx/2023/credentials/v1.0.0`

## 3.2. Individual VC Contexts

Individual VC contexts define terms specific to the VC and should be referenced using a URL similar to the following:

`https://w3id.org/tractusx/2023/credentials/traceability/v1.0.0`

This URL is constructed by taking determining the year the VC definition is published, appending it to the base W3ID
url, and further appending the VC name and version.

## 3.3. Term Definitions

Term definitions that represent types should use term keys that are mixed-case, for example, `DismantlerCredential`.
Term definitions that do not represent types should use camel case syntax, for example, `holderIdentifier`. Term keys
should be unambiguous and must be associated with a proper IRI so that they are not removed during Json-Ld expansion:

```json
{
  "@context": {
    "@version": 1.1,
    "ex": "https://w3id.org/2023/tractusx/credentials/example/",
    "ExampleCredential": {
      "@id": "ex:ExampleCredential",
      "exampleData": {
        "@id": "ex:exampleData"
      }
    }
  }
}

```

# 4. Testing

All VC and context definitions must be tested for proper Json-Ld expansion.

> Note it is important to test for incorrect Json-Ld contexts as these may result in stripping out terms that are not
> part of a vocabulary from the canonical data used for the proof algorithm. 



