
# BPN Credential 
```json

ADD LINK TO proof
{
    "id": "UUID",
    "@context": [
        "https://www.w3.org/2018/credentials/v1",
        "https://w3id.org/security/suites/jws-2020/v1",
        "https://raw.githubusercontent.com/catenax-ng/product-core-schemas/main/businessPartnerData"
    ],
    "type": ["VerifiableCredential", "BpnCredential"],
    "issuer": "<did>",
    "issuanceDate": "2021-06-16T18:56:59Z",
    "credentialSubject": {
        "id":"<did>",
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
    "type": ["VerifiableCredential", "MembershipCredential",],
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",
    "issuer": "did", 
    "credentialSubject": {
        "id": "<did>",
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
    "id": "UUID",
    "issuer": "<did>",
    "type": ["VerifiableCredential", "DismantlerCredential"],
    "issuanceDate": "2021-06-16T18:56:59Z",
    "expirationDate": "2022-06-16T18:56:59Z",
    "credentialSubject": {
        "id": "<did>",
        "type": "DismantlerCredential", 
        "holderIdentifier": "<BPN>",
        "allowedVehicleBrands": ["Alfa Romeo", "Alpina", "BMW"] 
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
    "id": "UUID",
    "issuer": "<did of OpCo>",
    "type": ["VerifiableCredential", "UseCaseFrameworkConditionCX"],
    "issuanceDate": "somedate",
    "expirationDate": "somedate",
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "BPN",   
        "type": "BehaviorTwinCredential",
        "contract-template": "https://public.catena-x.org/contracts/behavior_twin.v1.pdf",
        "contract-version": "1.0.0"
        
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
    "expirationDate": "2022-06-16T18:56:59Z",
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "<BPN>",
        "type": "PcfCredential",
        "contract-template": "https://public.catena-x.org/contracts/pcf.v1.pdf",
        "contract-version": "1.0.0",  
        
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
        "type": "SustainabilityCredential",
        "contract-template": "https://public.catena-x.org/contracts/sustainability.v1.pdf",
        "contract-version": "1.0.0"   
        
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
        "type": "QualityCredential",
        "contract-template": "https://public.catena-x.org/contracts/quality.v1.pdf",
        "contract-version": "1.0.0"   
        
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
        "type": "ResiliencyCredential",
        "contract-template": "https://public.catena-x.org/contracts/resiliency.v1.pdf",
        "contract-version": "1.0.0"  
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
    "expirationDate": "2022-06-16T18:56:59Z", 
    "credentialSubject": {
        "id": "<did>",
        "holderIdentifier": "<BPN>",
        "type": "TraceabilityCredential",
        "contract-template": "https://public.catena-x.org/contracts/traceabilty.v1.pdf",
        "contract-version": "1.0.0",   
    }
}
```
