# Attestation Rulebook for attestations of type  "EHIC"

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

This rulebook defines the requirements and constrains pertaining to EHIC PuB-EAAs as used within social security coordination in Europe.

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

### 1.5 Legal & Regulatory framework
The basic legal and regulatory environment is defined in the common rulebook `attestation-rulebook-wp6-common.md`.

#### 1.5.1	PRIMARY LEGAL INSTRUMENTS
In addition to the legal instruments set out in the common rulebook `attestation-rulebook-wp6-common.md` the following specific legal foundations apply to the EHIC:
| Regulation / Directive | Description |
|------------------------|-------------|
| Decision No S1 of 12 June 2009 |	Sets general provisions for the “traditional”  EHIC, including its purpose, legal effects, and fallback procedures such as provisional replacement certificates. |
| Decision No S2 of 12 June 2009 |	Specifies the technical design, visible information, and model for the “traditional” EHIC and its provisional replacement certificate.|

## 2 Attestation attributes and metadata

The European Health Insurance Card (EHIC) credential is a specialised instance of the common PuB-EAAS attribute block defined in the Rulebook `attestation-rulebook-wp6-common.md`. 

It does *not* introduce additional attributes or metadata.

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
| document_number | Unique document identifier. | string | 80067899202020289076 |

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


# 3 Attestation encoding 

## 3.1 ISO/IEC 18013-5-compliant encoding 
 FULL OR PARTIAL mDOC OF THE ATTESTATION: to be done
 
 ATTRIBUTES AND THEIR VALUES INCLUDED IN THE EXAMPLE: to be done

### 3.2 SD-JWT VC-based encoding 
Below, an example of a verifiable credential, issued during the DC4EU Pilot.

#### Example SD-JWT Claim Set

The following is an example of a claim set for an EHIC SD-JWT VC:

```json
{
  "vct": "urn:eudi:ehic:1",
  "jti": "urn:uuid:9b1deb4d-5b1d-47b5-9e3e-2b0e1b123456",
  "sub": "did:example:1234567890",
  "iss": "https://ehic.issuer.example.eu",
  "iat": 1721478000,
  "exp": 1753014000,
  "nbf": 1721474400,
  "cnf": {
    "jwk": {
      "kty": "EC",
      "crv": "P-256",
      "x": "4j5_9EF4ac9J6TR2z2eMgN3sZ2mD8X_Pb8hx7rk_F1U",
      "y": "7FsapV3Z1QGX7YZbVC1Vhqf1rXe6M3sBL0GgQoKlA9U"
    }
  },
  "personal_administrative_number": "DE987654321",
  "issuing_authority": {
    "id": "DVKA",
    "name": "GKV Spitzenverband - Deutsche Verbindungsstelle Krankenversicherung - Ausland",
    "country": "DE"
  },
  "date_of_issuance": "2025-07-15",
  "date_of_expiry": "2030-07-30",
  "authentic_source": {
    "id": "DE: 103411401",
    "name": "AOK Nordwest"
  },
  "starting_date": "2025-07-01",
  "ending_date": "2030-07-30",
  "document_number": "80112233445566778043"
}
```
### Example SD-JWT in Base64

> eyJ0eXAiOiJzZCtqd3QiLCJhbGciOiJFUzI1NiJ9.eyJ2Y3QiOiJ1cm46ZXVkaTplaGljOjEiLCJqdGkiOiJ1cm46dXVpZDo5YjFkZWI0ZC01YjFkLTQ3YjUtOWUzZS0yYjBlMWIxMjM0NTYiLCJzdWIiOiJkaWQ6ZXhhbXBsZToxMjM0NTY3ODkwIiwiaXNzIjoiaHR0cHM6Ly9laGljLmlzc3Vlci5leGFtcGxlLmV1IiwiaWF0IjoxNzIxNDc4MDAwLCJleHAiOjE3NTMwMTQwMDAsIm5iZiI6MTcyMTQ3NDQwMCwiY25mIjp7Imp3ayI6eyJrdHkiOiJFQyIsImNydiI6IlAtMjU2IiwieCI6IjRqNV85RUY0YWM5SjZUUjJ6MmVNZ04zc1oybUQ4WF9QYjhoeDdya19GMVUiLCJ5IjoiN0ZzYXBWM1oxUUdYN1laYlZDMVZocWYxclhlNk0zc0JMMEdnUW9LbEE5VSJ9fSwiaXNzdWluZ19hdXRob3JpdHkiOnsiaWQiOiJEVktBIiwibmFtZSI6IkdLViBTcGl0emVudmVyYmFuZCAtIERldXRzY2hlIFZlcmJpbmR1bmdzc3RlbGxlIEtyYW5rZW52ZXJzaWNoZXJ1bmcgLSBBdXNsYW5kIiwiY291bnRyeSI6IkRFIn0sImRhdGVfb2ZfaXNzdWFuY2UiOiIyMDI1LTA3LTE1IiwiZGF0ZV9vZl9leHBpcnkiOiIyMDMwLTA3LTMwIiwiYXV0aGVudGljX3NvdXJjZSI6eyJpZCI6IkRFOiAxMDM0MTE0MDEiLCJuYW1lIjoiQU9LIE5vcmR3ZXN0In0sInN0YXJ0aW5nX2RhdGUiOiIyMDI1LTA3LTAxIiwiZW5kaW5nX2RhdGUiOiIyMDMwLTA3LTMwIiwiX3NkIjpbIlpuOFlYMWo1bkRTb1Z2TFNQUWVBMi04TkRSYjUyNVgtQ0tuejdJQ2d1b1kiLCJqTmcxVmFzREJkdDlNZTFsbTF0N1dPS2JFQU0yaVNjTVlGY0o4eGFUZlc0Il0sIl9zZF9hbGciOiJTSEEtMjU2In0.lIz6T7ooFK90g2LZYOIv3VfVR3VMzeIujPd4mbTuqJty4AgxvPQNJSDKTQ5oZcTNkIdIM91UervHFtOSHKUEkA~WyI5MWQ2OTk0ODc3MGFmOGUyIiwicGVyc29uYWxfYWRtaW5pc3RyYXRpdmVfbnVtYmVyIiwiREU5ODc2NTQzMjEiXQ~WyIwOTVkNWUxYWIyNzFkN2U4IiwiZG9jdW1lbnRfbnVtYmVyIiwiODAxMTIyMzM0NDU1NjY3NzgwNDMiXQ~

Use https://www.sdjwt.co/decode to decode the SD-JWT

### Example payload for the SD-JWT VC
```json
{
  "vct": "urn:eudi:ehic:1",
  "jti": "urn:uuid:9b1deb4d-5b1d-47b5-9e3e-2b0e1b123456",
  "sub": "did:example:1234567890",
  "iss": "https://ehic.issuer.example.eu",
  "iat": 1721478000,
  "exp": 1753014000,
  "nbf": 1721474400,
  "cnf": {
    "jwk": {
      "kty": "EC",
      "crv": "P-256",
      "x": "4j5_9EF4ac9J6TR2z2eMgN3sZ2mD8X_Pb8hx7rk_F1U",
      "y": "7FsapV3Z1QGX7YZbVC1Vhqf1rXe6M3sBL0GgQoKlA9U"
    }
  },
  "issuing_authority": {
    "id": "DVKA",
    "name": "GKV Spitzenverband - Deutsche Verbindungsstelle Krankenversicherung - Ausland",
    "country": "DE"
  },
  "date_of_issuance": "2025-07-15",
  "date_of_expiry": "2030-07-30",
  "authentic_source": {
    "id": "DE: 103411401",
    "name": "AOK Nordwest"
  },
  "starting_date": "2025-07-01",
  "ending_date": "2030-07-30",
  "_sd": [
    "Zn8YX1j5nDSoVvLSPQeA2-8NDRb525X-CKnz7ICguoY",
    "jNg1VasDBdt9Me1lm1t7WOKbEAM2iScMYFcJ8xaTfW4"
  ],
  "_sd_alg": "SHA-256"
}
```
### Disclosures in the SD-JWT VC

    Salt: 095d5e1ab271d7e8
    Key: document_number
    Value: 80112233445566778043

    Salt: 91d69948770af8e2
    Key: personal_administrative_number
    Value: DE987654321



## 4 Attestation usage
### 4.1	Primary Use Case Scenario: Requesting Health Care Services during a temporary stay abroad
#### 4.1.1	The Setup
Alberto, an Italian musician, performs with an orchestra across multiple EU countries. He seamlessly manages his healthcare documents through modern technology. Through a harmonized digital issuance procedure, he securely stores his digital EHIC in his EUDI Wallet, ensuring he can easily access necessary healthcare services while traveling abroad.
#### 4.1.2	The Need for Verification
Alberto arrives in Germany for a concert. After a small accident while jogging the night before the event, he needs to access healthcare services and must present his EHIC to the local healthcare provider. The healthcare provider ensures that the EHIC is authentic, valid, and that Alberto is the rightful owner.
#### 4.1.3	The Business Context
Healthcare providers in Germany automatically check the entitlement to healthcare services, ensuring that Alberto gets access to healthcare at the same costs as locals and that the reimbursement process for the provided treatment is efficient and fast.
#### 4.1.4	The Verification Process
-	After the accident, Alberto visits a local healthcare provider. The provider, onboarded in the EUDI wallet ecosystem, uses a hardware device with proximity (e.g. NFC or Bluetooth) or non-proximity (e.g. internet endpoint) technology to request Alberto’s EHIC and his PID.
- The request is sent through a secure channel using a standard protocol for digital information exchange between the wallet and the healthcare provider’s device to protect Alberto’s data.
-	Alberto’s EUDI Wallet receives the request and evaluates it according to the registered and published disclosure policy of social security coordination. This evaluation includes a verification of the relying party (which may be represented by the healthcare provider’s organisation).
- Alberto reviews the evaluation of the healthcare provider’s device’s request and gives consent to share the requested information.
-	The wallet ensures the consented information is securely shared using standard protocols, confirming the credential is rightfully owned by the holder of the wallet and that the wallet is a valid EUDI wallet.
-	The healthcare provider’s device receives the information and signals, that it has been received.
-	The healthcare provider’s device automatically reviews the document with the necessary information, confirming its authenticity, validity at the time of verification, and possession by Alberto through a reliable verification process.
- They trust that Alberto is using his own EUDI Wallet, since an attested photo is part of the identity data presented on Alberto’s phone. If a photo is unavailable or insufficient, identity cards can be requested.
-	The result of the verification process, regardless of whether it is positive or negative, is presented on the healthcare provider’s device as well as on Alberto’s wallet.
#### 5.1.5	Positive Verification
-	Alberto receives healthcare services at the same costs as locals.
-	An information exchange between the healthcare provider and relevant social security institutions in the member state of stay using the information presented is initiated immediately to handle the cost reimbursement process. This requires an interface to the systems of social security institution.
-	A process is triggered, which automatically creates or updates the patient records in the healthcare provider’s software by using the presented information. This step may be different in other member states.
- The information transfer is logged in Alberto’s wallet.
-	The information (verification proof) and the result of the verification are created, signed and stored in the health care provider’s software for further processing (depending on national legislation)..
#### 4.1.6	Negative Verification
Negative verification implicates, that Alberto presents a digital EHIC that is not valid (e.g. expired, revoked, or issued by an untrusted source etc.).
-	Alberto must pay the full amount for the healthcare services himself in case he decides to receive them. Alternatively, he can decide to leave the healthcare provider without receiving treatment.
-	After the treatment he might be able to get the costs reimbursed by his social insurance company. 
- The information transfer is logged in Alberto’s wallet.
- The information and the result of the verification may be stored in the health care provider’s software for further processing (depending on national legislation).

In case Alberto did not download his EHIC credential before travelling to Germany or the information in the credential on his wallet is outdated (e.g. the EHIC was revoked and a new one has been issued), he can just download the latest credential on-site and present it to the health care provider and start the verification process again.

Verification processes may utilize proximity or non-proximity technologies, thereby supporting both offline and online operational contexts.

## 5 Trust anchors

Trust anchors for EHIC PuB-EAAs are the same as defined in the common rulebook `attestation-rulebook-wp6-common.md`.

## 6 Revocation

Revocation patterns for EHIC PuB-EAAs are the same as defined in the common rulebook `attestation-rulebook-wp6-common.md`.

## 7 Compliance

The Compliance follows the same principles as set out in the common rulebook `attestation-rulebook-wp6-common.md`.

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

## Annex 1 - Schema for an EHIC SD-JWT

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "title": "DC4EU EHIC SD-JWT VC Schema",
  "type": "object",
  "additionalProperties": false,
  "properties": {
    "vct": {
      "type": "string",
      "description": "The Verifiable Credential type identifier, as defined in ietf-oauth-sd-jwt-vc (draft 09).",
      "enum": ["urn:eudi:ehic:1"]
    },
    "jti": {
      "type": "string",
      "description": "Verifiable Credential unique identifier to prevent replay attacks. It needs to be unique for the JWT effective lifespan.",
      "minLength": 1,
      "maxLength": 255
    },
    "sub": {
      "type": "string",
      "description": "Subject identifier for the JWT, representing the principal that is the subject of the JWT. This is a case-sensitive string containing a unique identifier, as defined in RFC 7519 (JWT)."
    },
    "iss": {
      "type": "string",
      "format": "uri",
      "description": "Issuer identifier for the JWT, expressed as a URI, according to RFC 7519 (JWT)."
    },
    "iat": {
      "type": "integer",
      "description": "Issued at time indicating when the JWT was issued, represented as a NumericDate (number of seconds since 1970-01-01T00:00:00Z UTC) according to RFC 7519 (JWT)."
    },
    "cnf": {
      "type": "object",
      "description": "Contains confirmation key information used to prove possession of a private key, as defined in RFC 7800 (Proof-of-Possession Key Semantics for JWTs).",
      "properties": {
        "jwk": {
          "type": "object",
          "description": "JSON Web Key (JWK) object. Structure not fully specified here."
        }
      },
      "required": ["jwk"],
      "additionalProperties": true
    },
    "exp": {
      "type": "integer",
      "description": "Expiration time on or after which the JWT must not be accepted for processing, represented as a NumericDate (number of seconds since 1970-01-01T00:00:00Z UTC) according to RFC 7519 (JWT)."
    },
    "nbf": {
      "type": "integer",
      "description": "Not before time before which the JWT must not be accepted for processing, represented as a NumericDate (number of seconds since 1970-01-01T00:00:00Z UTC) according to RFC 7519 (JWT)."
    },
    "personal_administrative_number": {
      "type": "string",
      "minLength": 4,
      "maxLength": 50,
      "description": "The unique personal identifier assigned to the natural person for social security services and benefits by the competent institution (Social Security Number). The electronic identification scheme under which the identifier is issued, as well as the policy applied to the values of this attribute including, where applicable, specific conditions for its processing must be defined by the competent institution as part of this schema.",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:personal_administrative_number"
    },
    "issuing_authority": {
      "type": "object",
      "description": "The authority responsible for issuing the EHIC.",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority",
      "properties": {
        "id": {
          "type": "string",
          "minLength": 1,
          "maxLength": 20,
          "description": "The unique identifier of the EHIC issuing authority.",
          "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority:id"
        },
        "name": {
          "type": "string",
          "minLength": 1,
          "maxLength": 100,
          "description": "The full name of the EHIC issuing authority.",
          "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority:name"
        },
        "country": {
          "type": "string",
          "pattern": "^[A-Z]{2}$",
          "description": "Member State code (ISO 3166-1 alpha-2) representing the country under whose jurisdiction the EHIC is issued.",
          "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:issuing_authority:country"
        }
      },
      "required": ["id", "name", "country"],
      "additionalProperties": false
    },
    "date_of_issuance": {
      "type": "string",
      "format": "date",
      "description": "Date determined by the competent institution as either the start of the administrative validity period of the record represented by this EHIC, or the issuance date of the EHIC credential. The value is expressed as a full-date (YYYY-MM-DD) in accordance with ISO 8601-1 and RFC 3339. The exact interpretation is to be defined by the competent institution as part of this schema.",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:date_of_issuance"
    },
    "date_of_expiry": {
      "type": "string",
      "format": "date",
      "description": "Date determined by the competent institution as the end of the administrative validity period of the record represented by this EHIC, or the expiration date of the EHIC credential. The value is expressed as a full-date (YYYY-MM-DD) in accordance with ISO 8601-1 and RFC 3339. The exact interpretation is to be defined by the competent institution as part of this schema.",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:date_of_expiry"
    },
    "authentic_source": {
      "type": "object",
      "description": "The competent institution responsible for the EHIC, as registered in the Electronic Exchange of Social Security Information (EESSI).",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:authentic_source",
      "properties": {
        "id": {
          "type": "string",
          "minLength": 1,
          "maxLength": 20,
          "description": "The unique identifier of the competent institution responsible for the EHIC, as registered in the Electronic Exchange of Social Security Information (EESSI).",
          "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:authentic_source:id"
        },
        "name": {
          "type": "string",
          "minLength": 1,
          "maxLength": 100,
          "description": "The full name of the competent institution responsible for the EHIC, as registered in the Electronic Exchange of Social Security Information (EESSI).",
          "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:authentic_source:name"
        }
      },
      "required": ["id", "name"],
      "additionalProperties": false
    },
    "starting_date": {
      "type": "string",
      "format": "date",
      "description": "Date determined by the competent institution as the start date of the insurance coverage. The value is expressed as a full-date (YYYY-MM-DD) in accordance with ISO 8601-1 and RFC 3339.",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:starting_date"
    },
    "ending_date": {
      "type": "string",
      "format": "date",
      "description": "Date determined by the competent institution as the end date of the insurance coverage. The value is expressed as a full-date (YYYY-MM-DD) in accordance with ISO 8601-1 and RFC 3339.",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:ending_date"
    },
    "document_number": {
      "type": "string",
      "minLength": 4,
      "maxLength": 50,
      "description": "Unique document identifier assigned by the competent institution. This value identifies the specific EHIC document and may be used for administrative validation.",
      "$comment": "Namespace: urn:dgempl:pubeaas:v1:attribute:document_number"
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
    "document_number"
  ]
}
```

## Annex 2 - Schema for EHIC Credential Display & Disclosures
```json
{
  "vct": "urn:eudi:ehic:1",
  "name": "DC4EU EHIC SD-JWT VCTM",
  "description": "Selective disclosure metadata for EHIC SD-JWT VC",
  "$comment": "Implementation of the DC4EU VCTM may require Member State-specific clarifications to align with national policies governing the display of included claims.",
  "display": [
    {
      "lang": "en-EU",
      "name": "EHIC SD-JWT VC",
      "description": "European Health Insurance Card (EHIC) SD-JWT VC",
      "rendering": {
        "svg_templates": [
          {
            "uri": "https://demo-issuer.wwwallet.org/public/creds/ehic/european-health-insurance-card-svg-dc4eu-01.svg",
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
      "path": ["personal_administrative_number"],
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
      "path": ["issuing_authority"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Issuing Authority",
          "description": "The authority responsible for issuing the EHIC."
        }
      ]
    },
    {
      "path": ["issuing_authority", "id"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Issuing Authority ID",
          "description": "The unique identifier of the EHIC issuing authority."
        }
      ]
    },
    {
      "path": ["issuing_authority", "name"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Issuing Authority Name",
          "description": "The full name of the EHIC issuing authority."
        }
      ]
    },
    {
      "path": ["issuing_authority", "country"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Issuing Country",
          "description": "Country of the EHIC issuing authority."
        }
      ]
    },
    {
      "path": ["date_of_issuance"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Date of Issuance",
          "description": "Issuance date of the EHIC."
        }
      ]
    },
    {
      "path": ["date_of_expiry"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Expiry Date",
          "description": "EHIC credential expiry date."
        }
      ]
    },
    {
      "path": ["authentic_source"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Authentic Source",
          "description": "Competent institution as registered in the EESSI Institution Repository."
        }
      ]
    },
    {
      "path": ["authentic_source", "id"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Authentic Source ID",
          "description": "Identifier of the competent institution as registered in the EESSI Institution Repository."
        }
      ]
    },
    {
      "path": ["authentic_source", "name"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Authentic Source Name",
          "description": "Name of the competent institution as registered in the EESSI Institution Repository."
        }
      ]
    },
    {
      "path": ["starting_date"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Starting Date",
          "description": "Start date of the insurance coverage."
        }
      ]
    },
    {
      "path": ["ending_date"],
      "sd": "never",
      "display": [
        {
          "lang": "en-EU",
          "label": "Ending Date",
          "description": "End date of the insurance coverage."
        }
      ]
    },
    {
      "path": ["document_number"],
      "sd": "always",
      "display": [
        {
          "lang": "en-EU",
          "label": "Document Number",
          "description": "Unique EHIC document identifier."
        }
      ]
    }
  ]
}
```
