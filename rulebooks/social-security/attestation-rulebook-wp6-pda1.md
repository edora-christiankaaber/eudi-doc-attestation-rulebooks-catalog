
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
  "vct": "urn:eudi:pda1:1",
  "jti": "urn:uuid:12345678-abcd-ef01-2345-6789abcdef01",
  "sub": "did:example:abc123",
  "iss": "https://pda1.issuing-authority.example",
  "iat": 1721470000,
  "exp": 1724072000,
  "nbf": 1721460000,
  "cnf": {
    "jwk": {
      "kty": "EC",
      "crv": "P-256",
      "x": "abc...xyz",
      "y": "123...789"
    }
  },
  "personal_administrative_number": "1717150699",
  "issuing_authority": {
    "id": "AUTH123",
    "name": "Austrian Social Insurance",
    "country": "AT"
  },
  "date_of_issuance": "2025-06-01",
  "date_of_expiry": "2026-06-01",
  "authentic_source": {
    "id": "AT:9900",
    "name": "Austrian Social Insurance Institution"
  },
  "starting_date": "2025-05-01",
  "ending_date": "2026-06-01",
  "document_number": "PDA1-AT-2025-000123",
  "employer": [
    {
      "type": "01",
      "id": "AT-COMPANY-001",
      "name": "Vienna Logistics GmbH",
      "country": "AT"
    }
  ],
  "work_information": {
    "work_address": [
      {
        "formatted": "Industriestrasse 10, 1200 Wien, Austria",
        "street_address": "Industriestrasse",
        "house_number": "10",
        "postal_code": "1200",
        "locality": "Wien",
        "region": "Wien",
        "country": "AT",
        "company_name": "Vienna Logistics GmbH",
        "company_id": "AT-COMPANY-001"
      },
      {
        "formatted": "Freight Port 5, 20457 Hamburg, Germany",
        "street_address": "Freight Port",
        "house_number": "5",
        "postal_code": "20457",
        "locality": "Hamburg",
        "region": "Hamburg",
        "country": "DE",
        "company_name": "Vienna Logistics GmbH",
        "company_id": "AT-COMPANY-001"
      }
    ]
  },
  "legislation_country": "AT",
  "transitional_rules": false,
  "status_confirmation": "01"
}
```
### Example SD-JWT in Base64
> eyJ0eXAiOiJzZCtqd3QiLCJhbGciOiJFUzI1NiJ9.eyJ2Y3QiOiJ1cm46ZXVkaTpwZGExOjEiLCJqdGkiOiJ1cm46dXVpZDoxMjM0NTY3OC1hYmNkLWVmMDEtMjM0NS02Nzg5YWJjZGVmMDEiLCJzdWIiOiJkaWQ6ZXhhbXBsZTphYmMxMjMiLCJpc3MiOiJodHRwczovL3BkYTEuaXNzdWluZy1hdXRob3JpdHkuZXhhbXBsZSIsImlhdCI6MTcyMTQ3MDAwMCwiZXhwIjoxNzI0MDcyMDAwLCJuYmYiOjE3MjE0NjAwMDAsImNuZiI6eyJqd2siOnsia3R5IjoiRUMiLCJjcnYiOiJQLTI1NiIsIngiOiJhYmMuLi54eXoiLCJ5IjoiMTIzLi4uNzg5In19LCJpc3N1aW5nX2F1dGhvcml0eSI6eyJpZCI6IkFVVEgxMjMiLCJuYW1lIjoiQXVzdHJpYW4gU29jaWFsIEluc3VyYW5jZSIsImNvdW50cnkiOiJBVCJ9LCJkYXRlX29mX2lzc3VhbmNlIjoiMjAyNS0wNi0wMSIsImRhdGVfb2ZfZXhwaXJ5IjoiMjAyNi0wNi0wMSIsImF1dGhlbnRpY19zb3VyY2UiOnsiaWQiOiJBVDo5OTAwIiwibmFtZSI6IkF1c3RyaWFuIFNvY2lhbCBJbnN1cmFuY2UgSW5zdGl0dXRpb24ifSwic3RhcnRpbmdfZGF0ZSI6IjIwMjUtMDUtMDEiLCJlbmRpbmdfZGF0ZSI6IjIwMjYtMDYtMDEiLCJlbXBsb3llciI6W3sidHlwZSI6IjAxIiwiaWQiOiJBVC1DT01QQU5ZLTAwMSIsIm5hbWUiOiJWaWVubmEgTG9naXN0aWNzIEdtYkgiLCJjb3VudHJ5IjoiQVQifV0sIndvcmtfaW5mb3JtYXRpb24iOnsid29ya19hZGRyZXNzIjpbeyJmb3JtYXR0ZWQiOiJJbmR1c3RyaWVzdHJhc3NlIDEwLCAxMjAwIFdpZW4sIEF1c3RyaWEiLCJzdHJlZXRfYWRkcmVzcyI6IkluZHVzdHJpZXN0cmFzc2UiLCJob3VzZV9udW1iZXIiOiIxMCIsInBvc3RhbF9jb2RlIjoiMTIwMCIsImxvY2FsaXR5IjoiV2llbiIsInJlZ2lvbiI6IldpZW4iLCJjb3VudHJ5IjoiQVQiLCJjb21wYW55X25hbWUiOiJWaWVubmEgTG9naXN0aWNzIEdtYkgiLCJjb21wYW55X2lkIjoiQVQtQ09NUEFOWS0wMDEifSx7ImZvcm1hdHRlZCI6IkZyZWlnaHQgUG9ydCA1LCAyMDQ1NyBIYW1idXJnLCBHZXJtYW55Iiwic3RyZWV0X2FkZHJlc3MiOiJGcmVpZ2h0IFBvcnQiLCJob3VzZV9udW1iZXIiOiI1IiwicG9zdGFsX2NvZGUiOiIyMDQ1NyIsImxvY2FsaXR5IjoiSGFtYnVyZyIsInJlZ2lvbiI6IkhhbWJ1cmciLCJjb3VudHJ5IjoiREUiLCJjb21wYW55X25hbWUiOiJWaWVubmEgTG9naXN0aWNzIEdtYkgiLCJjb21wYW55X2lkIjoiQVQtQ09NUEFOWS0wMDEifV19LCJsZWdpc2xhdGlvbl9jb3VudHJ5IjoiQVQiLCJzdGF0dXNfY29uZmlybWF0aW9uIjoiMDEiLCJfc2QiOlsiTlRtSzZ4aWQyYzZSVFhOVnB3bkxhbEtSTnRrV01obWtlMXdpN3RPSWx0RSIsInFNZVFfblBEUHNRTURSLU54NWJBU0J1bGNGWWpMQ3NrY2RZZzBISUdRWFUiLCJ0TmdrYlRBX2lNUExuN0N6RnE1Z2hWM05tb1k1enBzX1Y0NExsZTVXdWRnIl0sIl9zZF9hbGciOiJTSEEtMjU2In0.SPbYtES1lpZPEtopWJDs7cBh2d2PL773hdKJ9sSo1L4BoNQZQL4F4y71E_vVovhTO-iynNaHW9UD7w4Gepj-Lg~WyJlMTM1M2Y3YzllNTZjMGFhIiwicGVyc29uYWxfYWRtaW5pc3RyYXRpdmVfbnVtYmVyIiwiMTcxNzE1MDY5OSJd~WyIwNjMxYjk4YjEyNGU2YzcxIiwiZG9jdW1lbnRfbnVtYmVyIiwiUERBMS1BVC0yMDI1LTAwMDEyMyJd~WyI0ZTE4YjkzZWQ4MWVmNTFlIiwidHJhbnNpdGlvbmFsX3J1bGVzIixmYWxzZV0~

### Example payload for the SD-JWT VC
```json
{
  "vct": "urn:eudi:pda1:1",
  "jti": "urn:uuid:12345678-abcd-ef01-2345-6789abcdef01",
  "sub": "did:example:abc123",
  "iss": "https://pda1.issuing-authority.example",
  "iat": 1721470000,
  "exp": 1724072000,
  "nbf": 1721460000,
  "cnf": {
    "jwk": {
      "kty": "EC",
      "crv": "P-256",
      "x": "abc...xyz",
      "y": "123...789"
    }
  },
  "issuing_authority": {
    "id": "AUTH123",
    "name": "Austrian Social Insurance",
    "country": "AT"
  },
  "date_of_issuance": "2025-06-01",
  "date_of_expiry": "2026-06-01",
  "authentic_source": {
    "id": "AT:9900",
    "name": "Austrian Social Insurance Institution"
  },
  "starting_date": "2025-05-01",
  "ending_date": "2026-06-01",
  "employer": [
    {
      "type": "01",
      "id": "AT-COMPANY-001",
      "name": "Vienna Logistics GmbH",
      "country": "AT"
    }
  ],
  "work_information": {
    "work_address": [
      {
        "formatted": "Industriestrasse 10, 1200 Wien, Austria",
        "street_address": "Industriestrasse",
        "house_number": "10",
        "postal_code": "1200",
        "locality": "Wien",
        "region": "Wien",
        "country": "AT",
        "company_name": "Vienna Logistics GmbH",
        "company_id": "AT-COMPANY-001"
      },
      {
        "formatted": "Freight Port 5, 20457 Hamburg, Germany",
        "street_address": "Freight Port",
        "house_number": "5",
        "postal_code": "20457",
        "locality": "Hamburg",
        "region": "Hamburg",
        "country": "DE",
        "company_name": "Vienna Logistics GmbH",
        "company_id": "AT-COMPANY-001"
      }
    ]
  },
  "legislation_country": "AT",
  "status_confirmation": "01",
  "_sd": [
    "NTmK6xid2c6RTXNVpwnLalKRNtkWMhmke1wi7tOIltE",
    "qMeQ_nPDPsQMDR-Nx5bASBulcFYjLCskcdYg0HIGQXU",
    "tNgkbTA_iMPLn7CzFq5ghV3NmoY5zps_V44Lle5Wudg"
  ],
  "_sd_alg": "SHA-256"
}
```

### Disclosures in the SD-JWT VC
    Salt: e1353f7c9e56c0aa
    Key: personal_administrative_number
    Value: 1717150699

    Salt: 0631b98b124e6c71
    Key: document_number
    Value: PDA1-AT-2025-000123

    Salt: 4e18b93ed81ef51e
    Key: transitional_rules
    Value: false


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

## Annex 1 - Schema for a PD A1 SD-JWT Credential
```json
{
 "$schema": "https://json-schema.org/draft/2020-12/schema",
 "title": "DC4EU PDA1 SD-JWT VC Schema",
 "type": "object",
 "additionalProperties": false,
 "properties": {
 "vct": {
 "type": "string",
 "description": "The Verifiable Credential type identifier, as defined in ietf-oauth-sdjwt-vc (draft 09).",
 "enum": [
 "urn:eudi:pda1:1"
 ]
 },
 "jti": {
 "type": "string",
 "description": "Verifiable Credential unique identifier to prevent replay attacks. It 
needs to be unique for the JWT effective lifespan.",
 "minLength": 1,
 "maxLength": 255
 },
 "sub": {
 "type": "string",
 "description": "Subject identifier for the JWT, representing the principal that is the 
subject of the JWT. This is a case-sensitive string containing a unique identifier, as defined 
in RFC 7519 (JWT)."
 },
 "iss": {
 "type": "string",
 "format": "uri",
 "description": "Issuer identifier for the JWT, expressed as a URI, according to RFC 7519 
(JWT)."
 },
 "iat": {
 "type": "integer",
 "description": "Issued at time indicating when the JWT was issued, represented as a 
NumericDate (number of seconds since 1970-01-01T00:00:00Z UTC) according to RFC 7519 (JWT)."
 },
 "cnf": {
 "type": "object",
 "description": "Contains confirmation key information used to prove possession of a 
private key, as defined in RFC 7800 (Proof-of-Possession Key Semantics for JWTs).",
 "properties": {
 "jwk": {
 "type": "object",
 "description": "JSON Web Key (JWK) object. Structure not fully specified here."
 }
},
 "required": [
 "jwk"
 ],
 "additionalProperties": true
 },
 "exp": {
 "type": "integer",
 "description": "Expiration time on or after which the JWT must not be accepted for 
processing, represented as a NumericDate (number of seconds since 1970-01-01T00:00:00Z UTC) 
according to RFC 7519 (JWT)."
 },
 "nbf": {
 "type": "integer",
 "description": "Not before time before which the JWT must not be accepted for processing, 
represented as a NumericDate (number of seconds since 1970-01-01T00:00:00Z UTC) according to RFC 
7519 (JWT)."
 },
 "personal_administrative_number": {
 "type": "string",
 "minLength": 4,
 "maxLength": 50,
 "description": "The unique personal identifier assigned to the natural person for social 
security services and benefits by the competent institution (Social Security Number). The 
electronic identification scheme under which the identifier is issued, as well as the policy 
applied to the values of this attribute including, where applicable, specific conditions for its 
processing must be defined by the competent institution as part of this schema.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:personal_administrative_number"
 },
 "issuing_authority": {
 "type": "object",
 "description": "The authority responsible for issuing the PDA1.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority",
 "properties": {
 "id": {
 "type": "string",
 "minLength": 1,
 "maxLength": 20,
 "description": "The unique identifier of the PDA1 issuing authority.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority:id"
 },
 "name": {
 "type": "string",
 "minLength": 1,
 "maxLength": 100,
 "description": "The full name of the PDA1 issuing authority.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority:name"
 },
 "country": {
 "type": "string",
 "pattern": "^[A-Z]{2}$",
 "description": "Member State code (ISO 3166-1 alpha-2) representing the country under 
whose jurisdiction the PDA1 is issued.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority:country"
 }
 },
 "required": [
 "id",
 "name",
 "country"
 ],
 "additionalProperties": false
 },
"date_of_issuance": {
 "type": "string",
 "format": "date",
 "description": "Date determined by the competent institution as either the start of the 
administrative validity period of the record represented by this PDA1, or the issuance date of 
the PDA1 credential. The value is expressed as a full-date (YYYY-MM-DD) in accordance with ISO 
8601-1 and RFC 3339. The exact interpretation is to be defined by the competent institution as 
part of this schema.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:date_of_issuance"
},
"date_of_expiry": {
 "type": "string",
 "format": "date",
 "description": "Date determined by the competent institution as the end of the administrative 
validity period of the record represented by this PDA1, or the expiration date of the PDA1 
credential. The value is expressed as a full-date (YYYY-MM-DD) in accordance with ISO 8601-1 and 
RFC 3339. The exact interpretation is to be defined by the competent institution as part of this 
schema.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:date_of_expiry"
},
"authentic_source": {
 "type": "object",
 "description": "The competent institution responsible for the PDA1, as registered in the 
Electronic Exchange of Social Security Information (EESSI).",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:authentic_source",
 "properties": {
 "id": {
 "type": "string",
 "minLength": 1,
 "maxLength": 20,
 "description": "The unique identifier of the competent institution responsible for the 
PDA1, as registered in the Electronic Exchange of Social Security Information (EESSI).",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:authentic_source:id"
 },
 "name": {
 "type": "string",
 "minLength": 1,
 "maxLength": 100,
 "description": "The full name of the competent institution responsible for the PDA1, as 
registered in the Electronic Exchange of Social Security Information (EESSI).",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:authentic_source:name"
 }
 },
 "required": [
 "id",
 "name"
 ],
 "additionalProperties": false
},
"starting_date": {
 "type": "string",
 "format": "date",
 "description": "Date determined by the competent institution as the start date of the business 
decision validity period of the PDA1. The value is expressed as a full-date (YYYY-MM-DD) in 
accordance with ISO 8601-1 and RFC 3339.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:starting_date"
},
"ending_date": {
 "type": "string",
 "format": "date",
 "description": "Date determined by the competent institution as the end date of the business 
decision validity period of the PDA1. The value is expressed as a full-date (YYYY-MM-DD) in 
accordance with ISO 8601-1 and RFC 3339.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:ending_date"
},
"document_number": {
 "type": "string",
 "minLength": 4,
 "maxLength": 50,
 "description": "Unique document identifier assigned by the competent institution. This value 
identifies the specific PDA1 document and may be used for administrative validation.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:document_number"
},
"employer": {
 "type": "array",
 "minItems": 1,
 "description": "A list of employer details/details of self-employment, based on EU or Member 
State registries.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:employer",
 "items": {
 "type": "object",
 "properties": {
"type": {
 "type": "string",
 "enum": [
 "01",
 "02"
 ],
 "description": "The type of employment. Allowed values: 01 = Employment, 02= SelfEmployment",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:employer:type"
 },
 "id": {
 "type": "string",
 "minLength": 1,
 "maxLength": 20,
 "description": "The unique identifier of the employer/self-employment, in EU or Member 
State registries.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:employer:id"
 },
 "name": {
 "type": "string",
 "minLength": 1,
 "maxLength": 100,
 "description": "The full name of the employer/self-employment, in EU or Member State 
registries.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:employer:name"
 },
 "country": {
 "type": "string",
 "pattern": "^[A-Z]{2}$",
 "description": "Country code (ISO 3166-1 alpha-2) of the country where the 
employer/self-employed is registered.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:employer:country"
 }
 },
 "required": [
 "type",
 "id",
 "name",
 "country"
 ],
 "additionalProperties": false
 }
},
"work_information": {
 "type": "object",
 "description": "Information about the person's work location, either as a fixed address or no 
fixed place of work.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:work_information",
 "properties": {
 "no_fixed_place_of_work": {
 "type": "string",
 "pattern": "^[A-Z]{2}$",
 "description": "Country code (ISO 3166-1 alpha-2) of the country where there is no fixed 
place of work.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:no_fixed_place_of_work"
 },
 "work_address": {
 "type": "array",
 "minItems": 1,
 "description": "Structured address list for fixed places of work, with optional company 
details.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:work_information:work_address",
 "items": {
 "type": "object",
 "properties": {
 "formatted": {
 "type": "string",
 "minLength": 2,
 "maxLength": 512,
 "description": "Full formatted address per UPU S42 / ISO 19160-4 / OIDC standards.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:formatted"
},
 "street_address": {
 "type": "string",
 "minLength": 1,
 "maxLength": 100,
 "description": "Street name.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:street_address"
 },
 "house_number": {
 "type": "string",
 "minLength": 1,
 "maxLength": 20,
 "description": "House or building number.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:house_number"
 },
 "postal_code": {
 "type": "string",
 "minLength": 1,
 "maxLength": 20,
 "description": "Postal or ZIP code.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:postal_code"
 },
 "locality": {
 "type": "string",
 "minLength": 1,
 "maxLength": 100,
 "description": "City or locality.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:locality"
 },
 "region": {
 "type": "string",
 "minLength": 1,
 "maxLength": 100,
 "description": "Administrative region.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:region"
 },
 "country": {
 "type": "string",
 "pattern": "^[A-Z]{2}$",
 "description": "ISO 3166-1 alpha-2 country code.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:country"
 },
 "company_name": {
 "type": "string",
 "minLength": 1,
 "maxLength": 100,
 "description": "Name of the company or ship operator.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:company_name"
 },
 "company_id": {
 "type": "string",
 "minLength": 1,
 "maxLength": 20,
 "description": "Company ID from national or EU registries.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:company_id"
 },
 "flag_base_home": {
 "type": "string",
 "minLength": 1,
 "maxLength": 20,
 "description": " Flag state or home base of the company/ship where you will be 
employed.",
 "$comment": "Namespace: 
urn:dgempl:pubeaas:v1:attribute:work_information:work_address:flag_base_home"
 }
},
 "required": [ "locality", "country" ],
 "additionalProperties": false
 }
 }
 },
 "anyOf": [
 { "required": [ "no_fixed_place_of_work" ] },
 { "required": [ "work_address" ] }
 ],
 "additionalProperties": false
 },
 "legislation_country": {
 "type": "string",
 "pattern": "^[A-Z]{2}$",
 "description": "Country code (ISO 3166-1 alpha-2) whose legislation is to be applied 
during the work abroad.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:legislation_country"
 },
 "transitional_rules": {
 "type": "boolean",
 "description": "Indication, whether transitional rules apply as provided by the 
Regulation.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:transitional_rules"
 },
 "status_confirmation": {
 "type": "string",
 "enum": [
 "01",
 "02",
 "03",
 "04",
 "05",
 "06",
 "07",
 "08",
 "09",
 "10",
 "11",
 "12"
 ],
 "description": "Employment or posting legal framework category code applicable to the 
worker. Allowed values: 01 = Posted employed person, 02 = Employed in 2+ states, 03 = Posted 
self-employed, 04 = Self-employed in 2+ states, 05 = Civil servant, 06 = Contract staff, 07 = 
Mariner, 08 = Employed & self-employed in different states, 09 = Civil servant + employed/selfemployed, 10 = Flight crew, 11 = Exception, 12 = Local employment.",
 "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:status_confirmation"
 }
 },
 "required": [
 "vct",
 "jti",
 "sub",
 "iss",
 "iat",
 "cnf",
 "personal_administrative_number",
 "issuing_authority",
 "date_of_issuance",
 "authentic_source",
 "starting_date",
 "ending_date",
 "employer",
 "document_number",
 "work_information",
 "legislation_country",
 "status_confirmation"
 ]
}

```

## Annex 2 - Schema for PD A1 Credential Display & Disclosures
```json
{
 "vct": "urn:eudi:pda1:1",
 "name": "DC4EU PDA1 SD-JWT VCTM",
 "description": "Selective disclosure metadata for Portable Document A1 (PDA1) SD-JWT VC 
including subclaims.",
"$comment": "Implementation of the DC4EU VCTM may require Member State-specific clarifications 
to align with national policies governing the display of included claims.",
"display": [
 {
 "lang": "en-EU",
 "name": "DC4EU PDA1 SD-JWT VC",
 "description": " Portable Document A1 (PDA1) SD-JWT VC",
 "rendering": {
 "svg_templates": [
 {
 "uri": "https://demo-issuer.wwwallet.org/public/creds/pda1/portable-document-a1-svgdc4eu-01.svg",
 "uri#integrity": "sha256-kIV+WWH0aFROnkfy5gqx/cRivRNkCrkNBMgHgysNrn0=",
 "properties": {
 "orientation": "landscape",
 "color_scheme": "light",
 "contrast": "normal"
 }
 }
 ]
 }
 }
 ],
 "claims": [
 {
 "path": [
 "personal_administrative_number"
 ],
 "sd": "always",
 "display": [
 {
 "lang": "en-EU",
 "label": "Social Security PIN",
 "description": "Unique personal identifier used by social security services."
 }
 ]
 },
 {
 "path": [
 "issuing_authority"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Issuing Authority",
 "description": "The authority responsible for issuing the PDA1."
 }
 ]
 },
 {
 "path": [
 "issuing_authority",
 "id"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Issuing Authority ID",
 "description": "The unique identifier of the PDA1 issuing authority."
 }
 ]
 },
 {
"path": [
 "issuing_authority",
 "name"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Issuing Authority Name",
 "description": "The full name of the PDA1 issuing authority."
 }
 ]
 },
 {
 "path": [
 "issuing_authority",
 "country"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Issuing Country",
 "description": "Country of the PDA1 issuing authority."
 }
 ]
 },
 {
 "path": [
 "date_of_issuance"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Issuance Date",
 "description": "Issuance date of the PDA1."
 }
 ]
 },
 {
 "path": [
 "date_of_expiry"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Expiry Date",
 "description": "PDA1 credential expiry date."
 }
 ]
 },
 {
 "path": [
 "authentic_source"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Authentic Source",
 "description": "Competent institution as registered in the EESSI Institution 
Repository."
 }
 ]
 },
 {
 "path": [
 "authentic_source",
 "id"
 ],
 "sd": "never",
"display": [
 {
 "lang": "en-EU",
 "label": "Source ID",
 "description": " Identifier of the competent institution as registered in the EESSI 
Institution Repository."
 }
 ]
 },
 {
 "path": [
 "authentic_source",
 "name"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Source Name",
 "description": " Name of the competent institution as registered in the EESSI 
Institution Repository."
 }
 ]
 },
 {
 "path": [
 "starting_date"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Starting Date",
 "description": "Start date of the business decision validity period of the PDA1."
 }
 ]
 },
 {
 "path": [
 "ending_date"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Ending Date",
 "description": "End date of the business decision validity period of the PDA1."
 }
 ]
 },
 {
 "path": [
 "document_number"
 ],
 "sd": "always",
 "display": [
 {
 "lang": "en-EU",
 "label": "Document Number",
 "description": "Unique PDA1 document identifier."
 }
 ]
 },
 {
 "path": [
 "employer"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Employer",
 "description": "List of employer details/details of self-employment."
}
 ]
 },
 {
 "path": [
 "employer",
 "*",
 "type"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Employment Type",
 "description": "Type of the employment."
 }
 ]
 },
 {
 "path": [
 "employer",
 "*",
 "id"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Employer ID",
 "description": "Unique identifier of the employer/self-employment in EU or Member 
State registries."
 }
 ]
 },
 {
 "path": [
 "employer",
 "*",
 "name"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Employer Name",
 "description": "Name of the employer/self-employment in EU or Member State registries
."
 }
 ]
 },
 {
 "path": [
 "employer",
 "*",
 "country"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Employer Country",
 "description": "Country where the employer/self-employed is registered."
 }
 ]
 },
 {
 "path": [
 "work_information"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
"label": "Work Info",
 "description": "Information about the workplace."
 }
 ]
 },
 {
 "path": [
 "work_information",
 "no_fixed_place_of_work"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "No Fixed workplace",
 "description": "Country where there is no fixed place of work ."
 }
 ]
 },
 {
 "path": [
 "work_information",
 "work_address"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Place of Work",
 "description": "List of workplaces."
 }
 ]
 },
 {
 "path": [
 "work_information",
 "work_address",
 "*",
 "formatted"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Formatted Address",
 "description": "Full formatted address."
 }
 ]
 },
 {
 "path": [
 "work_information",
 "work_address",
 "*",
 "street_address"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Street name",
 "description": "Street name."
 }
 ]
 },
 {
 "path": [
 "work_information",
 "work_address",
 "*",
 "house_number"
 ],
 "sd": "never",
"display": [
 
{
 "lang": "en
-EU"
,
 "label": "House 
number"
,
 "description": "House/building number."
 
}
 
]
 },
 
{
 "path": [
 "work_information"
,
 "work_address"
,
 "*"
,
 "postal_code"
 ],
 "sd": "never"
,
 "display": [
 
{
 "lang": "en
-EU"
,
 "label": "Postal Code"
,
 "description": "ZIP or postal code."
 
}
 
]
 },
 
{
 "path": [
 "work_information"
,
 "work_address"
,
 "*"
,
 "locality"
 ],
 "sd": "never"
,
 "display": [
 
{
 "lang": "en
-EU"
,
 "label": "Locality"
,
 "description": "City or locality."
 
}
 
]
 },
 
{
 "path": [
 "work_information"
,
 "work_address"
,
 "*"
,
 "region"
 ],
 "sd": "never"
,
 "display": [
 
{
 "lang": "en
-EU"
,
 "label": "Region"
,
 "description": "Administrative region."
 
}
 
]
 },
 
{
 "path": [
 "work_information"
,
 "work_address"
,
 "*"
,
 "country"
 ],
 "sd": "never"
,
 "display": [
 
{
 "lang": "en
-EU"
,
 "label": "Country"
,
 "description": "Country code."
 
}
 
]
 },
 
{
"path": [
 "work_information",
 "work_address",
 "*",
 "company_name"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Company Name",
 "description": "Name of employer company."
 }
 ]
 },
 {
 "path": [
 "work_information",
 "work_address",
 "*",
 "company_id"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Company ID",
 "description": "Employer company ID."
 }
 ]
 },
 {
 "path": [
 "work_information",
 "work_address",
 "*",
 "flag_base_home"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Flag State Home Base",
 "description": "Flag state or home base of the company/ship where you will be 
employed."
 }
 ]
 },
 {
 "path": [
 "legislation_country"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Legislation Country",
 "description": "Country of applicable legislation."
 }
 ]
 },
 {
 "path": [
 "transitional_rules"
 ],
 "sd": "always",
 "display": [
 {
 "lang": "en-EU",
 "label": "Transitional Rules",
 "description": "Indication, whether transitional rules apply."
 }
 ]
},
 {
 "path": [
 "status_confirmation"
 ],
 "sd": "never",
 "display": [
 {
 "lang": "en-EU",
 "label": "Status Confirmation",
 "description": "Legal status category code applicable to the worker."
 }
 ]
 }
 ],
 "schema_uri": "https://demo-issuer.wwwallet.org/public/creds/pda1/portable-document-a1-schemadc4eu-01.json"
}
```




 
