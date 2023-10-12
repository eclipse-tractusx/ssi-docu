# Mapping Credentials

## Definition of terms

- Credential type: a [W3C Verifiable Credential type](https://w3c.github.io/vc-data-model/#types), for
  example `DismantlerCredential`. For every credential type there must be a resolvable context, which contains further
  schema and type information. Credentials can have multiple types. This is comparable to a class definition in OOP
  languages. Also referred to as: CredentialType, type

- Credential: an instance of a credential type, i.e. one materialization of a particular schema. This is comparable to a
  class instance in OOP languages. Also referred to as: vc, VC, VerifiableCredential

- Framework credential: a credential having the credential type `UseCaseFrameworkCondition`. All Framework credentials
  are the same type and therefore adhere to the same schema. Also referred to as: Framework agreement credential

- Use case type: refers to the `credentialSubject.type` property of the `UseCaseFrameworkCondition` type. The use case
  type discriminates which framework agreement use case the credential attests to. It is **not** a separate
  VerifiableCredential type! For
  example: [PCF Use case credential](https://github.com/eclipse-tractusx/ssi-docu/blob/main/docs/architecture/cx-3-2/3.%20Verifiable%20Credentials/CX-Credentials/Standardized%20CX-Credential.md#pcf-use-case-credential).
  Specifically, `subject.type = PcfCredential`. Also referred to as: use case

- Contract version: refers to the `credentialSubject.contractVersion` property and is expected to be
  a [SemVer string](https://semver.org/). The `contractVersion` discriminates which framework agreement use case version
  the credential attests to. Also referred to as a `framework agreement version`.

- Credential version: a credential version does not exist as a first-class concept.

## Referencing credentials in policies

Please check the
syntax [here](https://github.com/eclipse-tractusx/ssi-docu/blob/main/docs/architecture/cx-3-2/edc/policy.definitions.md)

## Mapping Framework credentials

Automatic mapping policy expression to credential type is possible assuming all framework credentials follow the same
schema. If all Framework credentials conform to the same schema, the evaluation of the policy (= the evaluation
function) can be generic.

In an actual example a policy constraint, requiring the "pcf" credential in version 0.4.2, would look like this:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.pcf",
    "operator": "eq",
    "rightOperand": "active:0.4.2"
  }
}
```

If a specific contract version is referenced in the policy constraint, like in the example above, it follows that the
policy must be **updated**, if version 43 of the `pcf` credential is released, and the policy should reference it.

If no contract version is specified in the policy constraint, then the policy **need not be updated**.

### Correlation with the credential type

A use case type can be constructed easily by simple string manipulation:

- remove `FrameworkAgreement.`
- capitalize the remainder (i.e. `pcf --> Pcf`)
- append the `Credential` literal

which would result in the term `PcfCredential`. In addition, parsing the `rightOperand` would yield the (optional)
version identifier. The version identifier is processed separately, e.g. in a database query.

Formally, the use case type can be constructed using the BNF below.

### Converting to a scope string

The conversion from use case type to scope string and vice versa can be performed without any static mapping, but by
relatively simple string manipulation:

- start with the (dataspace-specific) scope prefix (`org.eclipse.tractusx.vc.type`)
- append a `:`
- append the use case type
- [optional]: append a `.` and the version identifier (e.g. `0.4.2`)
- append a `:`
- append the operator (`read`, `write`, `*`)

resulting in something like `org.eclipse.tractusx.vc.type:PcfCredential_0.4.2:write`.

The scope prefix is configurable per dataspace, but in Tractus-X it *must* be `org.eclipse.tractusx.vc.type`.

Performing the inverse mapping of the scope string, it would result in a use case type `PcfCredential` and a contract
version information of `0.4.2` which could then be used to perform a database query similar to

```sql
SELECT * FROM credentials WHERE credentials.subject.type = 'PcfCredential' AND credential.credentialSubject.version = '0.4.2'
```

*NB: this is just an example*.

### Formal description

The relation between policy constraints, use case types and scope strings is defined by the following EBNFs

#### For constructing use case types:

```ebnf
USECASETYPE         ::= USECASEIDENT CREDENTIALLITERAL ;
USECASEIDENT        ::= #'[A-Z][a-z0-9]+' ;
CREDENTIALLITERAL   ::= 'Credential' ;
```

#### For constructing scope strings:

```ebnf
SCOPESTRING         ::= PREFIX COLON USECASETYPE( UNDERSCORE VERSION)? COLON OPERATOR ;
DOT                 ::= ".";
PREFIX              ::= "org.eclipse.tractusx.vc.type" ;
DIGIT               ::= "0" | "1" | "2" | "3" | "4" | "5" | "6" | "7" | "8" | "9" ;
VERSION             ::= DIGIT, DOT, DIGIT, DOT, DIGIT ;
UNDERSCORE          ::= "_" ;
OPERATOR            ::= "write" | "read" | "*" ;
COLON               ::= ":" ;
USECASETYPE         ::= USECASEIDENT CREDENTIALLITERAL ;
USECASEIDENT        ::= #'[A-Z][a-z0-9]+' ;
CREDENTIALLITERAL   ::= "'"Credential"'" ;
```

_NB: the `VERSIONIDENT` was simplified for readability, for example it omits metadata. In practice, it must conform to
the [official regex identifying a valid SemVer string](https://semver.org/#is-there-a-suggested-regular-expression-regex-to-check-a-semver-string)_<br/>

#### For constructing policy constraint left-operands:

```ebnf
POLICYLEFTOP      ::= FRAMEWORKLITERAL, DOT, IDENTPOSTFIX ;
FRAMEWORKLITERAL  ::= "FrameworkAgreement" ;
IDENTPOSTFIX      ::= #'[a-z][a-zA-Z0-9]+' ;
DOT               ::= "." ;
```

_NB: the EBNF sections can be validated with any tool of choice, for example [this](https://mdkrajnak.github.io/ebnftest/)_

## All other credentials:

automatic mapping is possible, but only to express a check for the mere existence of the credential:

```json
{
  "constraint": {
    "leftOperand": "Iso9001",
    "operator": "eq",
    "rightOperand": "active"
  }
}
```

would be interpreted as "Must have an active Iso9001Credential".

Any other constraints would require a customized evaluation function and thus require a rollout of EDC.

