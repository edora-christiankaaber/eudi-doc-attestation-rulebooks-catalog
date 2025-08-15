
# Attestation Rulebook for attestations of type  "PDA1"

* Author(s): 
    * Gerd Bauer, DC4EU WP6, dc4eu@sozialversicherung.at
    * Katharina Hilmar, DC4EU WP6
    * Christian Kaaber, DC4EU WP6

| Version | Date | Description |
|---------|------------|------------|
| 0.1 | 2025-06-02 | 1st version of the document for comments provided |
| 1.0 | 2025-06-27 | 2nd version of the document for comments provided |
| 1.1 | 2025-07-01 | Template adapted |


## 1 Introduction

### 1.1 Document scope and purpose

This rulebook defines the requirements and constrains pertaining to PDA1 PuB-EAAs as used within social security coordination in Europe.

### 1.2 Document structure

- Chapter 2, which describes the attestation attributes and metadata in an 
encoding-independent manner. 
- Chapter 3, which specifies how the attestation
attributes and metadata are encoded in case the attestation complies with [ISO/IEC
18013-5] and/or [SD-JWT VC] and/or [W3C VCDM v2.0]. 
- Chapter 4, which specifies attestation usage.
- Chapter 5, which defines trust anchors
- Chapter 6, which defines revocation mechanisms
- Chapter 7, which provides compliance information

### 1.3 Key words

This document uses the capitalised key words 'SHALL', 'SHOULD' and 'MAY' as
specified in [RFC 2119], i.e., to indicate requirements, recommendations and
options specified in this document.

In addition, 'must' (non-capitalised) is used to indicate an external
constraint, i.e., a requirement that is not mandated by this document, but, for
instance, by an external document. The word 'can' indicates a capability,
whereas other words, such as 'will', and 'is' or 'are' are intended as
statements of fact.

### 1.4 Terminology

This document uses the terminology specified in Annex 1 of the ARF.

## 2 Attestation attributes and metadata

The Portable Document A1 (PD A1) credential is a specialised instance of the common PuB-EAA attribute block defined in the Rulebook `attestation-rulebook-wp6-common.md`. 
### 2.1 Common mandatory attributes

| **Data Identifier** | **Definition** |**Data type** |**Example value** |
|------------------------|--------------|--------------|--------------|
| attestation_legal_category | | string | PuB-EAA |
| personal_administrative_number | Unique personal identifier used by the issuing social security services. | string | 123456789 |
| issuing_authority.id | Identifier of the issuing authority. | string | DE:456789 |
| issuing_authority.name | Name of the issuing authority. | string | DRVB |
| issuing_authority.country | Country under whose jurisdiction the credential is issued. | string (ISO 3166-1 alpha-2) | DE |
| authentic_source.id | ID of the competent institution (EESSI). | string | DE:456789 |
| authentic_source.name | Name of the competent institution (EESSI). | string | DRVB |
| document_number | Unique document identifier. | string | 83e1442d-1e4b-477f-8aeb-632e29d19255 |


### 2.2 Common optional attributes

| **Data Identifier** | **Definition** |**Data type** |**Example value** |
|------------------------|--------------|--------------|--------------|
| starting_date | Start date of coverage/benefit validity. | date | 2025-07-04 |
| ending_date | End date of coverage/benefit validity. | date | 2025-08-01 |

### 2.3 Common mandatory metadata 

| **Data Identifier** | **Definition** |**Data type** |**Example value** |
|------------------------|--------------|--------------|--------------|
| date_of_issuance | Credential issuance/start date. | date | 2025-07-01 |


### 2.4 Common optional metadata 

| **Data Identifier** | **Definition** |**Data type** |**Example value** |
|------------------------|--------------|--------------|--------------|
| date_of_expiry | Credential expiration date.| date | 2025-08-01 |


The PD A1 adds a number of private namespace attributes to the set inherited from the common.

### 2.5 Mandatory attributes

| **Data Identifier** | **Definition** |**Data type** |**Example value** |
|------------------------|--------------|--------------|--------------|
| employer.id	|	Unique identifier of the employer. | string | AT-COMPANY-001 |
| employer.name |	Name of the employer. | string |	Vienna Logistics GmbH |
| employer.country	| Country where the employer is registered. | string (ISO 3166-1 alpha-2) | AT |
| work_address.locality |	City, town, or locality of the workplace. | string | Vienna |
| work_address.country |Country of the workplace. | string (ISO 3166-1 alpha-2) | AT |
| legislation_country |	Country whose legislation applies. | string (ISO 3166-1 alpha-2) | DE |
| status_confirmation	|	Legal status category code applicable to the worker. |string |	01 |


### 2.6 Optional attributes

| **Data Identifier** | **Definition** |**Data type** |**Example value** |
|------------------------|--------------|--------------|--------------|
| work_address.region |	Region or state of the workplace. | string |	Hamburg |
| work_address.formatted | Full formatted workplace address. |string | Freight Port 5, 20457 Hamburg, Germany |
| work_address.street_address	|	Street name of the workplace. | string | Freight Port |
| work_address.building_number | Building number of the workplace. | string	| 5 |
| work_address.postal_code	|	Postal or ZIP code of the workplace.	| string |	20457 |


# 3 Attestation encoding 

## 3.1 ISO/IEC 18013-5-compliant encoding 

| **Data Identifier** | **Attribute identifier** | **Encoding format** |**Namespace**|
|------------------------|--------------|------------------|------------------|
| employer.type |employer.type|tstr |urn:dgempl:pubeaas:pda1:v1:attribute:employer:type|
| employer.id	|	employer.id | tstr |	urn:dgempl:pubeaas:pda1:v1:attribute:employer:id |
| employer.name |	employer.name | tstr |	urn:dgempl:pubeaas:pda1:v1:attribute:employer:name |
| employer.country	| employer.country | tstr (ISO 3166-1 alpha-2) |urn:dgempl:pubeaas:pda1:v1:attribute:employer:country |
| work_address.locality |	work_address.locality | tstr |	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:locality |
| work_address.country |work_address.country | tstr (ISO 3166-1 alpha-2) |	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:country |
| legislation_country |	legislation_country | tstr (ISO 3166-1 alpha-2) |	urn:dgempl:pubeaas:pda1:v1:attribute:legislation_country |
| status_confirmation	|	status_confirmation | tstr |	urn:dgempl:pubeaas:pda1:v1:attribute:status_confirmation |
| work_address.region |	work_address.region | tstr |	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:region |
| work_address.formatted | work_address.formatted | tstr | urn:dgempl:pubeaas:pda1:v1:attribute:work_address:formatted |
| work_address.street_address	|	work_address.street_address | tstr |	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:street_address
| work_address.building_number | work_address.building_number | tstr	|urn:dgempl:pubeaas:pda1:v1:attribute:work_address:building_number |
| work_address.postal_code	|	work_address.postal_code	| tstr |	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:postal_code |


Finally, illustrative examples SHALL be included. 

[RULEBOOK AUTHOR TO PROVIDE AN EXAMPLE OF FULL OR PARTIAL mDOC OF THE ATTESTATION]

[RULEBOOK AUTHOR TO PROVIDE THE ATTRIBUTES AND THEIR VALUES INCLUDED IN THE EXAMPLE]

### 3.2 SD-JWT VC-based encoding 

| **Data Identifier** | **Attribute identifier** | **Encoding format** | **Notes** |
|---------------------|--------------------------|---------------------|-----------|
| employer.id	|	urn:dgempl:pubeaas:pda1:v1:attribute:employer:id | string |	See section 2 |
| employer.name |	urn:dgempl:pubeaas:pda1:v1:attribute:employer:name | string | See section 2 |
| employer.country	| urn:dgempl:pubeaas:pda1:v1:attribute:employer:country | string | (ISO 3166-1 alpha-2) |
| work_address.locality |	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:locality | string | See section 2 |
| work_address.country | urn:dgempl:pubeaas:pda1:v1:attribute:work_address:country | string | (ISO 3166-1 alpha-2) |
| legislation_country |	urn:dgempl:pubeaas:pda1:v1:attribute:legislation_country | string |(ISO 3166-1 alpha-2) |
| status_confirmation	|	urn:dgempl:pubeaas:pda1:v1:attribute:status_confirmation | string |	See section 2 |
| work_address.region |	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:region | string | See section 2 |
| work_address.formatted | urn:dgempl:pubeaas:pda1:v1:attribute:work_address:formatted | string | See section 2 |
| work_address.street_address	|	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:street_address | string | See section 2 |
| work_address.building_number | urn:dgempl:pubeaas:pda1:v1:attribute:work_address:building_number | string	| See section 2 |
| work_address.postal_code	|	urn:dgempl:pubeaas:pda1:v1:attribute:work_address:postal_code	| string | See section 2 |


The PD A1 credential implements selective disclosure using the SD-JWT model. This allows a credential holder to disclose only the minimum required claims to a verifier, supporting GDPR-compliant privacy by design.
-	Claims marked "always" in the SD policy must be selectively disclosed by the holder.
-	Claims marked "never" are always publicly visible and required for verification.

|Claim Path |	Disclosure (sd) |	Purpose |
|-----------|-----------------|---------|
| personal_administrative_number |	always	| Protected identifier; disclosed only when required for verification|
| document_number	| always	| PD A1 document ID; disclosed only when required |
| issuing_authority (and subfields id, name) | never	| Issuance authority metadata; always visible |
| authentic_source (and subfields id, name) |	never	| Verification source; always visible |
| issuing_country	| never	| Jurisdiction and national policy context |
| date_of_expiry, date_of_issuance |	never |	Credential administrative validity |
| starting_date, ending_date	| never	| Coverage period for social security |
| employer (and subfields id, name, country) | never |	Workplace identification; mandatory for entitlement verification |
| work_address (all fields)	| never |	Location of work; mandatory for coverage assessment |
| legislation_country |	never |	Applicable legal framework |
| status_confirmation |	never |	Legal status code determining applicable law |

This embedded policy establishes a verifier-agnostic framework for enforcing disclosure behaviour, regardless of wallet implementation.



#### Example SD-JWT Claim Set

```json
{
  "authentic_source": {
    "id": "DK:DC4EUINST",
    "name": "DC4EUINST"
  },
  "cnf": {
    "jwk": {
      "kid": "default_signing_key_id",
      "crv": "P-256",
      "kty": "EC",
      "x": "EPqQJRHlaHBQ6gTNcmb5p04fNu5PwQBuxd1vblB5mqM",
      "y": "BnF-La22tTbgXqRX_rTagSscVQkOfJiNm4YaZ-u9zmk"
    }
  },
  "date_of_expiry": "",
  "date_of_issuance": "",
  "employer": {
    "country": "",
    "id": "",
    "name": ""
  },
  "ending_date": "2025-07-01",
  "exp": 1786793463,
  "iss": "https://dc4eu.dev-eessi.dk:444",
  "issuing_authority": {
    "id": "DK:Playground",
    "name": "Danish Playground Issuer"
  },
  "issuing_country": "DK",
  "jti": "6005ac36-4b6a-40a1-9973-2b93131ca64d",
  "legislation_country": "AT",
  "nbf": 1755257463,
  "starting_date": "2025-06-01",
  "status_confirmation": "",
  "vct": "urn:eudi:pda1:1",
  "personal_administrative_number": "70",
  "document_number": "276a060517d94e918657314d095463bc_3",
  "work_address": {
    "country": "",
    "formatted": "",
    "house_number": "",
    "locality": "",
    "postal_code": "",
    "region": "",
    "street_address": ""
  }
}
```
### Example SD-JWT in Base64
> eyJ0eXAiOiJzZCtqd3QiLCJhbGciOiJFUzI1NiJ9.eyJhdXRoZW50aWNfc291cmNlIjp7ImlkIjoiREs6REM0RVVJTlNUIiwibmFtZSI6IkRDNEVVSU5TVCJ9LCJjbmYiOnsiandrIjp7ImtpZCI6ImRlZmF1bHRfc2lnbmluZ19rZXlfaWQiLCJjcnYiOiJQLTI1NiIsImt0eSI6IkVDIiwieCI6IkVQcVFKUkhsYUhCUTZnVE5jbWI1cDA0Zk51NVB3UUJ1eGQxdmJsQjVtcU0iLCJ5IjoiQm5GLUxhMjJ0VGJnWHFSWF9yVGFnU3NjVlFrT2ZKaU5tNFlhWi11OXptayJ9fSwiZGF0ZV9vZl9leHBpcnkiOiIiLCJkYXRlX29mX2lzc3VhbmNlIjoiIiwiZW1wbG95ZXIiOnsiY291bnRyeSI6IiIsImlkIjoiIiwibmFtZSI6IiJ9LCJlbmRpbmdfZGF0ZSI6IjIwMjUtMDctMDEiLCJleHAiOjE3ODY3OTM0NjMsImlzcyI6Imh0dHBzOi8vZGM0ZXUuZGV2LWVlc3NpLmRrOjQ0NCIsImlzc3VpbmdfYXV0aG9yaXR5Ijp7ImlkIjoiREs6UGxheWdyb3VuZCIsIm5hbWUiOiJEYW5pc2ggUGxheWdyb3VuZCBJc3N1ZXIifSwiaXNzdWluZ19jb3VudHJ5IjoiREsiLCJqdGkiOiI2MDA1YWMzNi00YjZhLTQwYTEtOTk3My0yYjkzMTMxY2E2NGQiLCJsZWdpc2xhdGlvbl9jb3VudHJ5IjoiQVQiLCJuYmYiOjE3NTUyNTc0NjMsInN0YXJ0aW5nX2RhdGUiOiIyMDI1LTA2LTAxIiwic3RhdHVzX2NvbmZpcm1hdGlvbiI6IiIsInZjdCI6InVybjpldWRpOnBkYTE6MSIsIl9zZCI6WyIyYzExaHdxRUFoZnJvM0YtQ2FIOHg4SmN2SFRfMEF6T3ducG5mVHZwUENJIiwiX01iRmVxb3dEYkJqNUpTZUdteUt1bXFaYjNBTVVmNFhJWlZaaFhIbVpJcyIsImVWQW0xTHRydmY2WFNnSFlnV3VKZFFjdVZPSmZveE9oMVV2eUxOY1pkTjQiXSwiX3NkX2FsZyI6IlNIQS0yNTYifQ.FDX3fKiwDutKrR9-OFHVwIz0ubzA04JyRpk0cmr5OtisgJwosbJR6zeJgZTdkpZkF5Tv-eprI2VoWKuX3Uv3kA~WyI5NWE5MDE4OTljMzQ3ZjBjIiwid29ya19hZGRyZXNzIix7ImNvdW50cnkiOiIiLCJmb3JtYXR0ZWQiOiIiLCJob3VzZV9udW1iZXIiOiIiLCJsb2NhbGl0eSI6IiIsInBvc3RhbF9jb2RlIjoiIiwicmVnaW9uIjoiIiwic3RyZWV0X2FkZHJlc3MiOiIifV0~WyJjNmIyZDdiNjBmNWNiNjVkIiwicGVyc29uYWxfYWRtaW5pc3RyYXRpdmVfbnVtYmVyIiwiNzAiXQ~WyI3MTdiODQ1MzdjMTRmZGIyIiwiZG9jdW1lbnRfbnVtYmVyIiwiMjc2YTA2MDUxN2Q5NGU5MTg2NTczMTRkMDk1NDYzYmNfMyJd~

### Example payload for the SD-JWT VC
```json
{
  "authentic_source": {
    "id": "DK:DC4EUINST",
    "name": "DC4EUINST"
  },
  "cnf": {
    "jwk": {
      "kid": "default_signing_key_id",
      "crv": "P-256",
      "kty": "EC",
      "x": "EPqQJRHlaHBQ6gTNcmb5p04fNu5PwQBuxd1vblB5mqM",
      "y": "BnF-La22tTbgXqRX_rTagSscVQkOfJiNm4YaZ-u9zmk"
    }
  },
  "date_of_expiry": "",
  "date_of_issuance": "",
  "employer": {
    "country": "",
    "id": "",
    "name": ""
  },
  "ending_date": "2025-07-01",
  "exp": 1786793463,
  "iss": "https://dc4eu.dev-eessi.dk:444",
  "issuing_authority": {
    "id": "DK:Playground",
    "name": "Danish Playground Issuer"
  },
  "issuing_country": "DK",
  "jti": "6005ac36-4b6a-40a1-9973-2b93131ca64d",
  "legislation_country": "AT",
  "nbf": 1755257463,
  "starting_date": "2025-06-01",
  "status_confirmation": "",
  "vct": "urn:eudi:pda1:1",
  "_sd": [
    "2c11hwqEAhfro3F-CaH8x8JcvHT_0AzOwnpnfTvpPCI",
    "_MbFeqowDbBj5JSeGmyKumqZb3AMUf4XIZVZhXHmZIs",
    "eVAm1Ltrvf6XSgHYgWuJdQcuVOJfoxOh1UvyLNcZdN4"
  ],
  "_sd_alg": "SHA-256"
}
```

### Disclosures in the SD-JWT VC
    Salt: 95a901899c347f0c
    Key: work_address
    Value: { "country": "", "formatted": "", "house_number": "", "locality": "", "postal_code": "", "region": "", "street_address": "" }

    Salt: c6b2d7b60f5cb65d
    Key: personal_administrative_number
    Value: 70

    Salt: 717b84537c14fdb2
    Key: document_number
    Value: 276a060517d94e918657314d095463bc_3


## 4 Attestation usage
*Briefly describe the primary use cases or scenarios for which this attestation 
type is intended*

*Additionally, in this section it SHOULD  be specified whether a Relying Party receiving the attestation
must request and verify a PID (see ARB_27 in [Topic 12]). Also beyond PID verification, 
it SHOULD be defined what other key obligations does a Relying Party have when processing 
this attestation type (e.g., signature verification, freshness checks)*

*Furthermore, provide potential presentation requirements, e.g., are there specific 
requirements for how this attestation must be presented (e.g., online, offline, specific protocols)?"*

*Finally, in this section information about potential transactional data
SHALL be defined (see [Topic 20] of Annex 2 of the ARF).*

## 5 Trust anchors

Trust anchors for EHIC PuB-EAAs are the same as defined in the common rulebook.

## 6 Revocation

Revocation patterns for EHIC PuB-EAAs are the same as defined in the common rulebook.

## 7 Compliance

The Compliance follows the same principles as set out in the common rulebook.

## 8 References
| **Item Reference** | **Standard name/details**|
|--------------------|---------------------------|
| [European Digital Identity Regulation] | [Regulation (EU) 2024/1183](https://eur-lex.europa.eu/legal-content/EN/TXT/HTML/?uri=OJ:L_202401183) of the European Parliament and of the Council of 11 April 2024 amending Regulation (EU) No 910/2014 as regards establishing the European Digital Identity Framework |
| [HAIP] | Yasuda, K. *et al,* OpenID4VC High Assurance Interoperability Profile, OpenId Foundation, Version draft-03 |
| [IANA-JWT-Claims] | IANA JSON Web Token Claims Registry. Available: <https://www.iana.org/assignments/jwt/jwt.xhtml> |
| [ISO/IEC 18013-5] |  ISO/IEC 18013-5, Personal identification --- ISO-compliant driving licence - Part 5: Mobile driving licence (mDL) application, First edition, 2021-09 |
| [OIDC] | Sakimura, N. et al., "OpenID Connect Core 1.0", OpenID Foundation. Available: <https://openid.net/specs/openid-connect-core-1_0.html> |
| [RFC 3339] | RFC 3339  - Date and Time on the Internet: Timestamps, G. Klyne et al., July 2002 |
| [RFC 8610] | RFC 8610  - Concise Data Definition Language (CDDL): A Notational Convention to Express Concise Binary Object Representation (CBOR) and JSON Data Structures, H. Birkholz et al., June 2019 |
| [RFC 8943] | RFC 8943  - Concise Binary Object Representation (CBOR) Tags for Date, M. Jones et al., November 2020 |
| [RFC 8949] | RFC 8949 - Concise Binary Object Representation (CBOR), C. Bormann et al., December 2020 |
| [SD-JWT VC] |  SD-JWT-based Verifiable Credentials (SD-JWT VC). Available: <https://datatracker.ietf.org/doc/draft-ietf-oauth-sd-jwt-vc/>, version draft-ietf-oauth-sd-jwt-vc-09  |
| [Topic 7] | ARF Annex 2 - Topic 7 - Attestation revocation and revocation checking Available: <https://eu-digital-identity-wallet.github.io/eudi-doc-architecture-and-reference-framework/latest/annexes/annex-2/annex-2-high-level-requirements/#a237-topic-7-attestation-revocation-and-revocation-checking>|
| [Topic 10] | ARF Annex 2 - Topic 10 - Issuing a PID or attestation to a Wallet Unit: <https://eu-digital-identity-wallet.github.io/eudi-doc-architecture-and-reference-framework/latest/annexes/annex-2/annex-2-high-level-requirements/#a2310-topic-10-issuing-a-pid-or-attestation-to-a-wallet-unit>|
| [Topic 12] | ARF Annex 2 - Topic 12 - Attestation Rulebooks, Available: <https://eu-digital-identity-wallet.github.io/eudi-doc-architecture-and-reference-framework/latest/annexes/annex-2/annex-2-high-level-requirements/#a2312-topic-12-attestation-rulebooks>|
| [Topic 20] | ARF Annex 2 - Strong User authentication for electronic payments, Available: <https://eu-digital-identity-wallet.github.io/eudi-doc-architecture-and-reference-framework/latest/annexes/annex-2/annex-2-high-level-requirements/#a2320-topic-20-strong-user-authentication-for-electronic-payments>|
| [W3C VCDM v2.0] | Sporny, M. *et al,* Verifiable Credentials Data Model v2.0, W3C Recommendation.  |








 
