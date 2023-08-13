# 0. Introduction

The document provides a policy specification for Catena-X verifiable credentials (VC).

### 0.1. Decoupling Policy Definitions from VC Schemas

The key architectural principle underlying this specification is that policy definitions must be decoupled from their
corresponding VC schema. Namely, the specific constraints and shape of the VC schema must not be reflected in the
policy definition. This allows VC schemas to be altered without impacting policy definitions.

> Policy definition decoupling will be used to provide a migration path from the temporary _**Summary VC**_ (S-VC) to
> individual VCs with the T-X 3.3 release. In this case, for the T-X 3.2, the policy definitions detailed in this
> document will be evaluated against the S-VC. When TX-3.3 is released, the same definitions will be evaluated against
> individual VCs. This will allow end-user policy definitions to remain the same when migrating from TX-3.2 to TX-3.3.
> Caveat: some policy definitions described in this document will not be supported in TX-3.2 (where noted) because the
> S-VC does not contain the required metadata.

### 0.2. Policy Constraints

Usage requirements involving VCs are expressed as **_ODRL Policy Constraints_**.

### 0.2.1. Left Operand Constraint Schema

Catena-X will use the left operand of a _constraint_ to associate a specific VC. The left operand value will correspond
to the form:

`[VC type].[subtype]

The `subtype` segment is optional.

### 0.2.2. The Right Operand

To indicate the need for an active (valid) credential the string value 'active' will be used. The value may contain an
optional version postfix separated by `:`

`active:[version]`

The version segment can optionally be used to specify a credential variant. For example, requiring a specific version of
a credential could be expressed as:

`active:2.0.0`

The version should followg [semantic versioning](https://semver.org/) If the version is omitted, the latest credential
version will be used.

# 1. Membership Constraint

The `Membership` constraint requires a participant to possess a VC attesting to C-X membership. It is expressed as
follows:

```json
{
  "constraint": {
    "leftOperand": "Membership",
    "operator": "eq",
    "rightOperand": "active"
  }
}
```

The `Membership` constraint may only be used as an ODRL `Permission`.

Valid `rightOperand` values are: `active`.

> ISSUE: What are the `rightOperand` values?

# 2. Dismantler Constraint

The `Dismantler` constraint requires a participant to possess a VC attesting to its status as a verified dismantler. The
constraint has two subtypes

## 2.1. Dismantler

The `Dismantler` root constraint requires a participant to be a certified dismantler. It is expressed as follows:

```json
{
  "constraint": {
    "leftOperand": "Dismantler",
    "operator": "eq",
    "rightOperand": "active"
  }
}
```

The `Dismantler` constraint and its subtypes may only be used as an ODRL `Permission`.

## 2.2. Dismantler.activityType

***Not supported in 3.2**

The `Dismantler.activityType` subtype requires the dismantler to be certified for a given activity. It is expressed as
follows:

```json
{
  "constraint": {
    "leftOperand": "Dismantler.activityType",
    "operator": "eq",
    "rightOperand": "vehicleDismantle"
  }
}
```

> ISSUE: What are the `rightOperand` values?

## 2.3. Dismantler.allowedBrands

***Not supported in 3.2**

The `Dismantler.allowedBrands` subtype requires the dismantler to be certified for a set of brands. It is expressed
using an `in` operator as
follows:

```json
{
  "constraint": {
    "leftOperand": "Dismantler.allowedBrands",
    "operator": "in",
    "rightOperand": [
      "Brand A",
      "Brand B"
    ]
  }
}
```

The `rightOperand` is an array of type `string` containing one or more elements. The elements are evaluated using a
logical OR.

# 3. Framework Agreement Constraints

Framework agreement constraints adhere to the following syntax:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.[type]",
    "operator": "eq",
    "rightOperand": "active:[version]"
  }
}
```

The `type` segment specifies the framework case agreement type. The version postfix in the right operand is optional.

Framework agreement constraints may only be used as an ODRL `Permission`.

> ISSUE: What are the `rightOperand` values?

## 3.1. PCF

The PCF framework agreement is expressed as:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.pcf",
    "operator": "eq",
    "rightOperand": "active:[version]"
  }
}
```

## 3.2. Sustainability

The Sustainability framework agreement is expressed as:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.sustainability",
    "operator": "eq",
    "rightOperand": "active:[version]"
  }
}
```

## 3.3. Quality

The Quality framework agreement is expressed as:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.quality",
    "operator": "eq",
    "rightOperand": "active:[version]"
  }
}
```

## 3.4. Resiliency

The Resiliency framework agreement is expressed as:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.resiliency",
    "operator": "eq",
    "rightOperand": "active:[version]"
  }
}
```

## 3.5. Traceability

The Traceability framework agreement is expressed as:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.traceability",
    "operator": "eq",
    "rightOperand": "active:[version]"
  }
}
```

## 3.6. Behavioral Twin

The Behavior framework agreement is expressed as:

```json
{
  "constraint": {
    "leftOperand": "FrameworkAgreement.behavioraltwin",
    "operator": "eq",
    "rightOperand": "active:[version]"
  }
}
```

## 3.7. BPN

> ISSUE: The Membership VC appears to contain the same information. Is the BPN VC needed?

# 4. Policy Example

The following is an `Offer` that requires the data user to be a certified dismantler for `Brand A` vehicles and to have
an active signed traceability agreement:

```json
 {
  "@context": [
    "https://www.w3.org/ns/odrl.jsonld",
    {
      "cx": "https://w3id.org/catenax/v0.0.1/ns/"
    }
  ],
  "@type": "Offer",
  "@id": "a343fcbf-99fc-4ce8-8e9b-148c97605aab",
  "permission": [
    {
      "action": "use",
      "constraint": {
        "and": [
          {
            "leftOperand": "Dismantler.allowedBrands",
            "operator": "in",
            "rightOperand": [
              "Brand A"
            ]
          },
          {
            "leftOperand": "FrameworkAgreement.traceability",
            "operator": "eq",
            "rightOperand": "active"
          }
        ]
      }
    }
  ]
}
```

> Note The Tractus-X context file is not yet publicly available. This will be provided TBD.
