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
Finally, illustrative examples SHALL be included. 

[RULEBOOK AUTHOR TO PROVIDE AN EXAMPLE OF FULL OR PARTIAL mDOC OF THE ATTESTATION]

[RULEBOOK AUTHOR TO PROVIDE THE ATTRIBUTES AND THEIR VALUES INCLUDED IN THE EXAMPLE]

### 3.2 SD-JWT VC-based encoding 

Finally, illustrative examples SHALL be included. 

[RULEBOOK AUTHOR TO PROVIDE AN EXAMPLE OF THE JWT CLAIM SET USED BY THE PROVIDER]
#### Schema for an EHIC SD-JWT
```json
{
  "vct": "urn:eudi:ehic:1",
  "name": "DC4EU EHIC SD-JWT VCTM",
  "description": "DC4EU European Health Insurance Card (EHIC) SD-JWT Verifiable Credential Type Metadata, based on ietf-oauth-sd-jwt-vc (draft 09), using a single language tag (en-US).",
  "$comment": "Implementation of the DC4EU VCTM may require Member State-specific clarifications to align with national policies governing the display of included claims.",
  "display": [
    {
      "lang": "en-US",
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
      "svg_id": "personal_administrative_number_6",
      "display": [
        {
          "lang": "en-US",
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
          "lang": "en-US",
          "label": "Issuing authority"
        }
      ]
    },
    {
      "path": ["issuing_authority", "id"],
      "sd": "never",
      "display": [
        {
          "lang": "en-US",
          "label": "Issuing authority id",
          "description": "EHIC issuing authority unique identifier."
        }
      ]
    },
    {
      "path": ["issuing_authority", "name"],
      "sd": "never",
      "display": [
        {
          "lang": "en-US",
          "label": "Issuing authority name",
          "description": "EHIC issuing authority name."
        }
      ]
    },
    {
      "path": ["issuing_country"],
      "sd": "never",
      "svg_id": "issuing_country_2",
      "display": [
        {
          "lang": "en-US",
          "label": "Issuing country",
          "description": "EHIC issuing country."
        }
      ]
    },
    {
      "path": ["date_of_expiry"],
      "sd": "never",
      "svg_id": "date_of_expiry_9",
      "display": [
        {
          "lang": "en-US",
          "label": "Expiry date",
          "description": "EHIC expiration date."
        }
      ]
    },
    {
      "path": ["date_of_issuance"],
      "sd": "never",
      "display": [
        {
          "lang": "en-US",
          "label": "Issue date",
          "description": "EHIC validity start date."
        }
      ]
    },
    {
      "path": ["authentic_source"],
      "sd": "never",
      "display": [
        {
          "lang": "en-US",
          "label": "Competent institution"
        }
      ]
    },
    {
      "path": ["authentic_source", "id"],
      "sd": "never",
      "svg_id": "authentic_source_id_7a",
      "display": [
        {
          "lang": "en-US",
          "label": "Competent institution id",
          "description": "Identifier of the competent institution as registered in the EESSI Institution Repository."
        }
      ]
    },
    {
      "path": ["authentic_source", "name"],
      "sd": "never",
      "svg_id": "authentic_source_name_7b",
      "display": [
        {
          "lang": "en-US",
          "label": "Competent institution name",
          "description": "Name of the competent institution as registered in the EESSI Institution Repository."
        }
      ]
    },
    {
      "path": ["ending_date"],
      "sd": "never",
      "display": [
        {
          "lang": "en-US",
          "label": "Ending date",
          "description": "End date of the insurance coverage."
        }
      ]
    },
    {
      "path": ["starting_date"],
      "sd": "never",
      "display": [
        {
          "lang": "en-US",
          "label": "Starting date",
          "description": "Start date of the insurance coverage."
        }
      ]
    },
    {
      "path": ["document_number"],
      "sd": "always",
      "svg_id": "document_number_8",
      "display": [
        {
          "lang": "en-US",
          "label": "Document number",
          "description": "EHIC unique document identifier."
        }
      ]
    }
  ],
  "schema_uri": "https://demo-issuer.wwwallet.org/public/creds/ehic/european-health-insurance-card-schema-dc4eu-01.json",
  "schema_uri#integrity": "sha256-lNMpT2YzCPU1AuIpSIjryv6KUgBUBUVs3eNbZQoMJNA="
}
```

#### Example SD-JWT Claim Set

The following is an example of a claim set for an EHIC SD-JWT VC:

```json
{
  "iss": "https://issuer.example.org",
  "sub": "did:example:123456789abcdefghi",
  "iat": 1719907200,
  "exp": 1722585600,
  "vc": {
    "vct": "urn:eudi:ehic:1",
    "personal_administrative_number": "123456789",
    "issuing_authority": {
      "id": "DE:456789",
      "name": "DRVB",
      "country": "DE"
    },
    "authentic_source": {
      "id": "DE:456789",
      "name": "DRVB"
    },
    "document_number": "80067899202020289076",
    "starting_date": "2025-07-04",
    "ending_date": "2025-08-01",
    "date_of_issuance": "2025-07-01",
    "date_of_expiry": "2025-08-01"
  }
}
```
[RULEBOOK AUTHOR TO PROVIDE AN EXAMPLE OF THE ISSUED SD-JWT (IN base64 ENCODING)]

[RULEBOOK AUTHOR TO PROVIDE AN EXAMPLE OF A HUMAN READABLE VERSION OF THE SD-JWT PAYLOAD
AND A DESCRIPTION OF THE DISCLOSURES INCLUDED IN THE EXAMPLE]


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
