# Test specification

This document defines all relevant test that test subjects must successfully complete in order to receive compliance approval. Note that all tests are to be numbered sequentially starting at `v-t_0001` and `i-t_0001` for verifier and issuer tests, respectively. In addition, all tests SHOULD provide a textual description, e.g. using `@DisplayName` in JUnit 5.

> Unless explicitly stated otherwise, all JSON-LD documents can be presented in expanded or in compacted form.

## Overview

### Test suite for verifiers

- `v-t_0001` verify a valid VC with linked proof
- `v-t_0002` verify a valid VC with embedded proof
- `v-t_0003` detect a forged VC with linked proof
- `v-t_0004` detect a forged VC with embedded proof
- `v-t_0005` verify canonicalization by altering the sequence of the JSON-LD
- `v-t_0006` detect a forged credential subject, issuer, issuance date (document hash)
- `v-t_0006` detect a tampered proof object, e.g. by adding a random property (proof hash)
- `v-t_0007` verify a VC with multiple valid proofs (mixture of embedded and linked)
- `v-t_0008` detect one or more forged proofs in a set of proofs (mixture of embedded and linked)
- `v-t_0009` verify a valid VP
- `v-t_0010` detect a forged VP proof (over one single valid VC)
- `v-t_0011` detect a valid VP containing an invalid VC: the VP is valid, but was generated over `[1, 2, N]` invalid VCs

### Test suite for issuers

- `i-t_0001` Sign a credential with `[0, 1, N]` claims
- `i-t_0002` Sign a compacted credential with `[0, 1, N]` claims
- `i-t_0003` Sign a credential embedding the verification method
- `i-t_0004` Create a VerifiablePresentation out of `[0, 1, N]` VerifiableCredentials
- `i-t_0005` Create a compacted signed VerifiablePresentation
- `i-t_0006` Create a VerifiablePresentation with embedded proof
- `i-t_0007` Sign a credential using `did:key` as verification method


## Verifier test descriptions
To be written

## Issuer test descriptions
To be written