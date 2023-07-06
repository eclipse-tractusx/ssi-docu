# Test compliance for credentials issuers and verifiers

This document outlines test cases, which must be completed successfully by every participant claiming to have a certain set of capabilities. For example, an entity claiming to be capable of issuing VerifiableCredentials MUST successfully complete all issuer test cases. Similarly, verifier implementations must successfully complete all verifier tests.

Partial implementations, such as services that can only create VerifiablePresentations but cannot sign VerifiableCredentials, MUST mark all other issuer tests as "disabled".

## Definition of terms

- **Test case**: is the description of test data, pre-conditions, defined execution procedure, post-conditions and an expected result. Typically represented by - but not limited to - the JUnit `@Test` method annotation.
- **Test suite**: is a set of multiple test cases that are executed together and that have a contextual coherence
- **Test subject**: in this document, "test subject" refers to one particular Issuer or Verifier implementation (or combination thereof). For example a wallet implementation of Company ABC that is capable of issuing VCs would be one test subject. For the purposes of this document, the term "client code" is used somewhat synonymously, referring to the actual implementation code in the test subject.
- **Verifier**: is an entity that is capable of asserting that VerifiableCredentials and VerifiablePresentations have not been altered (= integrity) and that they were indeed signed by a specific party (= provenance). A Verifier does **not** implicitly establish or check trust.
- **Issuer**: is an entity that can create VerifiableCredentials (=a set of claims) and compute a mathematical proof for them in such a way that every Verifier is able to perform the corresponding verification. If an Issuer is only capable of generating VPs from existing VCs, but cannot issue VCs, we refer to it as _Presentation Issuer_.
- **Presentation Issuer**: this is an Issuer entity that can only create VPs out of existing VCs, but cannot issue VCs. This may be due to any number of legal or business limitations, for example because only Government bodies may issue VCs, etc.
- **Trust**: for the purposes of this document, trust is not particularly relevant, because it exists intrinsically, not by any mathematical means. In other words, as long as the provenance of a signature or a token can be traced to one particular entity, and that entity is inherently trusted, the token is implicitly trusted. 
- **Crypto suite**: a collection of cryptographic primitives that are used to create and verify VerifiableCredentials and VerifiablePresentations. A list of currently known suites is posted [here](https://w3c-ccg.github.io/ld-cryptosuite-registry/). Every Issuer and Verifier must publish the crypto suite(s) it supports.
- **Compliance**: is established once all relevant test cases have been passed. Test reports SHOULD be provided in an [automated way](#automatic-certificate-of-compliance). All tests MUST be executed for each crypto suite, that is supported by a particular issuer or verifier. For example, if an issuer only supports `RsaSignature2018` and `Ed25519`, it must perform all test using each of these crypto suites.


## Test specification


Please find the exact test specification in this [accompanying document](./test_specification.md).



## Automatic certification of compliance
The following section outlines two recommended ways for test subjects (or "client code") to prove compliance with the test specification.

### 1. Embedding in client code

For implementations that are based on a JVM-language, the [Eclipse Dataspace TCK project](https://github.com/eclipse-dataspacetck) provides an SPI to which test subjects can delegate test execution. Practically, implementors simply inherit a test base class that contains all test code and that only delegates back to client code for business logic invocations. 

Throwing an `UnsupportedOperationException` in client code marks the test as "disabled".

For example, the TCK would set up test data (i.e. a JSON-LD file containing a VC) and possibly generate a keypair, and would pass the JSON-LD back into the test subject for signing. The test subject signs it, and returns it to the TCK, where it is subsequently validated.

Tests are self-contained and quick to execute. In order to ensure continued and reproducible compliance, it is advisable to execute test tests in a CI/CD environment. Test reports MAY be published somewhere.

### 2. Remote execution of tests

If the implementation is done in another programming language, or if the aforementioned approach is not suitable for some other reason, the TCK will offer a network-based compliance check: instead of extending an abstract base class in the test subject's code base, the test subject implements a simple and standardized REST API, over which it receives the test data, invokes the appropriate methods, and then sends back the results to the (remote) TCK.

Returning an HTTP 204 No Content marks the test as "disabled".

That way, the implementation of the tests and the implementation of the business code is completely decoupled: tests still run within the TCK, but the test subject's implementation runs in its own process. 

This approach provides two major advantages: 
- test certification: the test code (in the TCK) can be certified and developed individually. Changes there won't affect the client code.
- portability: running TCK compliance tests could be done in CI, or even as a `helm test`
- the TCK MAY record test runs in its system-of-records for future reference

### 3. [Not recommended] Test-by-contract

If neither of the previous approaches cannot be used for some reason, it is theoretically possible to download the TCKs test vectors (= JSON-LD files) and to implement all tests directly in the test subject's code base. 

However, this approach is **not recommended**, because it would require updating the test vectors frequently to guard against stale test data, and it would require an additional in-depth review of the test implementation. Certification may be limited if this approach is used.
