# Test specification

This document defines all relevant test that test subjects must successfully complete in order to receive compliance
approval. Note that all tests are to be numbered sequentially starting at `v-t_0001` and `i-t_0001` for verifier and
issuer tests, respectively. All tests SHOULD provide a textual description, e.g. using `@DisplayName` in
JUnit 5, containing at least the sequential number.

> Unless explicitly stated otherwise, all JSON-LD documents can be presented in expanded or in compacted form or both.

## Overview

### Test cases for verifiers

1. `v-t_0001` verify a valid VC with linked proof. A valid VerifiableCredential in JSON-LD format containing a linked
   proof object is successfully verified. _Example
   input:_ [v-t_0001_valid_vc_linked_proof.json](./sample_input/v-t_0001_valid_vc_linked_proof.json).

2. `v-t_0002` verify a valid VC with embedded proof. A valid VerifiableCredential in JSON-LD format containing an
   embedded proof object is successfully verified. _Example
   input:_ [v-t_0002_valid_vc_embedded_proof.json](./sample_input/v-t_0002_valid_vc_embedded_proof.json).

3. `v-t_0003.a` detect a forged claim. An entry in the `credentialSubject` object was _modified_. The test subject must
   detect that and report a validation error. _Example
   input:_ [v-t_0003.a_vc_embedded_forged_claim.json](./sample_input/v-t_0003.a_vc_embedded_forged_claim.json).

4. `v-t_0003.b` detect an altered claim (removal). An entry in the `credentialSubject` object was _removed_. The test
   subject must detect that and report a validation error. _Example
   input:_ [v-t_0003.b_vc_embedded_altered_credentialsubject.json](./sample_input/v-t_0003.b_vc_embedded_altered_credentialsubject.json).

5. `v-t_0003.c` detect an altered claim (alteration). Any other claim, e.g. `issuer`, `expirationDate`,... was modified.
   The test subject must detect that and report a validation error. Note that this test case may consist of several
   sub-testcases, one per claim that was altered/removed. So at runtime, this test case may get invoked several times.
   _Example
   input:_ [v-t_0003.c_vc_embedded_altered_claim.json](./sample_input/v-t_0003.c_vc_embedded_altered_claim.json).

6. `v-t_0004.a` detect a tampered/modified proof object. The `proof` object was modified, for example, by altering
   the `proofPurpose`. The test subject must detect that and report a validation error. Note that this test case may
   consist of several sub-testcases, one per addition, modification or removal. So at runtime, this test case may get
   invoked several times. _Example
   input:_ [v-t_0004.a_vc_embedded_forged_proof.json](./sample_input/v-t_0004.a_vc_embedded_forged_proof.json).

7. `v-t_0004.b` detect an invalid proof. In particular, the mathematical properties of the proof are invalid. Depending
   on the cryptographic primitives that are used, this could be an invalid curve coordinate (EC keys, Octet Key Pairs),
   tampered exponent, factors or prime values (RSA keys). (Embedded) proofs are represented in JWK format. Test
   subjects must detect that and report an error that is _not_ a
   validation error. _Example
   input:_ [v-t_0004.b_vc_embedded_invalid_proof.json](./sample_input/v-t_0004.b_vc_embedded_invalid_proof.json)

8. `v-t_0005` verify canonicalization by altering the sequence of the JSON-LD. An otherwise valid JSON-LD is changed in
   _ordering_. Some entries in the VC as well as within the `proof` object have been re-ordered. The test subject should
   verify the document successfully. _Example
   input:_ [v-t_0005_vc_canonicalization.json](./sample_input/v-t_0005_vc_canonicalization.json).

9. `v-t_0008.a` verify a VC with multiple valid proofs (proof set, mixture of embedded and linked), where the sequence
   does not matter. A valid VerifiableCredential contains
   a ["Proof Set"](https://w3c.github.io/vc-data-integrity/#proof-sets). All proofs are valid, at least one is
   embedded and at least one is linked. Their sequence does not matter, all proofs assert the same VC.

10. `v-t_0008.b` verify a VC with multiple valid proofs (proof chain, mixture of embedded and linked), where the
    sequence does matter. A VerifiableCredential contains
    a ["Proof chain"](https://w3c.github.io/vc-data-integrity/#proof-chains), that asserts the _order_ of proofs.

11. `v-t_0009` detect one or more forged proofs in a Proof Set (mixture of embedded and linked). A VerifiableCredential
    contains a Proof Set with one or several invalid proofs. The test subject must report a validation error.

12. `v-t_0010` detect invalid order in a Proof Chain. A VerifiableCredential contains a Proof Chain with a cyclic
    reference.

13. `v-t_0010` verify a valid VP. Verify a valid VerifiablePresentation containing one or more VCs. _Example
    input:_ [v-t_0010_vp_compacted.json](./sample_input/v-t_0010_vp_compacted.json).

14. `v-t_0011` detect a forged VP proof (over valid VCs). A VP contains one or several valid VCs, but the VP proof is invalid (= spoofed).

15. `v-t_0012` detect a valid VP containing an invalid VC: the VP is valid, but was generated over `[1, 2, N]` invalid
    VCs. The VP proof is valid, but the contained VCs are invalid. The test subject must report a validation error. 

### Test cases for issuers

- `i-t_0001` Sign a credential with `[0, 1, N]` claims
- `i-t_0002` Sign a compacted credential with `[0, 1, N]` claims
- `i-t_0003` Sign a credential embedding the verification method
- `i-t_0004` Create a VerifiablePresentation out of `[0, 1, N]` VerifiableCredentials
- `i-t_0005` Create a compacted signed VerifiablePresentation
- `i-t_0006` Create a VerifiablePresentation with embedded proof
- `i-t_0007` Sign a credential using `did:key` as verification method

## Resolving linked data

VerifiableCredentials contain [LinkedDataProofs](https://w3c.github.io/vc-data-integrity/), for example,
the `verificationMethod` property, which maps to another document containing the actual proof information.

For the purposes of maintaining portability and self-contained-ness in testing, it is permissible for the test
environment to hold all linked data documents in a test resources folder, and to provide a customized document loader
that loads those documents instead of hosting and loading them from a publicly accessible internet location.

For example, this can be achieved by interpreting the URL of the linked data, and simply reinterpreting it as a local
file path in the test resources folder.

The URL may get reinterpreted as file path, except for the host name, and the `.json` file extension may be appended.
That means, `https://org.eclipse.tractusx/vt0001/verification-method` would map
to `src/test/resources/vt0001/verification-method.json`.

## Issuer test descriptions

To be written