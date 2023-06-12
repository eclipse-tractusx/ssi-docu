# Technical Debts 

## DID Technical Debts

* did document covers only varification method. No service endpoints. 
* 
## MiW Technical Debts

* No real Tenant System.
* Private Keys ar AES encrypted stored in the MiW Postgres Database.  
* No Revocation Service 
* Summary Credential used as token. 
* Only 1 VC in a VP possible. 
* Summary VC created in the backend with the private key of the auhtority. 
* DID documents are stored in the MiW. 
* Summary Credentials always get deleted when new CX Credential is added to the MiW. 
* Creation of CX-Credential are located in the MiW. Should be a dedicated service outside of the wallet. 
* Only Central Wallet available. No self-mangaged wallet. 
* No Issuer Registry. Only one trusted issuer available. 
* Download of VC to own wallet not possible. 
* No varifiable data registry in place. 
* No key rotation. 
* No update possibility of credentials. Credentials need to be deleted and new generated. 

## Verifiable credential

* CX-Credentials are not consistent

## SSI Lib
  
  * No complete JsonWebSignature2020. Only ED22519 is supported.
  * No validation for JsonWebSignature2020 with RSA key.
  * No Security valdition only Sercurity Assesment. No attack vectors are tested. 
  * ...

## EDC 
 .... HHTP header limition of 8KB 