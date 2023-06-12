
# BPN Credential 
```json
{
    "id": "UUID",
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/businessPartnerData"
    ],
    "type": ["VerifiableCredential", "BpnCredentialCX"],
    "issuer": "<did>",
    "issuanceDate": "2021-06-16T18:56:59Z",
    "credentialSubject": {
        "type":"BpnCredential",
        "bpn":"bpn"
    }
}
```
# Membership Credential 

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
    "issuer": "did", //operating environment
    "credentialSubject": {
        "type":"MembershipCredential",
        "holderIdentifier": "bpn",
        "memberOf":"Catena-X",
        "status":"Active",
        "startTime":"2021-06-16T18:56:59Z"
    }
}
```
# Dismantler Credential
```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
         "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/businessPartnerData"
    ],
    "id": "http://example.edu/credentials/58473",
    "issuer": "<did>",
    "type": ["VerifiableCredential", "DismantlerCredentialCX"],
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "<BPN>",
        "allowedVehicleBrands": ["Alfa Romeo", "Alpina", "BMW"] 
    },        
    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "did:example:123#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A"
    } 
}
```
# Behavior Twin Use Case Credential
```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/UseCaseVC"
    ],
    "id": "https://public.catena-x.org/contracts/behavior_twin.v1.pdf",
    "issuer": "<did of OpCo>",
    "type": ["VerifiableCredential", "UseCaseFrameworkConditionCX"],
    "issuanceDate": "somedate",
    "expirationDate": "somedate", //Optional Field
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "BPN",
        "usecase-agreement": {
            "value": "Behavior Twin",
            "type": "cx-behavior-twin",
            "contract-template": "https://public.catena-x.org/contracts/behavior_twin.v1.pdf",
            "contract-version": "1.0.0"
        }   
    },    
    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "did:example:123#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A"
    } 
}
```
# PCF Use Case Credential

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://www.w3.org/2018/credentials/examples/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/UseCaseVC"
    ],
    "id": "UUID",
    "issuer": "<issuerDID>",
    "type": ["VerifiableCredential", "UseCaseFrameworkConditionCX"],
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z", //Optional field
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "<BPN>"
        "usecaseAgreement": {
            "value": "PCF",
            "type": "cx-pcf",
            "contract-template": "https://public.catena-x.org/contracts/pcf.v1.pdf",
            "contract-version": "1.0.0",  
        }
    },    
    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "did:example:123#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A"
    } 
}
```
# Sustainablity Use Case Credential

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/UseCaseVC"
    ],    
    "id": "UUID",
    "issuer": "<issuerDID>",
    "type": ["VerifiableCredential", "UseCaseFrameworkConditionCX"],    
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",    
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "BPN of holder", 
        "usecase-agreement": {
            "value": "Quality",
            "type": "cx-quality",
            "contract-template": "https://public.catena-x.org/contracts/quality.v1.pdf",
            "contract-version": "1.0.0"   
        }
    },    
    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "did:example:123#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A"
    } 
}
```
# Quality Use Case Credential 

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/UseCaseVC"
    ],    
    "id": "UUID",
    "issuer": "<issuerDID>",
    "type": ["VerifiableCredential", "UseCaseFrameworkConditionCX"],    
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",    
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "BPN of holder", 
        "usecase-agreement": {
            "value": "Quality",
            "type": "cx-quality",
            "contract-template": "https://public.catena-x.org/contracts/quality.v1.pdf",
            "contract-version": "1.0.0"   
        }
    },    
    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "did:example:123#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A"
    } 
}
```
# Resiliency Use Case Credential 

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/UseCaseVC"
    ],   
    "id": "UUID",
    "issuer": "<issuerDID>",
    "type": ["VerifiableCredential", "UseCaseFrameworkConditionCX"],   
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",   
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "BPN of holder",
        "usecase-agreement": {
            "value": "Resiliency",
            "type": "cx-resiliency",
            "contract-template": "https://public.catena-x.org/contracts/resiliency.v1.pdf",
            "contract-version": "1.0.0"  
        }
    },    
    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "did:example:123#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A"
    } 
}
```
# Traceability Use Case Credential

```json
{
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/UseCaseVC"
    ],
    "id": "UUID",
    "issuer": "<issuerDID>",
    "type": ["VerifiableCredential", "UseCaseFrameworkConditionCX"],
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z", //Optional field
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "<BPN>", 
        "usecaseAgreement": {
            "value": "ID_3.0_Trace",
            "type": "cx-traceability",
            "contract-template": "https://public.catena-x.org/contracts/traceabilty.v1.pdf",
            "contract-version": "1.0.0",   
        }
    },    
    "proof": {
      "type": "JsonWebSignature2020",
      "created": "2019-12-11T03:50:55Z",
      "jws": "eyJhbGciOiJFZERTQSIsImI2NCI6ZmFsc2UsImNyaXQiOlsiYjY0Il19..MJ5GwWRMsadCyLNXU_flgJtsS32584MydBxBuygps_cM0sbU3abTEOMyUvmLNcKOwOBE1MfDoB1_YY425W3sAg",
      "proofPurpose": "assertionMethod",
      "verificationMethod": "did:example:123#_Qq0UL2Fq651Q0Fjd6TvnYE-faHiOpRlPVQcY_-tA4A"
    } 
}
```
